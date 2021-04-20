## Pipelining

- 파이프라이닝은 여러 명령어가 중첩되어 실행되는 구현 기술이다. 어떤 명령이 일부 리소스를 사용하고 다른 리소스를 사용하지 않을 때, 사용되지 않는 리소스를 다른 명령이 사용하도록 한다. 

- 명령이 처리되는 사이클을 여러 단계로 나눈다. 

- 일 하나를 하는 시간 자체를 줄이는 것은 아니다. 하지만 일이 병렬로 처리되므로 전체 시간은 줄어든다.

- pipeline rate은 단계들 중 가장 오래 걸리는 것에 영향을 받는다. 

- 각 단계에 걸리는 시간이 거의 같고, 일이 충분히 많다면

  Potential speedup = Number of pipe stages






## Pipeline Hazard

### Structural Hazard

- 한 사이클 안에서 두개 이상의 명령이 같은 하드웨어를 사용하고자 하는 경우
- 해결법
  1. Stall:  이전 명령어가 해당 하드웨어를 다 쓸 때까지 기다렸다가 "버블"을 만들고 다음 명령을 처리한다. 쉽고 저렴하지만 CPI가 증가한다.
  2. 하드웨어적인 해결





### Data Hazard(Data Dependency)

- 서로 다른 명령이 같은 저장공간을 사용하고자 하는 경우(명령이 아직 파이프라인에 있는 이전 명령에 대하여 dependency가 있는 경우)



- Read After Write(RAW)

  - I가 r1을 쓰기 전에 다음 명령인 J가 r1을 읽으려고 하는 경우

    ```
    I:	add	r1, r2, r3
    J:	sub	r4, r1, r3
    ```

  - 해결법: Stall, Forwarding(이전 명령에서 값을 레지스터에 쓰기까지 기다리지 않고, ALU에서 계산이 끝나자마자 가져온다) 

  - Forwarding을 해도 데이터 해저드가 일어나는 경우도 있다. 하지만 forwarding을 하지 않는 것보다는 stall을 덜 할 수 있다. 

  - Pipeline scheduling으로 명령의 순서를 바꿔 stall을 줄일 수 있다. 







### Control Hazard

- 다음 PC를 어떻게 결정할 것인가?(분기를 할 것인가 말 것인가). 

- PC에 대한 dependency때문에 발생한다고 할 수 있다. 

- 해결법(static, 컴파일 단계에서 해결)

  1. Stall

  2. Predict Branch Not Taken

     ​	분기가 일어나지 않는다고 가정하고 다음 명령어들을 실행한다. 만약 분기가 일어나면 실행했던 명령들을 버리고(flush) Target address에서 명령을 실행한다. 

     

  3. Predict Branch Taken

     ​	 분기가 일어났다고 가정하고 분기 목적지에서 명령을 실행한다. 만약 분기가 일어나지 않으면 분기점의 다음 명령어들을 실행한다. 메모리 주소를 업데이트해야하므로 한 사이클정도 손해이다. 

     

  4. Taken Backwards, Not Taken Forwards

     ​	Target address가 현재 위치의 뒤에 있으면 분기가 일어난다고 가정하고, 앞에 있으면 분기가 일어나지 않는다고 가정한다. 분기 목적지가 뒤에 있는 경우(e.g. for문, while문)는 분기가 일어날 확률이 높다는 것을 이용하는 방법이다. 

     

  5. Delayed Branch

     ​	Pipeline scheduling과 비슷한 컨셉이다.  분기를 할 지 말 지 결정되는 동안 분기와 상관 없이 실행되어야 하는 명령어들이 실행되도록 명령어들의 위치를 조정한다. 

     
     
  6. Predicated Execution
  
     Control dependence를 data dependence로 바꾼다. 분기를 없애고 명령어들의 sequence로 문제를 바꾼다. 분기 결과에 따라 필요없어진 명령은 NOP처리한다. 예측하기 어려운 분기들을 제거하지만 모든 분기를 predecation으로 제거하기는 힘들다. 
  
     예측이 틀릴 경우 발생하는 손해가 predication에 의해 낭비되는 작업보다 클 경우 predication이 이득이다. 
  
     ex) ARM ISA의 Conditional execution: 거의 모든 ARM 명령어들은 condition code를 포함한다.  조건의 결과에 따라 뒤의 명령어들의 처리가 결정되는 구조이다. 
  
     


- 해결법(dynamic, run time 단계에서 해결)

  1. Last Time Prediction(single bit)

       BTB(Branch Target Buffer)가 이전에 실행되었던 분기 명령의 target address를 기억한다. 만약 BTB에 target address가 없으면 분기 명령이 아니므로 다음 명령은 PC+4로 처리한다. 

       이전에 분기가 일어났으면 이번에도 분기가 일어나고, 이전에 분기가 일어나지 않았으면 이번에도 분기가 일어나지 않을 것이라고 예측한다.

       분기가 일어나는 경우와 일어나지 않는 경우가 번갈아가며 나타날 때는 정확도가 매우 낮아진다. 

       

  2. Two Bit Counter Based Prediction

     예측이 두 번 연속으로 틀리면 예측을 바꾼다. 

     

  3. Two Level Prediction(Global, Local)

     - Global: 분기 결과가 다른 분기의 결과에 영향을 주는 경우가 있다. 이 경우, 현재 분기의 발생 여부에 따라 다른 분기가 일어날 것인지 일어나지 않을것인지 예측할 수 있다. 

     ```
     branch Y: if (cond1)
     ...
     branch Z: if (cond2)
     ...
     branch X: if (cond1 AND cond2)
     ```

     - Local: 분기의 결과는 같은 분기의 과거의 결과에 영향을 받을 수 있다.

     ```
     for(i=1;i<=4;i++){}
     ```

     

     - Two Level *Global* Branch Prediction
       - Level 1: GHR(Global History Register)에 이전 branch에서의 분기 결과를 저장한다. 
       - Level 2: 이전의 GHR값들을  Pattern History Table에 기록한다(History of "the" GHR).

       

       - 문제점: interference in the PHTs - 서로 다른 분기가 동일한 history register에 값를 기록하면 문제가 될 수 있다. 

         - Gshare: Global branch history와 branch PC를 XOR연산하여 테이블에 기록하는 방법이다. 
         - Gskew: 여러 PHT를 사용하여 각각 다른 hash function을 적용한다. 그리고 가장 많이 나온 prediction을 채택하는 방법이다. 

         

     - Two Level *Local* Branch Prediction(per-branch history register). 

       - Level 1: 하나의 분기에 대해 history register를 만든다.  
       - Level 2: PHT에 접근하여 예측 결과를 가져온다.  



  4. Loop Unrolling

     Loop안에서 코드들을 여러번 복제한다. Loop overhead가 줄어들고 Control dependence가 줄어들어 프로그램 효율이 향상된다.  더 많은 레지스터가 필요하다. 

     

     ```
     for (int i=0; i<16; i++)
     data[i] = i;
     ```

     ​			↓

     ```
     for (int i=0; i<16; i+=4)
     {
     data[i]=i;
     data[i+1]=i+1;
     data[i+2]=i+2;
     data[i+3]=i+3;
     }
     ```

     위의 경우, 

     Number of copies = Loop unrolling factor = 4

     Number of iteration = 16/4 = 4 

     이다. 

     

     