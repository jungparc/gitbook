## Application Service > Maps > Android 사용 가이드

Android 기반으로 Maps 서비스를 사용하는 방법을 설명합니다.

## API 공통 정보

### 사전 준비
- API를 사용하려면 앱키가 필요합니다.
- 앱키는 **TOAST Console** 상단 **URL & Appkey** 메뉴에서 확인할 수 있습니다.

### 요청 공통 정보

#### URL 정보
##### [지도 API]

| 항목        | URL                                      |
| --------- | ---------------------------------------- |
| 지도        | https://kr1-maps.api.nhncloudservice.com/maps/js/v1.0/map.js |
| 정적(static) 지도 | https://kr1-maps.api.nhncloudservice.com/maps/js/v1.0/staticMap.js |

## 지도

### 1. Android WebView 지도

Android에서 API를 호출하고 콜백 함수로 파라미터를 전달받는 방법을 설명합니다.

#### A. 주요 TOAST Maps Android WebView API 안내
##### 추가적인 TOAST Maps Android WebView API 사용법은 <a href="http://developers1.inavi.com:8086?key=19b6272o5" target="_blank" rel="nofollow">Thinkware API Center</a>를 참고하시기 바랍니다.

> ※ TOAST Maps API에서 사용되는 좌표는 팅크웨어 전용 좌표로만 사용됩니다.
> <br>팅크웨어 좌표를 경위도 좌표(WGS84)로 변환하려면 TMWA.getWgs84FromTw() 함수를 이용합니다. 반대로 경위도 좌표(WGS84)를 팅크웨어 좌표로 변환하려면 TMWA.getTwFromWgs84() 함수를 이용합니다.


