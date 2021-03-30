MIPS(Microprocessor without Interlocked Pipelined Stages)는 RISC(Reduced Instruction Set Computer)이다.

# MIPS Instruction type

한번에 한 종류의 연산만을 지시하고, 항상 세개의 변수를 갖는다.

### Arithmetic and logic operations

- operand에 연산을 수행한다(ADD, XOR, SHIFT 등).



### Data transfer instructions(memory instructions)

- 데이터를 메모리에서 레지스터로 옮기거나(LOAD) 레지스터에서 메모리로 옮긴다(STORE).



### Control transfer instructions(branch instructions)

- Control flow를 바꾼다(PC를 바꾸는 등).

  PC(Program Counter): 다음 실행할 명령어의 주소를 저장하는 레지스터.

  Branch: conditional transfer of control

  Jump: unconditional transfer of control

  

# MIPS instruction format

MIPS구조에서 레지스터의 크기는 32 bit이다. MIPS구조에서는 32비트가 한 묶음으로 처리되는 일이 많다. 



![http://db.cs.duke.edu/courses/cps104/fall98/lectures/week8-l1/img005.gif](http://db.cs.duke.edu/courses/cps104/fall98/lectures/week8-l1/img005.gif)

http://db.cs.duke.edu/courses/cps104/fall98/lectures/week8-l1/sld005.htm



### R Format

- Arithmetic instruction

- add, sll 등

- R type의 op는 항상 0000000

- ex) 

  ```
     add $8, $9, $10
     000000 01001 01010 01000 00000 100000
     op	  rs	rt    rd	shamt funct
  ```

  op: 항상 000000

  rs: 첫 번째 source register → $9(01001)

  rt: 두 번째 source register → $10(01010)

  rd: destination register → $8(01000)

  shamt: 00000

  funct: add에 해당하는 값은 32(100000)

  

### I Format

- Immediate값과의 연산, branch, data transfer

- addi, beq, bne, lw, sw 등

- ex1)

  ```
   lw $t0, 4($s2)
  ```

  메모리 주소 4($s2)의 값을 $t0 레지스터에 저장하는 것이므로

  ​	rs(base): $s2

  ​	rt(destination): $t0

  4는 레지스터에 없는 immediate 값(상수)이므로 나머지 16 bit에 저장됨

  4는 0100 이지만 16 bit를 채워야 하므로 나머지 자리에 0을 넣음(0000 0000 0000 0100)

  

- ex2)

  ```
   sw $t0, 4($s2)
  ```

  레지스터 $t0의 값을 메모리주소 4($s2)에 저장하는 것이므로

  rs(base): $t0

  rt(destination): $s2

  

### J Format

- j, jal 등 Jump instruction





# 상수(immediate operand)

연산 과정에서 상수를 사용하는 경우가 많다. 상수를 사용할 때마다 매번 메모리에서 읽어오는 것보다 상수 필드를 갖는 산술 명령어를 사용하는 것이 훨씬 빠르다.

operand에 상수가 들어가야 한다면, 산술연산 명령어를 사용하는 것이 빠르다. 이 상수를 immediate operand라고 한다.