# 1. JAVA

[mong-head/javastudy](https://github.com/mong-head/javastudy)

# JAVA build tool

- maven
- gradle ( 많이 씀)

## maven

1. 1개 생성해보기

    생성 : file - new - project - maven project 

    group id : 회사 도메인 거꾸로 (com.douzone)

    - jar : console
    - war : web

    github 에 올릴 때 : pom.xml (.project, .setting등 빼고)

    maven project 

    pom.xml 형태

    ```xml
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.douzone</groupId>
      <artifactId>helloworld</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      
      <packaging>jar</packaging>
      
      <dependencies>
      	<dependency>
        	<groupId>org.mariadb.jdbc</groupId>
        	<artifactId>mariadb-java-client</artifactId>
        	<version>2.7.2</version>
    	</dependency>
      </dependencies>
      
      <build>
      	
      </build>
    </project>
    ```

    - dependencies : (실습)mariadb jdbc maven 검색 후 2.72 버전 maven 복사 ([https://mvnrepository.com/artifact/org.mariadb.jdbc/mariadb-java-client/2.7.2](https://mvnrepository.com/artifact/org.mariadb.jdbc/mariadb-java-client/2.7.2))
    - build : ?
2. multi projects

    maven 장점 : multi projects (native eclipse는 안됨 (?))

    a project

    - mvc → war
    - api → war
    - .lib → jar file

    - 부모 project : pom으로 만들기(jar아닌)
        - pom.xml

        ```xml
        <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
          <modelVersion>4.0.0</modelVersion>
          <groupId>com.douzone</groupId>
          <artifactId>javastudy</artifactId>
          <version>0.0.1-SNAPSHOT</version>
          <packaging>pom</packaging>
          
          <modules>
          	<module>chapter03</module>
          </modules>
        </project>
        ```

    - 자식 project : jar로
        - 자식 project의 pom.xml

            ```xml
            <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
              <modelVersion>4.0.0</modelVersion>
              <parent>
                <groupId>com.douzone</groupId>
                <artifactId>javastudy</artifactId>
                <version>0.0.1-SNAPSHOT</version>
              </parent>
              <artifactId>chapter03</artifactId>
              <packaging>jar</packaging>
            </project>
            ```

- github에 올릴 때 .gitignore

    pom.xml이 중요한 파일

    ```
    **/.classpath
    **/.project
    **/.settings/
    **/target/
    **/build/
    ```

# 객체지향

### overview

### 클래스

---

필드

메소드

생성자

### 캡슐화

---

정보은닉

### 상속

---

### 다형성

---

오버로딩

오버라이딩(⭐)

### API

---

lang

util

io

### NP

---

= network programming

---

### JVM

method area : static 변수 저장

stack : 지역 변수 저장

heap : 인스턴스 변수 저장

### 클래스,객체

객체 : (=인스턴스) 객체가 메모리에 할당될 때

```java
책 b = new 책(); // b : reference 변수 - heap 참조
int i = 10; //i : 변수 - 메모리 내의 주소 저장
```

![1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled.png](1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled.png)

클래스 : (관례) 보통 첫 문자는 대문자로 함, 이름을 길게해도 어떤 함수인지 명확한 이름 짓기

cf) 변수 : 소문자

- instanceof 연산자
    - 참조 변수가 실제 참조하고 있는 인스턴스의 실제 타입을 알아보기 위한 연산자

    ```java
    System.out.println(c instanceof Drawable);
    ```

- final : 마지막으로 정의
    - 변수 : 대문자로만 이루어짐 (변경 불가능한 값)
    - class : 이후로 상속이 없을 것임을 알림

---

객체지향에서의 재사용성 재정립

- 추상화 : 필요한 것만 남기는 것

클래스는 재사용이 힘듦 : 추상화를 해서?

cf) AOP(관점지향) : 실제 세계에는 하나의 관점으로 ~~ , 그것을 토대로 구현하는 거는 또 다른 문제일 수 있음

자바에서는 변수(기본형 8가지)도 객체화하기를 지향함.

### 추상

추상클래스 : 포유류같은거 생각. → 구현이 안됨 : 인스턴스화 불가능

- 하나라도 추상함수(구현안함)등 있으면 추상클래스

extends ?

- 사람 extends 포유류

## 상속

- UML에서는 일반화

왜 사용?

1) 코드 재사용

