---
title: ID シンボル要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d02a26a6874165738d917a14986d16d142c01915
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710372"
---
# <a name="idsymbol-element"></a>ID シンボル要素
要素`IDSymbol`には、メニュー、グループ、またはコマンドを表す GUID:ID ペアの ID が含まれています。 GUID は親`GuidSymbol`要素から取得されます。 要素`IDSymbol`には、属性`name`に含まれる ID のフレンドリ名を提供する属性があります`value`。

## <a name="syntax"></a>構文

```xml
<IDSymbol name=ElementName value="0x0010" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|必須。 ID シンボルの名前。|
|value|必須。 ID シンボルの数値 ID 値。|

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[要素](../extensibility/guidsymbol-element.md)|メニュー、グループ、またはコマンドを表す GUID:ID ペアの GUID が含まれています。 複数の `IDSymbol` 要素をグループ化します。|

## <a name="remarks"></a>Remarks
 特定`IDSymbol``GuidSymbol`の要素のすべての要素は、一意`value`の . ただし、`IDSymbol`同じ値を持つ要素は、親が異なっている限り、パッケージ内に存在することができます。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
