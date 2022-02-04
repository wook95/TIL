# 컴퓨터 구조

[컴맹을 위한 Go 언어 기초 프로그래밍 기초 강좌 1 - 트랜지스터를 알아보자](https://www.youtube.com/watch?v=Tq3W8UyltFs&list=PLy-g2fnSzUTAaDcLW7hpq0e8Jlt7Zfgd6&index=1) 를 보고 정리했습니다.

1. 컴퓨터 구조

   - 트랜지스터

     ```
     0. 생물의 기본은C 탄소화합물 , 컴퓨터의 근본은?
     바로 바로 트랜지스터다 (cpu는 트랜지스터 덩어리)
     
     1. npn (-+-) 중간 p에 전압을 가해야 전류가 통할 수 있다 
     → 스위치 기능 및 증폭기능
     
     2. 전구를 껏다 키는것과 다른것은?
     → 물리적인 힘으로 스위치를 누르는게 아니라 전기적 신호로 켜진다 - 2진법
     
     3. 한 자리를 표현하는 단위 = 비트
     	1비트 = 1트랜지스터
     ```

   - 트랜지스터로 부울 대수 표현 가능

     ```
     not and or nor xor
     1bit 가산기를 생각해보자
     		 c	s
     0	0	 0	0
     1	0	 0	1
     0	1	 0	1
     1	1	 1	0
     
     c는 and, s는 xor로 만들 수 있다!
     2자리 이상의 경우 c를 해당 자리에 넣으면 n자리 계산 가능
     → 트랜지스터 계산기 만들기 가능
     
     트랜지스터 → 논리소자 →계산기 → 컴퓨터
     트랜지스터 ← 실리콘 ← 규소 ← 모래
     ```

   - 트랜지스터는 모래로 만든다

     ``` 
     모래를 끓이고, 빙글빙글 돌려서 원통형 으로 추출 (실리콘 잉갓)
     
     자르면 실리콘 원판 (웨이퍼) ← 화학 물질 추가 해 반도체로 만듬 
     
     회로를 인쇄, 트랜지스터를 만들어 cpu가 만들어진다~~!
     ```

   - 먼 옛날의 컴퓨터

     ``` 
     튜링 테스트 , 채팅해서 사람인지 기계인지 물어보는 테스트 ai
     
     튜링 머신 , 한줄 읽어서 연산 수행하는 기계
               add[2][3] [7] 뒤의 책장의 2칸 3칸의 카드를 더해 7에 써라
               
     초기의 컴퓨터는 프로그램 교체가 힘들었다,, 애니악은 명렁할 수 있는 곳와 저장하는곳 따로있어서 프로그램을 교체하려면 소프트웨어 역할을 하는 테이프를 배선판을 바꿔야 했음
     
     폰 노이만(우주 최강의 두뇌, 맨하탄 프로젝트, 컴퓨터)
     
     폰 노이만 기계, 프로그램과 메모리 같이 가자
     HW 전선을 재배치 할 필요 없이 SW만 교체, 메모리 안에 소프트웨어를 넣어 ip(instruction point) 명령 수행 지점 주소만 바꾸자 →현대는 폰 노이만 구조의 기계를 쓴다
     ```



2. 컴퓨터

   ```
   1.명령을 2.하나씩 3.순서대로 4.수행하는 기계
   
   명령 : add, sub, mul, div,jump,load,write
   하나씩: 코어는 하나당 명령을 하나씩
   순차적으로 실행하는 기계
   
   
   프로그램 : 어떤 명령을 어떤 순서로 수행할지에 대한 문서
   				(적는 방법에 따라 여러가지 프로그래밍 언어로 나뉜다)
   
   
   0과 1로 어떻게 그림,음악,문자를 표현할까?
   
   - 문자
   
   	A,B,C,D —> 65,66,67,68 (아스키, 255개 문자)
   		(255개인 이유)
   		1byte = 8bit = 2^8 = (0~255)
   
   	그 다음에 나온게 unicode (2byte) 1~3
   	utf-16 (2byte)
   	utf-8 (영문자,숫자 1 byte, 다른문자 2~3byte)
   
   - 그림
   
   	1080 X 720
   	색→숫자, rgb (0~255,0~255,0~255) 3byte 또는 rgba투명도까지 4byte
   
   - 소리
   
   	파장 및 진폭들을 숫자로 표현
   ```

   

3. 요리에 대한 비유

   ```
   요리책, 레시피 = 프로그램
   
   요리 재료를 사러 버스 타고 마트로 간다(멀다) = 하드디스크
   
   요리 재료를 냉장고에 넣어둠 (비교적 가까움) = 메모리
   
   필요한 재료 마늘과 고기 꺼내놈	= 캐쉬 (메모리에서 덩어리 큰 청크 툭 떼서 갖다놈) 크기는 4kb 정도
   
   도마 위에 올려놓는다 = 레지스터(실제 연산이 들어갈 때) , cpu는 레지스터만 보면 된다
   ```

   

4. 프로그램

   ``` 
   명령과 순서를 쓴 문서(글 <- 프로그래밍 언어로 작성됨)
   컴퓨터가 읽을 수 있도록 글로 된 문서(프로그램)를 0과 1로 바꿔줘야 해 (00111 이것도 프로그래밍 언어. 기계어)
   
   1. 기계어
   
   operator operand
   
   add				 	3,4
   
   sub				 	5,2
   
   mul		 			3,2
   
   
   add = 1, sub=10, mul=11, jump=100 등 명령어에 숫자 대입한 코드 opcode
   
   add 3,4 = 0001 0011 0100
   
   인간이 알아봄(어셈블리어 -저수준언어) → 기계가 알아봄
   인간이 알아볼수 있는 언어를 기계가 알아볼 수 있는 형태로 변환한다. 결과는 기계어 0과1
   
   
   고수준 언어 → 중간언어 → 기계어 (c# java) (python 인터프리터 언어, 중간언어 없음)
   고수준언어 					→ 기계어 (c, go 는 native) 
   
   
   프로그래머 → 코딩 → 빌드(변환) → 기계어
   
   
   멋진 해커님들, , 기계어만 가지고 어떤 프로그램인지 알아보고,, 고칠수도
   프로그램 = 언어 = 기계어 → 어셈블리어로 해석 가능 (하지만 어렵다)
   게임의 순간이동핵 → 프로그램을 해킹해서 기계어 해석 어떤게 이동을 담당하는지 보고 고쳐서 핵을 만들기도함
   ```

   

4. 언어를 컴파일언어와 동적언어로 나눌때

   ```
   기계어 0,1
   저수준언어(어셈블리어), 고수준 언어(c,c++,java,python,go)
   
   1. c,c++,go
   
   - 컴파일언어
   - 프로그래머가 코딩(명령과 순서를 문서화) → 빌드(컴파일러가 기계어로 변환) → 실행파일(기계어)
   - 속도 빠름
   - 문제 : 각 플랫폼 별로 다른 변환이 필요 (윈도우즈와 맥의 스타 실행파일은 완전히 다름 변환과정이 달라서 모두 다 빌드를 다르게 해야됨)
   - 과거엔 cpu만드는 회사 많았다. add 3,4 에서 opcode가 다 달랐음,,
       intel 의 add = 0001, ibm=0100, amd=0111 이었다면,, 만들어 내야했던 기계어들이 다 달랐다
       칩셋별로 컴파일러가 다르게 동작해야 했다
       만약 인텔 cpu만 쓰면 변환과정에서 add를 0001로만 쓰면 되는데,, 인텔 안에서도 opcode가 달라짐
       8086-80286-80386-80486-펜티엄-펜티엄mmx-i3 i5
       펜티엄mmx 실수 연산기 부동소수점 하나 추가 ,, 칩셋 발전하면서 없던 기능 생김 (부동소수점연산 등)
   - cpu,os에 따라 변환과정이 모두 달랐다 (미리 컴파일을 해 놓으니까, 각 플팻폼마다 변환을 해야해서)
       그래서 ,, 이 게임은 인텔cpu 윈도우즈에서 밖에 못해 ~ ← 이 문제를 해결하기 위해 동적언어 나옴
   
   
   
   2. c#,java,python,javascript
   
   - 동적언어
   - 컴파일 과정 필요 X
   - 코딩 (문서)→ ( 빌드 (자바,c# 빌드 필요 → 빌드 후 중간언어)) → 기계어(그때 그때 변환..?)  )
   - 컴파일 언어에 비해 속도 느림
   - 실행 할 때마다 어떤 플랫폼인지 파악해서 그 때 그 때 변환하자 ~
   
       코딩 → 결과 → 빌드 (.jar) → 어떤 운영체제 cpu던지 알아서 변환
   
   - 첨 나왔을 땐 비판 많았음 (처음 등장했을때 속도 많이 느렸음)
   - 언어적 완성도나 라이브러리 지원이 좋다,, 생산성 면에서 동적언어가 승,
   
   
   속도같은 경우 거의 비슷하다
   유니티, 언리얼엔진(게임) → c# c++ / 써야 되는 경우가 있다
   기본, 근간이 되는 기술,, 속도가 빨라야 하는 경우 c나 c++로 만들어 지는 경우 많다
   엔진 ? 은 c로 ui는 java로 ,, 만드는 경우 있음
   ```

   