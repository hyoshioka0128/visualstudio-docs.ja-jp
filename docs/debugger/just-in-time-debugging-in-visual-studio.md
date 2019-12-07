---
title: Just-in-time デバッガーを無効にする |Microsoft Docs
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
ms.openlocfilehash: eb66615abbd7124fd6b781598bd8eb28ea34756d
ms.sourcegitcommit: 0b90e1197173749c4efee15c2a75a3b206c85538
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/07/2019
ms.locfileid: "74903866"
---
# <a name="disable-the-just-in-time-debugger"></a>Just-In-Time デバッガーを無効にする

実行中のアプリでエラーが発生すると、[Just-in-time デバッガー] ダイアログボックスが開き、アプリが続行されないようにすることができます。

Just-in-time デバッガーでは、Visual Studio を起動してエラーをデバッグするオプションが用意されています。 エラーに関する詳細情報を表示したり、デバッグを試行したりするには、Visual Studio または別の選択したデバッガーがインストールされている必要があります。

既に Visual Studio ユーザーがいて、エラーのデバッグを試行する場合は、 [Just-in-time デバッガーを使用](../debugger/debug-using-the-just-in-time-debugger.md)したデバッグに関するを参照してください。 エラーを修正できない場合、または Just-in-time デバッガーを開いたままにしたい場合は、 [Visual Studio から just-in-time デバッグを無効](debug-using-the-just-in-time-debugger.md#BKMK_Enabling)にすることができます。

Visual Studio がインストールされていても、不要になった場合は、 [Windows レジストリから just-in-time デバッグを無効](debug-using-the-just-in-time-debugger.md#disable-just-in-time-debugging-from-the-windows-registry)にすることが必要になる場合があります。

Visual Studio がインストールされていない場合は、スクリプトのデバッグまたはサーバー側のデバッグを無効にすることで、Just-in-time デバッグを防止できます。

- Web アプリを実行しようとしている場合は、スクリプトのデバッグを無効にします。

  Windows の**コントロールパネル**で > [**ネットワークとインターネット** > の**インターネットオプション**] の **[スクリプトデバッグを無効にする (internet Explorer)]** を選択し、 **[スクリプトのデバッグを無効にする (その他)]** を選択します。 正確な手順と設定は、使用している Windows とブラウザーのバージョンによって異なります。

  ![JIT インターネットオプション](../debugger/media/jitinternetoptions.png "JIT インターネットオプション")

- IIS で ASP.NET web アプリをホストしている場合は、サーバー側のデバッグを無効にします。

  1. IIS マネージャーの **[機能ビュー]** の **[ASP.NET]** セクションで、 **[.net コンパイル]** をダブルクリックするか、 **[操作]** ウィンドウの 機能を **[開く]** を選択します。
  1. [**動作** > **デバッグ**] で、 **[False]** を選択します。 以前のバージョンの IIS では、手順は異なります。

Just-in-time デバッグを無効にすると、アプリはエラーを処理して正常に実行できる可能性があります。

アプリに未処理のエラーが残っている場合は、エラーメッセージが表示されるか、アプリがクラッシュまたはハングする可能性があります。 このエラーが修正されるまで、アプリは正常に実行されません。 アプリの所有者に連絡して、それを修正するように依頼することができます。
