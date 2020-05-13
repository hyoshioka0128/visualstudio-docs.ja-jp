---
title: サーバー ( ビジュアル スタジオ SDK) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 32fdbb5afca40c3b4fced468d2f9ef0ea5226c00
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712893"
---
# <a name="servers-visual-studio-sdk"></a>サーバー (Visual Studio SDK)
デバッガアーキテクチャでは、*サーバ*:

- ポートとポートのサプライヤーのコンテナーであり、ポートとポートサプライヤーをセッションデバッグ マネージャー (SDM) とデバッグ エンジンに通信します。

- 名前で自身を識別し、そのポートとポートのサプライヤーを列挙できます。

- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)インターフェイスによって表され、Visual Studio によってのみ実装されます (実行中の Visual Studio の各インスタンスに対してサーバーのインスタンスが 1 つ)。

## <a name="see-also"></a>関連項目
- [ポート](../../extensibility/debugger/ports.md)
- [港湾サプライヤー](../../extensibility/debugger/port-suppliers.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
