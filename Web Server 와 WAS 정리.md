# Web Server 와 WAS

(출처: [https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html))

(학습 후 재정리한 내용)

# Web Server

- Web Server의 개념
    
    Web Server는 소프트웨어와 하드웨어로 구분됨 (두 가지 개념을 동시에 포괄)
    
    - 1) 하드웨어
        - 웹서버(Web Server)가 설치되어 있는 컴퓨터
        - [Q.] 여기서의 '웹서버'는 웹서버라는 별개의 소프트웨어(OS같은..?) 인 것인가?(A) Or 클라이언트의 요청을 처리하는 프로그램(서버프로그램,서버애플리케이션) 을 말하는 것인가..? (B)
            
            : 일단 B는 아님,
            
            운영체제(OS) 도 아니고 **OS 위에 설치되는** 어떠한 프로그램
            
    - 2) 소프트웨어
        - 클라이언트로부터(웹브라우저) HTTP요청을 받아, 정적 컨텐츠(ex: .html, .jpg, .css 등)를 제공하는 처리를 수행하는 컴퓨터 프로그램
- Web Server의 기능
    - HTTP 프로토콜[HTTP 통신규약]을 기반으로 하여 **클라이언트**(ex: 웹브라우저, 웹크롤러 등)**로부터 오는 요청을 수행**하는 기능을 담당.
    - 요청에 따라서 아래 두 가지 기능 중 적절하게 선택하여 수행함
        - 기능 1) **정적 컨텐츠(static contents: .html / .css / .jpg 등) 를 제공**
            
                         (WAS를 거치지 않고 Web Server 자체로 바로 자원을 제공)
            
        - 기능 2) **동적 컨텐츠(dynamic contents)를 제공하기 위한 요청을 전달(to WAS)**
            - 클라이언트의 요청(request)를 WAS에 보내고, WAS가 처리한 결과를 클라이언트에게 전달(응답, Response)한다.
- Web Server의 예
    - Apache Server : Apache 사의 웹서버
    - Nginx : Nginx 사의 웹서버
    - IIS : windows 전용 Web Server

# WAS(Web Application Server)

- WAS 의 개념
    - DB 조회나 다양한 로직 처리를 요구하는 '**동적인 컨텐츠**'를 제공하기 위해 만드어진 Application Server
    - HTTP를 통해 컴퓨터나 장치에 애플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)이다.
        
        ( : HTTP통신을 통해 들어온 request에 의해 컴퓨터나 장치에서 **애플리케이션을 발동시켜주는 환경** 같은 것 (프로그램들의 활동이 일어나는 환경 격) )
        
    - '웹 컨테이너(Web Container)' 혹은 '서블릿 컨테이너(Servlet Container)' 라고 불림
        - Container 란 JSP, Servlet 등을 실행시킬 수 있는 소프트웨어[프로그램] 을 말한다
        - 즉, WAS는 JSP, Servlet 등의 구동 환경을 제공한다 (구동환경이 되어준다)
- WAS의 역할
    - WAS = Web Server + Web Container
        
         (웹서버: __곧작성예정__)  (JSP, Servlet 등의 구동환경)
        
    - Web Server 기능들을 구조적으로 분리하여 처리하고자 하는 목적으로 등장
        - 분산 트랜잭션, 보안, 메시징, 스레드 처리 등의 기능을 처리하는 분산환경에서 사용됨
        - 주로 DB 서버와 같이 수행됨
    - 현재는 WAS가 가지고 있는 Web Server도 정적인 컨텐츠를 처리하는데 있어 성능 상 큰 차이가 없음.
- **WAS의 주요 기능**
    1. **프로그램 실행 환경**과 **DB 접속 기능** 제공
    2. **여러 개의 트랜잭션**[논리적 작업 단위] **관리** 기능 제공
    3. **비즈니스 로직**(업무를 처리하는 로직인) 수행
- WAS 의 예 (존재하고 있는 WAS 제품들)
    - Tomcat : Apache 사의 (Apache 소프트웨어 재단) 오픈소스 WAS 제품
    - JBoss : RedHat 사의 오픈소스 WAS 제품 / Java EE의 전체 스택이 지원되는 서버(EJB, JMS, CDI, JTA, Servlet API 등을 지원) / Tomcat보다 무거움 / 자바 EE가 제공하는 모든 기능을 필요로 할 때 사용
    - Jeus : 티맥스소프트의 WAS 제품 / 웹서버인 WebtoB와 함께 사용됨 / WebTob와 항상 연결을 유지한 채 통신하여 Jeus의 부하상황을 즉각적으로 파악하여 부하를 분산시킴
    - Web Sphere : IBM 사의 WAS 제품 / 자바 기반의 Web Application Server / 마이크로 서비스 및 표준 기반 프로그래밍 모델을 지원 / 서비스지향아키텍처(SOA) 및 모듈식 애플리케이션의 토대
    - Web logic: Oracle사의 WAS 제품 / 유료 서비스로 기술지원 / 전체 Java EE 및 Jakarta EE 지원 / 2EE(자바 2 플랫폼, 엔터프라이즈 에디션)를 가장 잘 지원하는 제품 / 대부분의 클라우드 환경에서 Java 어플리케이션 실행을 지원(Oracle Cloud Infrastructure, Docker, Microsoft Azure... / 풍부한 관리도구와 API로 인해 운영이 자동화 / Oracle 제품 및 기술라인과 통합될 경우 성능, 가용성 등이 최적화 될 수 있음)

# Web Server와 WAS를 구분하는 이유

(작성 중)