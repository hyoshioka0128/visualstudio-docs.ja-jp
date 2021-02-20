---
title: Spy++ の起動 | Microsoft Docs
description: ソリューションをデバッグするときに、Visual Studio からまたはコマンド プロンプトで Spy++ ツールを起動する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/16/2018
ms.topic: how-to
helpviewer_keywords:
- Spy++, starting
ms.assetid: 1d36813a-dc2a-4fda-9b3d-a38928a62ced
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0e8b1125534e52c810f97c91bd00ea53dfd3d6de
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896625"
---
# <a name="how-to-start-spy"></a>方法: Spy++ の起動

Spy++ は、Visual Studio またはコマンド プロンプトから起動できます。

 Spy++ を起動すると、コンピューターを変更をするためのアクセス許可を求めるメッセージが表示される場合は、 **[はい]** を選択します。

> [!NOTE]
> Spy++ のインスタンスは 1 つだけ実行できます。 2 番目のインスタンスを起動しようとすると、現在実行中のインスタンスにフォーカスが設定されるだけです。

## <a name="prerequisites"></a>必須コンポーネント

Spy++ には、次のコンポーネントが必要です。 これらのコンポーネントを Visual Studio インストーラーから選択するには、 **[個別のコンポーネント]** タブを選択し、次のコンポーネントを選択します。

* [デバッグとテスト] で、 **[C++ のプロファイル ツール]** を選択します
* [開発作業] で、 **[C++ コア機能]** を選択します

変更を行った場合は、画面の指示に従ってこれらのコンポーネントをインストールします。

## <a name="start-spy-from-visual-studio"></a>Visual Studio から Spy++ を起動する

**[ツール]** メニューの **[Spy++]** を選択します。

Spy++ は独立して実行されるため、起動した後で Visual Studio を閉じることができます。

> [!NOTE]
> Spy++ でメッセージをログに記録すると、オペレーティング システムのパフォーマンスが低下する可能性があります。

## <a name="start-spy-at-a-command-prompt"></a>コマンド プロンプトで Spy++ を起動する

1. コマンド プロンプト ウィンドウで、ディレクトリを spyxx.exe が含まれるフォルダーに変更します。 通常、このフォルダーへのパスは ..\\<*Visual Studio インストール フォルダー*>\Common7\Tools\\ です。

2. 「**spyxx.exe**」と入力します。

## <a name="see-also"></a>関連項目
- [Spy++ の使用](../debugger/using-spy-increment.md)
- [Spy++ ビュー](../debugger/spy-increment-views.md)
- [Spy++ リファレンス](../debugger/spy-increment-reference.md)
