모바일 웹 애플리케이션 디버깅
-----------------------------

크롬과 크롬 확장 도구인 ADB 플러그인을 이용하여 로컬에서 작업한 파일을 Andriod 디바이스에 연결해 실시간으로 확인하고 디버깅하는 방법에 대해 살펴볼 것입니다. PC 웹 애플리케이션 디버깅 방법에서 살펴본 livereload 기능도 동일하게 사용할 수 있어 모바일 웹 애플리케이션 디버깅을 보다 손쉽게 할 수 있습니다.

### 사전 준비

Windows 개발환경에서 Android 모바일 디바이스에서 디버깅을 하기 위해 설치하고 설정해야 하는 목록은 다음과 같습니다.

1.	USB 드라이버 설치
2.	JDK 설치 및 환경변수 설정
3.	안드로이드 스튜디오 설치
4.	안드로이드 SDK 업데이트
5.	ADB 환경변수 설정
6.	ADB 플러그인 설치
7.	스마트폰 설정
8.	PC와 스마트폰 연결

#### USB 드라이버 설치

Windows 환경에서 개발하면서 테스트용으로 기기를 연결하고자 하는 경우, 연결하려는 디바이스에 맞는 드라이버를 설치해야 합니다.

- **참고 자료**<br>
삼성 통합 USB 드라이버 : <http://local.sec.samsung.com/comLocal/support/down/kies_main.do?kind=usb><br>
제조사별 USB 드라이버 : <https://developer.android.com/studio/run/oem-usb.html>

### 스마트폰 설정

스마트폰 설정 메뉴의 "개발자 옵션"에서 "USB 디버깅" 옵션을 선택해야지만 디바이스를 PC에 연결해 디버깅을 할 수 있습니다. 디바이스 마다 USB 디버깅 옵션을 선택하는 방법이 차이가 있을 수 있습니다.

**갤럭시 S4 - USB 디버깅 모드 사용 방법**

1. 환경설정
2. 더보기
3. 디바이스 정보
4. 빌드번호(7회에서 9회 정도 연속으로 터치하면 개발자 옵션 활성)
5. 디바이스 정보(상위 메뉴로 이동)
6. 개발자 옵션
7. USB 디버깅(항목 체크)

### JDK 설치 및 환경변수 설정

