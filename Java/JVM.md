- reference 1: https://inpa.tistory.com/entry/JAVA-%E2%98%95-JVM-%EB%82%B4%EB%B6%80-%EA%B5%AC%EC%A1%B0-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EC%98%81%EC%97%AD-%EC%8B%AC%ED%99%94%ED%8E%B8
- reference 2: https://steady-snail.tistory.com/67

JVM이 상당히 생소하기 때문에 다른 아티클을 많이 참조하며 이해를 해봅시다. 강의 시간에 자바 가상머신을 간단히 다루었지만, 아직 궁금한 부분이 많기 때문에 전반적인 동작 방식과 클래스 로더, 실행 엔진, 런타임 데이터 영역으로 구분되는 주요 영역들에 대해 알아봅시다.

한 번의 정리만으로 모든 것을 이해하기 어려운 분야임이 분명합니다. 향후 추가적인 공부를 계속 해 나갑시다!

# 자바 가상 머신의 동작 방식

> 소스파일이 컴파일러에 의해 클래스파일(바이트코드)로 컴파일된 이후,
> 자바 프로그램이 시행되기 위해서는 여전히 추가 작업이 필요하다.

바이트 코드는 JVM은 이해할 수 있지만
여전히 기계가 바로 수행할 수 있는 언어가 아니기 때문이다.

클래스 파일은 어떻게 처리되는가? 하면
JVM 내부의 3 구간을 거쳐 처리된다.

Class Loader가 필요한 클래스를 동적으로 끌어온다면,
Runtime Data Area(JVM의 메모리)에는 끌어온 클래스가 올라가고
Execution Engine은 바이트 코드를 기계어에 맞게 해석하고 실행한다.

>

자바 가상 머신인 JVM은 자바 애플리케이션을 클래스 로더를 통해 읽어 자바 API와 함께 실행한다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/1c790d4f-ef31-4b48-897c-415e9fb4a5d5/Untitled.png)

JVM이 자바 소스 파일 코드를 읽는 과정을 요약하면 다음과 같다.

1. 자바 프로그램을 실행하면 JVM은 OS로부터 메모리를 할당받는다 .
2. **자바 컴파일러**(javac)**가** **자바 소스코드**(.java)**를 자바 바이트 코드**(.class)**로 컴파일**한다
3. **클래스 로더**는 동적 로딩을 통해 **필요한 클래스들을** 로딩 및 링크하여 **Runtime Data Area(실질적인 메모리를 할당받아 관리하는 영역)에 올린다.**
4. **Runtime Data Area에 로딩된 바이트 코드는 Execution Engine을 통해 해석(실행)된다**
5. 이 과정에서 Execution Engine에 의해 Garbage Collector의 작동과 Thread 동기화가 이루어진다.

# 자바 가상 머신의 구조

> 클래스 로더 (Class Loader)

실행 엔진 (Execution Engine)

- 인터프리터
- JIT 컴파일러
- 가비지 콜렉터

런타임 데이터 영역 (Runtime Data Area)

- 메소드 영역(Runtime Constant Pool 포함)
- 힙 영역
- 스택 영역
- PC 레지스터
- 네이티브 메소드 스택
  >

Class Loader, Runtime Data Area, Execution Engine을 좀 더 상세화하면 아래와 같다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/489b2b86-1954-467e-bdd1-ea3effcc6b3a/Untitled.png)

JVM은 아래와 같이 구성되어 있다.

1. **클래스 로더(Class Loader)**
2. **실행 엔진(Execution Engine)**
   1. 인터프리터(Interpreter)
   2. JIT 컴파일러(Just-in-Time)
   3. 가비지 콜렉터(Garbage collector)
3. **런타임 데이터 영역(Runtime Data Area)**
   1. 메소드 영역
   2. 힙 영역
   3. PC Register
   4. 스택 영역
   5. 네이티브 메소드 스택
4. JNI - 네이티브 메소드 인터페이스(Native Method Interface)
5. 네이티브 메소드 라이브러리(Native Method Library)

