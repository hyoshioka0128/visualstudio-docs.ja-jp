---
title: ブレークポイントのエラー |Microsoft Docs
description: ブレークポイントがコードにバインドしようとして失敗し、ブレークポイントエラーのトラブルシューティングを行う方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 88a5003ce8abe79fcba9f9604047d2265810fda2
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914492"
---
# <a name="breakpoint-errors"></a>ブレークポイントエラー
ブレークポイントがコードにバインドしようとして失敗した場合のプロセスを次に示します。

## <a name="troubleshoot-a-breakpoint-error"></a>ブレークポイントエラーのトラブルシューティング

1. デバッグエンジン (DE) は、セッションデバッグマネージャー (SDM) に [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) を送信します。

2. SDM は [IDebugBreakpointErrorEvent2:: GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2 * * `ppErrorBP` ) を呼び出して、エラーのブレークポイントを取得します。

3. SDM は、 [IDebugErrorBreakpoint2:: GetPendingBreakpoint ポイント](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md) を呼び出して、エラーブレークポイントが発生した保留中のブレークポイントを取得します。

4. SDM は [IDebugErrorBreakpoint2:: GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) を呼び出して、エラーブレークポイントのバインドに失敗した理由を取得します。

## <a name="see-also"></a>関連項目
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
