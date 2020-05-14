---
title: ブレークポイント エラー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, errors
- debugging [Debugging SDK], breakpoint errors
- errors [Debugging SDK]
ms.assetid: 79221c6b-a924-4c8e-a778-e312e4e0c0c8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0766792f19faf7c1933c6576ab41f65ec1b31ae9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739219"
---
# <a name="breakpoint-errors"></a>ブレークポイント エラー
ブレークポイントがコードにバインドしようとして失敗した場合のプロセスを次に示します。

## <a name="troubleshoot-a-breakpoint-error"></a>ブレークポイント エラーのトラブルシューティング

1. デバッグ エンジン (DE) は、セッション デバッグ マネージャー (SDM) に[IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)を送信します。

2. SDM は[、エラー ブレークポイントを取得するために、IDebug ブレークポイントエラーイベント2::GetError ブレークポイント](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)(IDebugErrorBreakpoint2** `ppErrorBP`) を呼び出します。

3. SDM は、エラー ブレークポイントの発生元の保留中のブレークポイントを取得する[IDebugErrorBreakpoint2::GetPending ブレークポイント](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)を呼び出します。

4. SDM は、エラー ブレークポイントのバインドに失敗した理由を取得するのには[、IDebugErrorBreakpoint2:::ブレークポイントの解像度](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
