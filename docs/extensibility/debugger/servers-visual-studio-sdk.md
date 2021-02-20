---
title: サーバー (Visual Studio SDK) |Microsoft Docs
description: この記事では、Visual Studio のデバッガーアーキテクチャにおけるサーバーの定義と役割について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- servers, debugging
- debugging [Debugging SDK], servers
ms.assetid: 62236d64-7956-448c-9ac3-5528f3edac1d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d60c214fce57f5958d8b30ca231c3e8a2bc05194
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960807"
---
# <a name="servers-visual-studio-sdk"></a>サーバー (Visual Studio SDK)
デバッガーアーキテクチャでは、 *サーバー* は次のようになります。

- はポートおよびポートサプライヤーのコンテナーであり、ポートとポートサプライヤーをセッションデバッグマネージャー (SDM) およびデバッグエンジンに伝えます。

- では、名前によって自身を識別し、そのポートとポートサプライヤーを列挙できます。

- は、 [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md) インターフェイスによって表されます。これは、visual studio (を実行している visual studio のインスタンスごとにサーバーの1つのインスタンス) によってのみ実装されます。

## <a name="see-also"></a>関連項目
- [ポート](../../extensibility/debugger/ports.md)
- [ポートサプライヤー](../../extensibility/debugger/port-suppliers.md)
- [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)
- [IDebugCoreServer2](../../extensibility/debugger/reference/idebugcoreserver2.md)
