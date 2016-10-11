## 4. 하이브리드 앱 애플리케이션 디버깅

네이티브앱

모파일 플랫폼 API를 이용해 개발하는 앱을 말합니다. 디바이스의 저장된 연락처, 파일 등의 고유정보를 사용할 수 있으며, 카메라 등의 하드웨어도 사용할 수 있습니다. 웹앱이나 하이브리드앱에 비해 개발 난이도가 높으며 OS 및 디바이스 해상도 별로 개발해 높은 개발 비용이 필요합니다. 높은 사양의 그래픽과 다양한 기능이 필요한 경우에 적합합니다.

웹앱

HTML, CSS, 자바스크립트를 사용해 만들어진 애플리케이션을 말합니다. 사용자가 직접 모바일 브라우저의 주소 창에 웹 주소를 입력해 사용하는 인터넷 서비스도 웹앱의 범주에 속하게 됩니다. 사용자가 웹사이트의 주소를 입력하게 하지 않고 스마트폰의 홈에 아이콘을 위치시켜 마치 네이티브앱처럼 아이콘을 클릭할 때 앱이 실행되도록 할 수도 있고 태그로 브라우저 주소 입력창 등을 숨길 수도 있어 겉모습과 동작 과정을 네이티브앱처럼 보이게 할 수도 있습니다.

하이브리드앱

WebView를 이용해 웹 콘텐츠를 표현할 수 있도록하고 네이티브 API를 이용해 모바일의 고유정보를 이용할 수 있고 하드웨어를 제어할 수도 있습니다. 네이버앱 다음앱이 하이브리드 앱이라고 할 수 있습니다. 코드도바와 같은 크로스 플랫폼 모바일 앱 제작 도구를 사용해 자바스크립트 API로 모바일의 고유정보 및 하드웨어 등을 사용할 수도 있습니다.

네이티브앱과 하이브리앱 개발 방식의 선택

네이티브앱 개발 방식에서도 WebView를 사용하는 경우가 많아 네이티브, 하이브리드앱의 경계를 명확히 구분하는 것은 경우에 따라 큰 의미가 없는 일이 되기도 합니다.  WebView로 제공되는 콘텐츠를 어느정도 사용할 것인지에 따라 개발 방식을 선택하는 것이 바람직할 것입니다.



<https://cordova.apache.org/docs/ko/latest/guide/overview/index.html>
### 코르도바 설치

```bash
npm install -g cordova
```

### 응용 프로그램 만들기

```bash
cordova create hello com.example.hello HelloWorld
```

### 플랫폼 추가

```bash
cd hello
cordova platform add android
```

### 응용 프로그램 빌드

```bash
cordova build
```

#### 플랫폼에 따라 빌드 범위 제한

```bash
cordova build android
```

#### 컴퓨터에 휴대폰을 연결 하 고 직접 응용 프로그램을 테스트

```bash
cordova run android
```

### 환경설정



#### cordova-plugin-whitelist 플러그인 설정

cordova에서 지원하는 보안설정을 위한 플러그인 입니다.

#### Navigation Whitelist

App의 WebView가 이동할 수 있는 URL을 통제할 수 있습니다. Top-level 네비게이션에만 적용할 수 있습니다. 안드로이드에서는 Http(s) 스킴이 아닌 iframe에도 적용됩니다.

기본적으로 네비게이션은 file:// URL만 허용하도록 정의됩니다. 다른 URL을 허용하기 위해서는 <allow-navigation> 태그를 config.xml에 추가해야합니다.

```xml
<!-- example.com 링크를 추가합니다. -->
<allow-navigation href="http://example.com/*" />

<!-- 프로토콜, 호스트 접두사, 접미사에 와일드카드를 적용할 수 있습니다. -->
<allow-navigation href="*://*.example.com/*" />

<!-- 모든 네트워크, 프로토콜에 대해 허용하기 위해서는 아래를 사용합니다. (보안 상 권장하지 않음) -->
<allow-navigation href="*" />

<!-- 위의 *은 아래 3줄의 선언과 동일합니다. -->
<allow-navigation href="http://*/*" />
<allow-navigation href="https://*/*" />
<allow-navigation href="data:*" />
```

#### Intent Whitelist

시스템에 요청 가능한 URL을 통제할 수 있습니다. config.xml에서 다음과 같이 <allow-intent>를 설정하세요.

