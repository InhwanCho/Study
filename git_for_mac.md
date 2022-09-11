
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