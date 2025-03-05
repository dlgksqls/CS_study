<h1> Java 면접 대비 지식</h1>
<p>https://hoons-dev.tistory.com/96 의 내용 참고 학습</p>

<h3 style="color: cornflowerblue"> 1. Java의 장단점</h3>
<ul>
    <li>JVM 위에서 실행되기 때문에 OS에 종속적이지 않고, 독립적으로 실행될 수 있음</li>
    <li>객체지향 언어로, 객체지향 프로그래밍이 가능함</li>
    <li>클래스로더에 의해 동적 로딩을 지원함. 실행 시 모든 객체를 생성하는 것이 아니라, 필요한 시점에 클래스를 생성한다.</li>
    <li>바이트코드로 변환하고, JVM에 의해 기계어로 번역되므로 한번의 컴파일링을 거치는 언어에 비해서 조금 느리다.</li>
</ul>

<h3 style="color: cornflowerblue"> JVM?</h3>
<p>JVM은 Java Virtual Machine의 줄임말로, OS와 Java Application 사이를 중재해주는 가상 머신.</p>
<p>JVM은 크게 실행에 필요한 클래스를 Runtime Data Area로 링킹 하고 로딩을 해주는 ClassLoader, 실제 실행과 번역을 담당하는 Execution Engine, 별도의 쓰레드로써 힙 메모리의 참조되지 않는 객체를 삭제하는 Garbage Collector, 각 메모리의 영역 및 쓰레드가 담겨있는 Runtime Data Area로 구성되어 있음</p>

<h3 style="color: cornflowerblue"> Java Application이 JVM에서 실행되는 과정</h3>
<ol>
    <li>JVM은 OS로부터 적당한 메모리 (Runtime Data Area)를 할당 받음</li>
    <li>자바 소스 코드(.java)를 자바 컴파일러(javac)에 의해 바이트코드 (.class)파일로 변환</li>
    <li>Class Loader를 통해 .class파일을 Runtime Data Area로 로딩</li>
    <li>로딩된 class 파일을 Execution Engine을 통해 해석 및 실행</li>
</ol>

<h3 style="color: cornflowerblue"> JVM의 메모리(Runtime Data Area)구조</h3>
<ul>
    <li>메서드 (static) 영역
        <ul>
            <li>클래스가 사용되면 해당 클래스의 파일(.class)을 읽어들여, 클래스에 대한 정보(바이트 코드)를 메서드 영역에 저장</li>
            <li>클래스와 인스턴스, 메서드, 필드, static 변수, final 변수 등이 저장되는 영역</li>
        </ul>
    </li>
    <li>JVM 스택 영역
        <ul>
            <li>스레드마다 존재하여 스레드가 시작할 때마다 할당</li>
            <li>지역 변수, 매개 변수, 연산 중 발생하는 임시 데이터 저장</li>
            <li>메서드 호출 시마다 개별적 스택 생성</li>
        </ul>
    </li>
    <li>JVM 힙 영역
        <ul>
            <li>런타임 시 동적으로 할당하여 사용하는 영역</li>
            <li>new 연산자로 생성된 객체와 배열 저장</li>
            <li>참조가 없는 객체는 GC(가비지 컬렉터)의 대상</li>
        </ul>
    </li>
    <li>pc register
        <ul>
            <li>쓰레드가 현재 실행할 스택 프레임의 주소를 저장</li>
        </ul>
    </li>
    <li>Native Method Stack
        <ul>
            <li>C/C++등의 Low level 코드를 실행하는 스택</li>
        </ul>
    </li>
</ul>

<h3 style="color: cornflowerblue"> Garbage Collector가 무엇인지, 어떻게 동작하는지</h3>
<p>동적으로 할당한 메모리 영역 중, 사용하지 않는 영역을 탐지해 해제하는 역할을 함</p>
<p>Java에서 동적 변수를 할당하는 영역은 Heap 영역이므로, JVM의 GC의 작동 대상은 Heap 메모리임</p>
<p>기존 참조 변수와 참조 변수가 가리키는 동적 변수 관계에서 참조 변수가 함수 종료에 의해 pop되고 나면 힙 영역에 동적 변수만 남는데, 이러한 변수를 Unreachable Object라고 표현하고, 이 변수가 GC의 관리 대상이 된다.</p>

