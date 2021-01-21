---
title: CommandName 要素 |Microsoft Docs
description: CommandName 要素は、[オプション] ダイアログボックスの [キーボード] カテゴリ、および [ユーザー設定] ダイアログボックスのコマンド一覧に表示されるテキストを指定します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 8447213b14a3632197ea7ce27677423460315f71
ms.sourcegitcommit: 5027eb5c95e1d2da6d08d208fd6883819ef52d05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94974113"
---
# <a name="commandname-element"></a>CommandName 要素
要素は、[ `CommandName` **オプション**] ダイアログボックスの [キーボード] カテゴリに表示されるテキストと、[**カスタマイズ**] ダイアログボックスの [**コマンド**] ボックスの一覧に表示されるテキストを指定します。

## <a name="syntax"></a>構文

```
<CommandName>MyCommand</CommandName>
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性
 なし。

### <a name="child-elements"></a>子要素
 なし。

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[Strings 要素](../extensibility/strings-element.md)|やなどのテキスト要素をグループ化し `ButtonText` `CommandName` ます。|

## <a name="see-also"></a>関連項目
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
