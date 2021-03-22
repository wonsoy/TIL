### Escape Sequence

문자열 안에서 ' 혹은 '' 등의 기호를 사용할 때 escape sequence를 활용할 수 있다.

키보드의 역슬래쉬 ``\`` 를 escape라고 하며, 역슬래쉬 뒤에 하나의 문자를 입력하여 나타내는 표현 `` \x ``을 escape sequence라고 한다. 역슬래쉬는 문자열의 길이에 포함되지 않는다.

```python
str = 'The Queen\'s Gambit'
```

Escape sequence를 기능적으로 이용하는 것이 아니라, 해당 문자를 직접 출력하고 싶을 때는 역슬래쉬를 한 번 더 쓴다.

```python
>>> print('\\n')

>>> print('\\\\n')
\\n
>>> print('\\\\')
\\
```



Escape sequence의 종류

| Escape Sequence |   Description   |
| :-------------: | :-------------: |
|       \'        |  Single quote   |
|       \"        |  Double quote   |
|       \\        |    Backslash    |
|       \t        |       Tab       |
|       \n        |     Newline     |
|       \r        | Carriage return |





### \t, \n Example

```python
print('2x1=2\\t3x1=3\\t4x1\\n2x2=2\\t3x2=3\\t4x2\\n')
2x1=2	3x1=3	4x1
2x2=2	3x2=3	4x2
```