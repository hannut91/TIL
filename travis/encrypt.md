# Travis CI Encrypt

Tavis CI 환경변수 사용시 암화하 하기

## Install

```bash
$ gem install travis
```

## Login

`travis.com`을 사용한다면

```bash
$ travis login --pro
```

## Encrypt

```bash
$ travis encrypt --com ENV_NAME="ENV_VALUE" -r owner/repo --add
```

.travis.yml에 암호화된 환경변수가 추가된 것을 확인할 수 있습니다. 이 암호화한
변수는 레포를 소유한 소유자가 올린 pull request에서 동작하는 Travis CI에서만
접근할 수 있습니다. 즉 fork한 repo에서는 해당 환경변수를 사용할 수 없습니다.
보안상의 이유로 그러한데 만약 repo주인이 민감한 정보가 있어서 환경변수를
사용하여 암호화하여 travis.yml을 작성하였는데 다른 사람이 fork를 떠서 echo
$env처럼 환경변수를 출력해 볼 수 있다면 민감한 정보가 노출 될 수 있기
때문입니다.

## Sources

* <https://docs.travis-ci.com/user/best-practices-security/#Steps-Travis-CI-takes-to-secure-your-data>
