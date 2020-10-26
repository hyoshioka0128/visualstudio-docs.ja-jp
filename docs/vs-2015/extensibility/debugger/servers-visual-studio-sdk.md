---
title: サーバー (Visual Studio SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7ed2ce924b22827a82a67664e3e473f0930a87e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199396"
---
# <a name="servers-visual-studio-sdk"></a>サーバー (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーアーキテクチャに関しては、 **サーバー**は次のようになります。  
  
- はポートおよびポートサプライヤーのコンテナーであり、ポートおよびポートサプライヤーをセッションデバッグマネージャー (SDM) およびデバッグエンジンに伝達するために使用されます。  
  
- では、名前によって自身を識別し、そのポートとポートサプライヤーを列挙できます。  
  
- は、 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスによって表されます。これは、visual studio (を実行している visual studio のインスタンスごとにサーバーの1つのインスタンス) によってのみ実装されます。  
  
## <a name="see-also"></a>参照  
 [シリアル](../../extensibility/debugger/ports.md)   
 [ポートサプライヤー](../../extensibility/debugger/port-suppliers.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
