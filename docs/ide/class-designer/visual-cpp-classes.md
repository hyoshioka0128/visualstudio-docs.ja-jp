---
title: クラス デザイナーの C++ クラス
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.inheritancelinelabel
helpviewer_keywords:
- Class Designer [Visual Studio], classes
ms.assetid: 75e56f8c-11ef-42a3-b7ec-3d2cf25c581b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: d68391bbd4c6c873940bbc2714ee41db8309b629
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75590736"
---
# <a name="c-classes-in-class-designer"></a>クラス デザイナーの C++ クラス

**クラス デザイナー**は、C++ クラスをサポートし、Visual Basic および C# クラスの図形と同じ方法でネイティブの C++ クラスを視覚化します。ただし、C++ クラスは複数の継承関係を持つことができる点が異なります。 クラスの図形を展開して、表示されるクラスのフィールドとメソッドを増やしたり、図形を折りたたんでスペースを節約したりすることができます。

> [!NOTE]
> **クラス デザイナー**は、共用体 (共用体の最大データ メンバーに必要な量のメモリしか割り当てられない特殊なタイプのクラス) をサポートしていません。

## <a name="simple-inheritance"></a>単純な継承

クラス ダイアグラムに複数のクラスをドラッグした場合、これらのクラスにクラス継承関係があると、矢印によって各クラスが接続されます。 矢印は、基底クラスの方向を指し示します。 たとえば、クラス ダイアグラムに以下のクラスが表示される場合、矢印によって各クラスが接続され、B から A が指し示されます。

```cpp
class A {};
class B : A {};
```

また、クラス ダイアグラムに B クラスのみをドラッグしてから、B のクラス図形を右クリックして、 **[基底クラスの表示]** をクリックすることもできます。 このようにすると、基底クラスである A が表示されます。

## <a name="multiple-inheritance"></a>多重継承

**クラス デザイナー**は、複数クラスの継承関係の視覚化をサポートしています。 *多重継承*は、派生クラスが複数の基底クラスの属性を持つときに使用されます。 多重継承の例を次に示します。

```cpp
class Bird {};
class Swimmer {};
class Penguin : public Bird, public Swimmer {};
```

クラス ダイアグラムに複数のクラスをドラッグするときに、これらのクラスに複数クラスの継承関係があると、矢印によって各クラスが接続されます。 矢印は、基底クラスの方向を指し示します。

クラスの図形を右クリックして **[基底クラスの表示]** をクリックすると、選択したクラスの基底クラスが表示されます。

> [!NOTE]
> **[派生クラスの表示]** コマンドは、C++ コードについてはサポートされていません。 派生クラスは、 **[クラス ビュー]** に移動し、型ノード、 **[派生型]** サブフォルダーの順に展開して、これらの型をクラス ダイアグラムにドラッグすることで表示できます。

