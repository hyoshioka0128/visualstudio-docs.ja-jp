---
title: クラス デザイナーにおける Visual C++ の typedef | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.typedef
- vs.classdesigner.aliasofline
helpviewer_keywords:
- Class Designer [Visual Studio], typedefs
ms.assetid: c1984108-71fc-4d3a-b4d4-3eac2c6b4ebf
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 980c49aafba55e29714d786e492f7bb37a8ca621
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72646749"
---
# <a name="visual-c-typedefs-in-class-designer"></a>クラス デザイナーにおける Visual C++ の typedef
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

typedef ステートメントは、名前とその基になる型との間に間接参照のレイヤーを 1 つ以上作成します。 クラス デザイナーでは、キーワード `typedef` などで宣言される C++ の typedef 型をサポートしています。

```
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
} COORD;
```

 この型を使用して、インスタンスを宣言することができます。

 `COORD OriginPoint;`

 名前のない typedef を宣言することもできますが、クラス デザイナーでは指定したタグ名が使用されず、クラス ビューで生成される名前が使用されます。 たとえば、次の宣言は有効ですが、クラス ビューとクラス デザイナーでは **__unnamed** という名前のオブジェクトで表示されます。

```
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
};
```

 `typedef` 型の使用法の詳細については、「[(NOTINBUILD) typedef 指定子](https://msdn.microsoft.com/cc96cf26-ba93-4179-951e-695d1f5fdcf1)」を参照してください。

 C++ の typedef 図形には、typedef で指定された型の図形があります。 たとえば、ソースで `typedef class` が宣言されている場合、図形の角が丸くなり、**Class** のラベルが付きます。 `typedef struct` の場合、図形の角は四角で、**Struct** のラベルが付きます。

 クラスと構造体にはその内部で宣言された、入れ子にされた typedef を含めることができるため、クラスと構造体の図形では、入れ子にされた typedef 宣言を入れ子にされた図形として表示することができます。

 typedef の図形では、コンテキスト メニューとして **[関連として表示]** および **[コレクションの関連として表示]** のコマンドをサポートしています。

 次に、クラス デザイナーでサポートされる typedef 型の例を挙げます。

 `typedef type name`

 *name* : *type*

 Typedef

 可能であれば、型 *name* とつながる関連線を描画します。

 `typedef void (*func)(int)`

 `func: void (*)(int)`

 Typedef

 関数ポインターの typedef。 関連線は描画されません。

 ソースの型が関数ポインターの場合、クラス デザイナーに typedef は表示されません。

```
typedef int MyInt;
class A {
   MyInt I;
};
```

 `MyInt: int`

 Typedef

 `A`

 クラス

 ソースの型の図形からターゲットの型の図形にポイントする関連線を描画します。

 `Class B {};`

 `typedef B MyB;`

 `B`

 クラス

 `MyB : B`

 Typedef

 typedef の図形を右クリックして **[関連として表示]** をクリックすると、typedef またはクラスと、2 つの図形を結合する **[Alias of]** (エイリアス) の線 (関連線と似ています) が表示されます。

 `typedef B MyB;`

 `typedef MyB A;`

 `MyBar : Bar`

 Typedef

 上と同じ。

```
Class B {};
typedef B MyB;

class A {
   MyB B;
};
```

 `B`

 クラス

 `MyB : B`

 Typedef

 `A`

 クラス

 `MyB`は入れ子にされた typedef の図形です。

 `#include <vector>`

 `...`

 `using namespace std;`

 `...`

 `typedef vector<int> MyIntVect;`

 `vector<T>`クラス

 `MyIntVect : vector<int>`

 Typedef

 `class B {};`

 `typedef B MyB;`

 `class A : MyB {};`

 `MyB : B`

 Typedef

 -> B

 `B`

 `A`

 クラス

 -> MyB

 クラス デザイナーでは、コンテキスト メニュー コマンドを使用したこのような関係の表示はサポートしていません。

 `#include <vector>`

 `Typedef MyIntVect std::vector<int>;`

 `Class MyVect : MyIntVect {};`

 `std::vector<T>`

 クラス

 `MyIntVect : std::vector<int>`

 Typedef

 `MyVect`

 クラス

 -> MyIntVect

## <a name="see-also"></a>関連項目
 [ビジュアルC++コードの操作 (クラスデザイナー)](../ide/working-with-visual-cpp-code-class-designer.md) [(Notinbuild) typedef 指定子](https://msdn.microsoft.com/cc96cf26-ba93-4179-951e-695d1f5fdcf1)
