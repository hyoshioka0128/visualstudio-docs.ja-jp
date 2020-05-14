---
title: '方法: Spy + + | を開始するMicrosoft Docs'
ms.date: 12/16/2018
ms.topic: conceptual
helpviewer_keywords:
- Spy++, starting
ms.assetid: 1d36813a-dc2a-4fda-9b3d-a38928a62ced
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70874d70dd5f845e7b627f2aeb7ae51bafe45995
ms.sourcegitcommit: 7b07e7b5e06e2e13f622445c568b78a284e1a40d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2020
ms.locfileid: "76542621"
---
# <a name="how-to-start-spy"></a>方法: Spy++ を起動する

Spy + + を起動するには、Visual Studio またはコマンドプロンプトを使用します。

 Spy + + を起動するときに、コンピューターに変更を加えるためのアクセス許可を求めるメッセージが表示されたら、[**はい]** を選択します。

> [!NOTE]
> Spy + + のインスタンスは1つだけ実行できます。 2番目のインスタンスを開始しようとすると、現在実行中のインスタンスがフォーカスを取得するだけです。

## <a name="prerequisites"></a>Prerequisites

Spy + + には、次のコンポーネントが必要です。 **[個々のコンポーネント]** タブを選択し、次のコンポーネントを選択することで、これらのコンポーネントを Visual Studio インストーラーから選択できます。

* [デバッグとテスト] で、[  **C++プロファイルツール] を選択します。**
* [開発アクティビティ] で、[  **C++コア機能] を選択します。**

変更を行った場合は、画面の指示に従ってこれらのコンポーネントをインストールします。

## <a name="start-spy-from-visual-studio"></a>Visual Studio から Spy + + を起動する

**[ツール]** メニューの **[Spy + +]** を選択します。

Spy + + は独立して実行されるため、開始した後で Visual Studio を閉じることができます。

> [!NOTE]
> Spy + + を使用してメッセージをログに記録すると、オペレーティングシステムのパフォーマンスが低下する可能性があります。

## <a name="start-spy-at-a-command-prompt"></a>コマンドプロンプトで Spy + + を起動する

1. コマンドプロンプトウィンドウで、ディレクトリを spyxx を含むフォルダーに変更します。 通常、このフォルダーへのパスは. です。*Visual Studio のインストールフォルダー*\Common7\Tools\\を\\します。

2. 「 **Spyxx**」と入力します。

## <a name="see-also"></a>関連項目
- [Spy++ の使用](../debugger/using-spy-increment.md)
- [Spy++ ビュー](../debugger/spy-increment-views.md)
- [Spy++ リファレンス](../debugger/spy-increment-reference.md)
