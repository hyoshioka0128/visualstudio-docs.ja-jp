---
title: ブレークポイントを削除する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 42cd353c216c21d14c4f6592da809c72acdba664
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841800"
---
# <a name="deleting-a-breakpoint"></a>ブレークポイントの削除
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

保留中のブレークポイントを削除するプロセスを次に示します。  
  
## <a name="deletion-process"></a>削除プロセス  
 セッションデバッグマネージャー (SDM) は、 [IDebugPendingBreakpoint2::D e)](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) メソッドを呼び出して、保留中のブレークポイントとバインドされているすべてのブレークポイントを削除します。  
  
> [!NOTE]
> [IDebugBoundBreakpoint2::D e)](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md)を呼び出すことによって、1つのバインドされたブレークポイントを削除することもできます。  
  
## <a name="see-also"></a>参照  
 [デバッガーのイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
