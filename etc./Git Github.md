# Git / Github
### 글 쓰게 된 이유
`iOS`앱 개발자라면 협업과 버전 관리에 용이한 `Git/Github`를 쓰기 마련이다. <br>
`Git/Github`는 어떤 녀석인지 어떤 기능들을 가지고 있는지, 전체적으로 살펴보는 것은 큰 도움이 될 것 같다. <br>

---
### VCS
`VCS` (Version Control System) - 버전 관리 시스템  <br>
파일 변화를 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템 <br>
<파일의 변경 이력을 기록하여 관리를 용이하게 해주는 것> <br>
 - 변경 이력을 기록을 통해서 변경된 내용 공유 가능
 - 타인이 작업한 내용을 쉽게 병합 (팀 프로젝트에 용이, 역할을 나누어 작업을 진행할 경우에 용이)
 - 과거 상태로 쉽게 복구 가능 (특정 시점으로 쉽게 돌아갈 수 있다.)
 - 여러 분기(Branch)를 통해 병렬 관리 가능

---
### Git
버전관리 시스템이 필요한 이유?? <br>
**조금 더 생각해보기 + 알아보기** <br>
Git - 소스 저장소, VCS 중하나
 - 복잡한 Branch 관리에 적합
 - 심플하지만 핵심적인 기능이 강력
 - 로컬 저장소와 원격 저장소의 분리
 - 다양한 보조 툴

---
### Git에서의 작업 흐름
우선 Git 명령어들에 대해서 살펴보기 전에 Git에서의 작업 흐름에 대해서 살펴보고 가자 <br>
<img src="https://github.com/zziro95/zzipository/blob/main/images/gitbase.png" width="70%" height="70%" title="gitbase" alt="gitbase"></img> <br>

#### Working Directory
- 실제 작업하고 있는 공간
- **내 로컬 저장소에서의 작업 디렉토리** **(Local 저장소라는 표현이 틀린가?)다 정리후 다시 한 번 생각해보기** 

#### Staging Area
- index 하는 공간
- 쉽게 설명하면 준비 공간
- 추적되지 않은 작업 파일을 `git add`를 하여 추적하게 되면 Staging Area로 올라오게 된다.
- Git이 변경이력을 관리하는 부분
- Working Directory에서 git 명령어를 통해서 추가 가능
- 이 곳에 올라와 있는 파일만 저장소에 추가 및 수정 가능 하다

`Working Directory` > `Staging Area` > `.git directory(Repository)`

#### Repository (Local & Remote)
Local Repository
- 외부에 위치하지 않고 작업하고 있는 컴퓨터에 존재
- 외부 저장소에 손실이 발생하더라도 빠르게 복구 가능

Remote Repository
- 외부 서버(ex. github 서버)에 위치하여 변경 이력을 기록하는 부분
- 인터넷을 이용하여 접근 가능
- 다중 사용자로부터 관리되는 각 로컬 저장소의 접점

- 저장소의 위치가 내 컴퓨터에 있느냐, 서버에 있느냐 차이
서버에 있다면 나 뿐만이 아닌 다른 사람과 공유가 가능하기 때문에 협업에 매우 유리하다.

### Staging Area가 왜 필요한가??
왜애 필요한가~~ <br>

---
 ### Git 명령어
 - `git init`  새로운 저장소 생성
    - `.git` 이라는 하위 디렉토리 생성
    - 디렉토리에서의 변경 이력을 추적해 나가고 싶다면 `git init` 명령어를 실행
 - `git config --global user.name github사용자이름` & `git config --global user.email github이메일`
    - 저장소별 사용자명 / 이메일 구성하기 
 - `git config --global --list` 전역 설정 정보 조회
 - `git config --list` 저장소별 설정 정보 조회
 - `git status` 디렉터리 안에 변경사항에 대해 알아보기
    - 파일의 상태 확인
    - 추적되지 않거나(Untracked) 변경된(Modified) 상태의 파일이 있는지 알려준다.
 - `git add` 파일을 추적하기 (`Git Staging Area`로 보낸다)
    - 디렉토리의 변경 이력을 추적하기 위해 `git init`을 해주고, 새로운 파일을 생성하거나 변경해 주었다면 `git status` 명령어를 통해 (새로운 파일) 추적되지 않거나, (기존에 있었지만) 변경된 파일을 확인하게 된다.
    - `git add 파일이름` 특정 파일이나 디렉토리를 추적하기 또는 `git add .` 모든 변경 사항을 추적하기를 통해 파일을 추적한다.
 - `git commit` 추적되고 수정된 모든 파일의 변경 사항 커밋 하기
    - `git commit -m "커밋 내용에 대해서 적어주기"`
    - 나의 경우는 `git commit -m "feat: #이슈번호 커밋 내용`의 포멧으로 적어주고 있고, 이 스타일은 `git karma style`이다
 - `git log` 모든 이력 보기
    - 써본 적은 없는데 `git log -p`는 변경 사항과 로그를 함께 보여주는 것이고,  `git log -1`는 1개의 항목만 보이도록 로그 개수를 제한하는 것, `git log -20 -p`은 20개의 항목과 패치만 보이도록 제한한 것이라고 한다. 다양하게 활용할 수 있을 것 같다.
 - `git diff` 현재 `Working Directory`와 `Staging Area(Index)`의 차이점 보기
    - 이전 커밋 상태와 어느 부분이 변경 되었는지 상세하게 볼 수 있다.
 <br>
 <br>
 <br>
 
