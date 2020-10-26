---
title: '[Just-In-Time] ([オプション] ダイアログ ボックス - [デバッグ]) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Debugger.JIT
- vs.debug.options.JIT
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- Just-In-Time debugging, setting options
- Options dialog box, debugging
ms.assetid: 7f11b2e3-3fb5-449d-b07c-6ecf1d6a487d
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9b3bd6c6ee32145a94dbc4b751834ecc003f2bdf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201101"
---
# <a name="just-in-time-debugging-options-dialog-box"></a>[Just-In-Time] ([オプション] ダイアログ ボックス - [デバッグ])
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**[Just-In-Time]** ページを使用するには、 **[ツール]** メニューの **[オプション]** をクリックします。 **[オプション]** ダイアログ ボックスの **[デバッグ]** ノードを展開し、 **[Just-In-Time]** をクリックします。 このページでは、マネージド コード、ネイティブ コード、およびスクリプトでの Just-In-Time デバッグを有効にできます。 詳細については、「[Just-In-Time デバッグ](../debugger/just-in-time-debugging-in-visual-studio.md)」を参照してください。  
  
 Just-In-Time デバッグは次のプログラムの種類で有効です。  
  
- マネージド  
  
- ネイティブ  
  
- スクリプト  
  
  Just-In-Time デバッグは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の外部で起動されたプログラムをデバッグするための手法です。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] で作成されたプログラムを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 環境の外部で実行できます。 Just-In-Time デバッグを有効にすると、クラッシュの発生時に、デバッグを実行するかどうかを確認するダイアログ ボックスが表示されます。  
  
## <a name="associated-warnings"></a>関連する警告  
 **[オプション]** ダイアログ ボックスでこのページを開いたときに、次のような警告メッセージが表示される場合があります。  
  
 **別のデバッガーが Just-In-Time デバッガーとして登録されています。修復するには、Just-In-Time デバッグを有効にするか、または Visual Studio の修復を実行してください。**  
  
 このメッセージは、他のデバッガー (古いバージョンの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] デバッガーなど) が Just-In-Time デバッガーとして設定されている場合に表示されます。  
  
 次のメッセージが表示されることもあります。  
  
 **Just-In-Time デバッグの登録エラーが検出されました。修復するには、Just-In-Time デバッグを有効にするか、または Visual Studio の修復を実行してください。**  
  
 これらの警告のいずれかが表示されている場合、問題が解決されるまでの間、[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] で Just-In-Time デバッグを行うには管理者特権が必要になります。 この場合、管理者以外の権限で Just-In-Time デバッグを有効にしようとすると、次のメッセージが表示されます。  
  
 **アクセスが拒否されました。管理者に Just-In-Time デバッグを有効にしてもらうか、または Visual Studio のインストールを修復してください。**  
  
## <a name="see-also"></a>参照  
 [[デバッグ] ([オプション] ダイアログボックス)](../debugger/debugging-options-dialog-box.md)   
 [方法: デバッガー設定を指定する](../debugger/how-to-specify-debugger-settings.md)