2) 확장성 - 대부분 이 이유

확장성 : 상속 / 인터페이스 + 오버라이드 + 부모로 레퍼런싱

- 오버라이드 : 부모꺼 실행
- **부모 타입으로 referencing**

    부모 : 자동차 / 자식 : 버스, 포크레인,...

    → 자동차 a = new 버스() 로 사용.  (부모로 referencing)

    List< > l = new ArrayList() / new Vector() / new Linkedlist()

    - 확장성 별로

    ```
    주차시스템 {
    	주차하다(스포츠카 c){
    	}
    	주차하다(버스 c){
    	}
    }
    ```

    - 확장성이 좋아짐

    ```
    주차시스템 {
    	주차하다(자동차 c){
    	}
    }
    자동차 c = new 스포츠카();
    자동차 c = new 버스();
    ```

    - 인터페이스 개념까지 - 객체지향성 up

     : 자동차 클래스를 "주차하다"라는 메소드를 없애고(자동차 클래스는 더이상 추상 클래스가 아님) Parkable이라는 interface에 넣고, 자동차가 Parkable을 상속 

    ```
    주차시스템 {
    	주차하다(Parkable p){
    	}
    }
    Parkable b = new 자동차();
    ```

    ```
    주차시스템 —의존→ Parkable
    자동차 —구현→ Parkable
    버스, 스포츠카 —구현 → 자동차
    ```

    :  주차시스템과 버스사이 멀어짐.

좋은 코드 : 수정 close, 확장 open

### typecasting

- upcasting : 명시를 안해도 오류안남
- downcasting : 명시를 해야함 (부모가 다른 자식을 가리키고 있을 수도 있기 때문)

```java
package Person;

public class StudentTest {

	public static void main(String[] args) {
		Student s1 = new Student();
		s1.setName("둘리");
		s1.setGrade(4);
		s1.setMajor("CS");
		
		Person p1 = s1; //upcasting(암시적)
		//Student s2 = p1; //error : downcasting (p1이 가리키고 있는게 다른 자식일 수도 있기 때문에 오류임) - 명시적으로 알려줘야함
		Student s2 = (Student)p1; //downcasting(명시적)
	}
}
```

Person : 부모, Student: 자식

---

### 캡슐화

접근자 : 반드시 명시 (default는 잘 안쓰임 - 같은 package냐는 잘 따지지 않음)

정보 은닉 : field값에 대해 정보 은닉. 어떻게 구현되어있는 지 알 필요없이 만드는 것을 의미

interface로 진정한 캡슐화 가능

## Interface

- 기능 명세
- 보통 able로 끝남 (Parkable)
- 어색한 상속 피할 수 있음
    - Bird의 나는 기능이 Airplane에도 있다고 해서 airplane extends bird하는등의 어색한 상속을 피함

---

### Package : 소문자로만

cf) class, interface : 대문자로 시작

com.douzone.string String

서로 관련있는 클래스 및 인터페이스 모음

중복 회피위함

---

### 예외처리

코드

```java
		int a = 10;
		int b = 10 - a;
		
		System.out.println("some code...1");
		try {
			System.out.println("some code...2");
			int result = (1+2+3)/b;
			System.out.println("some code...3");			
		} catch(ArithmeticException e) {
			//1. 사과
			System.out.println("죄송합니다.");
			//2. 로깅 - 파일로 저장
			System.out.println("error:"+e);
			//3. 정상 종료
			//System.exit(0); //위험 - finally도 안함
			return; //finally는 실행됨
		} finally {
			//무조건 실행
			System.out.println("some code...finally(자원정리)");			
		}
		System.out.println("some code...5");
```

출력

catch로 정상종료 안하는 경우

```java
some code...1
some code...2
죄송합니다.
error:java.lang.ArithmeticException: / by zero
some code...4
some code...5
```

catch :  system.exit()사용

```java
some code...1
some code...2
죄송합니다.
error:java.lang.ArithmeticException: / by zero
```

catch : return;사용

```java
some code...1
some code...2
죄송합니다.
error:java.lang.ArithmeticException: / by zero
some code...finally(정상 종료)
```

