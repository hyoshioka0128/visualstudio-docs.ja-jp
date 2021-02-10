---
title: '[Just-In-Time] ([オプション] ダイアログ ボックス - [デバッグ]) | Microsoft Docs'
description: Just-in-time デバッグを使用すると、Visual Studio の外部で起動されるプログラムをデバッグできます。 さまざまなプログラムの種類に対して Just-In-Time デバッグを有効にする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Debugger.JIT
- vs.debug.options.JIT
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Just-In-Time debugging, setting options
- Options dialog box, debugging
ms.assetid: 7f11b2e3-3fb5-449d-b07c-6ecf1d6a487d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0ea88d141dd15e439fddd24b374d745a721d31b0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99876343"
---
# <a name="just-in-time-debugging-options-dialog-box"></a>[Just-In-Time] ([オプション] ダイアログ ボックス - [デバッグ])
**[Just-In-Time]** ページを使用するには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[デバッグ]** ノードを展開し、 **[Just-In-Time]** をクリックします。 このページでは、マネージド コード、ネイティブ コード、およびスクリプトでの Just-In-Time デバッグを有効にできます。 詳細については、「[Just-In-Time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)」を参照してください。

 Just-In-Time デバッグは次のプログラムの種類で有効です。

- マネージド

- ネイティブ

- スクリプト

  Just-In-Time デバッグは、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] の外部で起動されたプログラムをデバッグするための手法です。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] で作成されたプログラムを [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 環境の外部で実行できます。 Just-In-Time デバッグを有効にすると、クラッシュの発生時に、デバッグを実行するかどうかを確認するダイアログ ボックスが表示されます。

## <a name="associated-warnings"></a>関連する警告
 **[オプション]** ダイアログ ボックスでこのページを開いたときに、次のような警告メッセージが表示される場合があります。

 **別のデバッガーが Just-In-Time デバッガーとして登録されています。修復するには、Just-In-Time デバッグを有効にするか、または Visual Studio の修復を実行してください。**

 このメッセージは、他のデバッガー (古いバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーなど) が Just-In-Time デバッガーとして設定されている場合に表示されます。

 次のメッセージが表示されることもあります。

 **Just-In-Time デバッグの登録エラーが検出されました。修復するには、Just-In-Time デバッグを有効にするか、または Visual Studio の修復を実行してください。**

 これらの警告のいずれかが表示されている場合、問題が解決されるまでの間、[!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] で Just-In-Time デバッグを行うには管理者特権が必要になります。 この場合、管理者以外の権限で Just-In-Time デバッグを有効にしようとすると、次のメッセージが表示されます。

 **アクセスが拒否されました。管理者に Just-In-Time デバッグを有効にしてもらうか、または Visual Studio のインストールを修復してください。**

## <a name="see-also"></a>関連項目
- [[デバッグ] ([オプション] ダイアログ ボックス)](../debugger/debugging-options-dialog-box.md)
- [方法: デバッガー設定を指定する](../debugger/how-to-specify-debugger-settings.md)