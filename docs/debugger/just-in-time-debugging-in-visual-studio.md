---
title: Just-In-Time デバッガーを無効にする | Microsoft Docs
ms.date: 05/23/2018
ms.topic: troubleshooting
helpviewer_keywords:
- debugging [Visual Studio], Just-In-Time
- Just-In-Time debugging
ms.assetid: 14972d5f-69bc-479b-9529-03b8787b118f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3155c2cdc9ea3dc5208a52e5fe37f697a4ad5ef6
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86386122"
---
# <a name="disable-the-just-in-time-debugger"></a>Just-In-Time デバッガーを無効にする

実行中のアプリでエラーが発生すると、[Just-In-Time デバッガー] ダイアログ ボックスが開き、アプリが続行できない場合があります。

Just-In-Time デバッガーには、Visual Studio を起動してエラーをデバッグするオプションがあります。 エラーに関する詳細情報を表示したり、デバッグを試行したりするには、Visual Studio または別の選択したデバッガーがインストールされている必要があります。

既に Visual Studio を使用しており、エラーをデバッグしてみたるには、[Just-In-Time デバッガーを使用したデバッグ](../debugger/debug-using-the-just-in-time-debugger.md)に関するページを参照してください。 エラーを修正できない場合、または Just-In-Time デバッガーが開かないようにするには、[Visual Studio で Just-In-Time デバッグを無効にする](debug-using-the-just-in-time-debugger.md#BKMK_Enabling)ことができます。

Visual Studio が以前インストールされていたが、今はインストールされていない場合は、[Windows レジストリで Just-In-Time デバッグを無効にする](debug-using-the-just-in-time-debugger.md#disable-just-in-time-debugging-from-the-windows-registry)必要があります。

Visual Studio がインストールされていない場合は、スクリプトのデバッグまたはサーバー側のデバッグを無効にすることで、Just-In-Time デバッグを防ぐことができます。

- Web アプリを実行しようとしている場合は、スクリプトのデバッグを無効にします。

  Windows の **[コントロール パネル]**  >  **[ネットワークとインターネット]**  >  **[インターネット オプション]** で、 **[Disable script debugging (Internet Explorer)]\(スクリプトのデバッグを使用しない (Internet Explorer)\)** と **[Disable script debugging (other)]\(スクリプトのデバッグを使用しない (その他)\)** を選択します。 正確なステップと設定は、使用している Windows とブラウザーのバージョンによって異なります。

  ![JIT インターネット オプション](../debugger/media/jitinternetoptions.png "JIT インターネット オプション")

- IIS で ASP.NET Web アプリをホストしている場合は、サーバー側のデバッグを無効にします。

  1. IIS マネージャーの **[機能ビュー]** の **[ASP.NET]** セクションで、 **[.NET コンパイル]** をダブルクリックするか、それを選択して **[アクション]** ペインで **[機能を開く]** を選択します。
  1. **[動作]**  >  **[デバッグ]** の下で **[False]** を選択します。 以前のバージョンの IIS では、ステップは異なります。

Just-In-Time デバッグを無効にすると、アプリがエラーを処理して正常に実行できる可能性があります。

アプリに未処理のエラーが残っている場合は、エラー メッセージが表示されるか、アプリがクラッシュまたは応答しなくなる可能性があります。 エラーが修正されるまで、アプリは正常に実行されません。 アプリの所有者に連絡して、修正するように依頼することができます。
