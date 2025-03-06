<h1> Spring 면접 대비 지식</h1>
<p>https://hoons-dev.tistory.com/97 의 내용 참고 학습</p>

<h3 style="color: cornflowerblue"> Spring 프레임워크가 무엇인지</h3>
<p>스프링 프레임워크는 자바 플랫폼을 위한 오픈 소스 어플리케이션 프레임워크로 POJO 기반을 바탕으로, DI와 AOP, PSA를 지원하는 컨테이너를 제공하는 프레임워크임</p>

<h3 style="color: cornflowerblue"> IOC(Inversion of Control, 제어의 역전)이란</h3>
<p>객체의 생성부터 생명주기의 관리까지 모든 객체에 대한 제어권이 바뀐 것을 의미</p>
<p>디자인 원칙 중 하나로 클래스간의 결합도를 줄이기 위해 다양한 종류의 제어를 반전시킬 것을 권장하는 것</p>

<h3 style="color: cornflowerblue"> DI(Dependency Injection, 의존관계 주입)이란</h3>
<p>IOC가 디자인 원칙이라면, DI는 IOC를 구현할 때 자주 등장하는 '디자인 패턴'중 하나임</p>
<p>DI는 의존 관계 주입으로, 의존 객체를 직접 생성하는 것이 아니라, 생성자나 Setter를 통해 넣으줌으로써 의존 관계를 주입하는 것을 의미함</p>
<p>수정자 주입</p>
<ul>
    <li>대부분 의존 관계 주입은 한번 일어나면 종료시점까지 변경할 일이 거의 없다.</li>
    <li>Setter를 통해 주입하게 되면 변경될 위험이 존재한다</li>
    <li>Setter을 public으로 열어야한다</li>
</ul>
<p>생성자 주입</p>
<ul>
    <li>생성자 주입을 권장</li>
    <li>생성자 호출 시점에 딱 1번만 호출되는 것을 보장</li>
    <li>final 키워드를 통해 불변하게 설계 가능</li>
    <li>의존성 주입이 누락되는 것을 방지할 수 있다</li>
</ul>

<h3 style="color: cornflowerblue"> Spring에서 IOC와 DI를 어떻게 지원해 주는지?</h3>
<p>스프링은 IOC와 DI를 Container로써 제공한다.</p>
<p>클래스 사이의 의존 관계를 Bean 설정 정보를 바탕으로 컨테이너가 자동으로 연결해주는 방식으로 제공한다</p>
<p>장점</p>
<ul>
    <li>스프링 자체에서 설정을 통해 연관 관계를 맺어줌으로써 객체간 결합도를 낮춰준다</li>
    <li>클래스의 재사용성을 높이고, 유지보수가 편리해진다</li>
    <li>의존성 주입으로 인해 stub, mock 객체를 사용해 unit 테스트의 이점이 생긴다</li>
</ul>

<p>단점</p>
<ul>
    <li>의존성 주입을 위한 선행 작업이 필요해 간단한 프로그램에서는 번거롭다</li>
    <li>코드 추적이 어렵다</li>
</ul>

<p>DI 컨테이너는, 자바 객체의 생명 주기를 관리하며, 생성 자바 객체들에게 추가적인 기능을 제공한다</p>
<p>종류는 BeanFactory, ApplicationContext가 있다.</p>
<p>ApplicationContext는 BeanFactory의 빈 관리 기능을 상속 받고 국제화등의 추가 기능을 가지고 있어 ApplicationContext를 사용한다</p>

<h3 style="color: cornflowerblue"> Bean 객체와 Bean 생명주기에 대해</h3>
<p>DI 컨테이너 내부에 존재하며 관리를 받고 있는 객체</p>
<p>@Bean 어노테이션을 등록해 사용하거나, xml을 통해 등록할 수 있다. Bean으로 등록된 객체는 쉽게 주입하여 사용 가능</p>

