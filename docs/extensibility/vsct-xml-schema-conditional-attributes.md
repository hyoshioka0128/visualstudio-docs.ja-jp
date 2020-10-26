---
title: VSCT XML スキーマの条件付き属性 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80697944"
---
# <a name="vsct-xml-schema-conditional-attributes"></a>VSCT XML スキーマの条件付き属性
条件付き属性は、すべてのリストおよび項目に適用できます。 論理演算子と記号の展開式は、true または false に評価されます。 True の場合、関連付けられているリストまたは項目が結果の出力に含まれます。

 トークンの展開は、他のトークンの展開または定数に対してテストできます。 関数は、 `Defined()` 値がない場合でも、特定の名前が定義されているかどうかをテストします。

 条件属性がリストに適用されると、条件はリスト内のすべての子要素に適用されます。 子要素自体に Condition 属性が含まれている場合、その条件は AND 演算によって親式と結合されます。

 値1、' 1 '、' true ' は true と評価され、0、' 0 '、および ' false ' が false と評価されます。

## <a name="operators"></a>オペレーター
 条件式を評価するには、次の演算子を使用します。

|演算子|定義|
|--------------|----------------|
|(,)|グループ化|
|!|論理 NOT|
|\<, >, \<=, >=, ==, !=|関係と比較|
|および|Boolean|
|または|Boolean|

## <a name="examples"></a>例

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
- [Visual Studio コマンドテーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