<p>GC의 장단점</p>
<ul>
    <li>메모리 누수 방지</li>
    <li>해제된 메모리에 대해 접근하는 것을 방지</li>
    <li>해제한 메모리를 다시 해제하는 것을 방지</li>
    <li>개발자가 일일히 동적 변수의 제거 선언을 하지 않아도 됨</li>
    <li>하지만, 개발자가 GC가 언제 수행되는지 정확하게 알 수 없음</li>
    <li>실행중인 작업을 중단하고, 리소스를 GC 작업에 내줘야 하므로 오버헤드 발생</li>
</ul>

<p>Java는 Mark and Sweep 방식으로 GC르 진행함</p>
<p>Stack의 모든 변수를 스캔하면서 어떤 힙의 객체를 참조하는지 마킹하고, 마킹하고 있는 개체가 참조하고 있는 객체 또한 마킹한다. 마킹하지 않은 객체를 Heap에서 제거하는 알고리즘이다.</p>

<h3 style="color: cornflowerblue"> Java에서 ==과 equals의 차이 동일성(identity)vs 동등성(equality)</h3>
<p>'=='연산은 참조 비교로, 두 객체가 같은 메모리 공간을 가리키는 지를 확인하는 연산임 (동일성)</p>
<p>'equals'연산은, 두 객체의 내부 값이 같은 지 내용을 비교함. (동등성) 기본 타입에 대해서는 사용할 수 없고, 객체 비교시 override해서 원하는 방식으로 수정 가능</p>

<h3 style="color: cornflowerblue"> Java의 접근 제한자</h3>
<ul>
    <li>public : 접근에 제한 없음</li>
    <li>private : 자기 자신 클래스 내에서만 접근 가능</li>
    <li>default : 동일한 패키지 내에서만 접근 가능</li>
    <li>protected : 동일한 패키지 내에서만 접근 가능 + 상속을 이용한 접근 가능</li>
</ul>

<h3 style="color: cornflowerblue"> Java에서의 데이터 타입</h3>
<p>원시 자료형 타입(Primitive Type)</p>
<ul>
    <li>기본 타입의 크기가 작고 고정적이기 때문에 메모리 Stack 영역에 저장됨</li>
    <li>정수형 : byte, short, int, long</li>
    <li>실수형 : float, double</li>
    <li>논리형 : boolean</li>
    <li>문자형 : char</li>
</ul>

<p>참조 타입(Reference Type)</p>
<ul>
    <li>원시자료형을 제외하고는 모두 참조형</li>
    <li>String과 박싱 타입인 Integer등이 있음</li>
    <li>참조 타입은 데이터의 크기가 가변적이고, 동적이므로 Heap 영역에서 관리됨</li>
    <li>데이터는 Heap 영역에서 관리되지만 메모리의 주소값은 Stack 영역에 담김</li>
    <li>new 키워드를 이용해 객체를 생성하여 데이터가 생성된 주소를 참조하는 타입</li>
    <li>String과 배열은 일반적인 참조 타입과 달리 new 없이 생성 가능하지만 참조 타입임</li>
    <li>더 이상 참조하는 변수가 없을 때 GC에 의해 살제됨</li>
</ul>

<h3 style="color: cornflowerblue"> Java의 hashcode()란</h3>
<p>두 객체가 동일한 객체인지 비교할 때 사용하고, Heap 영역에 저장된 객체의 메모리 주소를 반환함</p>

<h3 style="color: cornflowerblue"> Java의 Wrapper Class란?</h3>
<p>원시 자료형 타입의 데이터를 객체로 취급해야 할 경우 사용하는 클래스, 기본 타입의 데이터를 객체로 변환해주는 클래스</p>
<p>산술 연산을 위해 정의된 클래스가 아니므로, 인스턴스 내의 값을 변경할 수 없다.</p>

<h3 style="color: cornflowerblue"> Boxing과 UnBoxing에 대해</h3>
<p>기본 타입의 변수를 래퍼클래스의 인스턴스로 변경하는 과정을 박싱, 래퍼클래스의 인스턴스를 다시 기본 타입으로 꺼내는 과정을 언박싱</p>

