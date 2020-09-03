---
title: ポートサプライヤー |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers
- debugging [Debugging SDK], port suppliers
ms.assetid: a8f3db96-1a13-4e93-9ef6-0861880369e0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6313a7afce9ed272177a26d8da1a9d1516c8022e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738296"
---
# <a name="port-suppliers"></a>ポートサプライヤー
デバッガーアーキテクチャでは、 *ポート供給業者*は次のようになります。

- はサーバーに含まれており、そのサーバーに要求するポートを提供します。

- 含まれているサーバーのポートを追加および削除できます。

- では、サーバーに提供されたすべてのポートを列挙できます。

- は、 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスによって表されます。これは、レジストリを使用して Visual Studio に登録されます。 このインターフェイスは、 [Getportsupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)を呼び出すことによって取得できます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 既定のポートサプライヤーと既定のポートを提供します。 カスタムポートを実装する必要がある場合は、カスタムポート供給業者を実装してカスタムポートを提供する必要もあります。

## <a name="see-also"></a>関連項目
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [ポート](../../extensibility/debugger/ports.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
