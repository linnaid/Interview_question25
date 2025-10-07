
#### 4. 不合群的数字

>在一个数组中，所有数字都出现了偶数次，只有两个数字出现了奇数次，请聪
明的你帮我看看以下的代码是如何找到这两个数字的呢？

```c
#include <stdio.h>

void findUndercoverIDs(int nums[], int size) {
    int xorAll = 0,id_a = 0,id_b = 0;
    for (int i = 0; i < size; i++) {
        xorAll ^= nums[i];
    }
    int diffBit = xorAll & -xorAll;
    for (int i = 0; i < size; i++) {
        (nums[i] & diffBit ? id_a : id_b) ^= nums[i];
    }
    printf("These nums are %d %d",id_a,id_b);
}
``` 
------

| **出题人** | **林芯宇**   |
| ---------- | ------------ |
| 知识点1    | 位运算 |
| 知识点2    | 分组异或   |
| 知识点3    | 时间与空间复杂度分析     |
| 知识点4    | 补码与位掩码   |

------

#### 问题
Q1. 简述函数 findUndercoverIDs 的功能，输入输出是什么？	10%   
Q2.	解释为什么 xorAll ^= nums[i] 可以抵消偶数次出现的元素，保留奇数次元素	30%  
Q3.	解释 diffBit = xorAll & -xorAll 的作用，以及为什么可以提取最低不同位 20%  
Q4.	说明为什么根据 diffBit 将数组分成两组，再分别异或可以得到两个奇数次元素	30%  
Q5.	分析函数的时间复杂度和空间复杂度  10%

------

#### 答案
```
A1. 在数组中找出两个出现奇数次的 ID  
A2. x ^ x = 0，x ^ 0 = x, 遍历数组并异或，偶数次出现的 ID 会被抵消为 0，剩下的就是奇数次的元素  
A3. diffBit = xorAll & -xorAll 提取 最低位的 1，保证 x 和 y 在这一位不同, 利用补码性质：-n = ~n + 1 获取  
A4. 根据 diffBit 将数组分成两组：该位为 1 的一组, 该位为 0 的另一组, 每组再异或，偶数次元素抵消，剩下的就是每组的奇数次元素  
A5. 时间复杂度：O(n)，数组遍历两次; 空间复杂度：O(1)，只用常数个整型变量
```