---

## 1️⃣ 클래스 로더(Class Loader)

JVM 내로 클래스 파일(.class)을 동적으로 로드하고 링크를 통해 배치하는 작업을 수행한다. 로드된 **바이트 코드(.class)들을 엮어서 JVM의 메모리 영역인 Runtime Data Area에 배치**한다. 로딩 기능은 클래스를 메모리에 한 번에 올리지 않고 어플리케이션에서 클래스를 필요로 하는 경우에 동적으로 메모리에 적재한다.

### 클래스 파일의 로딩 순서

Loading → Linking(Verifying → Preparing → Resolving) → Initialization

1. Loading : 클래스 파일을 가져와서 JVM의 메모리에 로드한다.
2. Linking : 클래스 파일을 사용하기 위해 검증한다
   1. Verifiying(검증) : 읽어들인 클래스가 JVM 명세에 명시된 대로 구성되어 있는지 검사한다.
   2. Preparing(준비) : 클래스가 필요로 하는 메모리를 할당한다.
   3. **Resolving(분석) : 클래스 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경한다.**
3. Initialization : 클래스 변수들을 **적절한 값으로 초기화**한다. (static 필드들을 설정된 값으로 초기화하는 등 .. )

---

## 2️⃣ 실행 엔진(Execution Engine)

클래스 로더를 통해 런타임 데이터 영역에 배치된 **바이트 코드를 명령어 단위로 읽어서 실행**한다. 자바 바이트 코드(.class)는 기계가 바로 수행할 수 있는 언어보다는 가상머신이 이해할 수 있는 중간 레벨로 컴파일 된 코드이다. 그래서 실행 엔진은 바이트 코드를 실제로 JVM 내부에서 기계가 실행할 수 있는 형태로 변경해준다.

이 수행 과정에서 실행 엔진은 **인터프리터**와 **JIT 컴파일러** 두 가지 방식을 혼합해 바이트 코드를 실행한다.

### 인터프리터

바이트 코드 **명령어를 하나씩 읽어서 해석하고 바로 실행**한다.

JVM 안에서 바이트 코드는 인터프리터 방식으로 동작한다. 다만 같은 메소드라도 여러 번 호출이 된다면 매번 해석하고 수행해야 돼서 전체적인 속도는 느리다.

### JIT 컴파일러

인터프리터의 단점을 보완하기 위해 도입되었다. 반복되는 코드를 발견해 **바이트 코드 전체를 컴파일해 Native Code로 변경**하고 이후에는 해당 메서드를 더 이상 인터프리팅 하지 않고 캐싱해 두었다가 **네이티브 코드로 직접 실행**하는 방식이다.

- 네이티브 코드
  자바에서 부모가 되는 **C, C++**, 어셈블리어로 구성된 코드

하나씩 인터프리팅해 실행하는 것이 아니라, 컴파일된 네이티브 코드를 실행하는 것이기 때문에 전체적인 실행 속도는 인터프리팅 방식보다 빠르다.

하지만 바이트코드를 Native Code로 변환하는 데에도 비용이 소요되므로, JVM은 모든 코드를 JIT 컴파일러 방식으로 실행하지 않고 인터프리터 방식을 사용하다 일정 기준이 넘어가면 JIT 컴파일 방식으로 명령어를 실행하는 식으로 진행한다.

### 가비지 컬렉터 (Garbage Collector, GC)

자바 가상 머신은 **가비지 컬렉터**를 이용해 **Heap 메모리 영역에서 더는 사용하지 않는 메모리를 자동으로 회수**해준다.

C언어의 경우 직접 개발자가 메모리를 해제해줘야 하지만 자바는 이 가비지 컬렉터를 이용해 자동으로 메모리를 실시간으로 최적화해준다. 따라서 개발자가 따로 메모리를 관리하지 않아도 된다.

GC가 실행되는 시간은 정해져 있지 않고, 일반적으로 자동으로 실행된다.

