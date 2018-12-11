shell 常用命令
===============

环境相关
---------------
当前 macos 版本 10.14

```shell
$ cat /System/Library/CoreServices/SystemVersion.plist |awk '/ProductVersion/{getline;v=$0;gsub(/\t*<\/*string>/,"",v); print v}'
> 10.14
```

### 变量

|命令|样例|说明|
|---|---|---|
|env|env [cmd]|在指定环境变量下执行命令,显示当前用户的环境变量|
|set| |包括用户环境变量和系统环境变量|
|export|export valName=value|当前进程及子进程有效|
|=|valName=value|当前进程有效|
|local|local valName=value|当前shell文件有效|
|\$0,\$1~n | \$0 脚本名,\$1~n 第一、第n个参数||
|\$?|上一条命令返回的状态码0-255||
|\$\$|当前进程的进程号 PID||
|\$!|最后运行的后台进程的PID||
|\$*|参数表||
|\$@|参数表||
|\$#|参数个数||

* $PATH

``` shell
$ echo $PATH # 显示变量$PATH
$ export WELCOME="hello" # 设置变量$WELCOME的值 ，对当前进程及其子进程有效
$ env # 显示所有环境变量
$ myText="hello world"  # 设置变量myText的值  ，只对当前进程有效
file> local value01=123 # 只对当前shell脚本有效
```

* env

``` shell
$  env
> 
TERM_PROGRAM=Apple_Terminal
SHELL=/bin/bash
TERM=xterm-256color
TMPDIR=/var/folders/6l/q6p00dzn4klcyqhsf_f6rnpm0000gn/T/
Apple_PubSub_Socket_Render=/private/tmp/com.apple.launchd.DuMS6fnMgQ/Render
TERM_PROGRAM_VERSION=421
TERM_SESSION_ID=7E80360F-DF05-4DD3-BBD7-06767120DB4B
USER=xxxx
SSH_AUTH_SOCK=/private/tmp/com.apple.launchd.B0oODDW1sP/Listeners
PATH=/opt/local/bin:/opt/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/go/bin:/opt/X11/bin:/Applications/Wireshark.app/Contents/MacOS
PWD=/Users/xxxx
LANG=en_US.UTF-8
XPC_FLAGS=0x0
XPC_SERVICE_NAME=0
SHLVL=1
HOME=/Users/xxxx
LOGNAME=xxxx
LC_CTYPE=en_US.UTF-8
DISPLAY=/private/tmp/com.apple.launchd.83VIc3mFjA/org.macosforge.xquartz:0
_=/usr/bin/env
```

* set

``` shell
$ set
> 
Apple_PubSub_Socket_Render=/private/tmp/com.apple.launchd.DuMS6fnMgQ/Render
BASH=/bin/bash
BASH_ARGC=()
BASH_ARGV=()
BASH_LINENO=()
BASH_REMATCH=([0]="g")
BASH_SOURCE=()
BASH_VERSINFO=([0]="3" [1]="2" [2]="57" [3]="1" [4]="release" [5]="x86_64-apple-darwin18")
BASH_VERSION='3.2.57(1)-release'
COLUMNS=80
DIRSTACK=()
...
```


### 引号
|命令|样例|说明|
|---|---|---|
|''|'hello'|不解析引号内的变量|
|""|"hello $userName"|解析引号内的变量|
|\`\`| echo \`date\`|引用命令的执行结果|

``` shell
$ name='zhangsan'
$ hi="hello $name"
$ echo $hi
> hello zhangsan
```

### 流程

|命令|样例|说明|
|---|---|---|
|if |if ...;then ...; elif ... ;then ...;else ...; fi||
|for | for ((i=0;i<10;i++)) ; do ... ; done <br> for i in 0 1 2 3 ; do ... ; done <br> for i in {0..3} ; do ... ; done||
|while | C=0 ; while [ $C -lt 5 ] ; do  C=`expr $C + 1` ; echo $C ; done||
|break|break 跳出所有循环 break n 跳出第n层循环||
|continue|跳出当前循环||
|case| N=3 ; case $N in  1) ... ; ;; *) ... ; ;; esac ||

* if

``` shell
$ if [ $a -gt 2 ] ; then echo "$a > 2 "; fi

> 3 > 2 

$ if [ $a -lt 2 ] 
  then 
    echo "$a < 2"
  elif [ $a -gt 2 ]
  then
    echo "$a > 2"
  else
    echo "$a = 2"
  fi
 
> 3 > 2

$ a=2
$ if [ $a -lt 2 ] ; then  echo "$a < 2"; elif [ $a -gt 2 ]; then echo "$a > 2"; else echo "$a = 2"; fi

> 2 = 2
```

* for

``` shell
$ for ((i=0;i<3;i++)) 
  do 
    echo $i 
  done

> 0
1
2

$ for i in 0 1 2 3 
  do 
    echo $i 
  done

> 0
1
2
3