複数クラスの継承の詳細については、「[Multiple Inheritance](https://msdn.microsoft.com/library/6td5yws2.aspx)」 (多重継承) と「[Multiple Base Classes](/cpp/cpp/multiple-base-classes)」 (複数の基底クラス) を参照してください。

## <a name="abstract-classes"></a>抽象クラス

**クラス デザイナー**は、抽象クラス ("抽象基底クラス" ともいう) をサポートしています。 これらは、インスタンス化されることはありませんが、他のクラスを派生させることができるクラスです。 このドキュメントで既に説明した "多重継承" の例を使用すると、次のように、`Bird` クラスを個々のオブジェクトとしてインスタンス化できます。

```cpp
int main()
{
   Bird sparrow;
   Bird crow;
   Bird eagle;
}
```

ただし、`Swimmer` クラスを個々のオブジェクトとしてインスタンス化するわけではありません。 そのクラスから、`Penguin`、`Whale`、`Fish` などのその他の種類の動物クラスを派生させるだけです。 この場合、`Swimmer` クラスを抽象基底クラスとして宣言することになります。

クラスを抽象として宣言するには、`abstract` キーワードを使用することができます。 抽象としてマークされているメンバー、または抽象クラスに含まれているメンバーは、仮想であり、抽象クラスから派生したクラスを使用して実装する必要があります。

```cpp
class Swimmer abstract
{
   virtual void swim();
   void dive();
};
```

1 つ以上の純粋仮想関数を含めることで、クラスを抽象として宣言することもできます。

```cpp
class Swimmer
{
   virtual void swim() = 0;
   void dive();
};
```

これらの宣言をクラス ダイアグラムで表示すると、クラス名の `Swimmer` とその純粋仮想関数である `swim` は、抽象クラスの図形で、 **[抽象クラス]** の表記とともに斜体で表示されます。 抽象クラス型の図形は、枠線が点線である点を除いて、通常のクラスと同じです。

抽象基底クラスからの派生クラスは、基底クラスの各純粋仮想関数をオーバーライドする必要があります。オーバーライドしない場合、派生クラスをインスタンス化できません。 そのため、たとえば、`Fish` クラスを `Swimmer` クラスから派生させた場合、`Fish` は `swim` メソッドをオーバーライドする必要があります。

```cpp
class Fish : public Swimmer
{
   void swim(int speed);
};

int main()
{
   Fish guppy;
}
```

このコードをクラス ダイアグラムで表示すると、**クラス デザイナー**は `Fish` から `Swimmer` へ継承線を描画します。

## <a name="anonymous-classes"></a>匿名クラス

**クラス デザイナー**は、匿名クラスをサポートしています。 *匿名クラス型*は、識別子なしで宣言されるクラスです。 これはコンストラクターもデストラクターも持てず、引数として関数に渡すこともできず、関数からの戻り値として戻すこともできません。 匿名クラスを使用して、次の例のように、クラス名を typedef 名に置き換えることができます。

```cpp
typedef struct
{
    unsigned x;
    unsigned y;
} POINT;
```

構造体も匿名にできます。 **クラス デザイナー**は、匿名クラスと匿名構造体を、それぞれの型を表示するのと同じ方法で表示します。 匿名クラスと匿名構造体はユーザーが宣言および表示できますが、**クラス デザイナー**はユーザーが指定したタグ名を使用しません。 クラス ビューが生成する名前を使用します。 クラス ビューおよび**クラス デザイナー**では、クラスまたは構造体は **__unnamed** という要素として表示されます。

匿名クラスの詳細については、「[匿名クラス型](/cpp/cpp/anonymous-class-types)」を参照してください。

## <a name="template-classes"></a>テンプレート クラス

**クラス デザイナー**は、テンプレート クラスの視覚化をサポートしています。 入れ子になった宣言がサポートされています。 次の表は、一般的な宣言を示しています。

| コード要素 | クラス デザイナー ビュー |
| - | - |
| `template <class T>`<br /><br /> `class A {};` | `A<T>`<br /><br /> テンプレート クラス |
| `template <class T, class U>`<br /><br /> `class A {};` | `A<T, U>`<br /><br /> テンプレート クラス |
| `template <class T, int i>`<br /><br /> `class A {};` | `A<T, i>`<br /><br /> テンプレート クラス |
| `template <class T, template <class K> class U>`<br /><br /> `class A {};` | `A<T, U>`<br /><br /> テンプレート クラス |

次の表は、部分的特殊化の例です。

|コード要素|クラス デザイナー ビュー|
|------------------| - |
|`template<class T, class U>`<br /><br /> `class A {};`|`A<T, U>`<br /><br /> テンプレート クラス|
|`template<class T>`<br /><br /> `class A<T, T> {};`|`A<T, T>`<br /><br /> テンプレート クラス|
|`template <class T>`<br /><br /> `class A<T, int> {};`|`A<T, int>`<br /><br /> テンプレート クラス|
|`template <class T1, class T2>`<br /><br /> `class A<T1*, T2*> {};`|`A<T1*, T2*>`<br /><br /> テンプレート クラス|

次の表は、部分的特殊化における継承の例です。

|コード要素|クラス デザイナー ビュー|
|------------------| - |
|`template <class T, class U>`<br /><br /> `class A {};`<br /><br /> `template <class TC>`<br /><br /> `class A<T, int> {};`<br /><br /> `class B : A<int, float>`<br /><br /> `{};`<br /><br /> `class C : A<int, int>`<br /><br /> `{};`|`A<T, U>`<br /><br /> テンプレート クラス<br /><br /> `B`<br /><br /> クラス<br /><br /> (クラス A を指します)<br /><br /> `C`<br /><br /> クラス<br /><br /> (クラス A を指します)|

次の表は、部分的特殊化テンプレート関数の例です。

|コード要素|クラス デザイナー ビュー|
|------------------| - |
|`class A`<br /><br /> `{`<br /><br /> `template <class T, class U>`<br /><br /> `void func(T a, U b);`<br /><br /> `template <class T>`<br /><br /> `void func(T a, int b);`<br /><br /> `};`|`A`<br /><br /> func\<T, U> (+ 1 オーバーロード)|
|`template <class T1>`<br /><br /> `class A {`<br /><br /> `template <class T2>`<br /><br /> `class B {};`<br /><br /> `};`<br /><br /> `template<> template<>`<br /><br /> `class A<type>::B<type> {};`|`A<T1>`<br /><br /> テンプレート クラス<br /><br /> `B<T2>`<br /><br /> テンプレート クラス<br /><br /> (B は、 **[入れ子にされた型]** の下のクラス A の中に含まれます)|
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `class A : C<int> {};`|`A`<br /><br /> クラス<br /><br /> -> C\<int><br /><br /> `C<T>`<br /><br /> テンプレート クラス|

次の表は、テンプレート継承の例です。

|コード要素|クラス デザイナー ビュー|
|------------------| - |
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {`<br /><br /> `class B {};`<br /><br /> `}`<br /><br /> `class A : C<int>::B {};`|`A`<br /><br /> クラス<br /><br /> ->B<br /><br /> `C<int>`<br /><br /> クラス<br /><br /> (B は、 **[入れ子にされた型]** の下のクラス C の中に含まれます)<br /><br /> `C<T>`<br /><br /> テンプレート クラス|

次の表は、標準特殊クラス接続の例です。

|コード要素|クラス デザイナー ビュー|
|------------------| - |
|`template <class T>`<br /><br /> `class C {};`<br /><br /> `template<>`<br /><br /> `class C<int> {};`<br /><br /> `class A : C<int> {};`<br /><br /> `class D : C<float> {};`|`A`<br /><br /> クラス<br /><br /> ->C\<int><br /><br /> `C<int>`<br /><br /> クラス<br /><br /> `C<T>`<br /><br /> テンプレート クラス<br /><br /> `D`<br /><br /> クラス<br /><br /> ->C\<float>|
|`class B {`<br /><br /> `template <class T>`<br /><br /> `T min (const T &a, const T &b);`<br /><br /> `};`|`B`<br /><br /> min \<T>|

## <a name="see-also"></a>参照

- [C++ のコードを操作する](working-with-visual-cpp-code.md)
- [クラスと構造体](/cpp/cpp/classes-and-structs-cpp)
- [匿名クラス型](/cpp/cpp/anonymous-class-types)
- [多重継承](https://msdn.microsoft.com/library/6td5yws2.aspx)
- [複数の基本クラス](/cpp/cpp/multiple-base-classes)
- [テンプレート](/cpp/cpp/templates-cpp)
