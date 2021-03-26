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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ba74c0a61ddf01407f2af6ebb8053e2f1e4fe6ac
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105089629"
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

## <a name="see-also"></a>こちらもご覧ください
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
