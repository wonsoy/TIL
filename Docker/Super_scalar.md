```
※ issue: 명령어들을 실행 가능한 유닛으로 보내는 것
```



## Superpipelining

- Pipeline의 depth를 증가시켜 더 짧은 clock cycle을 갖게 한다. 
- Instruction latency가 더 길다. 



## VLIW(Very Long Instruction Word architecture)

- Static multiple-issue processor.
- 컴파일 타임에 컴파일러에 의해 어떤 명령이 동시에 실행될지 결정된다. 
- 독립적인 연산 여러개를 긴 명령어 하나(VLIW)에 넣고 한꺼번에 내보낸다. 
- 하드웨어는 이 연산들을 동시에 fetch하고 execute한다. 
- 컴파일러가 복잡한 작업을 하는 대신 하드웨어는 간결하게 유지될 수 있다. 하드웨어를 동적으로 스케쥴링할 필요가 없다. VLIM 명령 안에서 dependency checking을 할 필요가 없다. 명령어 alignment/distribution도 할 필요 없다. 



## Super Scalar

- Dynamic multiple-issue processor.

- 한 사이클에 여러 명령어를 실행한다. 

- 어떤 명령들이 동시에 실행될지는 하드웨어에 의해 런타임에 결정된다. 

- 동시에 실행되는 명령어들에 대한 dependency check를 하드웨어가 한다. 더 많은 하드웨어 리소스가 필요하다. 

  #### In-Order Issue with In-Order Completion

  - 순서대로 issue되고 순서대로 종료된다. 

  

  #### In-Order Issue with Out-of-Order Completion

  - 순서대로 issue되고 순서와 다르게 종료된다. 
  - Out-of-Order completion의 경우 resource conflict가 있거나 아직 계산되지 않은 값을 소스로 써야 할 때 명령어가 stall된다.

  ```
  I1: writes to R3
  I2: writes to R3
  I5: reads R3
  ```

  위의 경우에서 만약 I2가 I1보다 먼저 완료되면 I5는 잘못된 값을 읽게 된다(write before write). 따라서 I2의 issue는 stall되어야 한다. 

  

  #### Out-of-Order Issue with Out-of-Order Completion

  - In-Order Issue의 경우에는 resource conflict나 data dependency가 있을 때마다 프로세서가 명령어 디코딩을 멈췄었다. 
  - Out-of-Order issue에서는 그 이후의 명령어를 fetch/decode하고, 그 명령어들을 명령어 buffer에 담은 뒤, resource conflict나 dependency가 없는 버퍼에 flag한다. flag된 명령어들은 프로그램의 순서와 상관없이 버퍼로부터 issue된다. 

  

  ​	<u>**R3**</u>:= *R3* * R5									  			**True data dependency**

  ​	R4:= **R3** + 1													<u>Output dependency</u>

  ​	*<u>R3</u>*:= R5 + 1													*Antidependency*

  

  - Out of order의 경우, 뒤의 명령의 결과가 이전 명령의 소스일 때 문제가 될 수 있다(Antidependency).
  - Antidependency와 Output dependency를 Storage conflict라고 한다. 
  - Storage conflict는 레지스터를 추가하여 해결할 수 있다. 
  -  Output dependency는 레지스터 renaming으로 해결할 수 있다. Free register 풀에서 대체용 레지스터를 찾은 뒤 리네이밍하여 쓴 뒤 다시 풀로 돌려주는 방법이다. 