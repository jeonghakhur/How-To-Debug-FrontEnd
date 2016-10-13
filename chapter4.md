4. 하이브리드 앱 디버깅 방법
-------------------------

하이브리드 앱 디버깅 방법에 앞서 모바일 애플리케이션을 개발하는 방식에 따라 구분하는 네이티브 앱, 웹 앱, 하이브리드 앱의 기본 개념을 이해애야 합니다. 웹앱의 경우는 모바일 기본 브라우저에서 실행을 하거나 크롬 브라우저를 통해 접속하게 되며, 하이브리드 앱은 웹뷰를 통해 콘텐츠를 확인하게 됩니다. 여기서 중요한 것은 모바일 기본 브라우저와 웹뷰가 webkit 버전이 다르며, 삼성과 같은 경우는 브라우저 성능 개선을 위해 Chrominu을 기반으로 SBrowser를 만들었고 갤럭시 S3 ~ 갤럭시 S4에 기본 브라우저로 탑재하였습니다. 그로 인해 다양한 버그가 존재하고 랜더링 성능에도 차이가 있습니다.

이런 현상을 브라우저 파편화라고 말하며 이를 개선하기 위해 Google에서는 Andorid 4.4(Kitkat) 버전부터 Chrominum을 Android의 기본 브라우저로 탑재였으나 삼성의 갤럭시 S4는 SBrowser를 기본 브라우저로 사용하고 있습니다.

> 모바일 웹 개발이나 하이브리드 앱 개발시 디바이스의 지원 범위를 Android는 4.4(Kitkat) 이상으로 협의하는 것을 권장합니다.

**네이티브 앱**

모파일 플랫폼 API를 이용해 개발하는 앱을 말합니다. 디바이스의 저장된 연락처, 파일 등의 고유 정보를 사용할 수 있으며, 카메라, 가속도계 등의 하드웨어도 사용할 수 있습니다. 웹앱이나 하이브리드 앱에 비해 개발 난이도가 높으며 OS 및 디바이스 해상도 별로 개발해 높은 개발 비용이 필요합니다. 높은 사양의 그래픽과 다양한 기능이 필요한 경우에 적합합니다.

> 애플리케이션 프로그래밍 인터페이스(API) 모바일 기기에 네이티브 앱을 설치하고 실행하면, 앱은 모바일 운영체제에서 제공하는 전용 API를 호출해 디바이스의 하드웨어를 제어할 수 있습니다.

**웹 앱**

웹 앱은 사용자가 모바일 디바이스에서 검색이나 브라우저의 주소창에 직접 웹 주소를 입력해 사용하는 인터넷 서비스를 말합니다. HTML, CSS, 자바스크립트를 사용해 만들어진 애플리케이션으로 네이티브 앱과 같은 사용자 인터페이스를 제공해 모바일 디바이스에서 사용성을 높일 수 있습니다. 스마트폰의 홈에 아이콘을 위치시켜 마치 네이티브 앱처럼 아이콘을 클릭할 때 앱이 실행되도록 할 수 있습니다. 웹 앱의 장점은 멀티 플랫폼을 지원하는 것과 개발 비용이 적게 든다는 것입니다. 그러나 모바일 플랫폼 API를 사용할 수 없고, 브라우저 API만 사용가능합니다.

**하이브리드 앱**

하이브리드 방식은 네이티브 개발과 웹 개발 방법을 혼합한 것입니다. WebView를 이용해 웹 콘텐츠를 표현할 수 있도록 하고 모바일 플랫폼 API를 이용해 모바일의 고유 정보를 이용할 수 있고 하드웨어를 제어할 수도 있습니다. 코드도바와 같은 하이브리드 앱 제작 도구를 사용하면 자바스크립트로 모바일 플랫폼 API을 연결해 모바일의 고유 정보를 사용할 수 있으며 하드웨어도 제어 가능합니다.

