---
title: IActiveScriptSiteDebug32 Interface |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 03f42217-303d-46e7-9792-61a5ab95252c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 2a55161f76fcd98b52ddb769c640aca0e903239b
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835265"
---
# <a name="iactivescriptsitedebug32-interface"></a>IActiveScriptSiteDebug32 インターフェイス
スマートホストは、 `IActiveScriptSiteDebug32` ドキュメントの管理を実行し、デバッグに参加するためのインターフェイスを実装します。 オブジェクトは、 `IActiveScriptSite` 通常、インターフェイスの実装を提供し `IActiveScriptSiteDebug32` ます。 この処理が完了したら、メソッドを呼び出して、 `IActiveScriptSite::QueryInterface` インターフェイスを取得し `IActiveScriptSiteDebug32` ます。  
  
 から継承されたメソッドに加えて、 `IUnknown` `IActiveScriptSiteDebug32` インターフェイスは次のメソッドを公開します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IActiveScriptSiteDebug32::GetApplication](../../winscript/reference/iactivescriptsitedebug32-getapplication.md)|このスクリプトサイトに関連付けられているデバッグアプリケーションオブジェクトを返します。|  
|[IActiveScriptSiteDebug32::GetDocumentContextFromPosition](../../winscript/reference/iactivescriptsitedebug32-getdocumentcontextfromposition.md)|言語エンジンがを委任するために使用し `IDebugCodeContext::GetSourceContext` ます。|