<p>Bean 생명주기</p>
<p>스프링 컨테이너 생성 -> 스프링 빈 생성 -> 의존 관계 주입 -> 초기화 콜백 -> 사용 -> 소멸 전 콜백 -> 스프링 종료</p>
<ul>
    <li>프링 컨테이너에 의해 생명주기 관리</li>
    <li>스프링 컨테이너 초기화 시 빈 객체 생성, 의존 객체 주입 및 초기화</li>
    <li>생성과 의존관계 주입과 초기화 분리
        <ul>
            <li>의존관계 주입(생성자 주입)은 필수 정보를 받고 메모리 할당을 통해 객체 생성 책임</li>
            <li>초기화는 생성된 값들을 활용해 외부 커넥션을 연결하는 등 무거운 작업 수행</li>
            <li>명확하게 분리하는 것이 유지보수 관점에서 좋다</li>
        </ul>
    </li>
    <li>싱글톤 빈들은 컨테이너가 종료되기 직전에 소멸전 콜백이 발생</li>
</ul>

<h3 style="color: cornflowerblue"> Annotation?</h3>
<p>프로그램에서 추가적인 정보를 제공하는 메타데이터</p>
<p>annotation을 정의하고, 원하는 위치에 배치한 후, 코드가 실행되는 도중 자바 리플레션을 이용해 추가 정보를 획득해 기능을 실시하는 방식</p>

<h3 style="color: cornflowerblue"> Spring에서 제공하는 대표적인 Annotation</h3>

```java
@ComponentScan
@EnableAutoConfiguration
@Component
@Bean
@Configuration
@Autowired
@Qualifier
@Resource
@Controller
@RestController
@SpringBootApplication
```

<h3 style="color: cornflowerblue"> 웹 서버(Web Server) vs 웹 애플리케이션 서버 WAS (Web Application Server)</h3>
<p>웹 서버</p>
<ul>
    <li>정적 리소스 파일을 제공하는 서버</li>
</ul>

<p>웹 애플리케이션 서버</p>
<ul>
    <li>웹 서버가 하는 일 + 애플리케이션 로직 (DB 연결, 동작 수행, 데이터 제공)까지 제공하여 동적인 처리를 하는 서버</li>
    <li>자바 진영에서는 서블릿 컨테이너 기능을 제공하면 WAS라고 한다</li>
</ul>

<h3 style="color: cornflowerblue"> 서블릿과 서블릿 컨테이너</h3>
<p>서블릿 컨테이너는 서블릿의 생명주기를 관리한다</p>

<h3 style="color: cornflowerblue"> Spring MVC</h3>
<p>Spring에서 제공하는 웹 모듈, Model, View, Controller 세 가지 구성요소를 사용하여 요청을 처리함</p>
<p>단순한 텍스트 형식의 응답, REST 형식의 응답, View를 표시하는 HTML을 Return하는 응답까지 다양한 응답을 가능하게 함</p>
<p>기능별로 코드를 분리하여 가독성을 높이고 재사용성을 증가시킨다.</p>
<p>view와 model 사이에 의존성이 높아서 애플리케이션이 커질수록 복잡해지고 유지보수가 어렵다</p>
<P>대규모의 프로그램에서 Controller에 다수의 Model와 View가 복잡하게 연결되어 코드 분석과 테스트가 어려워질 수 있다.</P>
<p>이런 의존성 문제를 해결하기 위해 MVVM, MVP구조가 등장함</p>

<h3 style="color: cornflowerblue"> 그렇다면, 어떻게 하나의 컨트롤러로 여러 요청을 받을까?</h3>
<p>컨트롤러는 컴포넌트 스캔이 되면서 스프링 빈 컨테이너에 올라간다</p>
<p>또한 빈 객체는 싱글톤 패턴으로 구현되어있기 대문에 여러 쓰레드의 요청이 들어와도 하나의 컨트롤러 객체를 공유하면서 처리한다.</p>
<p>즉, 여러 쓰레드가 메서드에 대해 공유 자원으로 접근해 사용한다</p>

