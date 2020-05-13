---
title: Guid シンボル要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, GuidSymbol
- GuidSymbol element (VSCT XML schema)
ms.assetid: 11fb3545-8974-4776-9a54-6b6e7739ae31
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59068a9ac9f952b5370681b3684ce4234354afc9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711126"
---
# <a name="guidsymbol-element"></a>要素
要素`GuidSymbol`には、メニュー、グループ、またはコマンドを表す GUID:ID ペアの GUID が含まれています。 ID は要素の`IDSymbol`要素から取得`GuidSymbol`されます。 要素`GuidSymbol`には、属性`name`に含まれる GUID のフレンドリ名を提供する属性があります`value`。

## <a name="syntax"></a>構文

```xml
<GuidSymbol name="guidMyCommandSet" value="{xxxxxxxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx}">
  <IDSymbol>... </IDSymbol>
  <IDSymbol>... </IDSymbol>
</GuidSymbol>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|必須。 GUID シンボルの名前。|
|value|必須。 GUID シンボルの GUID。|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[ID シンボル要素](../extensibility/idsymbol-element.md)|メニュー、グループ、またはコマンドを表す GUID:ID ペアの ID が含まれています。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[シンボル要素](../extensibility/symbols-element.md)|`GuidSymbol` *vsct*ファイル内の要素をグループ化します。|

## <a name="remarks"></a>Remarks
 通常 *、.vsct*ファイルには、`GuidSymbol`その`Symbols`セクションに 3 つの要素が含まれています。 特定`IDSymbol``GuidSymbol`の要素のすべての要素は、一意`value`の .ただし、`IDSymbol`同じ値を持つ要素は、親が異なっている限り、パッケージ内に存在することができます。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
