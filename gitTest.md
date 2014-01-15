# Git 및 Git Flow 적용
## Git
- 역사
	- 2002년부터 리눅스 커널에 사용된 BitKeeper 가 2005년 이익다툼으로 리눅스 커뮤니티와 관계가 틀어짐  
그 이후, 리누스 토발즈가 직접 git 을 만들었음.
- 강점
	- 빠른 속도로 대형 프로젝트에 사용하기 좋음
    - 편리한 브랜치 사용
- 추가 설명 내용 발췌([원본](http://www.slideshare.net/andabi/git-16126636))
![](http://image.slidesharecdn.com/git-130122191552-phpapp01/95/slide-10-638.jpg?cb=1359009131)
![](http://image.slidesharecdn.com/git-130122191552-phpapp01/95/slide-11-638.jpg?cb=1359009131)
- [Download git](http://git-scm.com/download)

## Git Flow
![](http://image.slidesharecdn.com/git-130122191552-phpapp01/95/slide-39-638.jpg?cb=1359009131)
![](http://image.slidesharecdn.com/git-130122191552-phpapp01/95/slide-40-638.jpg?cb=1359009131)
## Git Flow 에 대한 상세 설명
- 기본 Branch
	- master : 최종 릴리즈한 안정된 버전
    - develop : 다음 릴리즈를 위한 개발 중인 최신 빌드
- feature : 특정 기능을 위한 Branch
	- develop Branch에서 가져오며, 다시 develop Branch 로 merge.
    - develop Branch 이외의 Branch 는 merge 금지
    - 일반적으로 개발자의 로컬에서만 유지하고 origin 에 push 하지 않는다.
    - develop Branch에 merge 하면 feature Branche 는 삭제
- release : Release 점검을 위한 Branch
	- develop 브랜치에서 가져오며, develop 과 master 브랜치로 머지한다.
    - release-* 형태로 이름을 짓는다. 예를 들어, 다음 릴리즈 버전이 1.2라면, release-1.2 라고 한다.
    - 브랜치를 생성한 후, 소스 코드 내에 버전과 관련된 값을 수정하고 커밋한다.
    - 다음 릴리즈까지 개발이 최종 완료되었다고 판단하는 시점에서 브랜치를 생성한다.
    - 릴리즈 대상이 되는 feature 는 미리 develop에 머지되어 있어야 하고,
      다음에 릴리즈할 feature 라면 develop에 머지되어 있으면 안된다.
    - release 브랜치를 생성한 이후의 버그 픽스는, develop 이 아닌 release 브랜치에서 진행한다.
    - 릴리즈가 모두 준비되었다고 생각하면, release 브랜치를 master 에 머지한다.
    - master 브랜치에서 해당 버전으로 태그를 생성한다.
    - release 브랜치에서 버그 픽스한 것들을 develop 브랜치로 머지한다.
    - release 가 종료되면, release 브랜치를 삭제한다.
- hotfix : 긴급 버그 픽스를 위한 브랜치
    - master 에서 가져오며, master 와 develop 브랜치로 머지한다.
    - hotfix-* 형태로 이름을 짓는다.
    - release 브랜치와 사용 방법은 동일하지만, 예상치 못한 긴급 버그 수정을 위해 사용한다.
    - release 와 마찬가지로, 소스 코드 내 버전 정보를 업데이트 한다.
    - 작업이 완료되면, master 에 머지하고 버전을 태그로 남긴다.
    - 수정 사항을 develop 브랜치로 머지한다.
      만약, release 브랜치가 이미 존재하면, develop이 아닌 release 브랜치로 머지한다.
    - 핫픽스가 종료되면 브랜치를 삭제한다.

## 주의사항
- 브랜치를 머지할 때 --no-ff 옵션을 쓴다.  
fast forward 머징을 하지 않고, 머지 커밋을 생성하겠다는 의미다.  
머징 히스토리를 유지하기 위함이다.
- 가능하다면 버전 정보는 소스 코드 내에서 직접 작성하지 않는다. 
버전과 관련된 정보를 찾아 현재 버전으로 업데이트하는 스크립트를 작성하자

## SourceTree 에서의 Git Flow
#### Git flow 활성화
- 기초 설정
	- 주의사항의 --no-ff 옵션을 위한 설정
![merge 시 --no-off 설정](https://31.media.tumblr.com/0146655e469235ff1c49623fd330c9f0/tumblr_mzdfrlcTUv1t6jgjqo1_500.png)
- Git Flow 활성화 Button  
![git flow Action](https://24.media.tumblr.com/2d63303070862351ba590d475f25de93/tumblr_mzdgf37NRr1t6jgjqo1_400.png)  
초기화 및 가장 기본적인 ```develop Branch``` 를 만든다. 
```  source tree 에서 git flow 사용시 develop branch 를 삭제하되면 그 이후로 git flow 에 대한 내용이 오류가 나게 됨   ```  
해결 방법
- git 관리 폴더의 config 파일을 수정  
![config 에 설정되어 있는 git flow 설정](https://31.media.tumblr.com/0d792f62d10057008d3ee4e440ea08ce/tumblr_mzdfvwIt5R1t6jgjqo1_400.png)  
git flow 관련 설을 다 삭제 한다.

#### 참조 경로
- http://github.com
- http://pcottle.github.io/learnGitBranching/
- http://www.slideshare.net/andabi/git-16126636
- http://ohgyun.com/402
- http://nvie.com/posts/a-successful-git-branching-model/
- http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/
- https://github.com/nvie/gitflow
