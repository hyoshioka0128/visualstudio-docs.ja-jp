---
title: Port Supplier の実装と登録 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 377aa88df71fd0d3c42745fe2d3ce3b648191aa4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842112"
---
# <a name="implementing-and-registering-a-port-supplier"></a>ポート サプライヤーの実装および登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ポート供給業者の役割は、ポートを追跡して提供することで、プロセスを管理します。 ポートの作成が必要になった時点で、ポート供給業者の GUID と共に CoCreate を使用してポートサプライヤーがインスタンス化されます (セッションデバッグマネージャー [SDM] は、ユーザーが選択したポート供給業者、またはプロジェクトシステムによって指定されたポート供給元を使用します)。 その後、SDM は [Canaddport](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) を呼び出して、ポートを追加できるかどうかを確認します。 ポートを追加できる場合、 [Addport](../../extensibility/debugger/reference/idebugportsupplier2-addport.md) を呼び出し、ポートを説明する [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md) を渡すことによって、新しいポートが要求されます。 `AddPort` は、 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) インターフェイスによって表される新しいポートを返します。  
  
## <a name="discussion"></a>考察 (Discussion)  
 ポートは、コンピューターまたはデバッグサーバーに関連付けられているポート供給元によって作成されます。 サーバーは、[Enumportsuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md) メソッドを使用してポートサプライヤーを列挙できます。また、ポート供給元は、 [enumports](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md) メソッドを使用してポートを列挙できます。  
  
 一般的な COM の登録に加えて、ポート供給元は、CLSID と名前を特定のレジストリの場所に配置することによって、それ自体を Visual Studio に登録する必要があります。 というデバッグ SDK ヘルパー関数は、 `SetMetric` このような作業を処理します。これは、登録される項目ごとに1回呼び出されます。  
  
```cpp#  
SetMetric(metrictypePortSupplier,  
          <GUID of your port supplier>,  
          metricCLSID,  
          <CLSID of your port supplier>,  
          false,  
          NULL)  
SetMetric(metrictypePortSupplier,  
          <GUID of your port supplier>,  
          metricName,  
          <name of your port supplier>,  
          false,  
          NULL);  
```  
  
 ポートサプライヤーは、 `RemoveMetric` 登録された項目ごとに1回 (別のデバッグ SDK ヘルパー関数) を呼び出すことによって、自身の登録を解除します。  
  
```cpp#  
RemoveMetric(metrictypePortSupplier,  
             <GUID of your port supplier>,  
             metricCLSID,  
             NULL);  
RemoveMetric(metrictypePortSupplier,  
             <GUID of your port supplier>,  
             metricName,  
             NULL);  
```  
  
> [!NOTE]
> [デバッグおよびデバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) `SetMetric` は、 `RemoveMetric` dbgmetric .h で定義され、ad2de にコンパイルされた静的関数です。 、、およびの各 `metrictypePortSupplier` `metricCLSID` `metricName` ヘルパーは、dbgmetric. h でも定義されています。  
  
 ポートサプライヤーは、メソッド [GetPortSupplierName](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md) と [getportsupplierid](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)先を使用して、それぞれの名前と GUID を指定できます。  
  
## <a name="see-also"></a>参照  
 [ポートサプライヤーの実装](../../extensibility/debugger/implementing-a-port-supplier.md)   
 [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [ポート サプライヤー](../../extensibility/debugger/port-suppliers.md)
