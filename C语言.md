

# C语言 二进制转换

254 -> unsigned int -> 32位

十进制的 254  = 二进制(11 111 110) =  八进制 376

八进制可以采用二进制中的 从右边数每三位为421相加，不够三位的可以补个0如：

十进制的254的二进制为（11111110），可以分成 （011 111 110）2+1  4+2+1 4+2+0

十六进制可以采用二进制中的 从右边数每四位为8421相加，不够四位可以补个0

如：

十进制的254的二进制为（11111110），可以分成（1111 1110）8+4+2+1 8+4+2+0

![](https://cdn.svsvg.top/20220910155338.png)



## 数据类型

1 .所占字节数

2.存储区别

3.不同类型的数据间进行转换

4. 特殊性：

​		1）布尔型bool

​		2）float类型

​		3）char型是否哦呦符号

​		4）不同形式的0值

​		5）数据类型与后续代码中所使用的输入输出要相匹配

### 常量与变量

常量：在程序执行过程中值不会发生变化的量

分类： 整型常量，实型常量，字符常量，字符串常量，标识常量

​		整型常量：1，78

​		实型常量：3.14,5.54

​		字符常量：由单引号引起来的单个的字符或转义字符，如'a' 'b'

​		字符串常量：由双引号引起来的一个或多个字符组成的序列

​								如：“”

​		标识常量：#define,处理程序的预处理阶段

​		缺点：不检查语法，只是单纯的进行替换

```
#define MAX(a,b) \
({int A=a,B=b;(A) > (B)?(A):(B)})

({typeof(a) A=a,B=b;(A) > (B)?(A):(B)})
```



变量：用来保存一些特定内容，并且在程序执行过程中值随时会变化的量

定义：[存储类型]  数据类型  标识符  = 值

​								TYPE  NAME = VALUE;

​				标识符：有字母，数字，下划线组成且不能以数字开头的一个标识序列

写标识符尽量做到见名生义。

​				数据类型：基本数据类型 + 结构类型

​				存储类型： auto static register extern

​				auto：默认 自动分配空间，自动回收

​				register：（建议型）寄存器类型

​				static：静态型，自动初始化为0只或空值，并且其变量的值具有继承性，常用于修饰变量

​				extern：说明型，意味着不能改变被说明的变量的值或类型

变量的生命周期和作用范围

 1）全局变量和局部变量

2）局部变量和局部变量	

![](https://cdn.svsvg.top/20220911161820.png)



### 运算符和表达式

表达式与语句的区别

运算符部分：

​		1）每个运算符所需要的参与运算的操作数的个数

​		2）结合性

​		3）优先级

​		4）运算符的特殊用法

​			如：%，= 与==。逻辑运算符（&&，||）的短路特性

​		5）位运算的重要意义

​			按位或 |  只要有一个为1 按位都是1

​			如  1100

​				|1001

---------------------------------------

​				1101

​		按位与& 只有两者为真才为真

​	如：1100

​		& 1001

---------------------

​			1000

​	异或运算 ^ 相同为0 不同为1

​	将操作数中某一位置1，其他位不变：num = num | 1 <<  n;

​	将操作数中某一位清0，其他位不变：num = num & ~(1 <<  n);

​	测试第n位：if(num & 1 << n);

​	从一个指定宽度的数中取出其中的某几位： & 1111 << n



### 输出输入专题

input & output -> I/O(标准io，文件io)

1. 格式化输入输出函数：scanf printf
2. 字符输入输出函数：getchar,putchar
3. 字符串输入输出函数：gets（！），puts



标准输入

 int scanf(const char *format,.......);



## 控制流程

顺序，选择，循环

NS图 ，流程图  工具Dia

简单结构与复杂结构：自然流程



关键字：

选择：if-else  switch-case

循环：while  do-while for  if-goto

辅助控制：continue break



注意：else只和相近的if匹配



# 数组

一维数组

1.定义

[存储类型] 数据类型  标识符【下标】

2. 初始化

​	不初始化

​	全部初始化

​	部分初始化



3. 元素引用

​		数组名【下标】

4. 数组名

​		数据名是表示地址的常量，也是数组的起始位置

5. 数组越界



## 数组部分：

一维数组：

1. 求fibonacci数列的前十项，并在数组中逆序存放

```c
# 是等 数组元素的前1和2的元素相加
#define MAX 10

int main(int argc, char const *argv[])
{
    int fib[MAX] = {1,1};
    int i;
    int tmp;

    for ( i = 2; i < sizeof(fib) / sizeof(fib[0]); i++)
    {
        fib[i] = fib[i - 1] + fib[i - 2]; 
    }
    for(i = 0;i < sizeof(fib) / sizeof(fib[0]); i++)
        printf("%d ",fib[i]);
    printf("\n");

    int j = 0,k;
    k = sizeof(fib) / sizeof(fib[0]) -1;
    while( j < k)
    {
        tmp = fib[j];
        fib[j] = fib[k];
        fib[k] = tmp;
        j++;
        k--;

    }
    for(i = 0;i < sizeof(fib) / sizeof(fib[0]); i++)
        printf("%d ",fib[i]);
    printf("\n");
    return 0;
}

```



2. 数据排序：冒泡，选择，快速排序

​		

**冒泡排序**：一个数和其他数做比较，这个数比较大就往后移。

需要走 N-1趟

```c
//冒泡排序
int main(int argc, char const *argv[])
{
    int arr[] = {10,10,5,80,64,24,6,7,8,40};
    int i,j,tmp,arrNum;
    arrNum = sizeof(arr) / sizeof(arr[0]) - 1;

    for(i = 0; i < arrNum; i++){
        for(j = 0; j < (arrNum - i);j++){
            if(arr[j] > arr[j + 1]){
                tmp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = tmp;
            }
        }
    }
    for(i = 0; i < arrNum +1; i++){
        printf("%d ",arr[i]);
    }
    printf("\n");

    return 0;
}

```



**选择排序：**

```
int main(int argc, char const *argv[])
{
    int arr[] = {10,10,5,80,64,24,6,7,8,40};
    int i,j,tmp,arrNum,k;
    arrNum = (sizeof(arr) / sizeof(arr[0]));

    for(i = 0;i < arrNum; i++){
        printf("%d ",arr[i]);
    }
    printf("\n");

    for(i = 0; i < (arrNum - 1); i++){
        k = i;
        for(j = i + 1; j < arrNum; j++){
            if(arr[j] < arr[k]){
                k = j;
            }
        }
        if( i != k){
            tmp = arr[i];
            arr[i] = arr[k];
            arr[k] = tmp;
        }
    }
    for(i = 0;i < arrNum; i++){
        printf("%d ",arr[i]);
    }
    printf("\n");

    return 0;
}
```





3. 进制转换

```
#define N 128
//进制转换
int main(int argc, char const *argv[])
{
    int num,base,i = 0;
    printf("Please enter a num:");
    scanf("%d",&num);
    printf("Please enter the base:");
    scanf("%d",&base);
    int arr[N] ={0};

    do{
       arr[i] = num % base;
       num = num /base;
       i++;
    }while(num != 0);
    for(i--; i >= 0; i--){
        if(arr[i] >= 10){
            printf("%c",arr[i] - 10 + 'A');
        }
        else
            printf("%d",arr[i]);
    }
    printf("\n");
    return 0;
}
```




4. 删除法求质数





### 二维数组

1 定义，初始化

​	【存储类型】数据类型 标识符 【行下标】【列下标】

2 元素引用

​	数组名【行标】【列标】

3 存储形式

​	顺序存储，按行存储

4 深入理解二维数组



**二维数组**

1 行列互换

```
#define N 3
#define M 2
//二维数组行列转换
int main(int argc, char const *argv[])
{
    int a[][N] = {1,2,3,4,5,6},b[N][M];
    int i,j;
    for(i = 0; i < M; i++){
        for(j = 0; j < N; j++){
            printf("%d ",a[i][j]);
            b[j][i] = a[i][j];
        }
        printf("\n");
    }
    for(j = 0; j < N; j++){
        for(i = 0; i < M; i++){
            printf("%d ",b[j][i]);
        }
        printf("\n");
    }
    return 0;
}
```



2 求最大值及其所在位置

```
//二维数组寻找max
int main(int argc, char const *argv[])
{
    int a[M][N] = {1,2,3,4,5,6};
    int i,j,max,row,col;
    max = a[0][0];
    row = 0;
    col = 0;
    for(i = 0; i < M; i++){
        for(j = 0; j < N; j++){
            if(max < a[i][j]){
                max = a[i][j];
                row = i;
                col = j;
            }   
        }
    }
    printf("max[%d][%d] = %d\n",row,col,max);
    return 0;
}

```



3 求各行与各列的和

```
#define N 3
#define M 3
//二维数组sum
//从2x2的数组中 得到每行每列的sum，需要定义成3x3的数组 用于存放sum后的数值
int main(int argc, char const *argv[])
{
    int a[N][M] = {{5,3},{7,3}};
    int i,j;
    for(i = 0; i < (N - 1); i++){
        for(j = 0; j < (M -1); j++){
            a[N - 1][M - 1] += a[i][j];
            a[N -1][j] += a[i][j];
            a[i][M - 1] += a[i][j];
        }
    }
    for(i = 0; i < N; i++){
        for(j = 0; j < M; j++){
            printf("%4d ",a[i][j]);
        }
        printf("\n");
    }
    
    return 0;
}
```



4 矩阵乘积





### 字符数组

 1 定义，初始化，存储特点

​		【存储类型】 数据类型 标识符【下标】...

​			单个字符

2 输入输出

3常用函数

strcpy

strcat

strlen



多维数组。



## 指针

1变量与指针

指针就是地址，

变量是对地址进行抽象化，

2指针与指针变量



3直接访问与间接访问

```
int i = 1;
int *p = &i;
int **q = &p;

i  *p  **q
&i p  *q
```



4空指针与野指针



5空类型

void *

6定义与初始化的书写规则



7指针运算

 &  * 关系运算  ++ --

8指针与数组

​	指针与一维数组

​	指针与二维数组

​	指针与字符数组



9 const与指针

​	指针常量

​	int * const p；

可以修改指针空间的值，不能修改指针的指向

```
int i = 1;
int j = 100;
int * const p = &i;
T *p = 10;

F p = &j;
```



​	常量指针

​	可以修改指针的指向，但是不能修改值。

​	const int *p;

​	int const *p;

```

int i = 1;
int j = 100;
const int *p = &i;

T: p = &j;
// F *P = 10;
```



10 指针数组与数组指针

 数组指针：【存储类型】 数据类型  （*指针名）【下标】 = 值

​	如：int （*p）[3]；

指针数组：【存储类型】 数据类型  * 数组名 【长度】

​	如：int *p[3]；

11 多级指针



## 函数

1 函数的定义

​	数据类型 函数名（）

2 函数的传参

​	值传递

​	地址传递

3函数的调用



函数与一维数组

```
// 等价与
// void print_arr(int *arr,int len)
void print_arr(int arr[],int len)
{


}
```



函数与二维数组

```
#define N 4
#define M 3

void print_arr(int (*arr)[N],int m,int n)
{
	int i,j;
	for(i = 0;i < m; i++){
		for(j = 0; j< n; j++)
			printf("%4d ",arr[i][j]);
	}
}

int main(void)
{
	int arr[M][N] = {1,2,3,4,5,6,7,8,9,10,11,12};
	
	print_arr(arr,M,N);

}

```

```
int a[M][N] = {.....};
int *p = *a;
int (*q)[N] = a;

-> a[i][j] | *(a+i)+j  | a[i]+j | p[i] | *p
   q[i][j] |	*q	   |   q	| p+3  | q+2
			  *(q+0)
	
	int	   |  int *    | int*   | int  |   int
	int    | int *     | int(*)[N] |int *| int(*)[N]
```



函数与指针

​	指针函数

​		返回值 * 函数名 （形参）

​		如：int *fun(int);

​	函数指针

​			类型   (*指针名)   (形参)

​			如: int (*p)(int);

​	函数指针数组

​			类型   （*数组名 【下标】）（形参）

​			int （*arr[N]）(int)

​			

# 构造类型

结构体

1. 产生及意义



2. 类型描述

​		struct 结构体名

​		{

​				数据类型  成员1；

​				数据成员  成员2；

​		}

3. 嵌套定义



4. 定义变量（变量，数组，指针），初始化及成员英语

​	成员引用  ：变量名.成员名

​						  指针->成员名



5. 占用内存空间大小

```
__attribute__((packed))   //告诉编译器不对齐

struct simp_st
{
	int i;
	char ch;
	float f;
}__attribute__((packed))
```





共用体

1 产生及意义

​	同一时刻 只能存在一个地址

2 类型描述

​	union 共用体名

​	{

​			数据类型 成员名

​			数据类型 成员名

​			.........

​	}

3 嵌套定义



4 定义变量 （ 变量，数组，指针） 初始化及成员引用

​	成员引用：变量名.成员名

​						指针名->成员名

5 占用内存空间大小

 成员占空间最大的为 地址

6 参与函数传参（值  地址）

7 位域



枚举

