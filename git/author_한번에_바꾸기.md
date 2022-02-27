# 한번에 깃헙 author 바꾸기

옛날에 github desktop을 이용해 협업을 했을 때, author가 이상하게 들어가 잔디가 안 심겨지는 불상사가.. 일어났었다 ..

filter-branch를 이용하면 금방이다 ~

```bash
$ git filter-branch --commit-filter '
        if [ "$GIT_AUTHOR_EMAIL" = "wook@iugchang-ui-MacBookPro.local" ];
        then
                GIT_AUTHOR_NAME=wook95
                GIT_AUTHOR_EMAIL=uclee95@gmail.com
                git commit-tree "$@";
        else
                git commit-tree "$@";
        fi' HEAD
```

eval 코드를 실행한다.  
then 안에 있는 `GIT_AUTHOR_NAME`에 문자열이라고 쌍따옴표를 넣어주거나, 세미콜론을 넣어주었을땐 오류가 났다.

filter-branch는 한번에 수정 뿐아니라 한번에 지우기도 가능하다.
