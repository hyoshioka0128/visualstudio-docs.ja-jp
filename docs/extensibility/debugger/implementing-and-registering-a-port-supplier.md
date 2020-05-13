---
title: ポートサプライヤーの実装と登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], registering port suppliers
- port suppliers, registering
ms.assetid: fb057052-ee16-4272-8e16-a4da5dda0ad4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: efa9cdd8740648b66fe7190177b5fe769c4b2539
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738536"
---
# <a name="implement-and-register-a-port-supplier"></a>ポート サプライヤーの実装と登録
ポートサプライヤーの役割は、ポートを追跡して供給し、プロセスを管理することです。 ポートを作成する必要がある場合、ポート サプライヤーは、ポート サプライヤーの GUID を使用して CoCreate を使用してインスタンス化されます (セッション デバッグ マネージャー [SDM] は、ユーザーが選択したポート サプライヤーまたはプロジェクト システムで指定されたポート サプライヤーを使用します)。 SDM は[、次に CanAddPort](../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)を呼び出して、ポートを追加できるかどうかを確認します。 ポートを追加できる場合は[、AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)を呼び出して、ポートを記述する[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)を渡すことによって、新しいポートが要求されます。 `AddPort`[は、IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスで表される新しいポートを返します。

## <a name="discussion"></a>ディスカッション
 ポートは、マシンまたはデバッグ サーバーに関連付けられているポート サプライヤーによって作成されます。 サーバーは、そのポートサプライヤーを列挙する、[EnumPortSuppliers](../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)メソッド、およびポートサプライヤーは[、その](../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)ポートを列挙するメソッドを使用して、そのポートです。

 一般的な COM 登録に加えて、ポートサプライヤーは、特定のレジストリの場所に CLSID と名前を配置することによって、Visual Studio に登録する必要があります。 デバッグ SDK ヘルパー関数`SetMetric`は、この雑用を処理します: 登録する各項目に対して 1 回呼び出されます。

```cpp
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

 ポートサプライヤーは、登録された項目ごとに1`RemoveMetric`回呼び出すことによって登録を解除します(別のデバッグSDKヘルパー関数)。

```cpp
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
> `SetMetric`[デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)であり *、dbgmetric.h*`RemoveMetric`で定義され *、ad2de.lib*にコンパイルされた静的関数です。 ヘルパー `metrictypePortSupplier` `metricCLSID`、 `metricName` 、およびヘルパーは*dbgmetric.h*でも定義されます。

 ポートサプライヤーは、それぞれメソッド[を](../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)通じてその[名前と](../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)GUID を指定できます。

## <a name="see-also"></a>関連項目
- [ポート サプライヤーの実装](../../extensibility/debugger/implementing-a-port-supplier.md)
- [デバッグ用の SDK ヘルパー](../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [港湾サプライヤー](../../extensibility/debugger/port-suppliers.md)
