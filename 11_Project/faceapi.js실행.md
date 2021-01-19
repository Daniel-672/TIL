### 윈도우 faceapi.js를 실행하기 위한 패키지들

```bash
# 카르마설치
npm install -g karma
npm install -g karma-typescript


# rollup설치 이건 패키지용으로 설치
npm install --save-dev rollup


# node-gyp.js설치
npm install --global node-gyp 

npm install --global --production windows-build-tools 


```



### - pm2실행

```bash
# server.js실행
C:\Users\Daniel\face-api.js\examples\examples-browser> pm2 start server.js

# pm2중지
pm2 kill      
```

