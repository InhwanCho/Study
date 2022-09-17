
# git command
### git --version
깃이 깔렸는지 확인
### git --help
깃 명령어 확인(나가려면 q누르면 됨) 
### git config --list
깃 유저,이메일 등록 후 등록 되었는지 확인
### git init
깃에 연결할 폴더에 cd명령어로 이동 후, 해당 명령어 실행시 .git파일 생성(숨김 파일)됨과 동시에 깃페이지와 연결됨.
### git status
파일 수정 후 상태 확인 창.
### git add 'filename' or 
파일 수정 후 페이지에 변경할 파일명 등록 후 commit명령어 사용 가능
### git add -A
-A 입력 시 전체 파일 add함
### git commit -m 'message'
add한 파일들을 홈페이지에 올림.
### git push
commit한 파일을 홈페이지에 확정으로 올림.
### git pull
홈페이지에서 수정된 정보를 디렉토리와 비교해서 업데이트(혼자 작업할때는 거의 사용 안함)
### touch .ignore
디렉토리에있는 파일 중 깃에 올리고 싶지 않은 파일이 필요할때 생성 후 편집
### git reset
add명령어로 올린 파일들의 명령을 초기화시킴
### git log
여태까지 커밋한 로그를 보여줌 (메시지 중요)
### git remove -v
깃허브와 연결된 디렉토리를 확인해줌
### git branch -a
현재 연결된 브렌치를 확인 *로 표시됨.
### git diff
파일 수정 후 변경된 부분을 표시하는 명령어
### git branch 'name'
브랜치 생성(작업 후 add, commit까진 작업이 동일함) push를 git push 'branch name'으로 해야함
### git checkout 'branchname'
브랜치 선택
### git remote add origin http:...
깃이랑 연결
### git branch --merged 
브렌치 합치기 ->
### git branch -d 'branch name'
브렌치 삭제
### git branch -a
브렌치 상황 보기
### git push origin --delete calc-divide
삭제된 브렌치 메모리에서 완전 제거
### git push --set-upstream origin 'branch name'
브렌치에서 새로운 파일 생성 후 푸쉬할때 업스트림으로 세팅


# 맥북 terminal 명령어
###### 현재 디렉토리 pwd
###### 현재 디렉토리 파일리스트 보기 ls
###### 디렉토리 이동 cd 'nnn'
###### 디렉토리 생성(폴더 생성) mkdir
###### 디렉토리 삭제 rmdir
###### 디렉토리(파일을 가지고있는 폴더일 경우) 삭제 rm -r
###### 화면 클리어 clear
###### 파일 생성 touch ...txt
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
# https://richwind.co.kr/50
###### 파일을 나노 텍스트 편집기로 열기 nano 'mmm'

