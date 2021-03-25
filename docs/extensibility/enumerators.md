---
title: 列挙子 |Microsoft Docs
description: コマンドコード、メッセージ、ファイルステータスコード、ディレクトリステータスコードなど、ソース管理プラグイン API の列挙子データ型について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0bdc42901cbdad3b30bb6739ec93b8979b0d56ad
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075277"
---
# <a name="enumerators"></a>列挙子
このセクションでは、ソース管理プラグインが認識する必要があるソース管理プラグイン API の列挙子データ型について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [コマンドコード](../extensibility/command-code-enumerator.md)[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)関数と[SccPopulateList](../extensibility/sccpopulatelist-function.md)関数のオプションを列挙します。

- [メッセージ](../extensibility/message-enumerator.md) 印刷コールバック、 [Lptextoutproc](../extensibility/lptextoutproc.md)に使用されるフラグを列挙します。

- [ファイルの状態コード](../extensibility/file-status-code-enumerator.md) ソース管理下にあるファイルの状態を指定する名前付き定数値を格納します。

- [ディレクトリの状態コード](../extensibility/directory-status-code-enumerator.md) ソース管理下にあるディレクトリの状態を指定する名前付き定数値を格納します。

## <a name="related-sections"></a>関連項目
- [ソース管理プラグインを作成する](../extensibility/internals/creating-a-source-control-plug-in.md) ソース管理プラグイン SDK を定義し、含まれているリソースについて説明します。

- [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) 指定されたコマンドの詳細オプションをユーザーに表示します。

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) ファイルの一覧を調べて、現在の状態を確認します。 さらに、は関数を使用して、 `pfnPopulate` ファイルがの条件に一致しない場合に呼び出し元に通知し `nCommand` ます。

- [Lptextoutproc](../extensibility/lptextoutproc.md) IDE を介してソース管理プラグインからのメッセージを表示するために [Sccopenproject](../extensibility/sccopenproject-function.md) によって使用されるコールバック関数について説明します。

- [ソース管理プラグイン](../extensibility/source-control-plug-ins.md) ソース管理プラグイン API のすべての要素の完全な一覧を提供します。
