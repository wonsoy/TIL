c++로 쓰인 코드를 MIPS 어셈블리 코드로 번역해보자



### Conditional - if

---------------------------------

```c++
if ( i == j )
    i++ ;
j-- ;
```

i가 $s1에, j가 $s2에 지정된다고 하면  



```MIPS
	bne		$s1, $s2, L1	# !( i == j )이면 L1으로
	addi	$s1, $s1, 1		# i++
L1: addi	$s2, $s2, -1	# j--
```



### Conditional - compound AND condition

--------------------------------------------------



```C++
if ( i == j && i == k )
    i++ ;
else
    j-- ;
j = i + k ;
```

$s1, $s2, $3이 각각 i, j, k를, cond1이 ( i == j )를, cond2가 ( j == k )를 의미한다고 하면



cond1이 false라면 short-circuiting이 일어나서 cond2를 건너뛴다. 



cond1이 true라면 cond2를 살펴본다.



​		cond2가 false라면 if-body를 건너뛰고 else-body를 실행한다.



​		cond2가 true라면 if-bldy를 실행한다. 



```
	  bne	$s1, $s2, ELSE		# cond1이 false면 ELSE로
	  bne	$s1, $s3, ELSE		# cond2가 false면 ELSE로
	  addi	$s1, $s1, 1			# if-body: i++
	  j  NEXT					# NEXT로 점프
ELSE: addi	$s2, $s2, -1 		# else-body: j--
NEXT: add	$s2, $s1, $s3		# j = j + k
```

​                                                                                                                                                                

### Conditional - switch

-----------------------------



```
switch( i ){
	case 1: i++ ;
	case 2: i = i + 2;
			break;
	case 3: i = i + 3;
}
```

i가 $s1, temp변수가 $s2에 지정된다고 할 때

```
		 addi	$s4, $zero, 1		# case 1: temp를 1로 설정한다
		 bne	$s1, $s4, C2_COND	# temp와 i를 비교하여 i가 1이 아니면 두번째 조건을 검사한다
		 j C1_BODY					# i가 1이면 C1_BODY로
C2_COND: addi	$s4, $zero, 2		
		 bne	$s1, $s4, C3_COND	
		 j	C2_BODY					
C3_COND: addi	$s4, $zero, 3				
		 bne	$s1, $s4, EXIT				
		 j	C3_BODY
C1_BODY: addi	$s1, $s1, 1			# case 1: i++
C2_BODY: addi	$s1, $s1, 2			# case 2: i = i + 2
		 j	EXIT					# break
C3_BODY: addi	$s1, $s1, 3			# case 3: i = i + 3
EXIT:
```





### Loops - while

---------------------------



```
while ( i < j ){
	k++ ;
	i = i * 2;
}
```



while문은 if문으로 바꿀 수 있다. 



```
L1: if ( i < j){
		k++;
		i = i * 2;
		goto L1;
	}
```



i, j, k가 각각 $s1, $s2, $s3에 지정된다고 하면 간단하게 번역할 수 있다. 



```
L1:	bge		$s1, $s2, DONE		# !( i < j )면 DONE으로
	addi	$s3, $s3, 1			# k++
	add		$s1, $s1, $s1		# i = i * 2
	j	L1						# 다시 loop하라
DONE:
```



세번째 줄에서 mult를 쓰지 않고 add를 썼다. mult를 쓰면 값을 저장하기 위해 추가적인 메모리가 필요하기 때문이다. 



for문은 while문으로 바꿀 수 있고, 또다시 if문으로 바꾸어 번역할 수 있다.



