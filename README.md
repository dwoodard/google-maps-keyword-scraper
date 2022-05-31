# mv3-vue-chrome-extension-template
![demo](./demo.gif)
modern chrome-extension development template

Support 
- [x] Manifest V3
- [x] Vue3
- [x] Typescript
- [x] Hot Reload


# Quick Start 

## Install
```
git clone https://github.com/munron/mv3-vue-chrome-extension-template.git
cd mv3-vue-chrome-extension-template
npm install
npm run build
mv .env.sample .env
```

## Fix Extension ID

#### Open `chrome://extensions`
#### Click Pack Extension
#### Click `Browse` and select `dist` folder
`dist.crx` and `dist.pem` are generated.
  
![](https://gyazo.com/20b05012fc8d0bb3c4a82d016de08e3a/max_size/1000)

#### Edit `.env`
Copy private key from `dist.pem` and paste to `VUE_APP_MV3_KEY` 

```txt:.env
VUE_APP_FIREBASE_APIKEY=XXXXXXXX
VUE_APP_FIREBASE_AUTHDOMAIN=XXXXXXXX
VUE_APP_FIREBASE_PROJECTID=XXXXXXXX
VUE_APP_FIREBASE_STORAGEBUCKET=XXXXXXXX
VUE_APP_FIREBASE_MESSAGINGSENDERID=XXXXXXXX
VUE_APP_FIREBASE_APPID=XXXXXXXX
VUE_APP_MEASUREMENTID=XXXXXXXX
VUE_APP_OAUTH2_CLIENT_ID=XXXXXXXX
VUE_APP_MV3_KEY="-----BEGIN PRIVATE KEY-----\nXXXXX.....XXXXXX\n....\nXXXXXX.....XXXXXXX\n-----END PRIVATE KEY-----"
```

## Setup Firebase

#### Create New Project
[https://console.firebase.google.com](https://console.firebase.google.com)

#### Copy Firebase Configuration to `.env`

```js
const firebaseConfig = {
   apiKey: "XXX",
   authDomain: "XXX",
   projectId: "XXX",
   storageBucket: "XXX",
   messagingSenderId: "XXX",
   appId: "XXX",
   measurementId: "XXX"
};
```

#### Add Google to Sign-in provider in
![](https://gyazo.com/f5d3251d81f756b7dee16889d5f0b742/max_size/1000) 

#### Add `chrome-extension://{Chrome Extension ID}`
![](https://gyazo.com/a395f349088ab6663dadb32dabfd3efc/max_size/1000)

## Setup Google Cloud Platform

#### Open [https://console.cloud.google.com/](https://console.cloud.google.com/)

#### Open API&Service → Credential → +CREATE CREDENTIALS →　OAuth Client ID

#### Select Chrome App, fill Name and Application ID (Chrome Extension ID)
![](https://gyazo.com/aabef1b96183786de8b3bcaec2b0fea3/max_size/1000)

#### Edit `.env`.
Copy Your Client Id to `VUE_APP_OAUTH2_CLIENT_ID` 
![](https://gyazo.com/2f2c830cd7d38aafe4b9887c7d338a13/max_size/1000)

#### Edit `rollup.config.js`.
Uncomment oauth2 settings.

```js
chromeExtension({
  extendManifest: {
    "oauth2": {
      "client_id": process.envVUE_APP_OAUTH2_CLIENT_ID,
      "scopes": [
        "https://www.googleapis.com/authuserinfo.email",
        "https://www.googleapis.com/authuserinfo.profile"
      ]
    },
    "key": process.env.VUE_APP_MV3_KEY
  }
}),
```

## Build
`npm run build`

## Hot reload
`npm run dev`
