#### Information

| Command            | Description                  |
| ------------------ | ---------------------------- |
| docker --version   | 도커 버전                    |
| docker system info | 도커 실행환경                |
| docker system df   | 도커가 쓰고 있는 디스크 공간 |
| docker search      | 도커허브에서 검색            |
| docker stats       | 컨테이너 상세 정도           |



#### Clean up

| Command                                  | Description        |
| ---------------------------------------- | ------------------ |
| docker image rm {image ID}               | 이미지 삭제        |
| docker image rm $(docker image ls -a -q) | 모든 이미지 삭제   |
| docker image prune [-a]                  | 모든 이미지 삭제   |
| docker stop $(docker ps -a -q)           | 모든 컨테이너 stop |
| docker container prune                   | 모든 컨테이너 삭제 |
| docker system prune                      | 모두 삭제          |

