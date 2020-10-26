---
title: Visual C++ コード スニペット | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 74e26fd4-e5ca-4611-a816-0a521b4947a0
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 213f4299ac71c08118563a008abe065f2c02423e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72655393"
---
# <a name="visual-c-code-snippets"></a>Visual C++ コード スニペット
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio でコード スニペットを使用して、よく使用されるコードを C++ コード ファイルに追加することができます。 通常、C# の場合とほぼ同じ方法でコード スニペットを使用できますが、既定のコード スニペットのセットは異なります。

 コード スニペットをコードの特定の場所に追加することと (挿入)、選択したコードをコード スニペットで囲むことのいずれかが可能です。

## <a name="inserting-a-code-snippet"></a>コード スニペットの挿入
 コード スニペットを挿入するには、C++ コード ファイル (.cpp または .h) を開き、ファイル内の任意の場所をクリックして、次のいずれかを実行します。

- 右クリックしてコンテキスト メニューを表示し、 **[スニペットの挿入]** を選択する

- **[編集 / IntelliSense]** メニューの **[スニペットの挿入]** を選択する

- ホット キー **Ctrl + K + X** を使用する

  **#if** で始まる選択肢の一覧が表示されます。 **#if** を選択すると、ファイルに追加された次のコードが表示されます。

```cpp
#if 0

#endif // 0
```

 次に、0 を正しい条件に置き換えることができます。

## <a name="using-a-code-snippet-to-surround-selected-code"></a>コード スニペットを使用して、選択したコードを囲む
 コード スニペットを使用して、選択したコードを囲むには、行 (または複数の行) を選択し、次のいずれかを実行します。

1. 右クリックしてコンテキスト メニューを表示し、**[ブロックの挿入]** を選択する

2. **[編集 / IntelliSense]** メニューの **[ブロックの挿入]** を選択する

3. ホット キー **Ctrl + K + S** を使用する

   **#if** を選択します。 次のような結果が表示されます。

```cpp
#if 0
#include "pch.h"  // or whatever line you had selected
#endif // 0
```

 次に、0 を正しい条件に置き換えることができます。

## <a name="where-can-i-find-a-complete-list-of-the-c-code-snippets"></a>C++ コード スニペットの全一覧の確認場所
 **コード スニペット マネージャー** ( **[ツール]** メニュー) に移動し、 **[言語]** を **[Visual C++]** に設定すると、C++ コード スニペットの全一覧が表示されます。 下のウィンドウで、 **[Visual C++]** を展開します。 すべての C++ コード スニペットの名前がアルファベット順で表示されます。

 ほとんどのコード スニペットの名前は自明ですが、一部の名前は分かりにくい場合があります。

## <a name="class-vs-classi"></a>class と classi
 **class** スニペットは MyClass というクラスの定義を提供します。これは適切な既定のコンストラクターとデストラクターを持ち、コンストラクターとデストラクターの定義はクラスの外部に配置されます。

```cpp
class MyClass
{
public:
MyClass();
~MyClass();

private:

};

MyClass::MyClass()
{
}

MyClass::~MyClass()
{
}
```

 classi コード スニペットも MyClass というクラスの定義を提供しますが、既定のコンストラクターとデストラクターはクラス定義内で定義されます。

```cpp
class MyClass
{
public:
MyClass()
{
}

~MyClass()
{
}

private:

};
```

## <a name="for-vs-foreach-vs-forr-vs-rfor"></a>for と foreach と forr と rfor
 さまざまな種類の for ループを提供する 4 つのスニペットがあります。

 **for** スニペットは、条件がオブジェクトの長さ (`size_t`) に基づく `for` ループを提供します。

```cpp
for (size_t i = 0; i < length; i++)
{

}
```

 **foreach** スニペットは、コレクションのメンバーを反復処理する `for each` ループを提供します。

```cpp
for each (object var in collection_to_loop)
{

}
```

 **forr** スニペットは、条件がオブジェクトの長さ (整数) に基づく逆 `for` ループを提供します。

```cpp
for (int i = length - 1; i >= 0; i--)
{

}
```

 **rfor** スニペットは、[範囲に基づく](https://msdn.microsoft.com/library/5750ba1d-ba48-4236-a923-e32de8345c2d) for ループ (リンク) を提供します。

```cpp
for (auto& i : v)
{

}
```

## <a name="the-destructor-snippet-"></a>デストラクターのスニペット (~)
 デストラクターのスニペット ( **~** ) は、コンテキストに応じてさまざまな動作を示します。 このスニペットをクラス内に挿入すると、そのクラスのデストラクターが提供されます。 たとえば、次のような XML があるとします。

```cpp
class SomeClass {

};
```

 デストラクターのスニペットを挿入すると、SomeClass のデストラクターが提供されます。

```cpp
class SomeClass {
    ~SomeClass()
    {

    }
};
```

 デストラクターのスニペットをクラスの外部に挿入しようとすると、プレースホルダーの名前を持つデストラクターが提供されます。

```cpp
~TypeNamePlaceholder()
{

```
