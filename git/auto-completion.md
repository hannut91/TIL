# Git Auto-completion
깃을 사용할 때 사용되는 커맨드들이나 branch이름들을 입력할 떄 Auto-Completion을
이용하여 편리하게 사용할 수 있다. 

## Install
```sh
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash > ~/git-completion.bash
echo '~/git-completion.bash' >> ~/.bashrc
```

위의 2개의 커맨드 입력만으로 간단하게 설치 할 수 있고 설치가 올바르게 되었는지 
확인하려면 `$ git pu`까지 입력한 후 <Tab>키를 2번 눌러 자동완성이 되는지 
확인합니다.  

## Problem
제대로 동작하지 않는다면 Git을 최신버전으로 업데이트 해야합니다. 
```
$ brew install git
```

`.bash_profile`에서 `.bashrc`를 불러오지 않는다면 `.bash_profile`에 아래의 내용
을 추가합니다.
```
source  ~/.bashrc
```
## See also
https://git-scm.com/book/ko/v1/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%ED%8C%81%EA%B3%BC-%ED%8A%B8%EB%A6%AD
