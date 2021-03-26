---
title: Symbols 要素 |Microsoft Docs
description: Symbols 要素は、他の VSCT 要素によって使用される Guid と Id を定義します。 この記事には例が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9a013bbe438d1e4dd1f6b5149dcb7da78835fd09
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056052"
---
# <a name="symbols-element"></a>Symbols 要素
他の VSCT 要素によって使用される Guid と Id を定義します。 アンマネージコードの場合、この情報は通常、 [Extern 要素](../extensibility/extern-element.md)によって指定されたヘッダーファイルから取得されます。 マネージコードでは、Symbols 要素の子要素を使用して、この情報を定義します。

 既存の cto ファイルからの vsct ファイルを作成した場合、シンボルは Symbols 要素の子として生成されます。 詳細については、「 [方法: を作成する」を参照してください。既存のからの vsct ファイル。Cto ファイル](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

 Symbols 要素は、プリプロセッサによって使用される名前と値のペアを定義する [Define 要素](../extensibility/define-element.md)と混同しないようにしてください。

## <a name="syntax"></a>構文

```
<Symbols>
  <GuidSymbol>... </GuidSymbol>
  <GuidSymbol>... </GuidSymbol>
</Symbols>
```

## <a name="attributes-and-elements"></a>属性および要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|なし||

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|いる guidsymbol|GUID シンボルを定義します。 GuidSymbol には、名前と値の2つの必須の属性があります。 名前は記号の名前で、値は文字列としての GUID の値です。<br /><br /> 例:\<GuidSymbol name="guidVsPackage1Pkg"   value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />|
|IDSymbol|シンボルを定義します。 IDSymbol には、name と value という2つの必須の属性があります。 名前は記号の名前で、値は文字列として記号の値になります。<br /><br /> 例:\<IDSymbol name="MyMenuGroup" value="0x1020" />|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|Vsct ファイルのルート要素。|

## <a name="example"></a>例

```
<Symbols>
  <GuidSymbol name="guidVsPackage1Pkg" value="{c5f54698-101a-4846-84d3-dc748f9cd848}" />
  <GuidSymbol name="guidVsPackage1CmdSet" value="{cb9dfd7f-2fcc-4a3e-aae8-f7fe30b1cfac}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
    <IDSymbol name="cmdidMyTool" value="0x0101" />
  </GuidSymbol>
</Symbols>
```

## <a name="see-also"></a>関連項目
- [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