```xml
<!-- 브라우저에서 웹페이지로의 모든 http, https링크를 열수 있도록 허용합니다. -->
<allow-intent href="http://*/*" />
<allow-intent href="https://*/*" />

<!-- example.com 링크가 브라우저에서 열리도록 허용합니다. -->
<allow-intent href="http://example.com/*" />

<!-- 프로토콜, 호스트 접두사, 접미사에 대해 와일드카드를 적용할 수 있습니다. -->
<allow-intent href="*://*.example.com/*" />

<!-- SMS 링크가 메시징 앱을 열수 있도록 허용합니다. -->
<allow-intent href="sms:*" />

<!-- 전화번호 유형의 링크가 전화를 걸 수 있도록 합니다. -->
<allow-intent href="tel:*" />

<!-- 지도의 좌표를 나타내는 링크가 맵을 열수 있도록 허용합니다. -->
<allow-intent href="geo:*" />

<!-- 모든 유형의 URL을 허용합니다. 즉, 모든 URL이 모든 유형의 앱을 실행할 수 있습니다. (보안 상 권장되지 않음) -->
<allow-intent href="*" />
```

#### Network Request Whitelist

어떤 네트워크 유형(이미지, XHR, 기타 등등)을 허용할 지 통제할 수 있습니다. <access>태그를 설정하지 않으면, file:// URL만 허용됩니다. 그러나, 기본 Cordova Application에는 `<access origin="*">`이 포함되어 있습니다.

```xml
<!-- google.com의 이미지, XHR, 기타 등등의 네트워크 요청을 허용합니다. -->
<access origin="http://google.com" />
<access origin="https://google.com" />

<!-- maps.google.com의 하위 도메인에 대한 네트워크 요청을 허용합니다. -->
<access origin="http://maps.google.com" />

<!-- google.com의 하위 도메인에 대한 네트워크 요청을 허용합니다. -->
<access origin="http://*.google.com" />

<!-- content: URLs에 대한 요청을 허용합니다. -->
<access origin="content:///*" />

<!-- 모든 요청을 허용합니다. -->
<access origin="*" />
```

### 폰트 크기 설정

안드로이드 디바이스의 경우 시스템 설정의 글꼴 크기에 따라 CSS의 글꼴 크기가 상대적으로 반영됩니다. 그렇기 때문에 CSS의 설정 값에 따라 글꼴 크기가 반영되도록 수정해 주어야 합니다.

`\platforms\android\src\io\cordova\hellocordova\MainActivity.java` 파일 수정

```java
package com.example.hello;

import android.webkit.WebSettings;
import android.webkit.WebView;
import android.os.Bundle;
import org.apache.cordova.*;

public class MainActivity extends CordovaActivity
{
    @Override
    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        // Set by <content src="index.html" /> in config.xml
        loadUrl(launchUrl);
        WebView webView = (WebView) appView.getEngine().getView();
        WebSettings settings = webView.getSettings();
        settings.setTextZoom(100);
    }
}
```

### 디버깅 방법

WebView로 디버깅을 하기 위해서 [PC 웹 애플리케이션 디버깅](chapter4.md)을 위한 프로그램이 설치되어 있어야 합니다.

#### config.xml 수정

localhost는 PC의 로컬 서버 접속의 경로이므로 모바일 디바이스에서는 접근할 수 없습니다. 그렇기 때문에 모바일 디바이스에서 접근 가능한 주소가 필요합니다.
본인이 사용하고 있는 아이피 주소를 확인해 코드도바 애플리케이션 홈 디렉토리의 `config.xml`파일을 수정해 줍니다. `<content>` 태그의 속성값에 작성합니다.



```xml
...
<content src="http://210.16.216.126:3000" />
<plugin name="cordova-plugin-whitelist" spec="1" />
<access origin="*" />
<allow-intent href="http://*/*" />
<allow-intent href="https://*/*" />
...
```

#### livelorea.js 파일 경로 수정

로컬 파일 수정시 WebView가 갱신될 수 있도록 livereload.js 파일의 경로도 수정해 줍니다.

```html
<script src="http://210.16.216.126:3001/livereload.js"></script>
```
#### 디버깅 실행 순서

1. grunt로 로컬 웹 서버 구동
2. PC와 디바이스 USB 연결
3. 명령창에 'adb devices' 실행
4. 코르도바 애플리케이션 설치 위치로 이동
5. 명령창에 `cordova run android` 실행
5. 크롬 주소창에  `chrome://inspect/#devices` 입력
