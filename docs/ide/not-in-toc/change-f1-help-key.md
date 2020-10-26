---
title: F1 ヘルプ キーを変更する
description: F1 キーのマッピングを再マップまたは削除する方法について説明します
ms.date: 08/20/2020
ms.topic: how-to
ms.custom: contperfq1
robots: noindex,nofollow
manager: jillfra
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: debf469248a8ec1906f3692c37835d9f96476f54
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802296"
---
# <a name="change-the-f1-help-key-in-visual-studio"></a>Visual Studio の F1 ヘルプ キーを変更する

F1 ヘルプ サービスとは異なる機能のために F1 キーを使いたい場合、または単に F1 キーを使用したヘルプを無効にしたい場合は、キー マッピングを削除または変更できます。

> [!IMPORTANT]
> パフォーマンス上の問題のために F1 ヘルプを無効にする場合は、キー マッピングを一時的に変更することをお勧めします。これにより、Visual Studio の更新プログラムにおける F1 ヘルプ サービスの改善をテストできます。 ほとんどのシナリオでは、F1 キーを使用することで、簡単にコード エディターから言語のキーワードや API の参照ページを開いたり、IDE のウィンドウや UI 要素に関連付けられたヘルプ ページを開いたりすることができます。 無効にした場合は、Visual Studio 内からのすべての使用に対して無効になります。

**F1 ヘルプを無効にするには:**

1. Visual Studio で、 **[ツール]**  >  **[オプション]** の順に選択した後、 **[環境]** で **[キーボード]** を選択します。

1. **[以下の文字列を含むコマンドを表示]** テキスト ボックスに「**Help.f1**」と入力して、コマンドのビューをフィルター処理します。

   ![F1 ヘルプを無効にする](../not-in-toc/media/disable-f1-help-key.png)

1. キー マッピングを削除するには、 **[削除]** を選択します。

1. **[ショートカット キー]** テキスト ボックスを選択します。

1. キーボードで、F1 ヘルプ用の新しいキーまたはキーの組み合わせ (**Alt + F1** キーなど) を押し、 **[割り当て]** を選択して、 **[OK]** を選択します。

キーボード ショートカット設定の詳細については、[キーボード ショートカットの識別とカスタマイズ](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)に関する記事をご覧ください。
