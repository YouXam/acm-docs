# 代码片段

[TOC]


## FastIO

```c++
#define gc() (p1 == p2 ? (p2 = buf + fread(p1 = buf, 1, 1 << 20, stdin), p1 == p2 ? EOF : *p1++) : *p1++)
#define read() ({ int x = 0, f = 1; char c = gc(); while(c < '0' || c > '9') { if (c == '-') f = -1; c = gc();} while(c >= '0' && c <= '9') x = x * 10 + (c & 15), c = gc(); f * x; })
char buf[1 << 20], *p1, *p2;
```

### 高斯消元解异或方程组

```c++
std::bitset<1010> matrix[2010];  // matrix[1~n]：增广矩阵，0 位置为常数
// n 为未知数个数，m 为方程个数，返回方程组的解, 多解 / 无解返回一个空的 vector）
std::vector<bool> GaussElimination(int n, int m) {
  for (int i = 1; i <= n; i++) {
    int cur = i;
    while (cur <= m && !matrix[cur].test(i)) cur++;
    if (cur > m) return std::vector<bool>(0);
    if (cur != i) swap(matrix[cur], matrix[i]);
    for (int j = 1; j <= m; j++)
      if (i != j && matrix[j].test(i)) matrix[j] ^= matrix[i];
  }
  std::vector<bool> ans(n + 1, 0);
  for (int i = 1; i <= n; i++) ans[i] = matrix[i].test(0);
  return ans;
}
```
