---
title: クラス デザイナーにおける C++ の typedef
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.typedef
- vs.classdesigner.aliasofline
helpviewer_keywords:
- Class Designer [Visual Studio], typedefs
ms.assetid: c1984108-71fc-4d3a-b4d4-3eac2c6b4ebf
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 4c57382809b7730df2d7c674c24902d70ccab647
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590697"
---
# <a name="c-typedefs-in-class-designer"></a>クラス デザイナーにおける C++ の typedef

[typedef](/cpp/cpp/aliases-and-typedefs-cpp#typedefs) ステートメントは、名前とその基になる型との間に間接参照のレイヤーを 1 つ以上作成します。 **クラス デザイナー**では、キーワード `typedef` などで宣言される C++ の typedef 型をサポートしています。

```cpp
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
} COORD;
```

この型を使用して、インスタンスを宣言することができます。

`COORD OriginPoint;`

## <a name="class-and-struct-shapes"></a>クラスと構造体の図形

**クラス デザイナー**では、C++ の typedef には、typedef で指定された型の図形があります。 ソースで `typedef class` が宣言されている場合、図形の角が丸くなり、**Class** のラベルが付きます。 `typedef struct` の場合、図形の角は四角で、**Struct** のラベルが付きます。

クラスと構造体は、その中で宣言されている入れ子になった typedef を持つことができます。 **クラス デザイナー**では、クラスと構造体の図形は、入れ子になった typedef 宣言を入れ子にされた図形として表示できます。

typedef の図形では、右クリック メニュー (コンテキスト メニュー) として **[関連として表示]** および **[コレクションの関連として表示]** のコマンドをサポートしています。

### <a name="class-typedef-example"></a>クラスの typedef の例

```cpp
class B {};
typedef B MyB;
```

![クラス デザイナーでの C++ クラスの typedef](media/cpp-class-typedef.png)

### <a name="struct-typedef-example"></a>構造体の typedef の例

```cpp
typedef struct mystructtag
{
    int   i;
    double f;
} mystruct;
```

![クラス デザイナーでの C++ 構造体の typedef](media/cpp-struct-typedef.png)

## <a name="unnamed-typedefs"></a>名前のない typedef

名前のない typedef を宣言することもできますが、**クラス デザイナー**では、指定したタグ名が使用されません。 **クラス デザイナー**では**クラス ビュー**が生成する名前が使用されます。 たとえば、次の宣言は有効ですが、**クラス ビュー**と**クラス デザイナー**では **__unnamed** という名前のオブジェクトで表示されます。

```cpp
typedef class coord
{
   void P(x,y);
   unsigned x;
   unsigned y;
};
```

> [!NOTE]
> **クラス デザイナー**では、ソースの型が関数ポインターの typedef は表示されません。

## <a name="see-also"></a>関連項目

- [C++ のコードを操作する](working-with-visual-cpp-code.md)
- [Typedefs](/cpp/cpp/aliases-and-typedefs-cpp#typedefs)
