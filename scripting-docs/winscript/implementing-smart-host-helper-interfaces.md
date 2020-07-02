---
title: スマート ホスト ヘルパー インターフェイスの実装 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Smart Host Helper Interfaces, implementing
ms.assetid: b9c44246-4d4d-469e-91be-00c8f5796fa5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: deac5827aa38039099f1d0f5e621d473db96743d
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835603"
---
# <a name="implementing-smart-host-helper-interfaces"></a>スマート ホスト ヘルパー インターフェイスの実装
[IDebugDocumentHelper インターフェイス](../winscript/reference/idebugdocumenthelper-interface.md)は、スマート ホストに必要な多くのインターフェイスの実装を提供することで、アクティブ デバッグ用のスマート ホストを作成するタスクを大幅に簡略化します。  
  
 `IDebugDocumentHelper` を使うスマート ホストにするためにホスト アプリケーションで行う必要があることは、次の 3 つだけです。  
  
1. プロセス デバッグ マネージャーの `CoCreate` を実行し、[IProcessDebugManager インターフェイス](../winscript/reference/iprocessdebugmanager-interface.md)を使ってアプリケーションをデバッグできるアプリケーションのリストに追加します。  
  
2. [IProcessDebugManager::CreateDebugDocumentHelper](../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md) メソッドを使って、各スクリプト オブジェクトのデバッグ ドキュメント ヘルパーを作成します。 ドキュメント名、親ドキュメント、テキスト、およびスクリプト ブロックが定義されていることを確認します。  
  
3. [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) インターフェイス (アクティブ スクリプトに必要です) を実装しているオブジェクトに、[IActiveScriptSiteDebug インターフェイス](../winscript/reference/iactivescriptsitedebug-interface.md)を実装します。 `IActiveScriptSiteDebug` インターフェイスの重要なメソッドのみがヘルパーにデリゲートします。  
  
   ホストは、構文の色、ドキュメントのコンテキスト作成、その他の拡張機能をさらに制御する必要がある場合は、[IDebugDocumentHost インターフェイス](../winscript/reference/idebugdocumenthost-interface.md)を実装することもできます。  
  
   スマート ホスト ヘルパーの大きな制限として、スマート ホスト ヘルパーは追加された後で内容が変更または縮小されたドキュメントだけを処理できます (ドキュメントを展開することはできます)。 ただし、多くのスマート ホストでは、必要な機能はスマート ホスト ヘルパーによって提供されます。  
  
   以下では各ステップについて詳しく説明します。  
  
## <a name="create-an-application-object"></a>アプリケーション オブジェクトを作成する  
 スマート ホスト ヘルパーを使うには、その前に、デバッガー内でアプリケーションを表す [IDebugApplication インターフェイス](../winscript/reference/idebugapplication-interface.md) オブジェクトを作成する必要があります。  
  
#### <a name="to-create-an-application-object"></a>アプリケーション オブジェクトを作成するには  
  
1. `CoCreateInstance` を使って、プロセス デバッグ マネージャーのインスタンスを作成します。  
  
2. [IProcessDebugManager::CreateApplication](../winscript/reference/iprocessdebugmanager-createapplication.md) を呼び出します。  
  
3. [IDebugApplication::SetName](../winscript/reference/idebugapplication-setname.md) を使ってアプリケーションに名前を設定します。  
  
4. [IProcessDebugManager::AddApplication](../winscript/reference/iprocessdebugmanager-addapplication.md) を使って、デバッグできるアプリケーションのリストにアプリケーション オブジェクトを追加します。  
  
     プロセスの概要を示す次のコードには、エラー チェックや信頼性の高い他のプログラミング手法は含まれません。  
  
    ```cpp
    CoCreateInstance(CLSID_ProcessDebugManager, NULL,  
          CLSCTX_INPROC_SERVER | CLSCTX_INPROC_HANDLER  
          | CLSCTX_LOCAL_SERVER,  
    IID_IProcessDebugManager, (void **)&g_ppdm);  
    g_ppdm->CreateApplication(&g_pda);  
    g_pda->SetName(L"My cool application");  
    g_ppdm->AddApplication(g_pda, &g_dwAppCookie);  
    ```  
  
## <a name="using-idebugdocumenthelper"></a>IDebugDocumentHelper の使用  
  
#### <a name="to-use-the-helper-minimal-sequence-of-steps"></a>ヘルパーを使うには (最小限の手順)  
  
1. ホスト ドキュメントごとに、[IProcessDebugManager::CreateDebugDocumentHelper](../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md) を使ってヘルパーを作成します。  
  
2. ヘルパーで [IDebugDocumentHelper::Init](../winscript/reference/idebugdocumenthelper-init.md) を呼び出し、名前、ドキュメント属性、その他を指定します。  
  
