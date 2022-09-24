## Makefile 的变量、模式匹配



#### 变量

系统变量

####自定义变量

空赋值 ?=

追加赋值 +=

立即赋值 :=

自动化变量

$< 第一个依赖文件

$^全部的依赖文件

$@目标文件

### 匹配模式

%匹配任意多个非空字符

shell: *通配符

### 默认规则

.o文件默认使用.c文件来编译

# Makefile条件分支

### 条件分支

```
ifeq(var1,var2)#两个值相等为真
....
else
....
endif
```

```
ifneq(var1,var2)3两个值不相等为真
......
else
.......
endif
```



# Makefile函数

函数名称

patsubst 文本替换函数

```
$(patsubst %.c,%o,x.c bar.c)
```



notdir 取文件名函数

```
$(notdir src/foo.c hacks)
```



wildcard 获取匹配模式文件名函数

```
$(wildcard *.c)
```



foreach 循环函数 遍历

```
dirs := a b c d
$(foreadch dir,$(dirs),$(wildcard $(dir)/*)
```



# Makefile 解决头文件依赖



```
#ifndef __xxx_H
#define __xxx_H

#endif

```

```
#编译器信息
INC_DIR=include
CFLAGS=$(patsubst %,-I%,$(INC_DIR))
```

