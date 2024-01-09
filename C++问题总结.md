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



























































