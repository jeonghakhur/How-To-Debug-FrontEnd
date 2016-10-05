## 2. PC 웹 애플리케이션 디버깅

사전 준비를 통해서 express 프레임워크를 사용해 웹 서버를 구동시키는 방법에 대해서 살펴보았습니다. 그렇다면 이제부터 파일을 웹 서버로 전송해 확인할 필요 없이 바로 로컬 웹 서버에서 작업물을 저장하고 확인하시면 됩니다.

그리고 grunt의 watch 테스크를 이용해 js, css, html, images 등의 파일이 수정되거나 신규로 작성되었을 경우 웹 서버가 변경사항을 확인해 브라우저를 자동으로 갱신해 작업자가 브라우저를 갱신하는 수고를 덜어 줄 수 있습니다.

### 2.1. watch 태스크 설정

다음은 generator express로 express를 설치했을때 생성되는 gruntfile.js의 watch 태스크 내용입니다. `bin/www`, `app.js `, `routes/*.js` 파일이 변경되면 서버를 재 시작하는 태스크를 수행하며, `js`, `css`, `views`에 해당하는 파일이 변경되면 livereload 서버에 변경을 알림을 보냅니다.

```js
watch: {
  options: {
    nospawn: true,
    livereload: reloadPort
  },
  server: {
    files: [
      'bin/www',
      'app.js',
      'routes/*.js'
    ],
    tasks: ['develop', 'delayed-livereload']
  },
  js: {
    files: ['public/js/*.js'],
    options: {
      livereload: reloadPort
    }
  },
  css: {
    files: [
      'public/css/*.css'
    ],
    options: {
      livereload: reloadPort
    }
  },
  views: {
    files: ['views/*.ejs'],
    options: {
      livereload: reloadPort
    }
  }
}
```
html 파일의 변경 사항을 서버에 전달하려면 아래와 같이 작성하시면 되며, html 폴더의 하위 모든 폴더 및 파일의 변경 사항을 확인하려면 `public/html/**/*.html` 형식으로 작성하시면 됩니다.

```js
hmtl: {
  files: ['public/html/**/*.html'],
  options: {
    livereload: reloadPort
  }
}
```
watch 태스크에 대하여 더 자세히 알아보려면 grunt-contrib-watch(<https://github.com/gruntjs/grunt-contrib-watch>)에서 확인하세요.

### 2.2. livereload.js

livereload 서버에 변경된 사항이 있다면 웹 소켓을 통해 클라이언트 브라우저에 변경된 알림을 회신하게 됩니다. livereload.js는 변경된 알림을 수신받게 되면 브라우저를 자동으로 갱신하는 기능을 담당하게 됩니다.

html 파일에서 liverelaod.js를 사용하려면 `<head>` 태그안에 livereload.js 파일을 임포트해 사용하게 됩니다.

```html
<head>
...
<script src="http://localhost:35729/livereload.js"></script>
</head>
```

livereload와 비슷한 기능을 하는 browersync(<https://www.browsersync.io>)에 대해서도 한 번 살펴보세요.

### 2.3. HTML 파일 작성

정적 파일의 위치는 `app.js`파일에 정의되어 있으며, 기본 값이 `public` 폴더입니다. 정적 파일 위치는 수정 및 추가가 가능하므로 사용자의 환경에 맞춰 변경해 사용하시면 됩니다.

public 폴더의 구조는 다음과 같습니다.

```bash
public/
├── components/
├── css/
├── img/
└── js/  
```

정적 파일의 위치 변경 및 추가는 프로젝트 홈 디렉터리의 `app.js` 파일의 [express.static](http://expressjs.com/ko/starter/static-files.html) 미들웨어에서 설정합니다.

```js
app.use(express.static(path.join(__dirname, 'public')));
```

public 폴더에 html이라는 폴더를 만들고 그 안에  sample.html 파일을 생성해 `livereload.js`를 임포트합니다.


### 2.4. 웹 서버 실행

명령창을 열고 `grunt`를 입력합니다. 별다른 오류가 있지 않다면 다음과 같은 내용을 확인할 수 있습니다.

```
grunt
Running "develop:server" (develop) task

[grunt-develop] > started application "bin/www".
Running "watch" task
Waiting...

[grunt-develop] > Express server listening on port 3000
```

> 웹 서버를 중지하려면 명령창에서 Ctrl+C를 입력하면 됩니다.

브라우저를 열고 `http://localhost:3000/html/sample.html`으로 접속해 생성한 파일을 확인해 보세요. sample.html을 편집기에서 수정해 보고 watch 태스크에서 설정한 경로에 있는 파일들도 수정해 보면서 브라우저가 수정 내용을 즉시 반영하는지 확인해 보세요.

---------------------
#### 정리하며

우리는 이 작업을 통해 하루에도 수 없이 많이 진행되는 반복적인 작업과 낭비하는 시간을 보상받을 것입니다. 이 작업은 PC웹 디버깅에서만 사용되는 것이 아니라 모바일 디바이스에도 적용 가능합니다. 모바일 디바이스에서 실시간으로 작업물을 디버깅할 수 있다는 부분은 상당히 매력적인 작업 방법입니다. 다음 장에서는 모바일 디버깅 방법에 대해서 설명할 것입니다.
