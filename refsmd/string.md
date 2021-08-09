# <Yourein/string>

## pinput
Pythonの標準入力にならった関数です。
getlineなどで入力した文字列をpinputに、spliterを指定して投げることで、分割された文字列がvector\<string>型でreturnされます。
ただし、第一引数にistream型(```std::cin```等)を指定してはいけません。
<br>

```cpp
std::vector<std::string> pinput(std::string s, char spliter)
```
<br>
例えば、以下のように使うことができます。
<br>
<br>

```cpp
std::string sentence = "Hello, World!";
auto v = Yourein::strs::pinput(sentence, ',');

for (auto x : v){
    std::cout << x << endl;
}
```
このコードの出力結果は以下のようになります。

```
Hello
World!
```
この関数では先頭の空文字列(文字列の先頭に位置する空白文字のみの部分文字列)は削除されます。
そのため、上の出力結果では ```World!``` の前に本来存在する空白文字が削除されています。

## strcount
Pythonの文字列型のメンバ関数 ```.count(str)``` にならった関数です。

文字列sの中に文字列counterが何度登場するかをカウントします。

```cpp
int strcount(std::string s, std::string counter)
```

```cpp
std::string s = "Hello, There, Hello, Hello";
std::cout << Youdain::strs::strcount(s, "Hello") << std::endl;
```
出力結果は以下の通りです。

```
3
```

両引数がstd::string型であるので、引数に変数を渡さない限りダブルクオーテーションを忘れないでください。

また、この関数は計算量 $O(N)$ となるので、$|S| \le 5 \times 10^7$ 以下であることを想定しています。
加えて、std::wstring型には対応していません。(今後もしかしたらTemplateで作るかもしれません。)

## sfind
```
string::find
```
の劣化関数です。
前者が文字列の発見位置をreturnするのに対し、この関数はそもそも存在するか否かを判定する関数です。<br>

```cpp
bool sfind(std::string s, std::string finder)
```
このように定義され、

```cpp
std::string s1 = "I don't want to be just another";
std::cout << Yourein::strs::sfind(s1, "want") << std::endl;
std::cout << Yourein::strs::sfind(s1, "wanna") << std::endl;
```
以下のように動作します。

```
1
0
```

文字列sの中で文字列finderを発見したときは```true```を
見つからなかったときは```false```を返します。

また、この関数の計算量は最低$O(N)$、最悪$O(2N)$になります。
両者ともに線形時間ですが、```strcount```関数同様、$|S| \le 5 \times 10^7$ の制約下での使用を想定しています。

## strformat
```std::string```に対しての左揃え、右揃え、文字埋めなどのフォーマット要素を提供します。

**Definition**
```cpp
std::string strformat(std::string base, char filler, int length, bool Lspace = false)
```

baseに対して、フォーマット対象の文字列を。
fillerに対して、埋めるための文字を。例えばここに空白文字を入れると空白埋めをします。
lengthに対して、フォーマット後の文字列の長さを与えます。後述しますが文字列の長さによって関数の動作が変わります。
Lspaceに対して、true or falseの2値を与えます。文字列を左に寄せるか右に寄せてフォーマットするかを選択します。

**使用例**
```cpp
std::string s = "abcdefg";
std::string ss = "1234567890";

std::cout << Yourein::strs::strformat(s, ' ', 10) << std::endl;  //[abcdefg   ]
std::cout << Yourein::strs::strformat(s, ' ', 10, true) << std::endl; //[   abcdefg]

std::cout << Yourein::strs::strformat(s, ' ', 5) << std::endl; //[12345]
std::cout << Yourein::strs::strformat(s, ' ', 5, true) << std::endl; //[67890]
```
base.size() < lengthである場合はLspaceがtrueであるかfalseであるかによって右/左寄せでfillerを文字列に追加します。
一方base.size() > lengthである場合は文字列の左端もしくは右端をカットして返します。