CATCH

- 예외 처리하는 부분
- catch는 꼭 있어야 함 ( 몰라도 적어도 e.printStackTrace()를 적어놓아야함)
- 내용
    1. 사과
    2. 로깅 (보통 파일에 저장함)
    3. 정상 종료 (finally부분은 실행되고 종료되게 하기)

FINALLY

- 자원정리 코드

exception 종류

1) unchecked exception = error 

	logic error: 논리적인 이유로 나는 에러

	try-catch 안함 : 그냥 에러 고치는 식으로 함 (if-else문으로 해결)

	ex) ArithmeticException, ArrayIndexOutOfBoundsException

2) checked exception 

	try-catch 강제함 (boilerplate code 삽입 무조건 하게 함)

	try-catch는 처리하는게 많음, logic error의 경우 쓰지 않는 것이 좋음

	ex) FileInputStream의 경우

	```java
	FileInputStream fis = null;
	try {
		fis = new FileInputStream("./hello.txt");
		int data = fis.read();
		System.out.println(data);
	} catch (FileNotFoundException e) {
		// TODO Auto-generated catch block
		System.out.println("error:"+ e);
		//e.printStackTrace();
	} catch (IOException e) {
		System.out.println("error:"+ e);
	} finally {
		try {
			if(fis!= null) {
				fis.close();
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	```

예외처리 구문의 문제점

1) 코드 읽기 힘듦 (너무 복잡해짐)

** spring : AOP - 예외처리 더 나아짐 (핵심코드만 남게 할 수 있음) - 클래스랑 관련있는 듯(throw)

# API

lang, util, io, net

## 1. lang

### Object

기본적으로  Object 클래스를 상속받음

```
Object methods
--------------
getClass() #Class클래스 - reflection : 클래스 정보 알아냄
hashCode() #address기반 해싱값
equals()   #hashCode()와 단짝
toString() #getClass()+@+hashCode()
```

- hashing : 모든 값을 정수로 바꿈. 빠르게 비교할 때 good
- hashCode, equals 단짝인 이유
    - set에 넣을 때 동일 비교
        - hashCode먼저 비교 → 동일하다면 equals 비교" 순으로 진행.
        - hashCode가 오버라이딩되지 않았다면 서로 내용이 같은 객체들이 hash가 다르게 나옴.(주소 기반 해싱값이므로)
        - 다르다고 나오기 때문에 set에 동일한 내용의 객체인데도 다른 객체로 인식되어 들어가게 됨.
        - 따라서, 오버라이딩하는 경우 둘 다 고침

## 2. io

- network와 함께

|Input|InputStream|program|OutputStream|Output
|------|---|---|---|-----|
|file| | | |file|
|network| -> | | -> |network|
|keyboard| | | |console|
|memory| | | |memory|


1. 추상 클래스의 역할 ( ⭐ )
2. 주스트림 & 보조스트림 역할 ( ⭐ )

    보조스트림 : 주스트림에서 나온 데이터 가공 역할 (ex : byte로 들어온 것을 buffer에 저장해서 하나의 string으로 만든다던지 등등)

### 1. 추상 클래스

 - 4가지 알면 됨 : Inputstream, outputstream, Reader, Writer

![1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%201.png](1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%201.png)

read 시 byte 단위 / character 단위 나누어서 받음

1) Byte :  InputStream, OutputStream 

- memory to memory

    ```java
    public static void main(String[] args) throws IOException {
    	byte[] src = {1,2,3,4};
    	byte[] dest = null;
    	
    	InputStream is = new ByteArrayInputStream(src); //InputStream : 추상
    	OutputStream os = new ByteArrayOutputStream(); //OutputSteam : 추상
    	
    	//read & write
    	int data = -1;
    	while((data = is.read()) != -1 /*1byte read*/) {
    		os.write(data); //write
    	}
    	
    	dest = ((ByteArrayOutputStream)os).toByteArray(); //출력하기 위함
    	System.out.println(Arrays.toString(src));
    	System.out.println(Arrays.toString(dest));
    }
    ```

