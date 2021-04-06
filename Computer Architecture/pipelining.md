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
  - Stall: 기다렸다가 "버블"을 만들고 다음 명령을 처리한다. 쉽고 저렴하지만 CPI가 증가한다.





### Data Dependency(Data Hazard)

- 서로 다른 명령이 같은 저장공간을 사용하고자 하는 경우

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