<h3 style="color: cornflowerblue"> Java의 static 변수에 대해</h3>
<p>클래스당 하나만 생성되고, 동일한 클래스의 모든 객체들에 의해 공유됨</p>
<p>다른 객체들이 생기기 전에 이미 생성되고, 프로그램이 종료시에 사라짐</p>

<h3 style="color: cornflowerblue"> Java의 main 메소드가 static인 이유에 대해</h3>
<p>static 멤버는 프로그램 시작 시, 클래스 로더에 의해 메모리에 로드되어 인스턴스를 생성하지 않아도 호출이 가능하기 때문</p>
<p>Runtime Data Area에서 Method Area(=Class Area, Static Area)라고 불리는 영역에서 static 키워드를 가진 변수, 메소드가 생성됨.</p>
<p>따라서 JVM은 별도로 인스턴스를 생성하지 않아도, Method Area에 로드된 main()을 실행하게 됨</p>


<h3 style="color: cornflowerblue"> final, finally, finalize의 차이</h3>
<p>final 키워드</p>
<ul>
    <li>변수, 메서드 클래스가 변경 불가능 하도록 만든다</li>
    <li>기본 타입 변수에 적용 시 해당 변수의 값 변경이 불가능하다</li>
    <li>참조 변수에 적용 시 참조 변수가 힙 내의 다른 객체를 가리키도록 변경할 수 없다</li>
    <li>메서드에 적용 시 해당 메서드를 오버라이드 할 수 없다 (오버로딩은 가능)</li>
    <li>클래스에 적용 시 해당 클래스를 상속 받아서 사용할 수 없다</li>
</ul>

<p>finally 키워드</p>
<p>try catch 블록 뒤에서 항상 실행될 코드 불록을 정의하기 위해 사용된다.</p>

<p>finalize 메서드</p>
<p>가비지 컬렉터가 더 이상의 참조가 존재하지 않는 객체를 메모리에서 삭제하겠다고 결정하는 순간 호출된다.</p>

<h3 style="color: cornflowerblue"> try-catch-finally의 단점과, 이로 인해 나온 구문</h3>
<p>try-catch-finally 구문에서 리소스를 생성하게 되면, 생성은 try에서 하고 반납은 finally에서 하다보니 실수의 발생 여지가 있음</p>
<p>그래서 나온 구문으로 try-with-resources가 있다. try 옆에 괄호로 리소스를 생성해주면, 따로 반납 코드를 작성하지 않아도 자동으로 리소스르 반납한다.</p>

<h3 style="color: cornflowerblue"> Java의 제네릭</h3>
<p>제네릭(Generic)은 클래스 내부에서 타입을 지정하는 것이 아닌, 외부에서 사용자에 의해 지정되는 것을 의미함</p>
<p>특정 타입(Specific)을 미리 지정하는 것이 아니라, 필요에 의한 지정을 그때 그떄 할 수 있는 일반 타입(Generic)인 것이다.</p>
<p>장점</p>
<ul>
    <li>잘못된 타입이 들어오는 것을 컴파일 단계에서 방지할 수 있다.</li>
    <li>클래스 외부에서 타입을 지정하기 때문에 따로 타입을 체크하고 변환할 필요가 없어 관리하기 용이하다.</li>
    <li>비슷한 기능을 지원하는 경우 코드의 재사용성이 높아진다.</li>
</ul>

<h3 style="color: cornflowerblue"> Java의 직렬화와 역직렬화</h3>
<p>직렬화</p>
<ul>
    <li>자바 시스템 내부에서 사용되는 객체 또는 데이터를 외부의 자바 시스템에서도 사용할 수 있도록 바이트 형태로 데이터를 변환하는 기술</li>
    <li>조건
        <ul>
            <li>자바의 기본 타입</li>
            <li>Serializable 인터페이스 상속받은 객체</li>
        </ul>
    </li>
    <li>ObjectOutputStream 객체를 이용</li>
</ul>

