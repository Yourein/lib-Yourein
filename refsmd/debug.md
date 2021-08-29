# <Yourein/debug>

## debug_a
配列や集合などの値を表示する関数です。
ただし、出力は標準出力ではなく標準エラー出力に流されます。
また、すべての要素を出力後標準エラー出力をフラッシュします。
普通は以下のように書くところを省略するためだけの関数です。

```cpp
set<int> a;
for (auto x : a){
    cout << x << " "; 
}
cout << endl;
```

**Difinition**
```cpp
template <typename T> void debug_a(const T &a)
template <> void debug_a(const std::string &a)
template <typename T1, typename T2> void debug_a(const std::map<T1, T2> &a)
```

**使用例**
```cpp
set<int> a;

Yourein::debug::debug_a(a);
```

**出力結果**
```
要素1 要素2 要素3... 要素N
```

**注意点**
```cpp
vector
set
map
array
配列
string
```
への対応を確認しています。
それ以外の方を使う場合はイテレータさえあれば大丈夫だと思います。
よくわからなければ上に書かれた型だけを使っていればとくにバグることもなく安心ということです(エラーハンドリングを実装していないため絶対安心かは保証できませんが)。