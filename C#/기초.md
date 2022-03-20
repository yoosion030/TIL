# C# 기초

## 확장자

[파일이름].cs

## Write()

콘솔에 출력해줌

```C#
Console.Write(1);
Console.Write(2);
Console.Write(3);
```

결과

```C#
123
```

## WriteLine()

콘솔에 한줄 씩 출력해줌

```C#
Console.WriteLine(1);
Console.WriteLine(2);
Console.WriteLine(3);
```

결과

```C#
1
2
3
```

## 자료형

- bool : true or false (논리값)
- btye
- sbtye : 8비트 부호있는 정수
- char
- decimal
- double
- float
- int
- uint : 32비트 부호없는 정수
- long
- ulong
- short
- ushort

## ReadLine()

입력값을 받음 (c에서는 scanf)
문자열로 받기 때문에 숫자를 받고 싶다면 int로 형변환을 해줘야함

## int.Parse()

int.Parse('값')을 해주면 int 형으로 변환해줌

```C#
int input = int.Parse(ReadLine());
```

입력값을 문자열에서 int형으로 변환됨