특히 Full GC가 발생하는 경우, GC를 제외한 모든 스레드가 중지되기 때문에 장애가 발생할 수 있다.

- 수동으로 GC 실행하기
  `System.gc()`라는 메소드를 사용할 수는 있지만, 함수가 실제로 실행되는 것은 보장할 수 없다.

---

## 3️⃣ 런타임 데이터 영역(Runtime Data Area)

런타임 데이터 영역은 쉽게 말하면 JVM의 메모리 영역으로 **자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재**하는 영역이다. 런타임 데이터 영역은 크게 Method Area, Heap Area, Stack Area, PC Register, Native Method Stack으로 나눌 수 있다.

메서드 영역, 힙 영역은 모든 스레드가 공유하는 영역이고 stack area, pc register, native method stack은 각 쓰레드마다 생성되는 개별 영역이다.

### 메서드 영역(Method Area, aka Class Area or Static Area)

JVM이 시작될 때 생성되는 공간으로 **바이트 코드(.class)**를 처음 메모리 공간에 올릴 때 **초기화되는 대상을 저장**하기 위한 메모리 공간이다.

JVM이 동작하고 클래스가 로드될 때 적재되서 **프로그램이 종료할때까지 저장**된다.

모든 쓰레드가 공유하는 영역이라 다음과 같이 초기화 코드 정보들이 저장되게 한다.

1. `Field Info` : 멤버 변수의 이름, 데이터 타입, 접근 제어자의 정보
2. `Method Info` : 메소드 이름, return 타입, 함수 매개변수, 접근 제어자의 정보
3. `Type Info` : Class인지 Interface인지 여부를 저장한다. Type의 속성, 이름. Super Class의 이름.

간단히 말해 메서드 영역에는 **정적 필드**와 **클래스 구조**만을 갖고 있다.

- 메소드 영역 / 런타임 상수 풀의 사용기간과 스레드 공유 범위
  - 메소드 영역(과 그 내부의 런타임 상수 풀)은 JVM 시작 시 생성되어 프로그램이 종료할 때까지 클래스를 저장한다.
  - 명시적으로 null을 선언해도 종료되는 듯 ?
- **Runtime Constant Pool**
  - 메서드 영역에 존재하는 별도의 관리 영역으로, 메서드 영역에 포함되지만 독자적인 중요성을 띈다.
  - 각 클래스/인터페이스마다 별도의 constant pool 테이블이 존재하는데, 클래스를 생성할 때 참조해야 할 정보들을 상수로 가지고 있는 영역이다.
  - JVM은 이 Constant Pool을 통해 해당 메소드나 필드의 실제 메모리 상의 주소를 찾아 참조한다.
  - **상수 자료형을 저장해 참조하고 중복을 막는 역할**을 수행한다.

### 힙 영역(Heap Area)

힙 영역은 메서드 영역과 함께 모든 쓰레드가 공유하는 영역이다.

JVM이 관리하는 프로그램 상에서 데이터를 저장하기 위해 런타임 시 동적으로 할당해 사용하는 영역이다.

즉, **`new` 연산자로 생성되는 클래스와 인스턴스 변수, 배열 타입 등 Reference Type이 저장되는 곳이다.**

당연히 Method Area 영역에 저장된 클래스만이 생성되어 Heap Area에 적재된다.

- 힙 영역의 사용기간 및 스레드 공유 범위
  - 객체가 더이상 사용되지 않거나 명시적으로 null을 선언했을 때 종료된다.
  - GC(Garbage Collection)의 대상이다.

유의할 점은 힙 영역에 생성된 객체와 배열은 **Reference Type**으로서, JVM 스택 영역의 변수나 다른 객체의 필드에서 참조된다는 점이다. 즉, 힙의 참조 주소는 “스택”이 가지고 있고 해당 객체를 통해서만 힙 영역에 있는 인스턴스를 핸들링할 수 있는 것이다.

