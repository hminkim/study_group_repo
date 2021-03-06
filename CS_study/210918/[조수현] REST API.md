# REST Api  
  
## REST    
### Representational State Transfer  
- 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것  
- HTTP URI를 통해 자원을 명시하고, HTTP 메서드를 통해 URI에 대한 CRUD Operation을 적용하는 것  
  
>REST에서는 CRUD에 해당하는 4가지 HTTP Method만을 사용  
> - Create -> POST 생성  
> - Read -> GET 조회 / HEAD 헤더 정보 조회  
> - Update -> PUT 수정  
> - Delete -> DELETE 삭제  
  
>자원의 표현에 의한 상태 전달  
>	- 자원 : 해당 소프트웨어가 관리하는 모든 것  
>		(문서, 그림, 데이터, 해당 소프트웨어 자체)  
>	- 자원의 표현 : 그 자원을 표현하기 위한 이름  
>		(‘student’라는 이름이 붙은 DB의 학생 정보에서의 이름)  
>	- 상태 교환  
>		데이터가 요청되어지는 시점에서 자원의 상태를 전달  
>		JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적  
  
**REST API** : REST 아키텍쳐 스타일의 디자인 원칙을 준수하는 API  
- 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있음  
- REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램언어로 클라이언트, 서버를 구축 가능  
- REST API를 제작하면 델파이 클라이언트 뿐 아니라 자바, C#, 웹 등을 이용해 클라이언트 제작 가능  
  
### REST 구성 요소  
**자원 (Resource)** : URI  
	- 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재  
	- 자원을 구별하는 ID는 HTTP URI	- 클라이언트는 URI를 이용해서 자원을 지정하고 해당 자원의 상태에 대한 조작을 서버에 요청  
**행위 (Verb)** : HTTP Method  
	- HTTP의 GET, POST, PUT, DELETE와 같은 Method를 사용  
**표현(Representation of Resource)**  
	- 클라이언트가 자원의 상태에 대한 조작을 요청하면 서버는 이에 적절한 응답을 보냄  
	- REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있음  
	- JSON 혹은 XML을 통해 데이터를 교환하는 것이 일반적  
  
### REST 특징  
1. **Uniform Interface (인터페이스 일관성)**  
- 요청이 어디서 오는지와 무관하게 동일한 자원에 대한 모든 API 요청은 동일해야함  
- URI로 지정한 자원에 대한 조작을 통일되고 한정적인 인터페이스로 수행  
- 표준 HTTP를 따르는 모든 플랫폼에서 사용 가능  
    -> 특정 언어나 기술에 종속되지 않음  
2. **Stateless (무상태)**  
- HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 가짐  
- 사용자나 클라이언트의 context를 서버쪽에 유지 하지 않는다는 의미  
    -> HTTP Session과 같은 context 저장소에 상태 정보를 저장하지 않는 형태를 의미  
    -> context 정보를 신경쓰지 않아도 되므로 구현이 단순해짐  
- Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리  
    - 각 API 서버는 Client의 요청만을 단순 처리  
    - 이전 요청이 다음 요청의 처리에 연관되어서는 안됨  
    - 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용  
    - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아짐  
3. **Server-Client (서버-클라이언트 구조)**  
- 자원이 있는 쪽이 서버, 자원을 요청하는 쪽이 클라이언트  
    - REST Server : API를 제공하고 비즈니스 로직 처리 및 저장을 책임  
    - Client : 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임  
- 서버와 클라이언트의 개발해야 할 내용들이 명확하게 되고 개발에 있어서 서로간의 의존성이 줄어듬  
4. **Cacheable (캐시 처리 가능)**  
- 웹 표준 HTTP를 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용 가능  
    - HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용 가능  
    - HTTP 표준에서 사용하는 ‘Last-Modified’ 태그나 E-Tag를 이용하면 캐싱 구현이 가능  
- 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구됨  
- 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있음  
5. **Layered System (계층화)**  
- Client는 REST API Server만 호출  
- REST Server는 다중 계층으로 구성 가능  
    - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있음  
    - 또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있음  
- 프록시, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용 가능  
6. **Code-On-Demand (Optional)**  
- Server로부터 스크립트를 받아서 Client에서 실행  
- 반드시 충족할 필요는 없음  
  
  
### REST 인터페이스 원칙 가이드  
1. 자원의 식별  
- 요청 내에서 기술된 개별 자원을 식별할 수 있어야 함  
    -> URI는 정보의 자원을 표현해야 함  
- 자원 그 자체는 클라이언트가 받는 문서와는 개념적으로 분리되어 있음  
    -> 서버는 DB 내부의 자료를 직접 전송하는 대신 DB 레코드를 XML이나 JSON등의 형식으로 전송  
2. 표현을 통한 자원의 조작  
- 자원 자체를 전송하는 것이 아닌 자원의 표현을 전송  
    - 서버의 코드에 얽매이지 않고 클라이언트 구현 가능  
    - 서버의 수정에 대한 영향을 최소화 가능  
- 자원에 대한 행위는 HTTP 메서드로 표현  
3. 자기서술적 메세지  
- Self-descriptiveness  
    - 표준 메서드와 미디어 유형을 사용하여 별도의 설명 없이 그 자체만으로도 API의 목적을 명확하게 파악할 수 있도록 함  
    - Response에 캐시 가능성을 지정하여 클라이언트가 아닌 서버가 해당 내용을 헤더에 명시  
4. 애플리케이션의 상태에 대한 엔진으로서 하이퍼미디어  
- 클라이언트가 관련된 자원에 접근하기를 원한다면, 리턴되는 지시자에서 구별될 수 있어야 함  
  
### REST 설계 규칙  
- URI는 명사를 사용  
- 슬래시 구분자는 계층 관계를 나타내는데 사용  
- URI 마지막 문자로 슬래시는 포함하지 않음  
- 하이픈은 URI 가독성을 높이는데 사용    
- 언더바는 URI에 사용하지 않음  
- 파일확장자는 URI에 표함하지 않음  
  
### 장점  
- HTTP의 인프라를 그대로 사용하므로 REST Api 사용을 위한 별도의 인프라를 구출할 필요가 없음  
- HTTP의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해줌  
- 표준 HTTP에 따르는 모든 플랫폼에서 사용 가능  
- Hypermedia API의 기본을 충실히 지키면서 범용성을 보장  
- REST API 메세지가 의도하는 바를 그 자체만으로도 목적을 명확하게 파악 가능  
- 서버와 클라이언트의 역할을 명확하게 분리  
  
### 단점  
- 표준이 존재하지 않음  
- 사용할 수 있는 메소드가 4가지 (HTTP Method 형태가 제한적)  
- 구형 브라우저가 아직 제대로 지원하지 못함  
  
### 필요한 이유    
- 애플리케이션 분리 및 통합  
- 다양한 클라이언트의 등장  
- 다양한 브라우저, 안드로이드, iOS와 같은 모바일 디바이스에서도 통신이 가능해야 함  
  

### 출처  
  
[위키피디아](https://ko.wikipedia.org/wiki/REST)  
[Heee’s Development Blog](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)  
[조대협의 블로그](https://bcho.tistory.com/953 )  
