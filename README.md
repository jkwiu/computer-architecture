# computer-architecture
프로그래밍 관점에서 보는 컴퓨터 구조

1. 논리 회로
   1. 컴퓨터 구조 개론
      1. 하드웨어
         1. 중앙처리장치(CPU)
         2. 주기억 장치(main memory)
         3. 입출력 장치(I/O devices)
      2. 시스템 소프트웨어(OS)
      3. 응용 프로그램
   2. 논리 회로 관점에서의 컴퓨터 구조
      1. LSB(Least Significant Bit) : 가장 오른쪽의 비트, 가정 덜 중요한 비트
      2. MSB(Most Significant Bit): 가장 왼쪽의 비트, 가장 중요한 비트
      3. CPU의 가장 기본적인 연산은 덧셈이다. 덧셈기 하드웨어를 만들고 이를 수정해서 뺄셈기로 사용하고, 덧셈을 반복적으로 수행해서 곱셈, 뺄셈을 반복적으로 수행해서 나눗셈을 수행한다.
         1. 하지만 실제로 컴퓨터에서는 정수표현에서 부호와 절대값 방식을 사용하면 느리므로, **보수표현(complement representation)**을 사용한다.
      4. 2의 보수표현(two's complement binary representation)
         1. 2의 보수
            1. 서로 더해서 0이 되는 숫자 사이의 관계를 보수관계라 한다.
         2. **MSB가 1이면 음수, 0이면 0또는 양수다.**
         3. +10<sub>(10)</sub>의 2의 보수인 -10<sub>(10)</sub>을 찾으려면
            1. 0에서 10을 빼야 하는데 0에서 10을 뺄 수 없기 때문에 0000 0000<sub>(2)</sub>에서 자리내림을 받아 0000 1010<sub>(2)</sub>(10의 2진법화)을 뺀다. 즉 이 단계는 자리내림을 받은 수 1 0000 0000<sub>(2)</sub>에서 빼는 연산이다 보니 이보다 1<sub>(2)</sub>작은 1111 1111<sub>(2)</sub>에서 빼고 나중에 1<sub>(2)</sub>을 더하는 과정과 같다. 
            2. 위의 과정은 NOT을 취한 후 1<sub>(2)</sub>을 더해주는 것과 같다.
         4. NOT 연산
            1. 2진수에서의 NOT연산은 비트를 반전시키는 것을 말한다.
         5. 특징
            1. 부호가 없이 음수를 표현할 수 있다.
            2. **보수표현은 부호라는 개념을 전혀 고려하지 않는 방식이다. 컴퓨터 입장에서는 그냥 계산하면 된다.**
      5. 2의 보수 표현이 나타내는 10진수 숫자를 알고 싶다면?
         1. MSB가 0이면 비트들의 절대값
         2. MSB가 1이면 2의 보수를 구한 값에 ``-``를 붙이면 된다
      6. 정수 연산
         1. 덧셈
            1. LSB에서 MSB방향으로 차례로 더하면 된다. 부호를 고려할 필요가 없다.
         2. 뺄셈
            1. 2의 보수를 이용하여 덧셈으로 변환한 후 연산한다.
         3. 곱셈
            1. 10진법 곰셈과 동일
         4. 나눗셈
            1. 뺄셈을 반복적으로 해서 더 이상 뺄셈이 안될 때까지 수행한다.
      7. 실수의 표현 방법
         1. 고정 소수점 표현(fixed-point representation)
            1. 숫자 표현이 간단하기 때문에 연산 속도가 빠르지만, 일반적인 컴퓨터에서는 이 방식을 사용하지 않고, 절대값이 아주 큰 숫자거나 소수점 아래가 아주 길어서 정확한 실수 값을 사용하지 않는 경우에 제한적으로 사용한다.
         2. 부동 소수점 표현(floating-point representation)
            1. 0.34<sub>10</sub>를 컴퓨터에서 내부적으로 표현
            2. 2진수로 변환
               1. 0.010101110...<sub>2</sub>
            3. 정규형(normalized form)으로 변환: 정규형이란 ``정수 부분에 0 아닌 수 하나만 남도록 소수점을 옮기는 것``을 말한다. 2진수에서는 1이 하나 오게 하는 표현이다.
               1. 1.0101110 x 2<sup>-2</sup>
                  1. ``부호 | 지수 | 가수`` 의 위치로 표현
                     1. 부호는 양수이므로 0
                     2. 8비트를 사용하여 실수를 표현하는 경우에 부호 1비트, 지수 3비트, 가수 3비트를 할당한다고 가정한다.
                     3. 지수를 위해 3비트를 할당할 때는 지수를 ``3 초과표현(excess 3 representation)``으로 표기한다
                        1. 지수가 -2기 때문에 -2 + 3하여 1로 적는다.
                     4. 가수는 4비트밖에 없으므로 맨 앞에서부터 4비트를 선택하여 1010이 된다.
                     5. 0001 1010<sub>2</sub>가 된다.
            4. 위의 결과값을 10진수로 바꾸면 0.3125가 되는데 오차가 발생한다.
         3. 초과표현
            1. 표현하고자 하는 수보다 3을 초과시키면 ``3 초과 표현``
            2. 음수와 양수를 균등하게 표현하기 위해서 3 초과 표현을 사용한다. 
            3. 1.000 x 2<sup>0</sup>과 11.111 x 2<sup>-1</sup>을 비교할 때, 10진수로 바꿔서 비교하거나, 지수를 동일하게 맞추는 방법이 있다.
            4. 하지만, 정규형에서는 지수를 맞추는 과정을 거칠 필요도 없다.
            5. 1.000 x 2<sup>0</sup>과 1.111 x 2<sup>-1</sup>을 비교해보자.
               1. 1.000 x 2<sup>0</sup>: 00111000
               2. 1.111 x 2<sup>-1</sup>: 00101111
            6. 위와 같이 정규형에서는 가수를 볼 필요가 없다. **가수가 아무리 커도 언제나 2 미만의 값**이기 때문이다. 그러므로 지수만 비교하면 된다. 물론 지수의 값이 같으면 가수의 값을 비교한다.
            7. 위의 두 수를 8비트를 사용하여 표현한 뒤 MSB부터 오른쪽으로 한 비트씩 비교하는 방식으로 대소를 비교하면 된다.
            8.  **이처럼 지수영역을 초과표현을 사용하면 같은 부호일 경우 정수처럼 생각해도 대소관계를 파악할 수 있다.**
               1. 실수의 연산보다 정수의 연산이 컴퓨터에서 더 빠르다.
         4. 히든 비트
            1. 어차피 정규형으로 변환하면 정수 부분은 무조건 1이기 때문에 이부분을 표현하지 않으면 소수점 한자리를 더 표현할 수 있다.
               1. 1.0101110 x 2<sup>-2</sup>
                  1. 히든 비트 적용 X
                     1. 0 001 1010
                  2. 히든 비트 적용 O
                     1. 0 001 0101
         5. Special Values
            1. 특정 값을 지정해두는 것을 약속한 값
            2. 가장 작은 절대값의 양의 실수는 0.1328125
            3. 가장 큰 절대값의 양의 실수는 31.0
            4. 위의 두 값을 보면 0.0 ~ 0.1328125와 같은 구간에서는 공백이 생기고 이 영역이 계산될 때는 overflow 혹은 underflow가 발생한다.
         6. 부동 소수점 연산
            1. 지수를 똑같이 맞춰주고
            2. 가수들의 덧셈 연산
            3. 결과값을 정규화
         7. 문자의 표현(코드 테이블)
            1. 아스키 코드
               1. 2<sup>8</sup>(256)개의 문자를 표현
            2. 유니코드
               1. 2<sup>16</sup>(65,536)개의 문자를 표현
   3. 논리 회로 기초
      1. 전기 신호의 전압을 이용해서 전압이 5V면 1, 0V면 0으로 표현 가능하다.
      2. 게이트(gate)
         1. 다양한 연산들을 실제로 수행하는 하드웨어 소자
         2. 전기신호에 따라 가장 기본적인 연산을 수행하는 소자
         3. 게이트가 모이면 회로(circuit)이 되고, 회로가 모여서 컴퓨터가 된다.
      3. 기본 게이트
         1. AND(논리곱): A·B
            1. 두개의 입력이 모두 1일 때만 출력
         2. OR(논리합): A+B
            1. 두개 중 하나가 1일 때 1을 출력
         3. NOT(논리부정): A￣
            1. 한개의 입력값의 부정이 1일 경우 1을 출력
         4. XOR(배타적 논리합): A⊕B
            1. 두개의 입력 중 한개만 1일때 1을 출력
         5. NAND: A￣·B￣
            1. AND연산 후에 NOT연산을 수행
         6. NOR: A￣+B￣
            1. OR연산 후에 NOT연산을 수행
      4. 게이트들로 구성된 ``IC``칩을 빵판에 적절히 연결하여 회로를 구성한다.
      5. 논리 회로의 동작 원리를 표현 하는 방식
         1. 논리식
         2. 논리도
         3. 진리표
      6. 논리 회로
         1. 조합 논리 회로
            1. 입력값만으로 출력값이 결정되는 회로
         2. 순서 논리 회로
            1. 입력값과 회로 내부의 상태가 출력값을 결정하는 회로
            2. 클럭(clock)이 필요
   4. 조합 논리 회로
      1. 불 대수 법칙 
         1. 교환법칙
            1. x+y=y+x
            2. x*y=y*x
         2. 결합벅칙
            1. (x+y)+z=x+(y+z)
            2. (x*y)*z=x*(y*z)
         3. 분배법칙
            1. x+(y*z)=(x+y)*(x+z)
            2. x*(y+z)=(x*y)+(x*z)
         4. 항등법칙
            1. x+0=x
            2. x+1=1
            3. x*0=0
            4. x*1=x
         5. 보수법칙
            1. x+x'=1
            2. x*x'=0
         6. 멱등법칙
            1. x+x=x
            2. x*x=x
         7. 흡수법칙
            1. x+(x*y)=x
            2. x*(x+y)=x
         8. 드모르강의 법칙
            1.  (a*b)'=a'+b'
            2.  (a+b)'=a'*b'
         9.  부정
             1.  (x')'=x
             2.  1'=0
             3.  0'=1
         10. dual expression(짝 수식, 상대 수식)
             1.  +와 *을 서로 맞바꾸고
             2.  1과 0을 서로 맞바꾼다.
                 1.  x+x'=1 => x*x'=0
      2. And-Or(곱의 합)/Or-And(합의 곱) 회로
      3. 회로의 간소화하는 방법
         1. K-map(Kamaugh map, 카르노맵) 
            1. 진리표를 2차원으로 다시 정리한 표
         2. Don't Care 조건
            1. 진리표에서 입력값 이외의 값을 배제하는 것
            2. k-map에 don't care minterm(돈케어 최소항)은 x로 표시해두고 사용해도 되고 사용하지 않아도 된다. -> don't care condition
      4. 소자
         1. 작동 구동 신호(Enabling Lines)
            1. Enable이 1일때만 입력이 출력으로 전달되고 0일때는 0이 출력
         2. 멀티플렉서(multiplexer)
            1. 여러 개의 입력 신호로부터 원하는 하나의 신호를 선택해서 출력하는 것
         3. 디-멀티플렉서(de-multiplexer)
            1. 1개의 입력을 여러 출력 라인 중 하나로만 출력해주는 회로
         4. 이진 디코더(binary decoder)
            1. 2진수를 입력받아 출력 신호 중 하나만 1로 셋팅하고 나머지는 0으로 만드는 회로
         5. 이진 인코더(binary encoder)
            1. 2진 비트열을 받아 이를 2진수로 출력하는 회로
   5. 순서 논리 회로(순차 논리 회로)
      1. 동일한 입력값으로 동일한 출력값을 가지는 조합논리회로로는 컴퓨터를 만들 수 없다. 왜냐하면 컴퓨터는 메모리 기능을 필요로 하기 때문이다. 메인 메모리를 예로 동일한 주소값을 메인 메모리에게 주더라도, 메인 메모리의 내용물의 값에 따라 다른 값이 출력되어야 한다.
      2. 입력값, 회로의 상태에 따라 출력값이 결정된다.
      3. 플립플랍(flip-flop)
         1. 회로의 상태를 저장
         2. 한 비트의 정보를 저장하는 이진 셀(binary cell)
      4. SR latch
         1. 플립플랍의 값을 S(Set) 또는 R(Re-Set)한다는 의미
         2. 출력
            1. Q
            2. Q￣
         3. unstable하다는 의미는 Q와 Q`가 동일한 값을 가지는 경우다. 아직 자리를 잡지 못한 상황이다.
         4. SR=10이면 회로의 상태를 Set한다는 것이고 stable 상태가 된다.
         5. SR=01이면 회로의 출력값(Q)을 0으로 만들 수 있다.
         6. SR=00이면 현재의 출력값이 출력된다.
         7. 특성표(SR latch에서는 진리표라고 하지않고, 특성표라고 한다.)
      5. 클럭(clock)
         1. CPU의 속도를 나타내는 단위
         2. **1초동안 파장이 한 번 움직이는 시간**
         3. CPU를 포함한 컴퓨터 내의 모든 부품은 클럭에 맞추어 동작한다. 즉, 클럭은 컴퓨터 내부의 시계와 같은 역할을 한다.
         4. 버스를 통해서 모듈들이 서로 데이터를 송수신하기 위해서 모듈간의 동기화가 필요하며 이를 위해서 클럭 신호가 필요하다.
         5. 예를 들어 클럭 속도가 1.6Mhz라면, **클럭 발생기(오실레이터)**는 1초당 1,600,000 번의 클럭을 발생시키며, CPU를 포함한 모든 부품들이 클럭이 발생할 때마다 일을하므로 클럭 속도가 높을수록 초당 처리하는 명령어의 개수가 많아지므로 컴퓨터의 수행속도가 빨라진다.
         6. 과거에는 CPU의 성능을 높이기 위해 클럭(동작 주파수)을 올리는 것이였지만, 클럭이 높아질수록 발열량과 소비 전력이 커지는 문제가 발생하여 최근에는 클럭을 일정 수준으로 유지하는 대신, 멀티코어나 멀티스레드와 같은 방식으로 성능을 높인다.
      6. SR flip-flop
         1. SR latch에 클럭 신호를 추가한 것
         2. SR latch와 다른 점은 입력 부분에 AND게이트를 Enable신호를 사용하므로, 클럭이 들어올 때만 회로가 작동한다는 것이다.
      7. 순서 논리 회로 특징
         1. 입력값과 현재의 상태에 의해서 회로의 출력값이 결정
         2. 피드백을 가진다(회로의 출력결과가 회로의 상태변경을 위해서 다시 사용됨)
         3. 플립플랍과 같은 기억회로를 가진다.
         4. 클럭에 의해서 동작한다.
      8. 회로가 동작하는 방식
         1. 레벨 트리거 방식
            1. 클럭 신호의 전압 레벨이 높을 때 동작하는 방식
            2. 문제점
               1. 클럭신호가 1을 가지는 동안 SR=10이었다가 SR=01이 되면 리셋되버리는 상황이 발생할 수 있다.
         2. 에지 트리거 방식
            1. positive 에지 트리거 방식
               1. 클럭이 상승할 때 플립플랍이 작동
            2. negative 에지 트리거 방식
               1. 클럭이 하강할 때 플립플랍이 작동
      9. 여기표(excitation table)
         1. 원하는 출력을 얻기 위한 입력값을 적은표로써, 특성표로부터 만들 수 있다.
      10. 플립플랍 종류
          1.  SR 플립플랍
          2.  JK 플립플랍
              1.  SR 플립플랍이 SR=11을 사용하지 못하는 것을 수정한 플립플랍
              2.  SR=11이면 출력값이 반전(toggle)된다
          3.  D 플립플랍
              1.  Data를 delay하라는 의미로 입력하는 값을 그대로 저장하는 기능을 수행
          4.  T플립플랍(T는 toggle: 반전)
      11. 순서 논리 회로의 만드는 방법
          1.  회로의 **상태**와 **클럭**에 따른 신호의 타이밍을 고려해서 설계해야 한다.
          2.  종류
              1.  동기 순서 회로
                  1.  클럭 펄스에 동기화되어 동작
              2.  비동기 순서 회로
                  1.  클럭 펄스에 관계없이, 플립플랍의 입력이 변화하는 순서에 따라 동작하므로 첫 플립플랍에만 클럭펄스가 필요하다.
              3.  카운터 회로
                  1.  숫자를 순서대로 출력하는 회로
                  2.  비동기식 카운터
                      1.  0~3까지의 숫자를 카운팅하는 비동기식 카운터 회로 예제
                          1.  0->1->2->3->0->1->2->3->...
                      2.  출력의 결과를 2진수로 적어보면
                          1.  00->01->10->11->00...
                      3.  저장해야하는 상태정보에 따라 플립플랍의 개수를 정한다.
                          1.  4가지 상태이므로 2비트가 필요하다. 즉 2개의 플립플랍이 필요
                      4.  비동기식 카운터는 타이밍 다이어그램에서 규칙성을 찾는 것으로부터 시작한다.
                          1.  LSB(Q<sub>0</sub>): 비트는 클럭이 하강할 때마다 값이 변경(toggle)
                          2.  MSB(Q<sup>0</sup>): 비트는 LSB(Q<sub>0</sub>)값이 하강할 때마다 값이 변경(toggle)
                  3.  동기식 카운터
                      1.  K-map을 이용해서 만든다.
2.  하드웨어 관점에서의 컴퓨터 구조
    1.  컴퓨터 하드웨어
        1.  구성요소
            1.  중앙처리장치(CPU)
                1.  아래의 3모듈은 내부버스로 연결됨
                    1.  산술 논리 장치(ALU: Arithmetic Logic Unit)
                        1.  산술 연산(+, -, *, / 등)
                            1.  덧셈기 구현
                                1.  1비트 반가산기(half adder) 구성
                                2.  2개의 반가산기를 이용해서 1비트 전가산기(full adder) 구성
                                3.  여러 개의 전가산기를 이용해서 멀티 비트 전가산기 구성
                            2.  감산기
                            3.  상태 레지스터
                        2.  논리 연산(AND, OR, NOT, XOR 등)
                            1.  실행속도가 빠르다.
                                1.  *2는 피연산자를 메인 메모리에서 CPU로 로드해서 연산을 수행하고 그 결과를 다시 메인 메모리로 옮겨야 하지만, shift 연산은 레지스터 상에서 비트를 왼쪽으로 한 번만 이동시키면 된다.
                    2.  컨트롤 장치(CU: Control Unit)
                        1.  마이크로 프로그램 기반 제어 방식
                            1.  명령어 레지스터(IR): 현재 실행할 명령어를 기억
                            2.  명령어 해독기(instruction decoder): IR에 있는 명령어의 연산코드를 해독하여 해당 연산을 수행하기 위한 루틴의 시작 주소를 결정
                            3.  제어 주소 레지스터(CAR): 다음 실행할 명령어의 주소를 저장
                            4.  제어 기억장치: 마이크로 명령어들로 이루어진 마이크로 프로그램을 저장하는 내부 기억장치
                            5.  제어 버퍼 레지스터(CBR): 제어 기억장치로부터 읽혀진 마이크로 명령어 비트들을 일시적으로 저장
                            6.  디코더: 명령어의 해독 결과로 생성된 마이크로 명령어에 따라서 각 장치로 보낼 제어 신호를 생성하는 회로
                            7.  순서 제어 모듈
                        2.  하드와이어 제어 방식
                    3.  레지스터(Register)
                        1.  데이터는 주기억 장치에 있고 연산은 CPU 내부에서 하므로, CPU내부의 상태를 저장하는 공간이 필요하며 이것이 레지스터
                        2.  플립플랍 여러 개를 일렬로 배열해서 구성
            2.  주기억 장치(Main Memory)
            3.  입출력 장치(I/O Devices)
            4.  버스(BUS): 데이터를 주고 받는 경로
        2.  마이크로 인스트럭션
            1.  마이크로 명령어 형식은 4개의 필드로 구성
                1.  마이크로 오퍼레이션 필드
                2.  조건 필드
                3.  분기 필드
                4.  마이크로 주소 필드
            2.  명령어 형식
                1.  수평 마이크로 명령어
                    1.  마이크로 명령의 한 비트가 한 개의 마이크로 오퍼레이션을 관할하게 하는 명령
                        1.  명령어 형식이 길다
                        2.  마이크로 명령 수행시에 병렬도가 매우 높다
                        3.  제어 정보에 대한 인코딩이 필요없다
                2.  수직 마이크로 명령어
                    1.  제어 메모리의 외부에 디코딩 회로를 필요로 하는 마이크로 명령
                        1.  명령어 형식이 짧다
                        2.  마이크로 명령 수행시 병렬도가 매우 낮다
                        3.  제어 정보에 대한 인코딩이 필요하다
            3.  폰 노이만의 내장형 프로그램 방식
                1.  프로그램을 실행시키면 하드 디스크에 있는 프로그램이 메인 메모리로 로딩된다.
                2.  명령어 수행 사이클
                    1.  명령어 인출(Fetch)
                        1.  메인 메모리로부터 수행할 명령어를 가져온다. 가져올 명령어의 주소는 PC(program counter) 레지스터가 다음에 수행할 명령어의 주소를 가지고 있다.
                    2.  명령어 해독(Decode)
                        1.  인출된 명령어의 종류를 해독한다.
                    3.  명령어 실행(Execute)
                3.  인출 단계(Fetch Cycle)
                    1.  명령어를 가져온다
                4.  간접 사이클(Indirect Cycle)
                    1.  피연산자의 값을 가져온다
                5.  실행 단계(Execute Cycle)
                    1.  명령을 이행하는 단계, 인터럽트 요청 신호 플래그 레지스터를 검사하는 단계
                6.  인터럽트 사이클
                    1.  인터럽트 발생시 복귀 주소(pc)를 스택(stack)에 저장(PUSH)한 후 인터럽트를 처리한다. 인터럽트 실행시 IEN(Interrupt Enable)값은 0으로 변경(다른 인터럽트 요청을 막는다)
                    2.  인터럽트가 끝나면 Fetch 사이클로 가서 복귀 주소를 스택에서 POP하여 실행하던 것을 마무리한다.
            4.  파이프라이닝
                1.  한 사이클에 있어 병렬처리가 가능한 것
            5.  기계어 명령어
                1.  CISC(Complex Instruction Set Computer)
                2.  RISC(Reduced Instruction Set Computer)
            6.  버스(bus)
                1.  데이터 버스(Data Bus)
                    1.  data 이동
                2.  주소 버스(Address Bus)
                    1.  data address 이동
                3.  컨트롤 버스(Control Bus)
                    1.  컨트롤 관련 신호가 이동
                        1.  기억 장치 읽기/쓰기 신호
                        2.  입출력 장치 입력/출력 신호
                        3.  버스 중재 신호
                        4.  인터럽트 신호
                4.  내부 버스
                    1.  CPU 내부에 위치한 버스
                5.  외부 버스
                    1.  CPU와 메인 메모리, 입출력 장치를 연결하는 버스
            7.  기억(저장) 장치
                1.  내부 메모리
                    1.  RAM(Random Access Memory): 휘발성
                        1.  정적 RAM
                        2.  동적 RAM
                    2.  ROM(Random Access and Read Only Memory): 비휘발성
                        1.  입출력 시스템(BIOS)과 컴퓨터를 부팅할 때 수행되어야 하는 자가 진단 프로그램(POST), 부트스트랩 로더를 저장하고 있다.
                            1.  PROM(Programmable ROM)
                                1.  단 한번만 프로그래밍 할 수 있다.
                            2.  EPROM(Erasable PROM)
                            3.  EEPROM(Electrically Erasable PROM)
                                1.  빵판
                            4.  플래쉬 메모리
                                1.  RAM과 ROm을 잘 조합한 메모리으로 전원이 꺼져도 데이터가 지워지지 않는 반도체 기반의 메모리
                2.  외부 메모리(보조 기억 장치)
                    1.  자기 테이프
                    2.  자기 디스크
                    3.  Solid State Disk(SSD)
                        1.  플래쉬메모리를 이용한 하드디스크
                    4.  RAID(Redundant Array of Inexpensive Disks)
                        1.  중요한 데이터를 가지고 있는 서버에 주로 사용되며, 여러 대의 하드 디스크가 있을 때 동일한 데이터를 다른 위치에 중복해서 저장하는 방법
                        2.  여러 대의 디스크를 하나의 디스크처럼 사용
                        3.  하나의 RAID는 OS에게 논리적으로는 하나의 하드 디스크로 인식됨
                        4.  구현 방법
                            1.  RAID-0
                            2.  RAID-1
                                1.  디스크 미러링
                                2.  중복 저장된 데이터를 가진 적어도 두 개의 드라이브로 구성
                                3.  각 드라이브를 동시에 읽을 수 있으므로 읽기 성능은 향상되나 쓰기 성능은 단일 디스크 드라이브와 같다. 
                                4.  다중 사용자 시스템에서 최고의 성능과 고장대비 능력을 발휘한다.
                            3.  RAID-2
                                1.  비트-단위 인터리빙 방식을 사용하여 데이터를 각 디스크에 비트 단위로 분산 저장
                    5.  캐쉬 메모리
                        1.  빠른 CPU와 상대적으로 느린 메모리 사이에 위치하며, 속도 차이가 있는 메모리 사이의 데이터 접근 효율성을 향상시키기 위한 메모리
                        2.  지역성의 원칙을 활용한 아이디어
                            1.  시간적 지역성
                                1.  한번 사용된 정보는 다시 사용될 가능성이 있다.
                            2.  공간적 지역성
                                1.  한번 사용된 정보의 근처 영역이 다시 사용될 가능성이 있다.
                        3.  캐쉬 데이터가 다시 쓰이는 경우를 적중(hit)하였다고 하고 비율은 적중률(hit ratio)이다.
                        4.  캐시 메모리 교체 알고리즘
                            1.  최소 최근 사용(LRU: Least Recently Used) 알고리즘
                                1.  사용되지 않은 채로 가장 오래된 블록을 교체
                            2.  FIFO 알고리즘
                                1.  캐시에 적재된 가장 오래된 블록 교체
                            3.  최소 사용 빈도(LFU: Least Frequently Used) 알고리즘
                                1.  참조 횟수가 적은 블록 교체
                            4.  Write-through
                                1.  모든 쓰기 동작이 캐시 뿐만 아니라 주기억 장치로도 수행
                            5.  Write-back
                                1.  캐시 데이터가 변경되도 주기억 장치에는 변경이 반영되지 않는 방식
                        5.  캐쉬 메모리를 고려한 코딩
                            1.  2차원 배열에 저장할 때 행-우선 방식으로 사용할 때가 열-우선 방식보다 빠르다.
                                1.  일반적으로 2차원 배열은 메인 메모리에 행-우선으로 저장된다.
                    6.  입출력 장치(I/O Device)
    2.  기계어 프로그래밍을 통한 컴퓨터 구조 이해
        1.  기계어
        2.  어셈블리 언어
            1.  고급언어와 기계어의 중간
    3.  요즘 PC들은 대부분 4개의 코어가 있는 CPU들을 장착하지만 실제로 프로그래밍 할 때는 단일 코어만 사용하게 된다. 그러므로 멀티 코어의 특성을 살릴 수 있는 프로그래밍 기법이 필요하다.
    4.  병렬 컴퓨터를 만드는 방법은 크게 아래의 2가지 방법이 있다.
        1.  공유 메모리
        2.  메시지 패싱
    5.  쓰레드
        1.  일련의 연속적으로 실행되는 인스트럭션
    6.  멀티 쓰레딩
        1.  마스터 쓰레드가 다수의 슬레이브 쓰레드를 실행해서 병행처리 하는 방법
3.  결론
    1.  도입부에서는 책의 의도가 그럴 듯하게 흘러가다가 중간부터는 사실 말 할 내용은 한 줄로 충분했는데 책은 마무리해야겠고 해서 200장을 억지로 이것저것 말하면서 쓴 느낌이 든다.
    2.  원했던 내용과는 많이 벗어났다. 프로그래밍 관점에서 하드웨어를 이해하면서 프로그래밍 할 수 있는 방법과 개념을 원했지만, 그에 관한 내용은 그저 한 두 줄 나온 것 같다.
    3.  암튼 수고~