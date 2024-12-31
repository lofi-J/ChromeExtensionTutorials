# Chrome Extension Tutorial 

### [documents (공식 문서)](https://developer.chrome.com/docs/extensions/get-started/tutorial/hello-world?hl=ko)


### 코드 수정 후 확장프로그램 *reload* 해야하는 경우

여기서 reload는 확장프로그램 관리 탭에서 회전 아이콘을 통한 새로고침을 말한다.
 - manifest.json 수정
 - service_worker 수정
 - content_script 수정 


### TypeScript를 사용하는 경우
```bash
  npm install chrome-types 
```
크로미움과 함께 배포되고 관리되는 패키지이다. 자주 업데이트 해줄 것을 권장하고있다.
해당 패키지를 통해 자동완성을 지원받을 수 있다.


### manifest.json
```json
{
  "manifest_version": 3,
  "name": "Reading time",
  "version": "1.0",
  "description": "Add the reading time to Chrome Extension documentation articles"
}
```
각 key에는 확장 프로그램의 기본 메타 데이터를 의미한다.
 * 해당 파일은 root 경로에 존재해야한다.
 * 필수 key는 "manifest_version", "name", "version" 뿐이다. (3개)
 * 개발 중에는 // (주석)을 지원하지만 Chrome 웹 스토어에 코드를 업로드하기 전에 제거해야한다.

```json
{
  "icons": {
    "16": "images/icon-16.png",
    "32": "images/icon-32.png",
    "48": "images/icon-48.png",
    "128": "images/icon-128.png"
  }
}
```
manifest에 지정된 각 사이즈의 아이콘들은 png를 권장한다. (svg를 제외한 다른 형식들도 허용) <br/>
 - 16 x 16 : 확장 프로그램 페이지 및 컨텍스트 메뉴의 파비콘
 - 32 x 32 : Windows 컴퓨터에는 해당 크기를 필요로하는 경우가 많다. (필수)
 - 48 x 48 : 확장 프로그램 페이지에 표시된다.
 - 128 x 128 : 설치 시, Chrome 웹 스토어에 표시된다.

```json
{
  "content_scripts": [
    {
      "js": ["scripts/content.js"],
      "matches": [
        "https://developer.chrome.com/docs/extensions/*",
        "https://developer.chrome.com/docs/webstore/*"
      ]
    }
  ]
}
```
*"matches"* 필드를 이용해 콘텐츠 스크립트를 삽입할 웹 사이트를 식별한다.
