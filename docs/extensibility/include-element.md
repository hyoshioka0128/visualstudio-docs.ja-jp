---
title: 要素を含める |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Include
helpviewer_keywords:
- Include element (VSCT XML schema)
- VSCT XML schema elements, Include
ms.assetid: c923dfe6-084a-4105-aec1-f0a3f8399c54
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7ea89185d28be2816a690d867dbb3eccbb739e04
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710359"
---
# <a name="include-element"></a>要素を含める
Include 要素は、現在のファイルに挿入するために指定されたインクルード パス上に配置できるファイルを指定します。  定義されたすべてのシンボルと型は、コンパイルされた結果の一部になります。

## <a name="syntax"></a>構文

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|href|必須。 ヘッダー ファイルへのパス:<br /><br /> href="stdidcmd.h"|
|条件|省略可能。 [「条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|[なし] :|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|コマンドを表す要素 、つまり、メニュー項目、メニュー、ツールバー、およびコンボ ボックスを表す、VSPackage が IDE に提供するすべての要素を定義します。|

## <a name="example"></a>例

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