하이브리드 앱의 WebView에서 보여지는 콘텐츠는 서버에 올려놓은 파일이 될 수도 있고, 애플리케이션의 포함되어 디바이스의 로컬에 저장되는 파일이 될 수도 있습니다. 두 방식 모두 각각 장단점이 있습니다. 서버에 올려놓은 파일은 앱스토어에서 규정하는 승인, 배포, 보안 규칙에 상관없이 앱을 업데이트할 수 있습니다. 하지만 이 방식은 디바이스가 네트워크에 연결되어있지 않으면 콘텐츠에 액세스 할 수 없어 앱 사용이 불가능하고 네트워크 접속 환경에 따라 콘텐츠 이용 속도가 결정됩니다. 반면 애플리케이션에 포함되어 있는 파일의 경우는 성능과 속도를 높일 수 있지만 원격 업데이트가 불가능합니다. 모바일 디바이스의 캐시를 사용해 두 가지 기능을 결합하여 사용할 수도 있습니다.

**네이티브 앱 VS 하이브리 앱**

네이티브 방식은 성능과 디바이스의 고유 자원 및 하드웨어 제어가 가능하지만 높은 개발 비용과 업데이트 문제가 단점입니다. 웹 방식은 상대적으로 간단하고 비용이 적게 들며 업데이트가 쉽지만, 기능상 제한이 따르므로 플랫폼 API 사용하여 제공할 수 있는 우수한 사용자 환경을 제공하기 어렵습니다. 하이브리드 방식은 이 두 방식의 절충안으로 크로스 플랫폼을 지원하고 개발 비용을 절감하기 위해 선호되는 방식입니다.

네이티브 앱 개발 방식에서도 WebView를 사용하는 경우가 많아 네이티브, 하이브리드 앱의 경계를 명확히 구분하는 것은 경우에 따라 큰 의미가 없는 일이 되기도 합니다. WebView로 제공되는 콘텐츠를 어느 정도 사용할 것인지에 따라 개발 방식을 선택하는 것이 바람직할 것입니다.

https://cordova.apache.org/docs/ko/latest/guide/overview/index.html

### 4.1. Cordova 설치