JDK(Java Development Kit)는 자바 프로그램의 개발을 위한 소프트웨어와 라이브러리 모음입니다.
Oracle 홈페이지(<https://www.oracle.com/index.html>)에 접속해 사용자의 OS 환경에 맞는 JDK를 다운로드하여 설치합니다.

JDK 설치를 완료하였다면 자바 프로그램을 시스템 어느 곳에서든 실행할 수 있도록 환경변수를 설정해 주어야 합니다. 우선 JDK 설치 경로를 복사합니다. 설치 시 디렉터리를 변경하지 않았다면 `C:\Program Files\Java\jdk1.7.0_79\bin`에 설치가 되었을 것입니다. 아래의 순서에 따라 이동하면 환경변수 편집창을 열수 있습니다.

1. 제어판
2. 시스템
3. 고급 시스템 설정
4. 환경변수
5. 시스템 변수

시스템 변수의 Path 항목을 선택한 후 편집 버튼을 클릭해 시스템 변수 편집창을 열어 복사한 JDK 설치 경로를 텍스트의 끝에 붙여 넣습니다. 텍스트의 끝 문자가 세미콜론으로 끝나지 않으면 세미콜론을 작성하고 경로를 붙여 넣습니다.

```
;C:\Program Files\Java\jdk1.7.0_79\bin;
```

> 시스템 변수에서 세미콜론은 변수와 변수를 구분하는 구분자 역활을 합니다.

환경변수 설정이 잘 되었는지 확인은 명령창을 열고 "javac"를 입력해 확인할 수 있습니다.

```
javac
where possible options include:
  -g                         Generate all debugging info
  -g:none                    Generate no debugging info
  -g:{lines,vars,source}     Generate only some debugging info
...
```

### 안드로이드 스튜디오 설치

안드로이드 스튜디오를 설치해 Android SDK Manager를 통해 Google USB Driver를 설치하고 필수 SDK 도구를 설치합니다. 안드로이드 스튜디오 홈페이지(<https://developer.android.com/studio/index.html>)에 접속해 프로그램을 다운로드하여 설치를 진행합니다.

![안드로이드 스튜디오 설치](img/android-setting-1.PNG)

최초 설치 후 뜨는 창으로 이전 환경설정을 사용할 것인지 확인하는 창입니다. 이전 설정이 없으므로 다음으로 넘어가시면 됩니다. 설치가 완료되면 Welcome to Andriod Studio 창이 나타나며 'Start a new Android Studio project'를 클릭해 신규 프로젝트를 생성합니다.


안드로이드 SDK 설치 경로
C:\Users\Administrator\AppData\Local\Android\sdk

C:\Users\Administrator\AppData\Local\Android\sdk\platform-tools

### 안드로이드 SDK 도구 업데이트

SDK Manager 열어 Google USB Driver를 설치할 것입니다.

1. Tool
2. Android
3. SDK Manager

![SDK Manager 열기](img/android-setting-2.PNG)

Default Setting 창이 열리며 Android SDK 항목이 선택되어 있습니다. 우측 탭에서 SDK Tools를 클릭해 Google USB Driver를 선택하고 "OK" 버튼을 클릭해 설치를 진행합니다.

![Default Setting 창](img/android-setting-3.PNG)

SDK Manager에 대한 자세한 정보는 <https://developer.android.com/studio/intro/update.html#sdk-manager>에서 확인해 보세요.

### ADB 환경변수 설정

스마트폰을 PC에 연결하기 위해서는 ADB라는 프로그램이 사용됩니다. ADB 프로그램을 시스템 어디에서도 실행할 수 있도록 환경변수를 설정할 것입니다. 우선 ADB 설치 위치를 클립보드에 복사해 둡니다. 설치 위치는 SDK 설치를 받은 경로 하위의 "platfrom-tools" 디렉터리입니다. 안드로이드 SDK 설치 위치 확인 방법은 SDK Manager를 열어 확인할 수 있습니다. 아래의 순서에 따라 이동하면 환경변수 편집창을 열수 있습니다.

1. 제어판
2. 시스템
3. 고급 시스템 설정
4. 환경변수
5. 시스템 변수

시스템 변수의 Path 항목을 선택한 후 편집 버튼을 클릭해 시스템 변수 편집창을 열어 복사한 ADB 설치 경로를 텍스트의 끝에 붙여 넣습니다. 텍스트의 끝 문자가 세미콜론으로 끝나지 않으면 세미콜론을 작성하고 경로를 붙여 넣습니다.

```
;C:\Users\Administrator\AppData\Local\Android\sdk\platform-tools;
```

> 시스템 변수에서 세미콜론은 변수와 변수를 구분하는 구분자 역활을 합니다.

ADB 환경변수 설정이 완료 되었다면 명령창을 열고 "adb version"라고 입력해 봅니다.

```
adb version
Android Debug Bridge version 1.0.36
Revision e02fe72a18c3-android
```

### ADB 플러그인 설치

크롬에 ADB 플러그인을 설치에

### PC와 스마트폰 연결

PC와 디바이스를 USB 케이블로 연결합니다. USB 디버깅 허용에 대한 알림 창이 열리게 되며 확인 버튼을 눌러 창을 닫습니다.

![USB 디버깅 허용 알림 창](img/android-setting-4.PNG)

크롬 브라우저를 열고 주소창에 "chrome://inspect/#devices"을 입력합니다. 모든 프로그램의 설치와 설정이 잘되었고 디바이스가 PC와 연결되었다면 아래와 같은 화면을 볼 수 있습니다. ADB 프로그램을 실행하지 않아 디바이스와 PC가 아직 연결되지 않은 상태입니다.

![chrome://inspect/#devices](img/chrome-inspact-devices.png)

명령창을 열고 `adb devices`를 입력합니다.

```
adb devices
List of devices attached
42f06f18acbf5fcf        device
```

PC와 디바이스가 연결되면 디바이스 이름이 표시되며 크롬 브라우저에서 열여 있는 URL 목록이 나타나게 됩니다. "Open tab with url" 입력창에 URL을 입력하면 연결되어있는 디바이스의 크롬 브라우저에서 해당 URL이 새창으로 열리게 됩니다.

![chrome://inspect/#devices](img/chrome-inspact-devices-2.png)
