# 变量
## 变量声明
```
# 等号两端不能有空格
% num1=123
% num2=123.456
% str1=abcde

# 如果字符串中包含空格等特殊字符，需要加引号.也可以用双引号，但和单引号有区别，比如双引号里可以使用变量，而单引号不可以。
% str2='abc def'
% str3="abc def $num1"

# 在字符串中可以使用转义字符，单双引号均可
% str4="abc\tdef\ng"

# 输出变量，也可以使用 print
% echo $str1
abcde

# 简单的数值计算
% num3=$(($num1 + $num2))
# (()) 中的变量名可以不用 $
% num3=$((num1 + num2))

# 简单的字符串操作，字符串下标从1开始，下标-1代表最后一个字符
% str=abcdef
# 2 和 4 都是字符在数组的位置，从 1 开始数，逗号两边不能有空格
% echo $str[2,4]
bcd
% echo $str[4,-1]
def
```
## 变量比较
```
# 比较数值，(()) 用于数值比较等操作，如果为真返回 0，否则返回 1，&& 后边的语句在前边的语句为真时才执行，(()) 里边可以使用与（&&）或（||）非（!）操作符，同 c 系列语言
% num=123
% ((num == 123)) && echo good
good
% ((num == 1 || num == 2)) && echo good

# 比较字符串，比较字符串要用 [[]]，内侧要有空格，
% str=abc
% [[ $str == abc ]] && echo good
good

# 可以和空字符串 "" 比较，未定义的字符串和空字符串比较结果为真
# [[]] 里也可以用 && || !
% [[]] $str == "" || $str == 123 ]] && echo good
```
# 语句
## 条件语句
```
# 格式
if (()) {
} elif {
} else {
}

# 用于比较数值
if (( )) {
}

# 用于比较字符串
if [[ ]] {
}

# 用于运行{}中的shell命令并判断运行结果
if { } {
}

#用于在子shell运行命令并判断运行结果，用法同{}
if ( ) {
}

#各种括号可以混合使用混合判断，需要用 { } 把语句包含起来
# 格式
if {[[ ]] && (( ))} && { } {
}
```
## 循环语句
### while
```
# 格式，break用于循环结束，continue用于直接进入下一次循环
while [[ ]] {
    break/continue
}

while (( )) {
    break/continue
}

while { } {
    break/continue
}

while ( ) {
    break/continue
}
```
### until
```
# 格式，until和while相反，util是不满足条件时运行，一旦满足则停止
until [[ ]] {
}
```
### for
```
for i (aa bb cc) {
    echo $i
}

# 枚举当前目录的 txt 文件
for i (*.txt) { 
    echo $i
}

# 枚举数组
array=(aa bb cc)
for i ($array) {
    echo $i
}

for ((i=0; i < 10; i++)) {
    echo $i
}

# 样例，{1..10} 可以生成一个 1 到 10 的数组
for i ({1..10}) {
    echo $i
}
```
### repeat
```
# 格式 repeat 语句用于循环固定次数，n 是一个整数或者内容为整数的变量。
repeat n {
}
```
## 分支语句
```
# ;; 代表结束 case 语句，;& 代表继续执行紧接着的下一个语句，;| 代表继续往下匹配看是否还有满足条件的分支。
case $i {
    (a)
    echo 1
    ;;

    (b)
    echo 2
    # 继续执行下一个
    ;&

    (c)
    echo 3
    # 继续向下匹配
    ;|

    (c)
    echo 33
    ;;

    (d)
    echo 4
    ;;

    (*)
    echo other
    ;;
}
```
## 异常处理语句
```
# 格式
{
    语句 1
} always {
    语句 2
}
```