<p>역직렬화</p>
<ul>
    <li>바이트로 변환된 데이터를 다시 객체로 변환하는 기술</li>
    <li>ObjectInputStream 객체를 이용</li>
</ul>

<h3 style="color: cornflowerblue"> 추상클래스와 인터페이스</h3>
<p>추상클래스는, abstract 키워드를 사용해 선언한 클래스로, 추상 메소드를 최소 한 개 이상 포함한 클래스</p>
<p>추상메소드는, abstract 키워드를 사용해 원형만 선언되고 내부 코드는 작성하지 않은 메서드를 뜻함</p>
<p>추상클래스 내부에 추상메소드 외에 다른 것들도 추가가 가능하다는 것이 특징이고, 추상클래스의 사용 주 목적은 관령성이 높은 클래스 간의 코드를 공유하고 확장하고 싶은 목적</p>

<p>인터페이스는, interface 키워드를 사용해 선언하며 default와 static를 제외하고는 추상 메소드와 상수만을 포함함</p>
<p>interface 내부의 모든 메소드는 추상 메소드로, abstract public이 생략되어 있는 상태임</p>
<p>상수 필드는 public static final이 생략되어 있음</p>
<p>인터페이스는 다중 상속이 가능하여 관련성이 없는 클래스들의 논리적으로 같은 기능을 자신에 맞게 구현을 강제하는데 목적을 가짐</p>

<h3 style="color: cornflowerblue"> Error vs Exception</h3>

<h3 style="color: cornflowerblue"> String vs StringBuilder vs StringBuffer</h3>
<p>새로운 값을 할당할 때마다 새로운 동적 변수(인스턴스)가 생성됨, String에 대한 연결 연산으로 '+'를 사용하면, 두 String을 연결한 새로운 객체가 생성됨</p>
<p>가비지 컬렉터가 호출되기 전까지 생성된 String 객체들은 Heap에 계속해서 머물기 때문에 메모리 관리 측면에서 치명적임</p><br>

<p>StringBuilder는 String과 다르게 가변성을 가지는 클래스, append(), delete()등의 method를 사용해 동일 객체 내에서 문자열을 변경하는 것이 가능함</p>
<p>동기화를 지원하지 않기 때문에, 멀티 쓰레드 환경에서 사용하는 것은 적합하지 않음, 하지만 동기화를 고려하지 않는 만큼 단일스레드에서의 성능은 StringBuffer보다 뛰어남</p><br>

<p>StringBuffer는 String과 다르게 가변성을 가지는 클래스임 append(), delete()등의 method를 사용해 동일 객체 내에서 문자열을 변경하는 것이 가능하다.</p>
<p>동기화를 지원하기 때문에 멀티 스레드 환경에서 thread-safe하다.</p>

<h3 style="color: cornflowerblue"> new String("")와 ""의 차이</h3>
<p>""로 문자열을 초기화 하게 되면, Java Heap 메모리의 String Pool에 저장이 된다.</p>
<p>만약 두개의 객체를 ""로 선언하면 두개는 똑같은 String Pool내의 ""를 가리키게 됨</p><br>
<p>new 키워드를 사용하는 것은, new를 사용하여 객체를 새로 생성했기 때문에, String Pool이 아닌, 그냥 Heap영역에 각각 생성됨</p>
<p>두 개의 단어는 다른 주소를 가리킴</p><br>

<p>굳이 객체로 만들어 GC의 대상이 되는 것보다, String Pool로 만들어 활용하는 것이 메모리 효율 측면에서 유리할 것으로 보임</p>

<h3 style="color: cornflowerblue"> Java 리플렉션에 대해 <strong style="color:red;">공부하기</strong></h3>
<p>컴파일 시간이 아닌, 런타임 시간에 메모리에 올라간 클래스나 메소드의 정의를 동적으로 찾아서 조작할 수 있는 기술</p>

<h3 style="color: cornflowerblue"> Stream() <strong style="color:red;">공부하기</strong></h3>
<h3 style="color: cornflowerblue"> Fork-Join-Pool</h3>
<h3 style="color: cornflowerblue"> Optional</h3>
<h3 style="color: cornflowerblue"> MultiThread</h3>
<h3 style="color: cornflowerblue"> 동기화</h3>




