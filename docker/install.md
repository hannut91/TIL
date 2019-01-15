# Docker install on macOS

Docker를 맥os에 설치하는 방법

## Install

* https://hub.docker.com/editions/community/docker-ce-desktop-mac에서
  `stable`버전을 다운로드 받습니다.
* 다운받은 파일로 설치합니다.
* `Docker`를 실행합니다.
* `Docker`를 실행하면 화면 오른쪽 상단에 아이콘이 생깁니다.

```bash
docker version
```

## CLI

### Shell completion

* bash shell에서 자동완성을 사용하려면 다음을 터미널에서 입력하세요.

```bash
etc=/Applications/Docker.app/Contents/Resources/etc
ln -s $etc/docker.bash-completion $(brew --prefix)/etc/bash_completion.d/docker
ln -s $etc/docker-machine.bash-completion $(brew --prefix)/etc/bash_completion.d/docker-machine
ln -s $etc/docker-compose.bash-completion $(brew --prefix)/etc/bash_completion.d/docker-compose
```

* 그 후 다음을 `~/.bash_profile`에 삽입합니다.

```bash
[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion
```

* 혹은 다음과 같이 입력합니다.

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
. $(brew --prefix)/etc/bash_completion
fi
```

## Sources

* https://docs.docker.com/docker-for-mac/
