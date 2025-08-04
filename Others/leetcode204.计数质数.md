# 204、计数质数
难度：mid

题目网址：https://leetcode.cn/problems/count-primes/

代码语言：cpp
## 题解
### 方法一、线性筛
思路来源：[acwing868.筛质数，视频讲解](https://www.acwing.com/problem/content/870/)

线性筛的核心思路是对于一个合数，使用它的**最小质因数**将其筛掉，从而保证每个合数只会被筛掉一次，从而使算法复杂度维持在O（N）

下面先放代码再证明方法的可行性

C++

```cpp
class Solution {
private: 
    bool st[5000010];
    int primes[5000010];
    int cnt = 0;
public:
    int countPrimes(int n) {
        memset(st, false, sizeof st);
        for (int i = 2; i < n; i ++ ) {
            if (!st[i]) 
            {
                st[i] = true;
                primes[cnt ++ ] = i;
            }
            for (int j = 0; primes[j] <= n / i; j ++ ) {
                st[i * primes[j]] = true;
                if (i % primes[j] == 0) break;
            }
        }
        return cnt;
    }
};
```

**证明合数一定是被最小质因子筛掉的：** 

* 如果`i % primes[j] == 0` ，那么primes[j]一定是i的最小质因子，primes[j]一定是primes[j]*i的最小质因子
* 如果`i % primes[j] != 0` ，那么primes[j]一定小于i的所有质因子，primes[j]也一定是primes[j]*i的最小质因子

**证明所有合数会被筛掉：**

对于一个合数x，假设primes[j]是x的最小质因子，当i枚举到`x / primes[j]`的时候就会把x筛掉（由于$`primes[j]^2 <= x`$，因此当i枚举到x / primes[j]时，primes[j]一定是存在的）
