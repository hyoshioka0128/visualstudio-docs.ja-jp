---
title: VSCT XML スキーマの条件属性 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, conditional attributes
- conditional attributes (VSCT XML schema)
ms.assetid: 754d4f32-319b-44c9-915f-f7c60e53222e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f2b1fb3ee1b2cd396f25ec5591a585f8d87648d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697944"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML スキーマの条件属性
すべてのリストとアイテムに条件属性を適用できます。 論理演算子とシンボル展開式は、true または false に評価されます。 true の場合、関連付けられたリストまたはアイテムが結果の出力に含まれます。

 トークンの拡張は、他のトークン拡張または定数に対してテストできます。 関数`Defined()`は、特定の名前が値を持たない場合でも、定義されているかどうかをテストします。

 条件属性がリストに適用されると、その条件はリスト内のすべての子要素に適用されます。 子要素自体に Condition 属性が含まれている場合、その条件は AND 演算によって親式と結合されます。

 値 1、'1'、'true' は真として評価され、0、'0'、および'false' は偽として評価されます。

## <a name="operators"></a>オペレーター
 条件式を評価するには、次の演算子を使用します。

|演算子|定義|
|--------------|----------------|
|(,)|グループ化|
|!|論理 NOT|
|\<、>、=、>\<==、!=|関係と比較|
|and|Boolean|
|or|Boolean|

## <a name="examples"></a>使用例

```xml
<Menu Condition="Defined(DEBUG)" ...
</Menu>

<Menu Condition="%(SKU_MODE) = 'Demo'" ...
</Menu>

<Menus Condition="Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>

<Menus Condition="Defined(DEMO_SKU)">
    <Menus Condition="!Defined(DEBUG)">
        <Menu ...
        </Menu>
    </Menus>

    <Menu ...
    </Menu>
</Menus>

<Menus Condition="(Defined(DEMO_SKU) or Defined(SAMPLE_SKU))
and !Defined(DEBUG)">
    <Menu ...
    </Menu>
</Menus>
```

## <a name="see-also"></a>関連項目
- [コマンド テーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
