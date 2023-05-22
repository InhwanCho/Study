## TensorRT Build Engine(trt 엔진 생성)

Onnx to Trt 모델 생성 및 추론 과정을 알아보겠습니다.

텐서알티(trt) 엔진 생성은 클래스(객체)를 아래의 객체들을 이용하여 만들 수 있습니다.

-   builder
-   network
-   parser
-   config
-   profile
-   parser

trt.Logger : logging을 어떻게 활용할 것 인지에 대한 객체  
\- avaiable level: VERBOSE, INFO, WARNING, ERRROR, INTERNAL\_ERROR

trt.Builder : network, config와 같은 다른 객체들을 만들어 낼 수 있는 객체. Engine을 빌드의 모든 정보를 가지고 있음.

config = builder.create\_builder\_config() : int8, tf32, fp16의 설정, sparse\_weights 설정을 할 수 있음.

network = builder.create\_network() : network에 대한 정보들 (num layers,inputs,outputs)

profile = builder.create\_optimization\_profile() : dynamic batch 설정을 해주는 역할

parser = trt.OnnxParser(network, logger) : Onnx 모델을 parsing 해주는 역할

### 코드를 통해 분석하기

```python
logger = trt.Logger(trt.Logger.WARNING)  # create Logger, avaiable level: VERBOSE, INFO, WARNING, ERRROR, INTERNAL_ERRO기

builder = trt.Builder(logger)  # create Builder

network = builder.create_network(1 << int(trt.NetworkDefinitionCreationFlag.EXPLICIT_BATCH))  # create Network

profile = builder.create_optimization_profile()  # create Optimization Profile if using Dynamic Shape mode

config = builder.create_builder_config()  # create BuidlerConfig to set meta data of the network

parser = trt.OnnxParser(network, logger)

with open(onnxFile, "rb") as model:
    if not parser.parse(model.read()):
        print("Failed parsing .onnx file!")
        for error in range(parser.num_errors):
            print(parser.get_error(error))
        exit()
    print("Succeeded parsing .onnx file!")


profile.set_shape(inputTensor.name, [1, 3, nHeight, nWidth], [opt_batch, 3, nHeight, nWidth], [max_batch, 3, nHeight, nWidth])
#여기에 batch_size 설정

config.add_optimization_profile(profile)
engineString = builder.build_serialized_network(network, config)  # create a serialized network

if engineString == None:
    print("Failed building engine!")
    exit()
print(f"Succeeded building engine!, Sparsity : {Sparsity}, opt_batch : {opt_batch}, max_batch : {max_batch}")
with open(trtFile, "wb") as f:  # create engine
    f.write(engineString)
```

---

### TensorRT Inference(trt 추론)

```python
#trt engine open
f = open(trtFile, "rb")
logger = trt.Logger(trt.Logger.WARNING)

# create inference Engine using Runtime
engine = trt.Runtime(logger).deserialize_cuda_engine(f.read())

# number of input+output = 여기선 2
nIO = engine.num_io_tensors

# nIO tensor_Name 부여(onnx 만들때) 여기선 [x(in), z(out-argmax)]
#torch의 모델 class를 보면 input과 output이 tensor_name으로 부여가 됨
lTensorName = [engine.get_tensor_name(i) for i in range(nIO)]

#number of input ==> 1 | input = x가 1개이기 때문에 1
nInput = [engine.get_tensor_mode(lTensorName[i]) for i in range(nIO)].count(trt.TensorIOMode.INPUT)

# 추론을 위한 context 객체 생성
context = engine.create_execution_context()

# 여기선 input='x'에 대한 shape
context.set_input_shape(lTensorName[0], [batch_size, 3, nHeight, nWidth])

def run(input_var):
    #input_var.shape = (batch,3,224,224) imagenet
    input_var = input_var.cpu().detach().numpy()

    # prepare the memory buffer on host
    bufferH = []
    bufferH.append(np.ascontiguousarray(input_var))
    for i in range(nInput, nIO):
        bufferH.append(np.empty(context.get_tensor_shape(lTensorName[i]), dtype=trt.nptype(engine.get_tensor_dtype(lTensorName[i]))))

    # prepare the memory buffer on device
    bufferD = []
    for i in range(nIO):
        bufferD.append(cudart.cudaMalloc(bufferH[i].nbytes)[1])

    # copy input data from host buffer into device buffer
    for i in range(nInput):
        cudart.cudaMemcpy(bufferD[i], bufferH[i].ctypes.data, bufferH[i].nbytes, cudart.cudaMemcpyKind.cudaMemcpyHostToDevice)

    # set address of all input and output data in device buffer
    for i in range(nIO):
        context.set_tensor_address(lTensorName[i], int(bufferD[i]))

    # do inference
    context.execute_async_v3(0)

    # copy output data from device buffer into host buffer
    for i in range(nInput, nIO):
        cudart.cudaMemcpy(bufferH[i].ctypes.data, bufferD[i], bufferH[i].nbytes, cudart.cudaMemcpyKind.cudaMemcpyDeviceToHost)

    # 결과 확인(torch와 과정 동일)
    # print(bufferH[1])
    bufferH[1] = torch.Tensor(bufferH[1])
    pred = torch.max(bufferH[1],1)[-1]

    for b in bufferD:  # free the GPU memory buffer after all work
        cudart.cudaFree(b)
    return pred
```

\-참고 :

[https://github.com/InhwanCho/Weight-pruning\_A100-A6000/blob/main/main/onnx2trt.py](https://github.com/InhwanCho/Weight-pruning_A100-A6000/blob/main/main/onnx2trt.py "my_github")
