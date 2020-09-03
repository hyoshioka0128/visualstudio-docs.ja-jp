---
title: ポート |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports
- debugging [Debugging SDK], ports
ms.assetid: 1d7f3aa7-7eff-4cab-bc53-0a566b1a9363
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7b42e7fa97c12afa07923e99d8b084840ee7ccad
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738305"
---
# <a name="ports"></a>ポート
デバッガーアーキテクチャでは、 *ポート*は次のようになります。

- は、サーバーで実行されている一連のプロセスのコンテナーです。 たとえば、ポートは、シリアルケーブルまたはネットワークに接続されていない非 DCOM マシンへの、Windows CE ベースのデバイスへの接続を表します。 ローカルポートと呼ばれる1つの特殊なポートには、ローカルコンピューター上で実行されているすべてのプロセスが含まれます。

- では、名前または識別子を使用して自身を識別できます。

- では、ポートで実行されているすべてのプロセスを列挙し、それらのプロセスを起動して終了できます。

- は、 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスによって表されます。これは、 [Addport](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)に[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)引数を渡すことによって作成されます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ネイティブとマネージの両方の Windows ベースのプロセスを処理する既定のポートを提供します。 Windows ベースではない外部デバイスとの接続には、カスタムポートを設定する必要があります。 このようなカスタムポートを指定するには、カスタムポート供給業者もセットアップする必要があります。

## <a name="see-also"></a>関連項目
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [処理](../../extensibility/debugger/processes.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
