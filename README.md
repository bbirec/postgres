Postgres 제대로 사용하기
--------------------
Postgres를 좀 더 제대로 사용하기 위한 정보 및 팁을 포스팅하는 블로그 이다.
Static site generator인 `hugo`를 이용하고, 글은 Markdown으로 쓴다.

## Hugo 설치

### Hugo
```
$ brew update && brew install hugo
```

### 테마 설치
```
$ mkdir themes
$ cd themes
$ git clone --depth 1 https://github.com/jbub/ghostwriter
```

## 글쓰기
아래와 같이 `hugo`를 켜면 자동으로 웹서버가 켜지고 그 결과를 브라우져로 확인 할 수 있다.
markdown파일이 바뀌면 자동으로 로딩되기 때문에 새로고침 할 필요없다.

```
$ hugo server --buildDrafts
```


## Github page로 deploy
TODO