<p>싱글톤 패턴으로 구현되어있다는 점은 Thread-safe하지 않다는 의미이므로, 상태를 공유하거나 저장하는 코드가 없도록 Stateless하게 정의해야한다.</p>

<h3 style="color: cornflowerblue"> 싱글톤 패턴?</h3>
<p>컨트롤러는 컴포터는트 스캔이 되면서 스프링 빈 컨테이너에 올라간다.</p>
<p>또한 빈 객체는 싱글톤 패턴으로 구현되어있기 때문에 여러 쓰레드의 요청이 들어와도 하나의 컨트롤러 객체를 공유하면서 처리한다</p>
<p>즉, 여러 쓰레드가 메서드에 대해 공유 자원으로 접근해 사용한다</p>
<p>최초 한번의 new 연산자를 통해 고정된 메모리 영역을 사용하기 때문에 메모리 낭비를 방지할 수 있고, 이미 생성된 인스턴스를 사용하기에 속도 측면에서도 이점이 있다.</p>

<p>다른 클래스 간의 데이터 공유가 쉽다. 싱글톤 인스턴스는 전역으로 사용되는 인스턴스이기 때문에 다른 클래스의 인스턴스들이 접근해 사용할 수 있다.</p>
<p>그렇게 때문에 '동시성 문제'가 일어나지 않도록 유의해야한다</p>

<h3 style="color: cornflowerblue"> AOP?</h3>
<p>관점 지향 프로그래밍의 약어로, 공통 관심사항과 핵심 관심사항을 분리하는 것을 의미함</p>
<p>각 소스코드에서 여러 번 반복해서 사용하는 코드를 흩어진 관심사라 부르고, 이것을 Aspect로 모듈화해 핵심 로직에서 분리해 재사용하는 것</p>
<p>예를 들어, 로그, 성능테스트, 권한, 트랜젹션 등을 모든 메소드에 적용하고 싶을 때 일일이 추가하는 것이 아니라 AOP를 활용해 적용할 수 있다</p>

<h3 style="color: cornflowerblue"> POJO?</h3>
<p>Plain Old Java Object의 약어로, 평범한 구식 자바 객체를 의미</p>
<p>프레임워크 인터페이스나 클래스를 구현하거나 확장하지 않은 단순한 클래스를 의미하는 것으로, 타 프레임워크에 종속되지 않아 코드가 간결하고 테스트 자동화에 유리함</p>
<p>Spring에서는 도메인과  비즈니스 로직을 수행하는 대상이 POJO대상이 될 수 있다</p>

<h3 style="color: cornflowerblue"> DAO, DTO, BO, VO</h3>
<p>DAO (Data Access Object)</p>
<ul>
    <li>DB데이터를 조회하거나 조작하는 기능을 전담하는 객체</li>
    <li>DB접근 로직과 비즈니스 로직을 분리하기 위해 사용</li>
</ul>

<p>DTO (Data Transfer Object)</p>
<ul>
    <li>계층간의 데이터 교환을 위한 객체</li>
    <li>로직을 갖지 않는 순수 데이터 객체로 getter, setter만 포함</li>
</ul>

<p>VO (Value Object)</p>
<ul>
    <li>DTO와 동일한 개념</li>
    <li>Read Only로 수정 불가</li>
    <li>getter, setter 이외의 추가 로직 포함 가능</li>
</ul>

<p>BO (Business Object)</p>
<ul>
    <li>비즈니스 로직을 포함하는 오브젝트, 여러 DAO를 사용해 데이터를 처리</li>
</ul>

<h3 style="color: cornflowerblue"> Spring의 레이어드 아키텍처</h3>
<p>Spring은 레이어드 아키텍처로 이루어져 있다.</p>
<p>하나의 레이어는 자신의 고유 역할을 수행하고, 인접한 다른 레이어에 무언가를 요청하거나 응답한다.</p>
<p>그 밖의 다른 레이어는 신경 쓸 필요가 없기 때문에 각 레이어는 자신의 역할에 충실할 수 있다.</p>
<p>재사용성이 좋고, 유지보스에도 유리하고, 테스트 구현이 편해지고 가독성도 높아진다</p>

