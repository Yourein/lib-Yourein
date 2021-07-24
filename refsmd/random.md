# <Yourein/random>

乱数に関わるライブラリです。

## xsrand
XOR SHIFTによって生成されるunsigned long long型の乱数を$O(1)$で返します。
シードとなるunsinged long long型の非負整数が必要です。

**Difinition**
```cpp
unsigned long long xsrand(unsigned long long x)
```

**使用例**
```cpp
unsigned long long a = Yourein::random::xsrand(chrono::steady_clock::now().time_since_epoch().count());
cout << a << endl;
```

## xsrand (overload)
ranged xsrandです。
以下のdifinitionに従い定義されていて、[L, R]の区間の乱数を返します。

xsrandのオーバーロードになっているので関数名など気にせず、範囲を指定すればOKです。

```cpp
unsigned long long xsrand(unsigned long long x, unsigned long long L, unsigned long long R)
```

```使用例
unsigned long long a = Yourein::random::xsrand(chrono::steady_clock::now().time_since_epoch().count(), 10, 15);
cout << a << endl;
```