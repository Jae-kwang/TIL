# url
* 주소에 해당하는 여러 구성요소를 자유자재로 분해하고 조립하고 할수 있는 모듈
* WHATWG 방식의 주소체계로 주소를 구분한다.

```javascript
const URL = url.URL;
const myURL = new URL("https://www.google.com/")
```
* myURL :  WHATWG 방식의 주소체계 Object
* url.format(URL) : url objct를 하나로 합쳐준다.
* url.Parse("https://www.google.com/") : 기존 방식의 주소체계


* url.URL은 search 처리가 편합니다. searchParams에는 다양한 method 들이 많다.
  * 도메인이 없을경우에는 처리 불가능
* url.Parse는 호스트가 없을 때도 쓸 수 있습니다.(같은 도메인일 경우)
---
# quertyString
* url.Parse 방식과 자주 쓰인다(WHATWG 방식은 searchParams를 이미 제공하고 있기 때문에.)
```javascript
const parsedUrl = url.parse("https://www.google.com/")
const query = queryString.parse(parsedUrl.query)
queryString.stringify(query) // 합침
```