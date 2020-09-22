---
title: '方法: RPC デバッグを使用して COM クライアントおよびサーバーをデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- RPC (Remote Procedure Call), debugging COM clients and servers
- COM, debugging
- RPC (Remote Procedure Call)
- RPC (Remote Procedure Call), debugging
- COM clients, debugging
- COM servers, debugging
- out-of-process remote procedure call debugging
- remote debugging, RPC (Remote Procedure Call)
- in-process remote procedure call debugging
ms.assetid: 3e8526c8-43b5-4b87-8e0d-b22c24f0a3ea
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fda2a10cd559f940ab87e5cc8c26f5b47dbec194
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842285"
---
# <a name="how-to-debug-com-clients-and-servers-using-rpc-debugging"></a>方法 : RPC デバッグを使用して COM クライアントおよびサーバーをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

リモート プロシージャ コール (RPC: Remote Procedure Call) デバッグを使用して、COM クライアント/サーバー アプリケーションをデバッグできます。 このデバッグを行うには、あらかじめ RPC デバッグを有効にする必要があります。 RPC デバッグを有効にすると、ステップ実行でクライアントからサーバーを呼び出すときに、デバッガーがサーバーにアタッチし、コードのデバッグができるようになります。 デバッガーをアタッチすることにより、クライアントおよびサーバーのどちらのプロセスでも、デバッガーのすべての機能を使用できます。  
  
### <a name="to-enable-rpc-debugging"></a>RPC デバッグを有効にするには  
  
1. **[ツール]** メニューの **[オプション]** をクリックします。  
  
2. **[オプション]** ダイアログ ボックスで、**[デバッグ]** フォルダーをクリックします。  
  
3. **[ネイティブ]** ページをクリックします。  
  
4. **[RPC デバッグ]** チェック ボックスをオンにします。  
  
    > [!NOTE]
    > RPC 呼び出しをデバッグするには、管理者またはパワー ユーザーの権限が必要です。  
  
    > [!NOTE]
    > Microsoft Windows Vista が実行されているリモート サーバーへの RPC ステップ実行は、そのリモート サーバーにネイティブ デバッガーがアタッチされている場合のみ機能します。 それ以外の場合、エラー メッセージが表示されることなく RPC 呼び出しが失敗します。 何らかの方法で RPC 呼び出しに成功したとしても、RPC 呼び出しへのステップ インは正常に機能しません。  
  
## <a name="see-also"></a>参照  
 [COM サーバーとコンテナーのデバッグ](../debugger/com-server-and-container-debugging.md)   
 [Visual Studio でのデバッグ](../debugger/debugging-in-visual-studio.md)