**Git Todos**
**명령어들 추가적으로 정리하기 git amend? apply? git reset soft git reset hard / reset / revert**
**git stash git stash pop git checkout 브랜치**
**브랜치가 여러개 있을 경우 작업중에 잠시 브랜치를 변경하고 싶을 때 용이하다.!**
**git reset과 revert의 차이, 야곰이 말한 revert(성공,실패)해보기**
**git reset과 revert할때 커밋번호! 해쉬번호였나? 해쉬라는 개념에 대해서도 정리해야 될 듯**
**Hash는 간단하게 다른 글로 정리 하는게 좋을듯**
**커널이란 간단하게 정리하는 글 쓰기? ㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋㅋ**

---
### gitignore
`Git`에서 `.gitignore` 파일을 통해 특정 파일들은 `Staging Area` 영역에 올라가지 않도록 무시해 준다. <br>
프로그램 툴을 사용하기 위해서는 필요하지만 변경 이력에 남길 필요가 없는 파일(추적하지 않을 파일)들을 `.gitignore`파일에 선언해 준다. <br>
`.gitignore`을 `Staging Area` 영역에 `git add` 하지 않은 상태에도 파일 내부에 무시하고자 하는 파일들을 적어주었다면 그 무시하고자 하는 파일들은 `git status` 키워드를 통해 추적조차  되지 않는다!! (신기해요) <br>
[gitignore](https://www.toptal.com/developers/gitignore, "gitignore")를 자동으로 생성해 주는 사이트가 있는데 `macOS`, `Swift`, `Xcode` 정도로 설정하고 프로젝트에 직접 추가해 보고자 한다. <br>
이 외에도 `SwiftPackageManager`, `SwiftPM`, `Objective-C`, `Linux`, `Windows`, `Sublimetext`것들을 추가하기도 하는데 작업하는 환경에 맞게 `gitignore` 파일을 만들어 주면 될 것 같고 모르는 용어(`SwiftPM`)에 대해서도 추후 살펴보자~~(회고할 거라는 가정하에)~~ <br>

---
### git karma style
`이니`에게 배워 지금까지도 잘 사용하고 있는 `git karma style` <br>
많은 개발자들이 사용하고 있고, 사용하다 보니 익숙해지기도 해서 쓰고 있다. <br>
이 스타일에 대해서 알아보고 키워드를 정리해봤다.

**카르마 스타일 정리한거 넣기**

---
### 마무리 글
`Git`을 조금 써왔지만 뭐였지.. 헷갈리는 명령어들도 있었고, 몰랐던 명령어들도 있었고, 편식한 키워드들도 많았다. 한 번 다시 살펴보게 되면서 전보다는 조금 틀이 잡힌 상태로 `Git`과 다시 마주하게 될 것 같아 들뜬 마음이다. <br>
이 외에도 `Git`에는 `issues`, `Actions`, `Projects`, `Milestones`, `Discussions` 등 많은 기능들을 지원하고 있다. <br>
이 부분에 대해 공부해보고 추가적으로 글을 적어보자! <br>

---
### 참고
- [Git설치](https://git-scm.com/download/mac, "Git설치")
- [Git](https://git-scm.com/book/ko/v2, "Git")
- [참고블로그](https://medium.com/@joongwon/git-git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC-c25b421ecdbd, "참고블로그")
- [gitignore](https://www.toptal.com/developers/gitignore, "gitignore")
- [GitBranchGame](https://learngitbranching.js.org/?locale=ko, "GitBranchGame")

***
