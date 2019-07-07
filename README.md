# browser-speaker-sample
ブラウザで文字列を発話させる時のサンプル。  
日本語のみ対応。  
herokuにアップロードしているので、[こちら](https://desolate-ravine-29849.herokuapp.com)からも確認できる。

## 既知の問題
- pitch(速度)は最大10となっているが、MacのChromeだと3.6を超えたあたりでうまく動かないので3.5までにしている。
- `speechSynthesis.getVoices();` で値が取れるようになるのに時間がかかることがある。取れなくてもデフォルトで日本語になっているので妥協しているが、プロダクトで使うなら呼べるようになるまでwait処理を入れるべき。
- vuetifyを使いこなせていない感が半端ない。

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
