---
title: ボタンテキスト要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59308feea2002a18662a7c04b95a92a920f934c4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739908"
---
# <a name="buttontext-element"></a>ボタンテキスト要素
このフィールドでは、さまざまなメニューに表示されるテキストを指定できます。 既定では、要素`ButtonText`はメニュー コント ローラーに表示されます。 また`ButtonText`、他のテキスト フィールドが空白の場合は、要素が既定値になります。 他`ButtonText`のテキスト フィールドが指定されていても、要素を空白にすることはできません。

## <a name="syntax"></a>構文

```xml
<ButtonText>My Command</ButtonText>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 [なし] :

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[文字列要素](../extensibility/strings-element.md)|や などの`ButtonText`テキスト要素を`CommandName`グループ化します。|

## <a name="text-value"></a>テキスト値
 `ButtonText`要素のテキスト値は、メニュー項目、コンボ、および表示テキストを持つその他のユーザー インターフェイス (UI) 要素に表示されるテキストを提供します。

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
