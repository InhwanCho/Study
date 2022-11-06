
# git command (처음 등록할 경우)

### git --version
>깃이 깔렸는지 확인<br>
### git --help
>깃 명령어 확인(나가려면 q누르면 됨) <br>
### git config 
>   >global user.name "your_name"<br>
>   >git config --global user.email "your_email"<br>
>   >git config --global user.password "your_token_password"<br>
>   >   >git config --list  >깃 유저,이메일 등록 후 등록 되었는지 확인(화면 나가려면 q누르기)<br>
### git init
깃에 연결할 폴더에 cd 명령어로 이동 후, 해당 명령어 실행 시 .git파일 생성(숨김 파일)됨과 동시에 깃명령어 수행하는 폴더로 변경(iterm2를 사용할 경우 브런치네임이 나옴)<br>
### git clone (보통 url)
> git clone ../StudyforGit(repository name)<br>
>   >상대방, 혹은 자신의 깃에 연결하여 다운받음<br>
>   >폴더나 url에 연결 url에 보통 연결<br>
### git status
파일 수정 후 상태 확인 창.(확인 할 필요는 없지만 초반에는 도움이 많이 되는 명령어)<br>
### git add 'filename' or . or '-A'
파일 수정 후 페이지에 변경할 파일명 등록. '.'이나 '-A'입력 시 폴더 전체를 등록함<br>
### git commit -m 'message'
add한 파일들을 홈페이지에 올림.<br>
### git push (-u)
commit한 파일을 홈페이지에 확정으로 올림. 파일이 처음 생성된 경우 <br>
>git push origin master로 입력해야함<br>
### git pull
홈페이지에서 수정된 정보를 디렉토리와 비교해서 업데이트(혼자 작업할때는 거의 사용 안함)<br>
### touch .gitignore
디렉토리에있는 파일 중 깃에 올리고 싶지 않은 파일이 필요할 경우 생성 후 편집<br>
ex) .gitignore 파일에 abc.text, *.csv  (이런식으로 와일드카드로 설정 가능) <br>
### git reset 파일 이름 or git reset(모든 파일 초기화)
add명령어로 올린 파일들의 명령을 초기화시킴 (add된 파일 working directory로 이동)<br>
### git log
여태까지 커밋한 로그를 보여줌 (커밋 메시지 중요)<br>
### git branch -a
현재 연결된 브렌치를 확인 *로 표시됨.<br>
### git diff
파일 수정 후 변경된 부분을 표시하는 명령어<br>
### git branch 'name'
브랜치 생성(작업 후 add, commit까진 작업이 동일함) push를 git push 'branch name'으로 해야함<br>
### git checkout 'branchname'
브랜치 선택<br>
### git remote add origin http:...
깃이랑 폴더를 연결<br>
(파일 처음 커밋하려면 푸시 안됨 이거 먼저 해줘야 함)<br>
### git branch --merged 
브렌치 합치기 <br>
### git branch -d 'branch name'
브렌치 삭제(merge안하고 하면 경고뜸. 무시해도 됨)<br>
### git branch -a
브렌치 상황 보기<br>
### git push origin --delete calc-divide
삭제된 브렌치 메모리에서 완전 제거<br>
### git push --set-upstream origin 'branch name'
브렌치에서 새로운 파일 생성 후 푸쉬할때 업스트림으로 세팅<br>
### git merge (branch name)
-> git push origin master<br>
# gti team project
### git clone 주소 폴더이름
주소는 깃허브에서 들고와야함
폴더이름은 선택사항이다 (즉 없어도됨) 폴더이름을 줄경우에는 그 폴더가 새로 생성이 되면서 그 안에 코드들이 다운로드가 되고, 폴더이름을 안줄경우엔 깃허브 프로젝트 이름으로 폴더가 자동으로 생기고 그안에 코드들이 다운로드된다.
Github에서 내 브렌치(branch)만들기

### git checkout -b 브렌치이름
내 브렌치에 소스코드 업데이트하기

### git add .
git commit -m "first commit"
git push origin 브렌치이름
마스터 브렌치에 소스 가져오기(pull)

### git pull origin master
pull을 하기전에는 기존에 소스코드들을 commit을 먼저 해놔야 한다 (2탄 강의참조)

