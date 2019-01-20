# Git Branch

이미 Merge되었거나 더이상 사용되지 않는 branch들은 정리하는것이 좋습니다.

## 1. merge되어있는 branch 조회하기

```bash
git branch --merged
```

현재 checkout되어있는 branch는 merge와 상관없이  반드시 표시되니 주의해야 
합니다.

### remote에 있는 branch도 확인하고 싶다면

```bash
git branch -a --merged
```

## 2. merge되어있는 branch 삭제하기

```bash
git branch -d <branch-name>
```

만약 해당 branch가 merge되어 있지 않다면 삭제가 되지 않습니다. 그래도 강제로 
삭제하고 싶다면 다음과 같이 입력하여 삭제할 수 있습니다.

```bash
git branch -D <branch-name>
```

### merged된 브렌치들을 전부 지우고 싶다면

```bash
git branch -d $(git branch --merged | master)
```

## 3. Github에 업로드 되어있는 branch 삭제하기

다른 remote에 merge되어 더이상 나의 remote에 사용되지 않는 branch를 삭제하려면 
다음과 같이 입력합니다.

```bash
git push <remote-name> :<branch-name>
```