- file to file

    ```java
    public static void main(String[] args) {
    	InputStream is = null;
    	OutputStream os = null;
    	try {
    		is = new FileInputStream("dooly.jpg");
    		os = new FileOutputStream("dooly.copy.jpg"); 
    		
    		int data = -1;
    		while((data = is.read()) != -1 /*1byte read*/) {
    			os.write(data); //write
    		}
    	} catch (FileNotFoundException e) {
    		System.out.println("file not found: "+ e);
    	} catch (IOException e) {
    		System.out.println("error"+e);
    	} finally {
    		//자원정리
    		try {
    			if(is != null) {
    				is.close();					
    			}
    			if(os != null) {
    				os.close();
    			}
    		} catch (IOException e) {
    			e.printStackTrace();
    		}
    	}
    }
    ```

2) Byte :  Reader, Writer

- file reader

    ```java
    public static void main(String[] args) {
    	Reader in = null;
    	InputStream is = null; //비교용(byte와 char사이)
    	
    	try {
    		in = new FileReader("1234.txt");
    		
    		//read : char 단위
    		System.out.println("** Character read");
    		int data = -1; //"가": 3byte, int: 4byte
    		int count = 0;
    		while((data=in.read())!= -1) {
    			System.out.print((char)data);
    			count++;
    		}
    		System.out.println();
    		System.out.println("FileReader count: "+count + "\n"); //총 몇 번 읽었는 지
    		
    		is = new FileInputStream("1234.txt");
    		
    		//read : byte 단위
    		System.out.println("** Byte read");
    		data = -1; //"가": 3byte, int: 4byte
    		count = 0;
    		while((data=is.read())!= -1) {
    			System.out.print((char)data); //깨져서 출력됨(한 바이트자체는 의미가 없는 값)
    			count++;
    		}
    		System.out.println();
    		System.out.println("FileInputStream count: "+count); //21번(3byte*7)
    		
    	} catch (FileNotFoundException e) {
    		System.out.println("file not found: "+e);
    	} catch (IOException e) {
    		System.out.println("error: "+e);
    	} finally {
    		try {
    			if(in!=null) {
    				in.close();
    			}
    		} catch (IOException e) {
    			e.printStackTrace();
    		}	
    	}

    }
    ```

### 2. 주 스트림과 보조 스트림

- I/O 디자인 패턴

![1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%202.png](1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%202.png)

Scanner 내부 구조가 이와 비슷함

- decoration : 상속받는 식으로 하지 않고, runtime때 확장시키는 식으로
    - mapping : bos(보조스트림 변수) → 보조스트림 버퍼 → (fis: 주스트림변수) → 주스트림
    - 장점 : 클래스 많이 만들지 않고도 기능 확장?가능

    ```java
    FileOutputStream fis = new FileOutputStream("test.txt");
    BufferedOutputStream bos = new BufferedOutputStream(fis);

    // 한줄로 많이 씀 (fis가 필요가 없음) - 나중에 close할 때에도 bos만 close해도 알아서 fis쪽도 close됨
    BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("test.txt"));
    ```

![1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%203.png](1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%203.png)

### 3. other API

### 1) String

### immutability (불변성)

toUpperCase() : String객체의 내용은 변경 불가능, 새로운 객체를 return함

코드

```java
String s1 = new String("ABC");
String s2 = new String("ABC");

System.out.println("== :"+(s1 == s2));
System.out.println("equals :"+(s1.equals(s2)));
System.out.println(s1.hashCode()+":"+s2.hashCode()); //오버라이딩 후의 해쉬코드
System.out.println(System.identityHashCode(s1)+":"+System.identityHashCode(s2)); //주소기반의 해쉬코드

System.out.println("=====================================================");

String s3 = "ABC";
String s4 = "ABC";

System.out.println("== :"+(s3 == s4));
System.out.println("equals :"+(s3.equals(s4)));
System.out.println(s3.hashCode()+":"+s4.hashCode()); //오버라이딩 후의 해쉬코드
System.out.println(System.identityHashCode(s3)+":"+System.identityHashCode(s4)); //주소기반의 해쉬코드
```

결과

```java
== :false
equals :true
64578:64578
604107971:123961122
=====================================================
== :true
equals :true
64578:64578
1227229563:1227229563
```

