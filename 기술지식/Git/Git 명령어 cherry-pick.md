# cherry-pick?
체리픽이란 명령어는 다른 브랜치의 일부 커밋만을 가져와서 반영 시킬수 있는 깃 명령어이다. 원하는 커밋만을 가져온다는 뜻에서 체리 픽이란 이름이 붙었는데 그 유래는 '나무에서 열린 체리 가운데 가장 탐스러운 열매만 따서 먹는 행위' 또는 '케이크 위에 얹어진 맛있는 부분인 체리만 집어 먹는 행위'라는 뜻에서 유래된 것으로 보여진다. 이러한 용어는 git명령어 뿐아니라 경제학에서도 사용되는 용어이다.
> 굳이 유래까지 알아본 이유는 원하는 부분만 따온다는 느낌을 이름에서 알수 있어서 한번 써본 기능이었지만 머릿속에 더 남아있었기 때문이다.

# cherry-pick의 사용법
사용법은 간단하다. cherry-pick을 가져오고 싶은 브랜치를 HEAD가 가르키게 한 뒤에 cherry-pick명령어를 통해 원하는 커밋을 선택하면 HEAD가 가리키는 브랜치에 커밋이 쌓이게 되는 형식이다.
```
$ git cherry-pick '커밋 번호'
```
위의 명령어를 사용하면 cherry-pick이 실행되고 아래의 그림과 같이 커밋이 쌓이게 된다. 첫번째 사진에 보이는 git log가 체리픽을 사용하기 전의 모습이고 두번째 사진이 rel_2.3브랜치에 체리픽을 이용해 F커밋을 끌어온 모습이다.<br>
![image](https://user-images.githubusercontent.com/85680496/159846159-604c8158-2afd-42e3-9404-2629cd1ff229.png)
![image](https://user-images.githubusercontent.com/85680496/159846167-b83732a9-99e7-42f8-85b3-5348c0c26ecb.png)
위의 예시처럼 체리픽을 사용하면 다른 브랜치의 일부 커밋을 가져오는 것이 가능한데 물론 그림처럼 변경된 부분의 기능이 완전히 분리되어 있다면 간단하게 가져오게 될수도 있지만 가져오면서 생기는 conflict즉, 충돌이 발생할 수도 있다. 이러한 경우에는 오류가 발생하고 충돌된 부분이 나타날 것이다.
> 보통 많이 사용하는 vscode에서는 충돌된 부분을 비교하여 간단하게 바꿀수 있다.

그 부분을 바꾸어 준 뒤에 add를 통해 수정된 코드를 올리고 체리픽 옵션중 하나인 -continue를 사용해 진행하던 체리픽을 마무리 하면된다.
```
$ git cherry-pick -continue
```
위의 명령어 말고도 체리픽을 중단하기 위한 옵션인 -abort명령어도 있다. 이 명령어를 사용하면 진행중이던 체리픽을 멈추고 이전의 상태로 돌아가게 된다. 
```
$ git cherry-pick -abort
```

# cherry-pick의 필요성
보통 해당 커밋이 필요하게 되는 상황들에서는 rebase를 통해서도 해결이 가능하지 않나? 라고 생각되었지만 생각보다 많은 상황에서 체리픽이 따로 필요한 경우도 있다는 것을 알게 되었다. <br><br>
- 팀 프로젝트를 진행하던중에 백엔드인 팀원이 자신의 기능을 확인하고 싶은데 해당 기능의 프론트 부분이 일부분만 구현되고 아직 작업이 진행중일 경우에 우선 일부분 완성이된 부분만 체리픽을 통해 백엔드 팀원의 브랜치에 가져가 먼저 확인하는 경우가 있을수가 있다. 
- 실수로 PR(Pull Request)를 머지 하기 전에 닫아버린 경우에도 체리픽을 통해 해당 커밋을 가져오면 다시 살릴수가 있다.

>###### 출처
>https://inpa.tistory.com/entry/GIT-%E2%9A%A1%EF%B8%8F-%EC%9B%90%ED%95%98%EB%8A%94-commit-%EA%B0%80%EC%A0%B8%EC%98%A4%EA%B8%B0-cherry-pick <br><br>
>https://webisfree.com/2017-04-11/git%EC%97%90%EC%84%9C-%EC%B2%B4%EB%A6%AC%ED%94%BD%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EC%BB%A4%EB%B0%8B(commit)-%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95%EC%9D%80
