## 1. REST(Respresentational State Transfe)
엄격한 의미로 REST는 네트워크 아키텍처 원리(or 스타일, 제약 조건)의 모음이다. 여기서 '네트워크 아키텍처 원리'란 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반을 일컫는다.

REST의 구성 요소는
- 자원(Resource): URI
- 행위(Verb): HTTP METHOD
- 표현(Respresentations)
로 이루어져 있습니다.

즉 REST는 URI를 통해 자원을 표시하고, HTTP 메소드를 이용하여 해당 자원의 행위를 정해주며 그 결과를 받는 것을 말합니다.

### REST를 왜 사용하는 가?
- Rest는 서버와 클라이언트가 각각 독립적 진화를 하기 위해 만들어졌다. 
- 독립 적인 진화란 서버의 기능이 변경 되어도 클라이언트를 업데이트할 필요가 없는 상태를 의미한다.
- 웹을 사용할 때, 웹페이지를 변경했다고 웹브라우저를 업데이트 할 필요가 없고, 웹 브라우저를 업데이트 했다고 웹페이지를 변경할 필요도 없다. HTTP, HTML 명세가 변경되어도 웹은 잘 작동한다.
 
###  HTML VS JSON
html는 하이퍼링크가 가능하고 Self-Descriptive(메시지는 스스로를 설명해야한다.) 가 가능하다. json은 되지않기 때문에 별도의 API 문서를 작성해야한다.

## 2. REST의 특징

- 인터페이스 일관성(Uniform Interface) 
 - 일관적인 인터페이스로 분리되어야 한다.
 - REST는 HTTP 표준에만 따른 다면, 어떠한 기술이라던지 사용이 가능한 인터페이스 스타일이다. 예를 들어 HTTP + JSON으로 REST API를 정의 했다면, 안드로이드 플랫폼이건, iOS 플랫폼이건 또는 C나 Java/Python이건 특정 언어나 기술에 종속 받지 않고 HTTP와 JSON을 사용할 수 있는 모든 플랫폼에 사용이 가능한 느슨한 결합 형태의 구조이다.
 
- 무상태(Stateless)
 - 각 요청 간 클라이언트의 컨텍스트가 서버에 저장되어서는 안 된다.
 - 상태가 있다 없다라는 의미는 사용자나 클라이언트의 컨텍스트를 서버쪽에 유지 하지 않는다는 의미로, 쉽게 표현하면 HTTP Session과 같은 컨텍스트 저장소에 상태 정보를 저장하지 않는 형태를 의미한다. 상태 정보를 저장하지 않으면 각 API 서버는 들어오는 요청만을 들어오는 메시지 로만 처리하면 되며, 세션과 같은 컨텍스트 정보를 신경 쓸 필요가 없기 때문에 구현이 단순해진다.
 
- 캐시 처리 가능(Cacheable)
 - WWW에서와 같이 클라이언트는 응답을 캐싱할 수 있어야 한다.
잘 관리되는 캐싱은 클라이언트-서버 간 상호작용을 부분적으로 또는 완전하게 제거하여 scalability와 성능을 향상시킨다.
- REST의 큰 특징 중의 하나는 HTTP라는 기존의 웹 표준을 그대로 사용하기때문에, 웹에서 사용하는 기존의 인프라를 그대로 활용이 가능하다. HTTP 프로토콜 기반의 로드 밸런서나 SSL은 물론이고, HTTP가 가진 가장 강력한 특징중의 하나인 캐슁 기능을 적용할 수 있다.

- 계층화(Layered System)
 -  클라이언트는 보통 대상 서버에 직접 연결되었는지, 또는 중간 서버를 통해 연결되었는지를 알 수 없다. 중간 서버는 로드 밸런싱 기능이나 공유 캐시 기능을 제공함으로써 시스템 규모 확장성을 향상시키는 데 유용하다.
 - 클라이언트 입장에서는 REST API 서버만 호출한다.
 - 서버는 다중 계층으로 구성될 수 있다. 순수 비즈니스 로직을 수행하는 API 서버와 그 앞단 사용자 인증(Authentication), 암호화 (SSL), 로드밸런싱 등을 하는 계층을 추가해서 구조상의 유연성을 줄 수 있다.

