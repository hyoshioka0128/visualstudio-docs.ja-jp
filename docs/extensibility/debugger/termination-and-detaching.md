---
title: 終了とデタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b88255d618ce42fa55d878f192d31523ba3f83b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712488"
---
# <a name="termination-and-detaching"></a>終了とデタッチ
次のセクションでは、通常の終了について説明します。

## <a name="discussion"></a>ディスカッション
 [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)または[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)インターフェイスが続行された後、デバッグするアプリケーションにブレークポイント、例外、ランタイム エラー、または無限ループがない場合、デバッグ中のプログラムは完了まで実行されます。 このプロセスは正常終了です。

 通常の終了を実装するには[、IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)を送信する必要があります。 通常の終了には、メソッドを実行[する必要があります](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)。

## <a name="see-also"></a>関連項目
- [カスタム デバッグ エンジンの作成](../../extensibility/debugger/creating-a-custom-debug-engine.md)
