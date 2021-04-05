# Dockerfile

Dockerfile을 run하여 image를 만든다. 



```dockerfile
FROM ubuntu:18.04
COPY . /app
RUN make /app
CMD python /app/app.py
```

``FROM`` 은 가장 근간이 되는 이미지를 Dockerhub로부터 가져온다. 

``COPY`` 는 로컬의 현재 디렉토리의 파일들을 도커 이미지의 /app에 카피한다. 

``RUN``은 ``make`` 를 통해 어플리케이션을 빌드한다.

``CMD``는 컨테이너 안에서 명령을 수행한다. 위 예제에서는 ``python``을 통해서 ``app.py``를 실행한다. 



----------

- ``WORKDIR``은 디렉토리를 설정한다.

- ``EXPOSE``는 포트를 설정한다. 

- ``CMD``를 통해 컨테이너를 실행할 때의 디폴트를 설정한다. 하나의 Dockerfile에는 하나의 ``CMD``만 존재할 수 있다. 

  ``CMD ["executable", "param1", "param2"]`` 혹은 ``CMD ["param1", "param2"]`` , shell에서 사용할 때는 ``CMD command param1 param2``와 같은 형태를 가질 수 있다. 







계속 참고할 것

-----

[Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