만일 참조하는 변수나 필드가 없다면 의미 없는 객체가 되기 때문에 이것을 쓰레기로 취급하고 JVM은 쓰레기 수집기인 Garbage Collector를 실행시켜 쓰레기 객체를 힙 영역에서 자동으로 제거한다.

이처럼 힙 영역은 **가비지 컬렉션**의 대상이 되는 공간이다. 그리고 효율적인 가비지 컬렉션 수행을 위해 힙 영역은 5가지 영역으로 나뉘게 된다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/a7f6b40d-6267-4368-a54c-65d274421389/Untitled.png)

1. Eden
2. Survivor 1
3. Survivor 2
4. Old
5. Permanent

이 다섯 영역은 다시 물리적으로 Young Generation과 Old Generation 으로 구분된다.

- Young Generation : 생명 주기가 짧은 객체를 GC 대상으로 하는 영역
  - Eden : new로 새로 생성된 객체가 위치한다. 정기적인 가비지 콜렉션 이후 살아남은 객체들은 Survivor로 이동한다.
  - Survivor 1, 2 : 각 영역이 채워지고 나면, 살아남은 객체는 비워진 Survivor에 순차적으로 이동한다.
- Old Generation : 생명 주기가 긴 객체를 GC 대상으로 하는 영역. Young Generation에서 마지막까지 살아남은 객체가 이동한다.

### 스택 영역(Stack Area)

스택 영역은 `int`, `long`, `boolean` 등 기본 자료형을 생성할 때 저장하는 공간으로, **임시적으로 사용되는 변수나 정보들이 저장되는 영역이다.**

자료구조 Stack은 마지막에 들어온 값이 먼저 나가는 LIFO (Last in First Out) 구조로 push와 pop 기능을 사용하는 방식으로 동작한다.

메서드를 호출할 때 마다 각각의 **스택 프레임(그 메서드만을 위한 공간)**이 생성되고 메서드 안에서 사용되는 값들을 저장하고, 호출된 메서드의 매개변수, 지역변수, 리턴 값 및 연산 시 일어나는 값들을 임시로 저장한다.

그리고 메서드 수행이 끝나면 프레임별로 삭제된다.

- **스택 프레임 (stack frame)**
  메소드가 호출될 때마다 프레임이 만들어지며, 현재 실행중인 메소드의 상태 정보를 저장하는 곳이다. 메서드의 호출 범위가 종료되면 스택에서 제거된다.
  스택 프레임에 쌓이는 데이터는 메서드의 매개변수, 지역변수, 리턴값, 연산 시 결과값 등이 있다.

단, 데이터 타입에 따라 스택(stack)과 힙(heap)에 저장되는 방식이 다르다는 점은 유의해야 한다.

1. **기본(원시)타입** 변수는 **스택 영역**에 직접 값을 가진다.
2. **참조타입** 변수는 **힙 영역이나 메소드 영역의 객체 주소**를 가진다.

- 예시
  가령 `Person p = new Person();`과 같이 클래스를 생성할 경우, `new`에 의해 생성된 **클래스는 Heap Area에 저장**되고, **Stack Area에는** 생성된 클래스의 참조인 **`p`만 저장**된다.

스택 영역은 각 스레드마다 하나씩 존재하며, 스레드가 시작될 때 할당된다. 프로세스가 메모리에 로드될 때 스택 사이즈가 고정되어 있어서 런타임 시에 스택 사이즈를 바꿀 수는 없다.

만일 고정된 크기의 JVM 스택에서 프로그램 실행 중 메모리 크기가 충분하지 않다면 `StackOverFlowError`가 발생한다.

쓰레드를 종료하면 런타임 스택도 사라진다.

여기까지 배운 메소드 영역, 힙 영역, 스레드 영역을 한 그림으로 표시하자면 아래와 같은 도식이 그려진다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e8f11927-b70c-4524-9227-a3efac08e7aa/1665a4f8-666b-414c-b12b-9a5557135f2f/Untitled.png)

### PC 레지스터(Program Counter Register)

