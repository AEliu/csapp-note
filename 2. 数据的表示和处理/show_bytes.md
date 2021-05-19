```c
#include <stdio.h>

typedef unsigned char *byte_pointer;

void show_bytes(byte_pointer start, size_t len)
{
    // size_t i;
    for (size_t i = 0; i < len; i++)
    {
        printf("%.2x ", start[i]);
    }
    printf("\n");
}

void show_int(int x)
{
    show_bytes((byte_pointer)&x, sizeof(int));
}

void show_float(float x)
{
    show_bytes((byte_pointer)&x, sizeof(float));
}

void show_pointer(void *x)
{
    show_bytes((byte_pointer)&x, sizeof(float));
}

void test_show_bytes(int val)
{
    int ival = val;
    float fval = (float)ival;
    int *pval = &ival;
    show_int(ival);
    show_float(fval);
    show_pointer(pval);
}

int main(int argc, char const *argv[])
{
    int val = 12345;
    test_show_bytes(12345);
    // 0x3039
    // output:
    //  39 30 00 00 小端法
    //  00 e4 40 46
    //  58 12 4c e6

    printf("======练习题 2.5=====\n");
    val = 0x87654321;
    byte_pointer valp = (byte_pointer)&val;
    show_bytes(valp, 1);
    show_bytes(valp, 2);
    show_bytes(valp, 3);

    printf("======练习题 2.6=====\n");
    val = 3510593;
    show_int(val);
    show_float((float)val);

    printf("======练习题 2.7=====\n");
    const char *s = "abcdef";
    show_bytes((byte_pointer)s, strlen(s) );
    // output, 字符串最后一位 00 
    // 与大小端无关
    // 61 62 63 64 65 66 

    return 0;
}
```