브렌치끼리 이동하는 법
### git checkout 브렌치이름
강의에서 소개하진 않았지만 내가 내 브렌치에서 마스터 브렌치로 이동을 하고 싶거나 다른 브렌치로 이동하고싶으면 해당 명령어를 쓰면 된다

# 맥북 terminal 명령어
###### 현재 디렉토리 pwd
###### 현재 디렉토리 파일리스트 보기 ls  & 숨김파일까지 확인할 경우 ls -la
###### 디렉토리 이동 cd 'nnn'
###### 디렉토리 되돌아가기 cd ..(바로 전 폴더로)
###### 디렉토리 생성(폴더 생성) mkdir   & 해당 폴더를 탭으로 ex)  touch test_directory/test_directory2
###### 디렉토리 삭제 rmdir  or  rm -R(디렉토리에 파일이 있을 경우)
###### 화면 클리어 clear & command + 'k' 
###### 파일 생성 touch ...txt   & 해당 폴더를 탭으로 ex)  touch test_directory/test_filea.txt
###### 파일 삭제 rm ... 
###### 파일 이동 mv '파일이름' '폴더이름' - 다운로드 받은 파일 드레그로 끓어옮기기 가능.
###### 파일/디렉토리 이름 바꾸기 mv
###### 열기 open
###### 파일 확인(내용확인) cat ...
###### 히스토리 history
#### cd 같은 명령어 뒤에 tap키 누르면 선택지에서 선택 가능
다운로드(finder)파일을 누르고 cd 뒤로 드레그로 옮겨서 여는것도 가능
###### 화면 세로 분할 command + d, 분할 해제 command + shift + d
###### 새로운 터미널 command + n
###### 속성 보기 command + i (화면 색상 및 정보 확인)
###### 터미널 닫기 command + w
###### 모든 탭 보기 또는 탭 개요 종료 command + shift + \
###### https://richwind.co.kr/50
###### 파일을 나노 텍스트 편집기로 열기 nano 'mmm'
#### 나노 텍스트 편집기로 열면 수정도 가능. 밑에 명령어 몇 개 사용 가능
###### 위 화살표 버튼을 눌러서 전에 수행한 명령어 불러오기 가능
###### 몇 개의 단어 입력 후 Tap키 누르면 자동완성 기능 수행하여 작업이 편해짐.
###### 바탕화면 파일 숨김 ->Defaults write com.apple.finder CreateDesktop false && killall Finder (해제하려면 true)
###### 파일 복사 cp filename newfilename
### find
###### find .(현재 디렉토리) -type f(file) -name 'test_1.text'
if u dont know specific file name use the wild card
###### like find .(현재 디렉토리) -type f(file) -name 'test*'
-iname으로 하면 대소문자 구분없이 검색 가능
##### find .(현재 디렉토리) -type f(file) -name 'test*' -maxdepth 1(현재 디렉토리)
##### grep "some word" somefile.txt ->파일내에 해당 내용이 있는지 확인 가능
##### 폴더 혹은 파일 위치 찾기 which f(filename)
##### rm -R filename,,, <해당 파일(혹은 폴더) 강제 삭제

. -> current directory(현재 폴더)
.. -> perent directory(전 폴더)
~ -> 폴더 자유롭게 참조할때

### 다운로드 받은 파일 쉽게 현재폴더(주피터노트북)으로 옮기기->
1. terminal을 cd명령어로 주피터노트북의 폴더로 이동해둔다.
2. (mv ~/Dow) 까지 입력 후 Tap키를 눌르고 다운받은 파일을 탭키를 이용하여 입력한다.
3. 스페이스바 후 (./)를 입력한다.
4. ex) mv ~/Downloads/testfile.text ./  이렇게 입력하면 해당 파일이 현재폴더로 옮겨진다.


# 주피터 노트북 주요 단축키
a == 위에 셀 생성
b == 아래 셀 생성
c == 셀 복사
x == 셀 자르기
v == 셀 붙여넣기
control + shift + '-' == 셀 나누기
shift + m == 셀 합치기
dd == 셀 삭제
y == code 모드(셀)
m == markdown 모드(셀)
o == 코드 결과 접기(열기)
% 입력 후 command 입력 가능
%% 입력하면 셀 전체 command 입력 가능

<iframe id="igraph" scrolling="no" style="border:none;" seamless="seamless" src="https://plotly.com/~InhwanCho/14.embed" height="525" width="100%"></iframe>