| API 이름                                   | 파라미터                  | 콜백 메서드           | 콜백 파라미터                                  | 설명                                       |
| ---------------------------------------- | --------------------- | ---------------- | ---------------------------------------- | ---------------------------------------- |
| TMWA.initMap(map_div_name, twX, twY, level, arrange_type, map_type) | map_div : String      | initCB <br><br>  | 지도 초기화 성공여부<br>'true': 성공<br> 'false': 실패 | 지도를 담을 div 태그 ID<br><br>지도를 사용하려면 최초에 반드시 호출해야 하는 초기화 함수입니다. |
|                                          | twX : Number          |                  |                                          | 지도 초기화 TW X 좌표                           |
|                                          | twY : Number          |                  |                                          | 지도 초기화 TW Y 좌표                           |
|                                          | level : Number        |                  |                                          | 지도 초기화 Level<br>- 일반 지도 : 1~13<br>- 항공 지도 : 1~13 |
|                                          | arrange_type : Number |                  |                                          | 지도 레이어 정렬 방식<br>1 : 중앙정렬 방식(resize효과 있음)<br>2 : 전체로딩방식(resize효과 없음)<br> 3 : 우상단정렬 방식(resize효과 있음) |
|                                          | map_type : String     |                  |                                          | 지도 타입 설정<br>'i' : 일반맵<br>'a' : 항공맵<br>'s' : 요약맵 |
| TMWA.getLevel()                          |                       | getLevelCB       | 지도의 현재 레벨                                | 지도의 레벨을 가져옵니다.                           |
| TMWA.getCenter()                         |                       | getCenterCB      | 지도의 현재 중심좌표<br> 'twX&#124;twY'           | 지도의 중심좌표를 가져옵니다.                         |
| TMWA.getExtent()                         |                       | getExtentCB      | 지도의 영역좌표<br> 'leftX&#124;topY&#124;rightX&#124;bottomY' | 현재 지도가 표출되는 영역좌표를 가져옵니다.                 |
| TMWA.setMoveend()                        |                       | setMoveendCB     | 확대, 축소,이동 후 지도 중심좌표와 레벨 <br>'twX&#124;twY&#124;level' | 지도에 moveend 이벤트를 등록합니다.<br>moveend: 지도 확대, 축소, 이동이 끝났을 때 |
| TMWA.removeMoveend()                     |                       |                  |                                          | 지도에서 moveend 이벤트를 제거합니다.                 |
| TMWA.setTouchend()                       |                       | setTouchendCB    | 터치한 지도 좌표<br> 'twX&#124;twY'             | 지도에 touchend 이벤트를 등록합니다.<br>  touchend: 지도 터치가 끝났을 때 |
| TMWA.removeTouchend()                    |                       |                  |                                          | 지도에서 touchend 이벤트를 제거합니다.                |
| TMWA.setZoomend()                        |                       | setZoomendCB     | 확대, 축소 후 지도 중심좌표와 레벨<br> 'twX&#124;twY&#124;level' | 지도에 zoomend 이벤트를 등록합니다. <br> zoomend: 지도 확대, 축소가 끝났을 때 |
| TMWA.removeZoomend()                     |                       |                  |                                          | 지도에서 zoomend 이벤트를 제거합니다.                 |
| TMWA.setTouchEvent(event_name)           | event_name: String   | setTouchEventCB  | 발생한 이벤트와 터치한 지도 좌표 <br>'event_name&#124;twX&#124;twY' | 등록할 이벤트 이름<br> 'touchstart': 지도터치를 시작했을 때<br>  'touchend': 지도 터치가 끝났을 때<br>  'longpress': 지도를 길게 눌렀을 때<br><br>지도에 터치(touch) 관련 이벤트를 등록합니다. |
| TMWA.removeTouchEvent(event_name)        | event_name: String   |                  |                                          | 등록할 이벤트 이름<br> 'touchstart': 지도 터치를 시작했을때<br>  'touchend': 지도 터치가 끝났을 때<br>  'longpress' : 지도를 길게 눌렀을 때<br><br>지도에서 touch 관련 이벤트를 제거합니다. |
| TMWA.createAndAddMarker(twX, twY, iconWidth, iconHeight, iconUrl, [param]) | twX : Number          | createMarkerCB   | Marker 객체 아이디와 사용자 변수 param<br> 'marker_id&#124;param' | Marker 객체의 TW X 좌표<br><br>Marker 객체를 생성하고 지도에 추가합니다. |
|                                          | twY : Number          |                  |                                          | Marker 객체의 TW Y 좌표                       |
|                                          | iconWidth : Number    |                  |                                          | Marker 이미지 너비                            |
|                                          | iconHeight : Number   |                  |                                          | Marker 이미지의 높이                           |
|                                          | iconURL : String      |                  |                                          | Marker 이미지의 URL                          |
|                                          | param : String        |                  |                                          | Marker 객체의 사용자 변수                        |
| TMWA.setTouchendMarkerCB(id)             | id : Number           | touchendMarkerCB | 이벤트를 등록할 대상 Marker 객체 아이디<br><br>Marker 객체 아이디와 Marker 객체의 TW X 좌표, TW Y좌표,<br> 사용자 변수 param<br> 'marker_id&#124;twX&#124;twY&#124;param' | Marker 객체에 touchend 이벤트를 등록합니다.          |
| TMWA.removeTouchendMarker(id)            | id : Number           |                  |                                          | 이벤트를 제거할 대상 Marker 객체 아이디<br><br>Marker 객체에 touchend 이벤트를 제거합니다. |
| TMWA.getTwFromWgs84(lon, lat)            | lon : Number          | getTwFromWgs84CB | 변환된 TW 좌표 <br>'twX&#124;twY'             | 변환할 WGS84 경도 좌표<br><br>WGS84 좌표를 TW 좌표로 변환합니다. |
|                                          | lat : Number          |                  |                                          | 변환할 WGS84 위도 좌표                          |
| TMWA.getWgs84FromTw(twX, twY)            | twX: Number           | getWgs84FromTwCB | 변환된 WGS84 좌표 <br>'lon&#124;lat'          | 변환할 TW X 좌표<br><br>TW 좌표를 WGS84 좌표로 변환합니다. |
|                                          | twY : Number          |                  |                                          | 변환할 TW Y 좌표                              |


#### TOAST Maps Android WebView API 사용

TOAST Maps Android WebView API를 사용하려면
<br>Android 프로젝트 경로(/app/src/main/manifest.xml) 파일에 android.permission.INTERNET 권한을 추가해야 합니다.
<br>팅크웨어 WebView API는 웹 사이트에 발급받은 앱키를 선언하여 해당 웹페이지를 WebView에서 호출하고
<br>발급 키 권한에 따라 다운로드된 API(JavaScript)를 호출해, 콜백 함수를 연결하여 사용합니다.
<br>※ 콜백 함수를 사용할 때 주의점: Android 버전 4.2 이상에서는 아래와 같이 콜백 함수 위에
<br>@JavascriptInterface 어노테이션을 꼭 써 주시기 바랍니다.

