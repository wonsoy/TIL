# Docker Storage

도커 컨테이너가 host machine에 데이터를 저장하는 방법에는 크게 네 가지가 있다. 

1. Volume
2. Bind mount
3. tmpfs mount (for Linux)
4. naped pipe (for Windows)



## 1. Volume

- Host의 filesystem 일부를 도커가 관리한다. 컨테이너가 사라져도 데이터는 사라지지 않는다. 

- 여러 컨테이너들이 동시에 하나의 volume을 쓸 수 있다.

- 다른 컴퓨터에 있는 volume도 쓸 수 있다.



```
docker volume create
docker volume prune
```



- Volume을 만들면 host안에 저장된다. Volume을 컨테이너와 연결하면 그 디렉토리가 컨테이너와 연결된다. Bind mount와 비슷하지만 Volume은 도커에 의해 관리된다는 점이 다르다. 



## 2. Bind mount

-  host의 디렉토리/파일과 컨테이너를 연결한다. Host컴퓨터에 있는 파일 어떤 것이든지 가능하다. 
- 디렉토리/파일은 host machine의 전체경로나 상대경로로 표시한다. 

- 컨테이너와 연결할 host의 디렉토리/파일은 컨테이너를 만들기 전에 이미 존재하지 않아도 된다. 필요할 때 컨테이너가 만드는 것도 가능하다. 

- CLI를 통해 제어하는 것이 불가능하다. .yml파일 안에서 설정해야 한다. 



## 3. tmpfs

리눅스에서만 쓸 수 있다. 컨테이너가 컴퓨터의 메모리(RAM)를 파일시스템처럼 쓴다. 컨테이너가 사라지면 데이터도 사라진다. 

다른 컴퓨터에서 접근할 수 없다. 



## 4. Named pipe

윈도우에서만 쓸 수 있다. 도커 컨테이너와 host사이의 통신을 뚫는 방법이다. 