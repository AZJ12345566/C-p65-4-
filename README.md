# C-p65-4-
C语言学习笔记 p65 动态内存分配(4)
#include<stdio.h>
#include<stdlib.h>
char* GetMemory(void)
{
    char p[]="hello world";
    return p;//返回栈空间的地址的问题
}
void Test(void)
{
    char* str=NULL;
    str=GetMemory();//这里确确实实的把p的值给返回来了，但是p他是局部变量，出了函数范围指向哪里就不清楚了
    printf(str);
}
int main()
{
    Test();
    return 0;
}


void test()
{
    int a=10;//栈区,如果在int前面加一个static，那么a就在静态区了，那么生命周期变长了，就可以使用了
    return &a;
}
int main()
{
    int* p=test();
    *p=20;
    return 0;
}

int* test()
{
    int* ptr=malloc(100);//堆区可返回值
    return ptr;
}
int main()
{
    int*p=tets();
    return 0;
}

int* f2(void)
{
    int* ptr;
    *ptr=10;//注：这里ptr是没有赋值的随机值，是不可以解引用的，这里的问题是非法访问
    return ptr;
}

void GetMemory(char** p,int num)
{
    *p=(char*)malloc(num);
}

void Test(void)
{
    char* str=NULL;
    GetMemory(&str,100);
    strcpy(str,"hello";
    printf(str);)
    //改进
    free(str);
    str=NULL;
}
int main()
{
    Test();
    return 0;
}//输出hello，但存在内存泄漏


void Test(void)
{
    char* str=(char*)malloc(100);
    strcpy(str,"hello");
    free(str);//考察的是free后不会变成空指针
    //改
    str=NULL;
    
    if(str!=NULL)
    {
        strcpy(str,"world);
        printf(str);
    }
}
int main()
{
    Test();
    return 0;
}//输出为world，但在82行非法访问内存

//字符串为不可修改的变量，因此不再栈、堆、静态，而是在代码段中，代码段中只放可执行代码和只读常量
