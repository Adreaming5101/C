#### 1.Clion IDE中文输出控制台乱码问题

```markdown
解决：https://blog.csdn.net/YSA_SFPSDPGY/article/details/132371890
```

#### 2.scanf格式化问题

```c++
#include <stdio.h>
int main() {
    int a;
    scanf("请输入一个整数:%d",&a);
    printf("-----------%d",a);
}
/*
运行程序，尝试输入整数10，但是打印出来的结果为--------0，即，
10
-----------0
原因：
scanf函数格式化字符串包含了额外的文本，这使得 scanf 函数尝试匹配整个字符串而不仅仅是数字。它试图寻找 :、%d、以及 \n 这些字符，但实际输入的数字10并不匹配该格式，所有无法存入内存空间a。
*/
修改后：
    #include <stdio.h>
    int main() {
        int a;
        printf("请输入一个整数: ");
    	fflush(stdout);      // 立即输出
        scanf("%d", &a);
        printf("-----------%d", a);
        return 0;
    }

```

#### 3.多个scanf函数用户输入问题，会键入换行符

```c++
#include <stdio.h>
int main() {
    int n = 0;
    int n1 = 0;
    char operator = '0';
    printf("请输入两个整数：");
    fflush(stdout);
    scanf("%d",&n);
    scanf("%d",&n1);    // 最后的回车会键入输入缓冲区
    printf("请输入一个运算符：");
    fflush(stdout);
    /*
     * 当不写\n时：
     * 当用户输入两个整数后按下Enter键，这个Enter键的换行符会留在输入缓冲区中。如果直接使用scanf("%c", &operator);接收运算符，它可能会读取到换行符，导致运算符接收不到用户的实际输入。
     * 写\n时(也可用空格(空字符)或\t替换)：
     * scanf会在读取字符之前先跳过输入缓冲区中的换行符，确保获取到用户输入的实际字符。------输入缓冲区先换行读取新的输入
     *
     * 这是一种常见的做法，以确保在读取字符之前清空输入缓冲区，防止换行符对后续输入的影响。在其他情况下，也可以使用getchar()来吸收多余的换行符。
     * */
    scanf("\n%c",&operator);
    int result = 0;
    switch (operator) {
        case '+':          // 只能用单引号''表示单个字符，在这里用双引号""会报错,双引号表示字符串
            result = n + n1;
            break;
        case '-':
            result = n - n1;
            break;
        case '*':
            result = n * n1;
            break;
        case '/':
            if (n1 == 0) {
                printf("除数不能为0");
                return 1;      //程序正常退出
            } else {
                result = n / n1;
            }
            break;
        default:
            printf("输入的字符错误，请重新输入");
            return 1;      // 程序正常退出
    }
    printf("计算结果为:%d\n",result);
    return 0;   // 程序结束

}





```



























































