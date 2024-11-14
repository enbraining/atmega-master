### 1번 인터럽트를 눌렀다가 떼었을 때, is_run이라는 변수를 반전(Not) 시켜보세요.

<details>
  <summary>코드 확인하기</summary>
  
  ```c
  #define F_CPU 16000000
  
  #include <avr/io.h>
  #include <avr/interrupt.h>
  #include <util/delay.h>

  volatile int is_run = 0;

  int main()
  {
    SREG = 0x80;
    EIMSG = 0b00000010;
    EICRA = 0b00001100;
  }

  ISR(INT1_vect)
  {
    is_run = !is_run;
  }
  ```
</details>

### 7번 인터럽트를 눌렀을 때, PORT A의 모든 LED를 반전시켜보세요.

<details>
  <summary>코드 확인하기</summary>
  
  ```c
  #define F_CPU 16000000
  
  #include <avr/io.h>
  #include <avr/interrupt.h>
  #include <util/delay.h>

  int main()
  {
    DDRA = 0xff;
    PORTA = 0x00;

    SREG = 0x80;
    EIMSG = 0b10000000;
    EICRB = 0b10000000;
  }

  ISR(INT7_vect)
  {
    PORTA = ~PORTA;
  }
  ```
</details>
