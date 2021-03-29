### Docker

도커는 다양한 OS를 지원하는 오픈소스 컨테이너 테크놀로지 기반의 프로그램이다.



도커를 통해 애플리케이션을 infrastructure와 구분하여 생각할 수 있으며 애플리케이션을 관리하듯이 infrastructure를 관리할 수 있다(Infrastructure as code).

![https://miro.medium.com/max/1273/1*p8k1b2DZTQEW_yf0hYniXw.png](https://miro.medium.com/max/1273/1*p8k1b2DZTQEW_yf0hYniXw.png)

https://blog.knoldus.com/docker-dockerfile/

Dockerfile에서는 code를 짜듯이 infrastructure를 구축한다(infrastructure as code) 그리고 build 하면 Image가 만들어진다.



이 Image를 필요할 때 필요한 만큼 필요한 곳에서 run 하는 것을 Docker Container를 실행한다고 한다.



### Docker Image

Infrastructure as concept를 도커에서 구현한 것이 Docker image이다.



Docker image는 코드, 라이브러리, 환경변수, configuration file 등 애플리케이션이 돌아가는 데 필요한 모든 것들을 담고 있다.



### Docker Engine

도커의 가장 핵심 소프트웨어이다. 컨테이너를 실행, 관리한다. 

![https://stefanjarina.gitbooks.io/docker/content/assets/engine-components-flow.png](https://stefanjarina.gitbooks.io/docker/content/assets/engine-components-flow.png)

https://stefanjarina.gitbooks.io/docker/content/basics/architecture.html



개발자는 CLI를 사용해서 명령을 내리고 REST API는 deamon에게 작업을 요청한다. 이 과정을 거쳐 daemon은 컨테이너, 이미지, 네트워크, 데이터볼륨 등을 다룬다. 



### 실습



```
docker run hello-world
```

hello-world라는 이미지를 docker에서 run하라.



만약 로컬에 없는 이미지를 입력하면 도커는 Docker Hub에 접속해서 이미 누군가가 만들어놓은 이미지를 pull한다. 



ubuntu 이미지를 실행하고 컨테이너를 만든 후 그 안에서 bash를 실행해보고 컨테이너와 이미지를 지우는 과정은 아래와 같다. 

```
docker run ubuntu
docker container run -it -d --rm --name ubuntuos ubuntu:latest
docker exec -it ubuntuos /bin/bash
docker container stop ubuntuos
docker image rm -f <image id>
```