<p>Presentation Layer</p>
<ul>
    <li>view를 담당하는 부분, 클라이언트와 직접적으로 맞닿는 부분</li>
</ul>

<p>Application Layer</p>
<ul>
    <li>비즈니스 핵심 로직을 처리하는 부분</li>
    <li>Service 객체라는 것은 하나의 트랜잭션으로 구성되어 작동</li>
</ul>

<p>Persistence Layer</p>
<ul>
    <li>데이터 관련 처리를 담당하는 부분</li>
</ul>

<h3 style="color: cornflowerblue"> 커넥션 풀? SpringBoot는 어떤 커넥션 풀을 사용하는가</h3>
<p>어플리케이션이 DB를 사용하기 위해서는 connection이 필요하다. 이 connection은 생성과 소멸 비용이 크다</p>
<p>그렇기 때문에 커넥션 풀을 미리 생성하고 애플리케이션이 시작하는 시점에 커넥션을 미리 다 생성하고 이것을 재활용하며 사용한다.</p>

<p>hikariCP를 사용한다</p>

<h3 style="color: cornflowerblue"> Datasource란?</h3>
<p></p>

<h3 style="color: cornflowerblue"> 트랜잭션을 추상화해서 사용하는 이유?</h3>
<p>다양한 데이터 접근 기술이 등장하면서, 코드레벨에서는 다르지만 논리적으로 같은 기능을 수행하기 때문에 트랜잭션을 추상화함</p>
<p>다양한 접근 기술로는 JDBC, JPA, 하이버네이트등이 있다</p>

<h3 style="color: cornflowerblue"> 트랜잭션 동기화 매니저</h3>
<p>보통 서비스단에서 트랜잭션을 시작하고 끝낸다</p>
<p>하나의 트랜잭션 내에서는 같은 커넥션을 사용 해야 한다.</p>
<p>하나의 트랜잭션에서 같은 커넥션을 사용하도록 도움을 주는 기능을 제공</p>

<ol>
    <li>서비스단에서 트랜잭션이 시작하면 트랜잭션 매니저가 커넥션을 생성하고 autocommit을 false로 세팅한 뒤 트랜잭션 동기화 매니저의 스레드 로컬에 커넥션을 보관</li>
    <li>이후 리포지토리 계층에서는 트랜잭션 동기화 매니저의 스레드 로컬에서 해당 커넥션을 가져와서 사용</li>
    <li>서비스 단에서 트랜잭션을 종료할 때는 트랜잭션 동기화 매니저에서 해당 커넥션을 가져와 커밋 또는 롤백을 수행하고 리소스를 정리하고 커넥션을 커넥션 풀에 반환함</li>
</ol>

<h3 style="color: cornflowerblue"> Spring을 사용해 트랜잭션을 적용하는 방법</h3>
<ol>
    <li>선언적 트랜잭션 : @Transactional 어노테이션을 사용 (AOP로 구성되어 프록시 패턴으로 동작함)</li>
    <li>프로그래밍 방식 트랜잭션 : 트랜잭션 매니저나 트랜잭션 템플릿을 사용해 프로그래밍 코드로 작성해 적용하는 방식</li>
</ol>

<h3 style="color: cornflowerblue"> JDBC, Spring JDBC, MyBatis, ORM, JPA, Hibernate, Spring Data Jpa</h3>
<h3 style="color: cornflowerblue"> 영속성 컨텍스트?</h3>
<h3 style="color: cornflowerblue"> JPA N+1 문제와 해결 방법</h3>
<h3 style="color: cornflowerblue"> 객체간의 상속관계를 DB에 적용시키기 위해 어떻게?</h3>
<h3 style="color: cornflowerblue"> Spring Batch에 대해</h3>