## git

1. ❗️commit은 `의미있는 변동사항`을 묶어서 만든다. commit 메세지는 시간을 조금 들여서도 생각하고 쓰자


   

2. 로컬 (push)→ 원격 저장소

- 깃으로 추적하는 파일은 4가지 상태) 추적 안됨 수정없음 수정함 스테이지됨

- 작업공간에 있는 (수정함,추적안됨)파일을 스테이지로 올려 (스테이지됨) 으로 변경

- 커밋하면 수정안됨으로 상태가 돌아가 다시 수정 가능

3.  CLI

    —처음 설정

    - $ cd 버전관리할 폴더
    - $ git init
    - git add readme.md        /// git add .  모든 파일 추가 (tab 누를시 자동완성)
    - git commit -m "커밋 메세지"
    - git log

    —원격저장소 커밋하기

    - git remote add origin(원격 저장소 닉네임) https://github.com/아이디/레파지토리이름.git
    - git push origin(원격저장소 닉) master(branch)

    -  원격저장소에서 받아오기

    - git clone (url)             : 레파지토리 최상위폴더부터 클론

    ❗️잘못 클론했을시 삭제 명령 : rm -rf (폴더이름)

    - git (url) .                      : 현재 폴더에서 받아오기/ 레파지토리 최상위폴더 아래에서부터 클론

    —원격저장소에서 새로고침

    - git pull origin master

    —브랜치

    - git branch cat     :브랜치 생성
    - git checkout cat : cat브랜치로 이동해라
  

4. GUI (소스트리)

    ❗️깃허브 연동 오류시) 개발자 옵션에서 personal access tokens 발급받자) 한번 받고 잃어버리지 말자

    
    (https://github.com/settings/tokens)

    요기로 들어가라

    출처

    [I can't connect to Github from Sourcetree](https://community.atlassian.com/t5/Git-questions/I-can-t-connect-to-Github-from-Sourcetree/qaq-p/30851)

5. 머지

    - base가 될 브랜치로 이동 (master로 이동)
    - compare 브랜치인 oct 브랜치를 나와 합친다고 명령 git merge oct
    - 머지는 합집합,, 모자가 여러개면 충돌..? (0+모자 , 모자+꽃, 모자+모자,,?)
    - 소스트리) 다른 브랜치에서 병합한 마스터 브랜치를 내 브랜치에서 볼때, 원격 master와 로컬 master가 많이 차이 날때 ,, 브랜치 탭의 master 우클릭, 원격 저장소 추적 눌러서 pull 받아온다

    1. 충돌

    - 기본 : 수동으로 고쳐주기

6. folk

    - 통째로 내 계정에 복제
    - 자유롭게 커밋,푸쉬
    - 멋지게 바꾸고 PR

    (원본 저장소의 이력을 보려면 따로 주소를 추가해줘야함)

7.  pull request

    - 머지하고 싶은 브랜치들 선택 (base: 머지 당할 브랜치 compare:내가 새로 만든 기능)
    - 어떤 변경했는지 제목과 내용에
    - 단일 저장소에서 보낼수도, 포크한 저장소에서 보낼수도 있음
    - 팀원이 있으면,, 팀원이 pr을 보고 리뷰 가능, chage request 보내기 가능
    - 오픈소스! 는 기여 안내문서 contributing guide 참고해서 보내야된다

8. 브랜치 전략 중 git flow
    - feat/기능이름 으로 한 사람이 개발하는 기능 브랜치
    - 작업이 끝나면 dev( 또는 master) 브랜치로 pr
    - dev에서 작업이 얼추 머지 되면 release브랜치로 머지, 실 서버 배포
    - 직접 커밋은 feat만
