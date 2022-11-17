# parquet(메모리 줄여줌)
```python
import gc
def csv_to_parquet(csv_path, save_name):
    df = pd.read_csv(csv_path)
    df.to_parquet(f'./{save_name}.parquet')
    # df.to_parquet('train.parquet', engine='fastparquet', compression='snappy')
    del df
    gc.collect()
    print(save_name, 'Done.')
csv_to_parquet('./train.csv', 'train')
train = pd.read_parquet('./train.parquet').drop('road_in_use',axis=1)

# from google.colab import files 코랩인 경우
# files.download("train.parquet")
```

### 코드 실행 방지 코드(입력시 코드 실행 안됨) -> 테스트 필요 안됨.
```python
EVAL = False 
```

### query함수(필터거는 함수) <u>열이름</u> 입력
```python
train.query('month==7 and year==2022 and day>15')
```
### Labelencoding(train과 test데이터의 값이 다를 경우)
```python
for i in str_col:
    le = LabelEncoder()
    le=le.fit(train[i])
    train[i]=le.transform(train[i])
    
    for label in np.unique(test[i]):
        if label not in le.classes_: 
            le.classes_ = np.append(le.classes_, label)
            #np.append하면 값이 추가되어 추가된 값이 라벨클래스에 추가되어 라벨링되는 구조
    test[i]=le.transform(test[i])
```