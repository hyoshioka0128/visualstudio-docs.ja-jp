---
title: ポート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 73003e00fef5c37db4a702e7a4a1121600673844
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153697"
---
# <a name="ports"></a>ポート
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッガーのアーキテクチャに関して、 **ポート**は次のようになります。  
  
- は、サーバーで実行されている一連のプロセスのコンテナーです。 たとえば、ポートは、シリアルケーブル、またはネットワークに Windows CE 接続されていない非 DCOM マシンへの接続を表す場合があります。 ローカルポートと呼ばれる1つの特殊なポートには、ローカルコンピューター上で実行されているすべてのプロセスが含まれます。  
  
- では、名前または識別子を使用して自身を識別できます。  
  
- では、ポートで実行されているすべてのプロセスを列挙し、それらのプロセスを起動して終了できます。  
  
- は、 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスによって表されます。これは、 [Addport](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)に[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)引数を渡すことによって作成されます。  
  
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Windows ベースのすべてのプロセス (ネイティブおよびマネージ) を処理する既定のポートを提供します。 Windows ベースではない外部デバイスとの接続には、カスタムポートを実装する必要があります。 このようなカスタムポートを提供するには、カスタムポート供給業者も実装する必要があります。  
  
## <a name="see-also"></a>参照  
 [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)   
 [プロセス](../../extensibility/debugger/processes.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)   
 [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)   
 [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
