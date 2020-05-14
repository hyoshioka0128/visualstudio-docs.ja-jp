---
title: ポート |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738305"
---
# <a name="ports"></a>Port
デバッガアーキテクチャでは、*ポート*:

- サーバー上で実行されている一連のプロセスのコンテナーです。 たとえば、シリアル ケーブルまたはネットワーク接続されていない DCOM マシンへの Windows CE ベースのデバイスへの接続を表すポートがあります。 ローカル ポートと呼ばれる 1 つの特殊ポートには、ローカル マシンで実行されているすべてのプロセスが含まれます。

- 名前または識別子で自分自身を識別できます。

- ポートで実行されているすべてのプロセスを列挙し、これらのプロセスを起動および終了できます。

- [は、IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)インターフェイスによって表され、これは[AddPort](../../extensibility/debugger/reference/idebugportrequest2.md)に引数を渡すことによって作成[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)されます。

  [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、ネイティブとマネージの両方のすべての Windows ベースのプロセスを処理する既定のポートを提供します。 Windows ベースではない外部デバイスとの接続には、カスタム ポートを設定する必要があります。 このようなカスタム ポートを提供するには、カスタム ポート サプライヤーも設定する必要があります。

## <a name="see-also"></a>関連項目
- [サーバー](../../extensibility/debugger/servers-visual-studio-sdk.md)
- [プロセス](../../extensibility/debugger/processes.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
