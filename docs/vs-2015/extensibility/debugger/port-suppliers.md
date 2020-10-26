---
title: ポートサプライヤー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e90871927c30399dea4691381baa749db2b3e8bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153700"
---
# <a name="port-suppliers"></a>ポート サプライヤー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーアーキテクチャに関して、 **ポート供給業者**は次のようになります。  
  
- はサーバーに含まれており、そのサーバーに要求するポートを提供します。  
  
- 含まれているサーバーのポートを追加および削除できます。  
  
- では、サーバーに提供されたすべてのポートを列挙できます。  
  
- は、 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスによって表されます。これは、レジストリを使用して Visual Studio に登録されます。 このインターフェイスは、 [Getportsupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)を呼び出すことによって取得できます。  
  
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 既定のポートサプライヤーと既定のポートを提供します。 カスタムポートを実装する必要がある場合は、カスタムポート供給業者を実装してカスタムポートを提供する必要もあります。  
  
## <a name="see-also"></a>参照  
 [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)   
 [シリアル](../../extensibility/debugger/ports.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
