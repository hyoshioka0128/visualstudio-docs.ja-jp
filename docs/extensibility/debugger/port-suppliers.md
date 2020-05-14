---
title: 港湾サプライヤー |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738296"
---
# <a name="port-suppliers"></a>港湾サプライヤー
デバッガアーキテクチャでは、*ポートサプライヤー*:

- サーバーに含まれ、そのサーバーに要求に応じてポートを提供します。

- 含まれているサーバーにポートを追加したり、ポートを削除したりできます。

- サーバーに提供したすべてのポートを列挙できます。

- レジストリを通じて Visual Studio に登録されている[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)インターフェイスによって表されます。 このインターフェイスは[、GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)を呼び出すことによって取得できます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、デフォルトのポートサプライヤーとデフォルトポートを提供します。 カスタム ポートを実装する必要がある場合は、カスタム ポートサプライヤーも実装して、カスタム ポートを提供する必要があります。

## <a name="see-also"></a>関連項目
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [ポート](../../extensibility/debugger/ports.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)
- [GetPortSupplier](../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