3. ドキュメントの親ヘルパー (または、ドキュメントがルートの場合は NULL) で [IDebugDocumentHelper::Attach](../winscript/reference/idebugdocumenthelper-attach.md) を呼び出して、ツリー内でのドキュメントの位置を定義し、デバッガーに認識されるようにします。  
  
4. [IDebugDocumentHelper::AddDBCSText](../winscript/reference/idebugdocumenthelper-adddbcstext.md) または [IDebugDocumentHelper::AddUnicodeText](../winscript/reference/idebugdocumenthelper-addunicodetext.md) を呼び出して、ドキュメントのテキストを定義します  (ブラウザーのようにドキュメントがインクリメント方式でダウンロードされる場合、これらのメソッドを複数回呼び出すことができます。)  
  
5. [IDebugDocumentHelper::DefineScriptBlock](../winscript/reference/idebugdocumenthelper-definescriptblock.md) を呼び出して、各スクリプト ブロックの範囲と、関連付けられているスクリプト エンジンを定義します。  
  
## <a name="implementing-iactivescriptsitedebug"></a>IActiveScriptSiteDebug を実装する  
 [IActiveScriptSiteDebug::GetDocumentContextFromPosition](../winscript/reference/iactivescriptsitedebug-getdocumentcontextfromposition.md) を実装するには、特定のサイトに対応するヘルパーを取得した後、次のようにして特定のソース コンテキストの開始ドキュメント オフセットを取得します。  
  
```cpp
pddh->GetScriptBlockInfo(dwSourceContext, NULL, &ulStartPos, NULL);  
```  
  
 次に、ヘルパーを使って特定の文字オフセットの新しいドキュメント コンテキストを作成します。  
  
```cpp
pddh->CreateDebugDocumentContext(ulStartPos + uCharacterOffset, cChars, &pddcNew);  
```  
  
 [IActiveScriptSiteDebug::GetRootApplicationNode](../winscript/reference/iactivescriptsitedebug-getrootapplicationnode.md) を実装するには、単に `IDebugApplication::GetRootNode` ([IRemoteDebugApplication::GetRootNode](../winscript/reference/iremotedebugapplication-getrootnode.md) から継承したもの) を呼び出します。  
  
 [IDebugDocumentHelper::GetDebugApplicationNode](../winscript/reference/idebugdocumenthelper-getdebugapplicationnode.md) を実装するには、プロセス デバッグ マネージャーを使って最初に作成した `IDebugApplication` を単に戻します。  
  
## <a name="the-optional-idebugdocumenthost-interface"></a>IDebugDocumentHost インターフェイス (省略可能)  
 ホストは [IDebugDocumentHelper::SetDebugDocumentHost](../winscript/reference/idebugdocumenthelper-setdebugdocumenthost.md) を使って [IDebugDocumentHost Interface](../winscript/reference/idebugdocumenthost-interface.md) の実装を提供し、ヘルパーに対する制御を追加できます。 ホスト インターフェイスを使って実行できる主な操作の一部を次に示します。  
  
- [IDebugDocumentHelper::AddDeferredText](../winscript/reference/idebugdocumenthelper-adddeferredtext.md) を使ってテキストを追加し、ホストが実際の文字をすぐに提供する必要がないようにします。 文字が本当に必要になると、ヘルパーはホストで [IDebugDocumentHost::GetDeferredText](../winscript/reference/idebugdocumenthost-getdeferredtext.md) を呼び出します。  
  
- ヘルパーによって提供される既定の構文の色分けをオーバーライドします。 ヘルパーは [IDebugDocumentHost::GetScriptTextAttributes](../winscript/reference/idebugdocumenthost-getscripttextattributes.md) を呼び出して文字の範囲の色を決定し、ホストが `E_NOTIMPL` を返す場合は既定の実装にフォールバックします。  
  
- [IDebugDocumentHost::OnCreateDocumentContext](../winscript/reference/idebugdocumenthost-oncreatedocumentcontext.md) を実装することでヘルパーによって作成されたドキュメント コンテキストで不明な制御を提供します。 これにより、ホストは既定のドキュメント コンテキストの実装の機能をオーバーライドできます。  
  
- ファイル システムでのドキュメントのパス名を提供します。 一部のデバッグ UI はこれを使って、ユーザーがドキュメントを編集して変更を保存できるようにします。 ドキュメントが保存された後は、ホストに通知するために [IDebugDocumentHost::NotifyChanged](../winscript/reference/idebugdocumenthost-notifychanged.md) が呼び出されます。  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプトのデバッグの概要](../winscript/active-script-debugging-overview.md)