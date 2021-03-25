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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 12e8efc7fc110f3f5c20c92d97cf3692094ef6aa
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055240"
---
# <a name="breakpoint-errors"></a>ブレークポイントエラー
ブレークポイントがコードにバインドしようとして失敗した場合のプロセスを次に示します。

## <a name="troubleshoot-a-breakpoint-error"></a>ブレークポイントエラーのトラブルシューティング

1. デバッグエンジン (DE) は、セッションデバッグマネージャー (SDM) に [IDebugBreakpointErrorEvent2](../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) を送信します。

2. SDM は [IDebugBreakpointErrorEvent2:: GetErrorBreakpoint](../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) (IDebugErrorBreakpoint2 * * `ppErrorBP` ) を呼び出して、エラーのブレークポイントを取得します。

3. SDM は、 [IDebugErrorBreakpoint2:: GetPendingBreakpoint ポイント](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md) を呼び出して、エラーブレークポイントが発生した保留中のブレークポイントを取得します。

4. SDM は [IDebugErrorBreakpoint2:: GetBreakpointResolution](../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md) を呼び出して、エラーブレークポイントのバインドに失敗した理由を取得します。

## <a name="see-also"></a>こちらもご覧ください
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
