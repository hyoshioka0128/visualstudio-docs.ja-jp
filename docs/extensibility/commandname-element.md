---
title: コマンド名要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- CommandName element (VSCT XML schema)
- VSCT XML schema elements, CommandName
ms.assetid: a338b767-aa7e-4536-9908-e19a50ab60ac
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8152942d015e21b1b80f735fd921a5ddde3674d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739752"
---
# <a name="commandname-element"></a>コマンド名要素
この`CommandName`要素は、[**オプション]** ダイアログ ボックスのキーボード カテゴリと、[**ユーザー設定**] ダイアログ ボックスの **[コマンド**] ボックスに表示されるテキストを指定します。

## <a name="syntax"></a>構文

```
<CommandName>MyCommand</CommandName>
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

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
