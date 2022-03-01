## 포크한 레포 잔디 심기

```bash
$ git clone --bare 복사할git저장소주소
$ cd 복사할git저장소주소.git
$ git push --mirror 새로운git저장소주소 // github에서 새로 레포를 만들어 줘야 한다
$ git remote set-url origin 새로운git저장소주소
```

1. bare 옵션으로 클론
2. mirror 옵션으로 푸쉬
3. 리모트 연결

위와 같이 진행하면, 이전의 커밋기록, 브랜치등을 유지한 채로, 새로운 레포가 origin이 되어 잔디를 심을 수 있다.
