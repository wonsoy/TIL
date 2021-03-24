# Permissions



## Symbolic: drwxr-xr-x 



네 부분으로 나눠보자. 



### d			rwx			r-x			r-x

Type               User                  Group              OTher



d: 디렉토리

-: 파일

rwx: read - 읽기 권한

​		write - 쓰기 권한

​		execute - 실행 권한



```
rwx: 읽기, 쓰기, 실행 권한
r-x: 읽기, 실행 권한
r--: 읽기 권한
```



## Numeric: 755

권한이 활성화되어 있으면 1을, 권한이 없으면 0을 넣는다. 



Symbolic: rwx	r-x	r-x

​					↓

Binary:     111	101	101

​					↓

 Decimal:   7		 5		 5



## 권한 변경: chmod



```
chmod u=rwx,g=rx,o=rx -R directory
chmod 755 -R directory
```



위의 두 명령은 같은 명령이다. 

-R: directory 안의 모든 파일들의 권한을 변경



파일 하나의 권한을 변경하는 명령어는 아래와 같다.

```
chmod 777 file.txt
```