[Cordova](https://cordova.apache.org/docs/ko/latest/guide/overview/index.html)는 크로스 플랫폼 개발을 지원하는 하이브리드 프레임워크입니다. cordova를 설치해 모바일 디바이스에 앱을 설치하고 WebView를 통해 작업 결과물을 확인하고 디버깅하는 방법에 대해 설명합니다.

> 이 문서는 windows 개발환경에서 android 디바이스에 대한 디버깅 방법만을 설명합니다.

**설치**

```bash
npm install -g cordova
```

**응용 프로그램 만들기**

```bash
cordova create hello com.example.hello HelloWorld
```

**플랫폼 추가**

```bash
cd hello
cordova platform add android
```

**응용 프로그램 빌드**

```bash
cordova build android
```

**앱 설치 및 실행**

```bash
cordova run android
```

### 4.2. 환경설정

#### 4.2.1. cordova-plugin-whitelist 플러그인 설정

cordova 프로젝트를 생성하면 기본적으로 설치되는 보안설정을 위한 플러그인으로 외부 자원(이미지, XHR, 기타 등등)에 대한 허용과 외부 링크 허용을 설정할 수 있습니다. 그리고 외부 링크는 WebView에서 보여줄지 새창으로 보여줄지를 결정할 수 있습니다. 기본 설정 값이 http(s)로 시작하는 주소는 새창으로 열리게 설정되어 있는데 프로젝트를 진행하다 보면 http(s)로 시작하는 주소를 WebViwe에서 열어야 할 때도 있을 것입니다. 상황에 따라 설정 파일을 수정해 프로젝트에 반영해 주시면 됩니다.

프로젝트의 홈 디렉토리의 `config.xml`을 수정해 설정 값을 변경할 수 있습니다.

**Navigation Whitelist**

외부 링크의 허용과 링크를 웹뷰에서 오픈할 수 있도록 설정합니다.

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

**Intent Whitelist**

외부 링크의 허용과 링크를 새창으로 오픈할 수 있도록 설정합니다.

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

**Network Request Whitelist**

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

#### 4.2.2. 폰트 크기 설정

안드로이드 디바이스의 경우 시스템 설정의 글자 크기에 따라 CSS의 글자 크기가 상대적으로 반영되어 원하는 결과가 나오지 않습니다. CSS 글자 크기 설정이 시스템의 글자 크기 설정 보다 우선하여 반영되도록 수정해야 합니다.

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

### 4.3. 디버깅 방법

작업자의 PC가 외부에서 접속 가능한 아이피를 가지고 있는 경우라면 로컬 서버를 구동해 보다 편리하게 디버깅할 수 있습니다. 그렇지 않은 환경이라면 애플리케이션에 작업파일을 포함해 디바이스에 빌드하여 디버깅해야 합니다.

#### 4.3.1. 외부 접속이 가능한 경우

애플리케이션의 홈 디렉토리에 있는 `config.xml`의 `<content>` 태그의 속성에 작업자의 로컬 서버 접속 정보를 입력합니다. 로컬 서버의 접속 URL은 `localhoat:3000`번이 아닌 아이피를 입력해 주어야 합니다.

> 이 방법으로 디버깅 작업을 진행하기 위해서는 [PC 웹 애플리케이션 디버깅](chapter2.md)을 위한 프로그램이 설치되어 있어야 합니다.

```xml
...
<content src="http://210.16.216.126:3000" />
<plugin name="cordova-plugin-whitelist" spec="1" />
<access origin="*" />
<allow-intent href="http://*/*" />
<allow-intent href="https://*/*" />
...
```

로컬 파일 수정시 WebView가 갱신될 수 있도록 livereload.js 파일의 경로도 수정해 줍니다.

```html
<script src="http://210.16.216.126:3001/livereload.js"></script>
```

**디버깅 실행 순서**

1.	grunt로 로컬 웹 서버 구동
2.	PC와 디바이스 USB 연결
3.	명령창에 'adb devices' 실행
4.	코르도바 애플리케이션 설치 위치로 이동
5.	명령창에 `cordova run android` 실행
6.	크롬 주소창에 `chrome://inspect/#devices` 입력

#### 4.3.2. 외부 접속이 되지 않는 경우

외부 접속이 되지 않는 환경일 경우 애플리케이션에 작업 파일을 포함해 디바이스에 애플리케이션을 설치해 디버깅 작업을 진행해야 합니다. 파일을 수정한 경우 매번 애플리케이션을 설치해야 되는 불편함이 있습니다.

애플리케이션의 홈 디렉토리에 있는 `config.xml`의 `<content>` 태그의 속성에 작업자의 로컬 파일 경로를 입력합니다. 로컬 파일은 홈 디렉토리의 www 폴더에 위치해야 합니다.

```xml
...
<content src="index.html" />
<plugin name="cordova-plugin-whitelist" spec="1" />
<access origin="*" />
<allow-intent href="http://*/*" />
<allow-intent href="https://*/*" />
...
```

**디버깅 실행 순서**

1.	PC와 디바이스 USB 연결
2.	명령창에 'adb devices' 실행
3.	코르도바 애플리케이션 설치 위치로 이동
4.	명령창에 `cordova run android` 실행
5.	크롬 주소창에 `chrome://inspect/#devices` 입력

-----

#### 정리하며

현재 사용되고 있는 모든 모바일 디바이스에 서비스를 제공해 사용자의 접근성을 높이는 일이 우선 되어야 합니다. 하지만 현실적으로 개발의 비용과 개발의 시간의 문제가 있어 타협이 필요할 수 있습니다. 또한 최신 기술을 오래된 디바이스에서 서비스할 수 없는 경우도 있을 것입니다. 그러므로 디바이스의 지원 범위를 적절하게 판단하고 협의하여 프로젝트를 시작하는 것이 중요할 것입니다.
