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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 95b4c88cc42879bf40278871a0e39de13f63a418
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99911221"
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