- s3,s4의 reference가 같다.(같은 객체를 가리키게 됨)
- s3,s4처럼 사용하는 것이 더 좋음

- String을 literal 로 초기화하게 된다면, JVM의 method area에서 literal Pool이 작동하게 됨(더 효과적임)

    ```java
    String s3 = "123"; //JVM의 method area에서 literal pool에 저장
    String s4 = "123"; //literal pool에 값이 저장되어 있으므로 위의 객체를 referencing함 (즉, 위와 같은 객체 reference)
    ```

- Integer등등 다른 것도 비슷함.

### 2) StringBuffer

- mutable (변경가능) :  버퍼크기가 달라지게됨
- String으로 쓰고 싶다면 toString으로 변경해야함

```java
StringBuffer sb = new StringBuffer(""); //mutable
sb.append("Hello ");
sb.append("World ");
sb.append("Java ");
sb.append(1.8);

String sb_s = sb.toString();
System.out.println(sb_s);
```

- String 대신 사용해야 하는 경우(성능면)
    - 문자열 + 연산을 하지 말아야 하는 경우 (밑 : 오래걸림)

    ```java
    String s7 = "";
    for(int i=0;i<1000000;i++) {
    	s7 = s7 + i;
    //s7 = new StringBuffer(s7).append(i).toString(); 와 같음
    }
    ```

StringBuffer사용이 훨씬 좋음

```java
StringBuffer s7 = new StringBuffer("");
for(int i=0;i<1000000;i++) {
	s7.append(i);
}
String n = s7.toString();
```

### 3) Wrapper

- 8가지 기본 데이터형을 객체형식으로 다루기 위한 클래스들 통칭
- 8가지 기본 데이터형 클래스들: Byte, Short, Integer, **Long**, Character, Float, Double, **Boolean**
    - Long, Boolean : Wrapper로 많이 쓰임
    - int, char : 기본 데이터형으로 많이 쓰임
- 쓰는 이유 : 잘못된 값이 들어온 경우 null로 저장할 수 있음. 기본 데이터형으로 쓰면 잘못된 값에 대한 저장할 만한 값이 없음.

### * Literal Pool / Auto Boxing

사용하지 않는 형태

```java
Integer i = new Integer(10);
int j3 = j1.intValue(); 
```

사용하는 형태 (같은 값을 가지는 객체는 한 번만 저장하기 위함)

```java
Integer i = 10; //Auto Boxing
int j3 = j1; //Auto Unboxing
```

- Literal Pool 이 관리함

 

## 3. util

Date, Calendar

collection

### Calendar

- Singleton : 객체 딱 하나만 만들 수 있는거 (외부에서 객체 못만듦)

### collection

![1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%204.png](1%20JAVA%20414bbeaee3c6415fb677476d8140d291/Untitled%204.png)

- Iterable에서 Iterator() 호출 - 순회시 사용가능
- List : 순서 O, 중복 O
    - ArrayList : DB에서 많이 쓰임 (순서대로 search)
        - multithread 동기화 X
    - vector
        - multithread 동기화 O
        - Synchronized keyword(lock관련) O
    - LinkedList : 중간 삽입이 많을 때 쓰임
    - tree : 검색, 정렬시 많이 사용하는 자료구조
- Map
    - HashMap
        - multithread 동기화 X
    - HashTable
        - multithread 동기화 O

- vector
    - 예전 방식
        - 함수 이름이 길다.
    - 현재 방식
        - 함수 이름이 짧다.
        - List<> I = new ArrayList()
        - 이식성이 좋음 : Vector로 쓰던 것을 ArrayList로 바꾸어야 하는 경우 쉽게 바꿀 수 있음 (어떤 연산을 많이 사용하는 지에 따라 자료구조 변경)
- ArrayList
    - vector코드에서 한 부분만 변경함
- Queue (⭐ : 많이 사용)
    - inputs(큐에 작업올려놓음) → [—-queue—>] → threads(큐의 작업 수행)
        - cafka
        - RabitMQ

요즘 사용하는 방식

```java
List<String> list = new ArrayList<>(); //자료구조 변경 용이

//순회
Iterator<String> it = list.iterator();
		while(it.hasNext()) {
			String s = it.next();
			System.out.println(s);
		}
```
