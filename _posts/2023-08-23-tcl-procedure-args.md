---
layout: post
title: "tcl procedure args"
categories: tcl
---
   
## tcl procedure args

> procedure argument 를 list 로 전달하고 싶을 때 {*} 또는 eval 을 이용하여 전달 할 수 있다.

### 1. {\*} - *Tcl 8.5 버전부터 사용 가능*   
 {\*} 은 tcl 에서 expansion 연산자로 리스트 원소를 하나씩 전개하여 전달하는 역할을 한다. {\*} 을 이용하여 procedure argument 로 list 를 전달하는 방법은 다음과 같다.
```tcl
proc myProc {arg1 arg2 arg3 arg4} {
    puts "$arg1 $arg2 $arg3 $arg4"
}

set myList [list a b c]
myProc {*}$myList d
# a b c d
```

### 2. eval   
eval 은 문자열로 된 tcl 코드를 실행하는 명령으로 eval 과 concat 을 사용하여 procedure argument 로 list 를 전달 할 수 있다.
```tcl
proc myProc {arg1 arg2 arg3 arg4} {
    puts "$arg1 $arg2 $arg3 $arg4"
}

set myList [list a b c]
eval [concat myProc $myList d]
# a b c d
```
   
---
   
procedure 내부에서 인자로 받은 args 를 그대로 다른 procedure args 로 전달할 때도 위 방법을 이용할 수 있다.
```tcl
proc myProc1 {args} {
    myProc2 {*}$args
    # eval [concat myProc2 $args]
}

proc myProc2 {args} {
    puts $args
}

myProc2 a b c
```
