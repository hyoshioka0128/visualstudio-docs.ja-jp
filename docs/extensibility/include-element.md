---
title: Include Element |Microsoft Docs
description: Include 要素は、現在のファイルに挿入するために指定されたインクルードパスにあるファイルを指定します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 71da1241863e41529af33bdd5e45dcf0a8bfbdb1
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996345"
---
# <a name="include-element"></a>Include 要素
Include 要素は、現在のファイルに挿入するために指定されたインクルードパスにあるファイルを指定します。  定義されているすべてのシンボルと型は、コンパイルされた結果の一部になります。

## <a name="syntax"></a>構文

```csharp
<Include href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|href|必須。 ヘッダーファイルのパス:<br /><br /> href = "stdidcmd"|
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|[なし] :|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンド (メニュー項目、メニュー、ツールバー、およびコンボボックス) を表すすべての要素を定義します。|

## <a name="example"></a>例

```
<Include href="PackagePlacements.vsct"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
