<div align="center">

![top](https://user-images.githubusercontent.com/26512984/173287314-ba3b8d9b-6303-4e20-93de-cc82f2bfce3a.png)

  <h1>Web Push | Getting Started</h1>

[Show article](https://geundung.dev/114)

</div>

## Project

```
.
├── README.md
├── config
│   └── default.example.json
├── css
│   └── common.css
├── index.html
├── login.html
├── package.json
├── src
│   ├── 💻 server
│   │   ├── constants.ts
│   │   ├── logger.ts
│   │   ├── middlewares.ts
│   │   ├── server.ts
│   │   └── types.ts
│   └── 🌍 web
│       ├── index.ts
│       └── service-worker.ts
├── tsconfig.json
├── tsconfig.server.json
├── tsconfig.web.json
└── yarn.lock
```

- Server
  - [src/server/server.ts](https://github.com/leegeunhyeok/web-push/blob/main/src/server/server.ts): server entry code
- Web page
  - [src/web/index.ts](https://github.com/leegeunhyeok/web-push/blob/main/src/web/index.ts): page script
  - [src/web/service-worker.ts](https://github.com/leegeunhyeok/web-push/blob/main/src/web/service-worker.ts): service worker script

## Setup

- Pre-requirements
  - > = Node 16
  - yarn
    ```bash
    npm i -g yarn
    ```
- create vapid key pairs
  ```bash
  yarn generate-vapid-keys
  ```
- create `config/default.json` (check config/default.example.json)
  ```json
  {
    "gcmKey": "GCM API Key HERE",
    "subject": "mailto:your@domain.com",
    "vapid": {
      "public": "PUBLIC KEY HERE",
      "private": "PRIVATE KEY HERE"
    }
  }
  ```
  - How to get GCM API key?
    - Visit [Google Firebase Console](https://console.firebase.google.com) and create project
    - Open Project > Project settings > Cloud Messaging
    - Cloud Messaging API > `Server Key`
- setup project

  ```bash
  # Install dependencies
  yarn

  # Build scripts (TS -> JS)
  yarn build

  # Start demo server
  yarn start
  ```

Done! visit [http://localhost:8080](http://localhost:8080)

## Preview

![main](https://user-images.githubusercontent.com/26512984/173250652-cdc843de-8c1c-4220-838c-40815189af26.png)

![notification](https://user-images.githubusercontent.com/26512984/173250678-a88651b4-87c5-4f62-b8d2-bdf625e0ac5b.png)

## Error

1. yarn generate-vapid-keys

- 'generate-vapid-keys'를 찾을 수 없다고 나옴
  > > > npx web-push generate-vapid-keys [--json]

2. No license field

- yarn start 시 'warning package.json: No license field' 에러메시지 발생
  > > > package.json 파일에 "private": true, 를 추가

3. 알림이 오지 않는 경우
   3.1) 브라우저 설정
   > > > 브라우저(크롬) '설정' > 개인 정보 보호 및 보안 > 사이트 설정 > 권한 > 알림 > '알림 전송이 허용됨' 내 해당 웹의 URL이 등록되어있는지 확인

3.2) 맥OS 설정

> > > 시스템 설정 > 알림 > Google Chrome > '알림 허용'

4. Error: Configuration property "gcmKey" is not defined

- /config/default.example.json 내 gcmKey값을 못 읽는 상태인데 해당파일 자체를 못 읽고 있었음
  > > > /dist/sever/constatns.js 내 해당 변수를 읽는 부분에 값을 강제 주입

## From

https://geundung.dev/114#google_vignette
