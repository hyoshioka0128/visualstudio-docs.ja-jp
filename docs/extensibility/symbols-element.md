---
title: シンボル要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Symbols element (VSCT XML schema)
- VSCT XML schema elements, Symbols
ms.assetid: 1cda43d8-42a5-4b1b-a3c8-cf0401c3202f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5c24c3f84df23a07b6b16272b66b29e32ad7b911
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699350"
---
# <a name="symbols-element"></a>Symbols 要素
他の VSCT 要素で使用される GUID と ID を定義します。 アンマネージ コードの場合、通常、この情報は[Extern Element](../extensibility/extern-element.md)で指定されたヘッダー ファイルから取得されます。 マネージ コードは、この情報を定義するのには、シンボル要素の子要素を使用します。

 既存の .cto ファイルから .vsct ファイルを作成すると、シンボルは Symbols 要素の子として生成されます。 詳細については、「方法[: を作成する」を参照してください。既存の Vsct ファイルから取得します。Cto ファイル](../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file).

 シンボル要素は、プリプロセッサで使用する名前と値のペアを定義する[Define 要素](../extensibility/define-element.md)と混同しないでください。

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
|Guidシンボル|GUID シンボルを定義します。 GuidSymbol には、名前と値の 2 つの必須属性があります。 名前はシンボルの名前で、値は文字列としての GUID の値です。<br /><br /> 例:\<GuidSymbol 名="guidVsPackage1Pkg" 値 ="{c5f54698-101a-4846-84d3-dc748f9cd848}"/>|
|Idsymbol|シンボルを定義します。 IDSymbol には、名前と値の 2 つの必須属性があります。 名前はシンボルの名前で、値はシンボルの値を文字列として表します。<br /><br /> たとえば、ID\<シンボル名="MyMenuGroup" 値="0x1020" />|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|vsct ファイルのルート要素。|

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
