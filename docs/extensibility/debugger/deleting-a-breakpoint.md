---
title: ブレークポイントを削除する |Microsoft Docs
description: 保留中のブレークポイントが削除されたときに、セッションデバッグマネージャーが保留中のブレークポイントとバインドされているすべてのブレークポイントを削除する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8ebd2922f48a53c371f4930e5de1fd86ed6852a0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99862176"
---
# <a name="deleting-a-breakpoint"></a>ブレークポイントの削除
保留中のブレークポイントを削除するプロセスを次に示します。

## <a name="deletion-process"></a>削除プロセス
 セッションデバッグマネージャー (SDM) は、 [IDebugPendingBreakpoint2::D e)](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) メソッドを呼び出して、保留中のブレークポイントとバインドされているすべてのブレークポイントを削除します。

> [!NOTE]
> [IDebugBoundBreakpoint2::D e)](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)を呼び出すことによって、1つのバインドされたブレークポイントを削除することもできます。

## <a name="see-also"></a>関連項目
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
