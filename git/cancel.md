# Git 취소하기

무언가를 잘 못했을 때는 되돌립시다.

## commit --amend 취소하기

새로운 commit을 해야하는데 --amend하는 경우가 있습니다.

1. `git reflog`를 통해 log를 불러옵니다.
2. 돌아가고자 하는 곳으로 `git reset --soft HEAD@{NUMBER}`리셋합니다.
3. 다시 커밋합니다.
