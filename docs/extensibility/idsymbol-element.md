---
title: IDSymbol 要素 |Microsoft Docs
description: 'IDSymbol 要素には、メニュー、グループ、またはコマンドを表す GUID: ID ペアの ID が含まれています。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 830324e708ff83fbcbbbdb98d261130e92c7ba00
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99883195"
---
# <a name="idsymbol-element"></a>IDSymbol 要素
要素には、 `IDSymbol` メニュー、グループ、またはコマンドを表す GUID: id ペアの id が含まれています。 GUID は親要素から取得され `GuidSymbol` ます。 `IDSymbol`要素には、 `name` 属性に含まれる ID のフレンドリ名を提供する属性があり `value` ます。

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
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[GuidSymbol 要素](../extensibility/guidsymbol-element.md)|メニュー、グループ、またはコマンドを表す GUID: ID ペアの GUID を格納します。 複数の `IDSymbol` 要素をグループ化します。|

## <a name="remarks"></a>解説
 `IDSymbol`指定された要素内のすべての要素は `GuidSymbol` 、一意である必要があり `value` ます。 ただし、 `IDSymbol` 同一の値を持つ要素は、異なる親を持つ限り、パッケージ内に存在することができます。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
