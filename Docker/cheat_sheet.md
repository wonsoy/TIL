#### Information

| Command            | Description                  |
| ------------------ | ---------------------------- |
| docker --version   | 도커 버전                    |
| docker system info | 도커 실행환경                |
| docker system df   | 도커가 쓰고 있는 디스크 공간 |
| docker search      | 도커허브에서 검색            |
| docker stats       | 컨테이너 상세 정보           |





#### Clean up

| Command                                  | Description               |
| ---------------------------------------- | ------------------------- |
| docker image rm {image ID}               | 이미지 삭제               |
| docker image rm $(docker image ls -a -q) | 모든 이미지 삭제          |
| docker image prune [-a]                  | stop된 모든 이미지 삭제   |
| docker stop $(docker ps -a -q)           | 모든 컨테이너 stop        |
| docker container prune                   | stop된 모든 컨테이너 삭제 |
| docker system prune                      | 모두 삭제                 |





#### Dockerfile

| Command                                                      | Description                                                 |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| docker build -t {image name} .                               | Dockerfile을 빌드하여 image 생성 (현재 디렉토리에서)        |
| docker build --no-cache -t {image name} .                    | 이전 기록을 캐싱하지 않도록 설정하여 빌드                   |
| docker run --name {container name} -d -p  4000:80 {image name} | image를 run하여 container 생성(포트 4000번을 80번으로 매핑) |





#### Docker Hub

| Command                                          | Description                        |
| ------------------------------------------------ | ---------------------------------- |
| docker login                                     | 로그인                             |
| docker tag {image} {username}/{repository}:{tag} | 업로드를 위해 이미지에 태그 붙이기 |
| docker push {username}/{repository}:{tag}        | 레지스트리에 태그된 이미지 업로드  |
| docker run {username}/{repository}:{tag}         | 레지스트리로부터 이미지 run        |





#### docker-compose

| Command              | Description          |
| -------------------- | -------------------- |
| docker-compose up    | 모든 서비스 시작     |
| docker-compose down  | 모든 서비스 stop     |
| docker-compose scale | 서비스의 스케일 조정 |



#### Docker storage

| Command                     | Description      |
| --------------------------- | ---------------- |
| docker volume create {이름} | 볼륨 생성        |
| docker volume prune {이름}  | 볼륨 삭제        |
| docker volume ls            | 볼륨 리스트 보기 |