```
@JavascriptInterface
public void setMoveendCB(String result){
	String msg = "moveend Event \n twX|twY|level : " + result;
	Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
	toast.show();
}
```


아래는 간단한 맵을 로딩하는 방법입니다.
<br>아래의 예제에서 어떻게 웹 페이지와 WebView 간 API를 호출하고 이벤트 발생 시 콜백 함수로 어떤 파라미터를 받는지 볼 수 있습니다.
<br>아래 파일의 경로: 프로젝트 경로 /app/src/main/assets/www/android_webview.html

```
<!DOCTYPE HTML>
<html>
<head>
	<meta charset="UTF-8">
	<title> Android API TEST </title>
	<script src="http://code.jquery.com/jquery-1.10.1.min.js"></script>
	<script type="text/javascript" src="https://kr1-maps.api.nhncloudservice.com/maps/js/v1.0/map.js"></script>
	<script>
	    // 지도 사용을 위한 인증을 진행합니다.
	    Map.authentification("appKey");
	</script>
	</head>
<body>
	<div id="div_map" style="position:absolute;top:0px;left:0px;width:100%;height:100%;z-index:10;"></div>
</body>
</html>
```
<center>**android_webview.html**</center>


```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        //Layout을 설정
        setContentView(R.layout.activity_main);

		//active_main에 선언한 Webview 타입을 생성
        mWebView = (WebView) findViewById(R.id.webView);

        //JavaScript 사용
        mWebView.getSettings().setJavaScriptEnabled(true);

        //WebView 클라이언트를 설정, 페이지 로딩 시작, 로딩 종료 등 이벤트를 가져올 수 있음
        mWebView.setWebViewClient(new WebViewClientClass());

        // API로 부터 콜백
        // JavaScript로부터 콜백 함수 발생 시 Android에서 사용할 객체와 JavaScript에서 사용할 객체 이름 설정
        mWebView.addJavascriptInterface(new AndroidBridge(), "tmjscall");
        // API 키로 권한이 부여된 JavaScript 기반 팅크웨어 API 다운로드
        mWebView.loadUrl("file:///android_asset/www/android_webview.html");

    }

    // WebView 이벤트 감지
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // 페이지 로딩이 끝나면
            // 지도를 초기화한다
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {
        // TMWA.initMap 콜백 함수
        @JavascriptInterface
        public void initCB(String init){
            String msg = "";
            if(init.equals("true")){
                msg = "지도 초기화 성공!";
            }else{
                msg = "지도 초기화 실패!";
            }
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>



[1] 지도 초기화와 정보 가져오기
<br>1번 예제에서는 지도를 초기화하고 지도 정보를 가져오는 방법을 설명합니다.
<br>지도를 초기화하는 방법은 두 가지입니다.
<br>WebView에서 로딩할 페이지 android_webview.html에서 THINKMAP.initMap을 호출하는 방법과
<br>Android 프로젝트에서 TMWA.initMap을 사용하는 방법입니다.
<br>지도 초기화 이후에 추가로 해야 할 작업이 있다면 TMWA.initMap을 사용하여 콜백 함수에서 추가 처리할 수 있습니다.
<br>이 예제에서는 TMWA.initMap을 호출하는 방법을 사용합니다.


```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    //버튼
    Button getLevel, getCenter, getExtent;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

		//Layout을 설정
        setContentView(R.layout.activity_main);

		//active_main에 선언한 Webview 타입을 생성
        mWebView = (WebView) findViewById(R.id.webView);

        //JavaScript 사용
        mWebView.getSettings().setJavaScriptEnabled(true);

        //WebView 클라이언트를 설정, 페이지 로딩 시작, 로딩 종료 등 이벤트를 가져올 수 있음
        mWebView.setWebViewClient(new WebViewClientClass());

        // JavaScript로부터 콜백 함수 발생 시 Android에서 사용할 객체와 JavaScript에서 사용할 객체 이름 설정
        mWebView.addJavascriptInterface(new AndroidBridge(), "tmjscall");
        // API 키로 권한이 부여된 JavaScript 기반 팅크웨어 API 다운
        mWebView.loadUrl("file:///android_asset/www/android_webview.html");

        // 버튼 이벤트 연결
        getLevel = (Button) findViewById(R.id.getLevel);
        getLevel.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getLevel()");
            }
        });

        getCenter = (Button) findViewById(R.id.getCenter);
        getCenter.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getCenter()");
            }
        });

        getExtent = (Button) findViewById(R.id.getExtent);
        getExtent.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getExtent()");
            }
        });

    }

    // WebView 이벤트 감지
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // 페이지 로딩이 끝나면
            // 지도를 초기화한다
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {
        // TMWA.initMap 콜백 함수
        @JavascriptInterface
        public void initCB(String init){
            String msg = "";
            if(init.equals("true")){
                msg = "지도 초기화 성공!";
            }else{
                msg = "지도 초기화 실패!";
            }
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        //  TMWA.getLevel 콜백 함수
        @JavascriptInterface
        public void getLevelCB(String level){
            String msg = "지도 레벨 :" + level;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

        }

        // TMWA.getCenter 콜백 함수
        @JavascriptInterface
        public void getCenterCB(String cn){
            String msg = "지도 중심 : " + cn;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // TMWA.getExtent 콜백 함수
        @JavascriptInterface
        public void getExtentCB(String ex){
            String msg = "현재 지도영역 : " + ex;

            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

        }

    }

}
```
<center>**MainActivity.java**</center>


[2] 지도 이벤트
<br>2번 예제에서는 지도에 이벤트를 등록하고 제거하는 방법을 설명합니다.

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    //버튼
    Button btnMove, btnTouchend, btnZoom, btnTouch;
    Boolean moveFlag = false;
    Boolean touchendFlag = false;
    Boolean zoomFlag = false;
    Boolean touchFlag = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // 공통 코드 생략(지도 초기화 예제 참조)

        // 버튼 이벤트 등록
        btnMove = (Button) findViewById(R.id.setMoveend);
        btnMove.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!moveFlag){
                    mWebView.loadUrl("javascript:TMWA.setMoveend()");
                    btnMove.setText("removeMoveend");
                    moveFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeMoveend()");
                    btnMove.setText("setMoveend");
                    moveFlag = false;
                }
            }
        });

        btnTouchend = (Button) findViewById(R.id.setTouchend);
        btnTouchend.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!touchendFlag){
                    mWebView.loadUrl("javascript:TMWA.setTouchend()");
                    btnTouchend.setText("removeTouchend");
                    touchendFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeTouchend()");
                    btnTouchend.setText("setTouchend");
                    touchendFlag = false;
                }
            }
        });

        btnZoom = (Button) findViewById(R.id.setZoomend);
        btnZoom.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!zoomFlag){
                    mWebView.loadUrl("javascript:TMWA.setZoomend()");
                    btnZoom.setText("removeZoomend");
                    zoomFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeZoomend()");
                    btnZoom.setText("setZoomend");
                    zoomFlag = false;
                }

            }
        });

        btnTouch = (Button) findViewById(R.id.setTouchEvent);
        btnTouch.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!touchFlag){
                    //longpress 이벤트 발생 시간을 2초로 설정, 설정하지 않은 경우 1.5초
                    mWebView.loadUrl("javascript:THINKMAP.setLongPressTime(2)");
                    mWebView.loadUrl("javascript:TMWA.setTouchEvent('longpress')");
                    btnTouch.setText("removeTouchEvent");
                    touchFlag = true;
                }else{
                    mWebView.loadUrl("javascript:TMWA.removeTouchEvent('longpress')");
                    btnTouch.setText("setTouchEvent");
                    touchFlag = false;
                }
            }
        });

    }

    // WebView 이벤트 감지
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // 페이지 로딩이 끝나면
            // 지도를 초기화한다
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {

        // setMoveend 콜백 함수
        @JavascriptInterface
        public void setMoveendCB(String result){
            String msg = "moveend Event \n twX|twY|level : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // setTouchend 콜백 함수
        @JavascriptInterface
        public void setTouchendCB(String result){
            String msg = "touchend Event \n twX|twY : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        // setZoomend 콜백 함수
        @JavascriptInterface
        public void setZoomendCB(String result){
            String msg = "zoomend Event \n twX|twY|level : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

        //setTouchEvent 콜백 함수
        @JavascriptInterface
        public void setTouchEventCB(String result){
            String msg = "event_name|twX|twY :\n" + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>



[3] 지도 마커
<br> 3번 예제에서는 지도에 마커를 추가한 후 마커에 이벤트를 등록하고 제거하는 방법을 설명합니다.

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    Button btnMarker;
    String marker_id = "";

    Button btnTouchend;

    Button btnRemoveTouchEnd;

    String imgUrl = "'http://dev.m.map.inavi.com/guide/img/img.png'";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // 공통 코드 생략(지도 초기화 예제 참조)

        // 버튼 이벤트 연결
        btnMarker = (Button) findViewById(R.id.createMarker);
        btnMarker.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if(marker_id.equals("")){
                    String imgUrl = "'http://dev.m.map.inavi.com/guide/img/img.png'";
                    mWebView.loadUrl("javascript:TMWA.createAndAddMarker(163670, 526934, 47, 46, " + imgUrl + ", 'Marker')");
                }

            }
        });


        btnTouchend = (Button) findViewById(R.id.setTouchEnd);
        btnTouchend.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!marker_id.equals("")){
                    mWebView.loadUrl("javascript:TMWA.setTouchendMarkerCB(" + marker_id + ")");
                    Log.d("setEvent", "Marker");
                }
            }
        });

        btnRemoveTouchEnd = (Button) findViewById(R.id.removeTouchEnd);
        btnRemoveTouchEnd.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                if(!marker_id.equals("")){
                    mWebView.loadUrl("javascript:TMWA.removeTouchendMarker(" + marker_id + ")");
                    Log.d("removeEvent", "Marker");
                }
            }
        });

    }

    // WebView 이벤트 감지
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // 페이지 로딩이 끝나면
            // 지도를 초기화한다
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }

    // Android Bridge
    private class AndroidBridge {

        @JavascriptInterface
        public void createMarkerCB(String result){
            StringTokenizer st = new StringTokenizer(result, "|");

            if(st.hasMoreTokens())
                marker_id = st.nextToken();

            String msg = "Create Marker \n marker_id|param : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();

            Log.d("marker_id", marker_id);
        }

        @JavascriptInterface
        public void touchendMarkerCB(String result){
            String msg = "Touch End \n marker_id|twX|twY|param : " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }

    }

}
```
<center>**MainActivity.java**</center>

[4] 기타
<br>4번 예제에서는 주소 검색, 경로 탐색, 좌표 변환과 계산 방법을 설명합니다.

```
public class MainActivity extends AppCompatActivity {
    private WebView mWebView;

    Button btnTwFromWgs84, btnWgs84FromTw;

    String lon = "37.573264";
    String lat = "126.979594";
    String twX = "163670";
    String twY = "526934";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        // 공통 코드 생략(지도 초기화 예제 참조)

        // 버튼 이벤트 연결
        btnTwFromWgs84 = (Button) findViewById(R.id.twFromWgs84);
        btnTwFromWgs84.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getTwFromWgs84(" + lon + "," +  lat + ")");
            }
        });

        btnWgs84FromTw = (Button) findViewById(R.id.wgs84FromTw);
        btnWgs84FromTw.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                mWebView.loadUrl("javascript:TMWA.getWgs84FromTw(" + twX + "," +  twY + ")");
            }
        });

    }

    // WebView 이벤트 감지
    private class WebViewClientClass extends WebViewClient {

        @Override
        public void onPageFinished(WebView view, String url) { // 페이지 로딩이 끝나면
            // 지도를 초기화한다
            mWebView.loadUrl("javascript:TMWA.initMap('div_map', 163670, 526934, 11, 2, 'i')");
            super.onPageFinished(view, url);
        }

    }
    // Android Bridge
    private class AndroidBridge {
        // WGS84 -> TW 콜백
        @JavascriptInterface
        public void getTwFromWgs84CB(String result){
            String msg ="twX, twY -> " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }
        // WGS84 -> TW 콜백
        @JavascriptInterface
        public void getWgs84FromTwCB(String result){
            String msg ="lon, lat -> " + result;
            Toast toast = Toast.makeText(mWebView.getContext(), msg, Toast.LENGTH_SHORT);
            toast.show();
        }
    }

}
```
<center>**MainActivity.java**</center>