$ for i in {0..3} 
  do 
    echo $i 
  done

> 0
1
2
3
```

* while

``` shell
$ C=0 
$ while [ $C -lt 5 ] 
  do 
    C=`expr $C + 1` 
    echo $C 
  done
  
> 1
2
3
4
5

$ echo "input num , ctrl+c done" 
$ while read NUM ; do 
    echo "get NUM is $NUM" 
  done

> get NUM is
< 2
> get NUM is 2
< ^C

```

* case

``` shell
$ N=3 
$ case $N in 
    1) 
      echo 1 
    ;; 
    2) 
       echo 2 
    ;; 
    *) 
       echo "num is $N" 
    ;; 
  esac
  
> num is 3
```

### 运算

|命令|样例|说明|
|---|---|---|
|expr |expr $a + $b| +-*/  加减乘除 <br> = % 取余 |
|[] or test |[ $N -lt 2 ] <br> test $N -lt 2 -a $N -gt 0 |-gt 大于 -lt 小于 -ge 大于等于 -le 小于等于<br> -eq == 等于 -ne != 不等于 <br> ! 非 -o \|\| 或 -a && 与 |

|[ 条件A ] && [条件B ]|逻辑运算[ 条件A ] && [条件B ] ((A&&B)) [[ A&&B ]]||

|-* file|-d 目录  -r 可读 -w 可写 -x 可执行 -s 空文件 -e 文件或目录是否存在||

### 函数

|命令|样例|说明|
|---|---|---|
|funName(){...;return NUM}|函数定义||
|\$0~n|||
|\$#|||
|\$*|||
|\$?|||
|read|标准输入||
|declare|定义变量 -r 只读 -i 整数 -a 数组||
|local|local valName=value|当前shell文件有效|

### 字符串

|命令|样例|说明|
|---|---|---|
|"..."|字符串 展开变量||
|'...'|字符串||
|\${#str1}|echo \${#str}|长度|
|\${str1:0:3|echo \${str: -3}|截取|
|\$str1""\$str2|拼接||
|arr=(1 2 3 4)|数组||
|arr[0]=2|赋值||
|unset arr[2]|删除||
|${arr[3]}|元素||
|${\#arr[*]|长度||
|${\#arr[@]|长度||

``` shell
$ a=(1 2 3 4 5) 
$ echo ${a[*]} 
> 1 2 3 4 5 
$ echo ${#a[*]} 
> 5 
$ echo ${a[2]} 
> 3 
$ echo ${a[@]:2:4} 
> 3 4 5	
$ echo ${a[@]: -2} 
> 4 5 
$ echo ${a[@]: 2} 
> 3 4 5 
$ unset a[3] 
$ echo ${a[@]} 
> 1 2 3 5
```

### 管道

|命令|样例|说明|
|---|---|---|
|cmd>file|输出重定向||
|cmd<file|输入重定向||
|cmd>>file|追加方式将输出写入文件||
|cmd n>file|将文件描述符为n的输出重定向||
|cmd n>&m |将输出描述符重定向到另一个描述符||
|cmd n<&m |将输入文件合并||
|cmd << tag |||
|/dev/null|空文件位置，用于输出重定向||
|描述符 0 标准输入 1 标准输出 2 标准错误输出|||
|cmd &|后台运行 <br> ctrl+z 暂停进程 <br> fg 将后台进程调出 bg 将暂停的进程压入后台 <br> jobs 后台进程表||
|nohub cmd &|后台运行，并且不依赖与当前进程，当前shell进程关闭不会影响nohub启动的进程 ||


### 常用命令

|命令|样例|说明|
|---|---|---|
|date |echo \`date +%Y-%m-%d-%H:%M:%S\`||
|crontab|crontab -l <br> crontab -e |定时器|
|* * * * * bash /opt/date.sh| 每隔一分钟执行一次 date.sh 命令 <br> * 分　时　日　月　周　命令||
|tail -f /var/log/cron |查看crontab日志 <br> * 必须打开rsyslog服务cron文件中才会有执行日志(service rsyslog status)||
|ps|ps aux <br> ps -ef|查看当前进程列表|
|jps||查看java进程列表|
|cat file| cat -n||
|tail|tail -f <br> tail -100||
|head|head -100||
|uptime|||
|df|df -h||
|du|du -h\|awk '\$1~/G\|T/'||
|awk|NR 当前行<br> FS -F 分隔符<br>if else <br> for in <br> getline 获取下一行 <br>next 跳出当前行的操作<br> BEGIN{#开始段}{#每一行}END{#最后段} <br> print ||
|wc|wc -l file||
|grep|||
|find |find . -name 'Li*'||
|ls|ls -nal||
|rm|||
|cd|||
|chmod|chmod +x file||
|echo|||
|printf|||






### 参考
- [shell 笔记（Mac 版）](https://www.jianshu.com/p/f7ef4f95f5c6)



  
  
  
  
