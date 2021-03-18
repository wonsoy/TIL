도커는 다양한 OS를 지원하는 오픈소스 컨테이너 테크놀로지 기반의 프로그램이다.



애플리케이션을 infrastructure와 구분하여 생각할 수 있다.



애플리케이션을 관리하듯이 infrastructure를 관리할 수 있다(Infrastructure as code).



![https://miro.medium.com/max/1273/1*p8k1b2DZTQEW_yf0hYniXw.png](https://miro.medium.com/max/1273/1*p8k1b2DZTQEW_yf0hYniXw.png)

https://blog.knoldus.com/docker-dockerfile/



Dockerfile에서 infrastructure를 마치 code를 짜듯이 구축한다(infrastructure as code) 그리고 build 하면 Image가 만들어진다.



이 Image를 필요할 때 필요한 만큼 필요한 곳에서 run 하는 것을 Docker Container를 실행한다고 한다.



### Docker Image란

-------------------------------------



Infrastructure as concept를 도커에서 구현한 것이 Docker image이다.



Docker image는 코드, 라이브러리, 환경변수, configuration file 등 애플리케이션이 돌아가는 데 필요한 모든 것들을 담고 있다.