- Code on demand (optional) - 자바 애플릿이나 자바스크립트의 제공을 통해 서버가 클라이언트가 실행시킬 수 있는 로직을 전송하여 기능을 확장시킬 수 있다. -> 클라이언트 스크립팅이라고 하며, 데이터는 물론 코드까지 클라이언트로 전송하여 서버의 부담을 클라이언트에게 나눠준다.

- 클라이언트/서버 구조 
 - 아키텍처를 단순화시키고 작은 단위로 분리(decouple)함으로써 클라이언트-서버의 각 파트가 독립적으로 개선될 수 있도록 해준다.
 - REST 서버는 API를 제공하고, 제공된 API를 이용해서 비즈니스 로직 처리 및 저장을 책임진다.
 - 클라이언트의 경우 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하고 책임진다.

## 3. REST API 설계 규칙

   1. URI는 정보 자원을 표현해야한다.
      자원의 이름은 동사보다는 명사를 사용한다.
      URI는 자원을 표현하는데 중점을 두어야 하기 때문에 행위에 대한 표현이 들어가면 안된다.
      (URI에 HTTP METHOD와 행위에 대한 동사 표현이 들어가면 안된다.)
       
   2. 자원에 대한 행위는 HTTP METHOD로 표현한다. (GET, POST, PUT,  DELETE)
       URI에 자원의 행위에 대한 표현이 들어가지 않는 대신 HTTP METHOD를 통해 대신한다.
           
           ``` 
           GET /users/321 321 ID를 가진 유저 정보를 가져오기
           DELETE /users/321 321 ID를 가진 유저 정보를 삭제하기
           POST /users 유저를 생성하기
           ```
           
   3. 슬래시(/)는 계층 관계를 나타내는 데 사용한다.
     
     ```
      http://restapi.test.com/users/rooms
      http://restapi.test.com/users/board
     ```
      
   4. URI 마지막은 슬래시(/)를 사용하면 안된다.
 
     ```
      http://restapi.test.com/users/rooms/ [X]
      http://restapi.test.com/users/rooms [O]
      ```
      
   5. 하이픈 ( - ) 은 URI의 가독성을 높이는 데 사용한다.
     불가피하게 긴 URI를 사용하게 될 경우 하이픈을 이용하여 가독성을 높인다.
      
   6. 언더바( _ ) 혹은 밑줄은 URI에 사용하지 않는 다.
          밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다.
          그래서 대신 언더바를 사용하지 않고 하이픈을 이용한다.
        
   7. URI 경로에는 소문자가 적합하다.  URI경로에는 대문자 사용을 피해야한다.
       대소문자에 따라 각자 다른 리소스로 인식하기 때문이다.
       RFC3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 
       대소문자를 구별하도록 규정하기 때문이다.
        
   8. 파일 확장자는 URI에 포함하지 않는다.
             REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 
             URI 안에 포함시키지 않는 다. Accept Header를 사용한다.
             
   9. 리소스 간의 관계를 표현하는 방법
           ```
           GET:/users/{userid}/devices
           ```

## 5. RESTFUL API 란?
 REST의 스타일(제약 조건)을 모두 만족하는 것을 의미한다.
 개발자 간 사용되는 언어로 명확하게 사전적으로 정의 되지는 않은 것 같다.
  
## 참고 사이트
 [NAVER d2 그런 REST API로 괜찮은가](https://www.youtube.com/watch?v=RP_f5dMoHFc&feature=youtu.be)
 
 [위키 백과](https://ko.wikipedia.org/wiki/REST)
 
  [이상백님의 SlideShare자료] (https://www.slideshare.net/SangBaekLee3/restful-api-67239776?qid=e125f342-ebf9-4472-8ade-1c5041cdc0b1&v=&b=&from_search=2)
  
 [insutance님의 블로그](https://velog.io/@insutance/REST-API)