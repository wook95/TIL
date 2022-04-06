# 리액트 네이티브와 firestore 연동시 unknown 오류

오류 내용

<br>

```bash
 Possible Unhandled Promise Rejection (id: 0):
Error: [storage/unauthorized] User is not authorized to perform the desired action.
NativeFirebaseError: [storage/unauthorized] User is not authorized to perform the desired action.
get@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:125843:42
@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:28967:25
invoke@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:24005:39
@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:24026:19
tryCallTwo@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:28654:9
doResolve@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:28818:25
Promise@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:28677:14
callInvokeWithMethodAndArg@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:24025:33
enqueue@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:24030:157
@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:24045:69
_callee@http://localhost:8081/index.bundle?platform=ios&dev=true&minify=false&modulesOnly=false&runModule=true&app=org.reactjs.native.example.wooksPublicGallery:124954:40

```

<br>

## 해결

**파이어베이스 콘솔의 파이어스토어 rules에서, 데이터베이스 생성이 금지되어 있어서 난 에러였다**  
파이어스토어를 쓰기 위해 생성한 `reference`와 관련된 메소드에 문제가 있어, 많은 시도를 통해 코드에는 문제가 없다는것으로 잠정결론을 내리고 콘솔을 들어와보니, 규칙이 있어 검색하고 해결했다.

<br>

전

쓰기가 금지되어있다.

```json
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if false;
    }
  }
}
```

<br>

후

쓰기를 풀어주었다.

```json
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read, write: if true;
    }
  }
}
```