**PC 레지스터**는 쓰레드가 시작될 때 생성되며, **현재 수행중인 JVM 명령어 주소를 저장**하는 공간이다. JVM 명령의 주소는 쓰레드가 어떤 부분을 무슨 명령으로 실행해야할 지에 대한 기록을 가지고 있다.

**일반적인 CPU Register**

일반적으로 프로그램의 실행은 **CPU에서 명령어(Instruction)를 수행**하는 과정으로 이루어진다. 이때 CPU는 연산을 수행하는 동안 필요한 정보를 레지스터라고 하는 CPU 내의 기억장치를 이용하게 된다. 가령 A, B라는 데이터와 피연산 값인 Operand가 있고 이를 더하라는 연산 Instruction이 있다고 하자. A, B, 그리고 더하기 연산이 순차적으로 진행되는데, 이때 A를 받고 B를 받는 동안 이 값을 CPU가 어디에 기억해 둬야 할 필요가 생긴다. 이 공간이 바로 CPU 내의 기억장치 Register이다.

**자바의 PC Register**

자바는 OS나 CPU의 입장에서는 하나의 프로세스이기 때문에 가상 머신(JVM)의 리소스를 이용해야 한다. 그래서 자바는 CPU에 직접 연산을 수행하도록 하는 것이 아닌, **현재 작업하는 내용을 CPU에게 연산으로 제공**해야 하며, **이를 위한 버퍼 공간**으로 PC Register라는 메모리 영역을 만들게 된 것이다.

따라서 JVM은 스택에서 비연산값 Operand를 뽑아 별도의 메모리 공간인 PC Register에 저장하는 방식을 취한다.

만약에 스레드가 자바 메소드를 수행하고 있으면 JVM 명령(Instruction)의 주소를 PC Register에 저장한다. 그러다 만약 자바가 아닌 다른 언어(C언어, 어셈블리)의 메소드를 수행하고 있다면, undefined 상태가 된다. 자바에서는 이 두 경우를 따로 처리하기 때문이다. (이 부분이 뒤에 언급되는 Native Method Stack 공간이다)

### 네이티브 메서드 스택(Native Method Stack)

**네이티브 메서드 스택**은 자바 코드가 컴파일되어 생성되는 바이트 코드가 아니라 실제 실행할 수 있는 **기계어로 작성된 프로그램을 실행**시키는 영역이다.

자바 이외의 언어(C, C++, 어셈블리 등)로 작성된 네이티브 코드를 실행하기 위한 공간이기도 하다. 일반적인 C 스택을 메모리 영역으로 사용한다.

JIT 컴파일러에 의해 변환된 Native Code도 여기에서 실행이 된다고 보면 된다.

일반적으로 메소드를 실행하는 경우 JVM 스택에 쌓이다가 해당 메소드 내부에 네이티브 방식을 사용하는 메소드가 있다면 해당 메소드는 네이티브 스택에 쌓인다.

그리고 네이티브 메소드 수행이 끝나면 다시 자바 스택으로 돌아와 작업을 수행한다. 그래서 네이티브 코드로 되어 있는 함수의 호출을 자바 프로그램 안에서도 직접 수행할 수 있고 그 결과를 받아올 수도 있는 것이다.

네이티브 메소드 스택은 네이티브 메소드 인터페이스(JNI)와 연결되어 있는데, JNI가 사용되면 네이티브 메서드 스택에 바이트 코드로 전환되어 저장된다.

---

## 4️⃣ JNI(Java Native Interface)

자바가 다른 언어로 만들어진 애플리케이션과 상호작용할 수 있는 인터페이스를 제공하는 프로그램이다. JNI는 JVM이 Native Method를 적재하고 수행할 수 있도록 한다. 실질적으로 잘 동작하는 언어는 C / C++밖에 없다고 .?

---

## 5️⃣ Native Method Library

C, C++로 작성된 라이브러리를 칭한다. 헤더가 필요하면 JNI는 이 라이브러리를 로딩해 실행한다.