---
title: ブレークポイント (Visual Studio SDK) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 39c13271bad984291f609ef45505549855bee99f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146428"
---
# <a name="breakpoints-visual-studio-sdk"></a>ブレークポイント (Visual Studio SDK)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ブレークポイントには、保留中、バインド、エラーの3種類があります。  
  
 **保留中のブレークポイント:**  
  
- は、1つまたは複数のプログラムの1つ以上のコードコンテキストにブレークポイントをバインドするために必要なすべての情報を含む抽象化です。 デバッグ中のプログラムによってコードが読み込まれるたびに、デバッグエンジンはすべての保留中のブレークポイントをチェックし、バインドできるかどうかを確認します。  
  
   保留中のブレークポイント自体はコードにバインドされるのではなく、によって収集され、生成されたすべてのバインドされたブレークポイントが含まれていると言います。  
  
- は、 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) インターフェイスによって表されます。  
  
  **バインドされたブレークポイント:**  
  
- は、単一のコードコンテキストに関連付けられた、またはバインドされているブレークポイントの抽象化です。 各バインドされたブレークポイントは、保留中のブレークポイントに応答して生成されます。 ただし、保留中のブレークポイントは、複数のバインドされたブレークポイントを生成できます。  
  
   コードがアンロードされると、バインドされたブレークポイントをバインド解除して破棄できます。  
  
- は、 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md) インターフェイスによって表されます。  
  
  **エラーのブレークポイント:**  
  
- は、保留中のブレークポイントをコードコンテキストにバインドしようとしたときに発生するエラーを記述するための抽象化です。 エラーブレークポイントは、位置またはブレークポイント式自体のエラーのいずれかを示します。 詳細については、「 [ブレークポイントのバインド](../../extensibility/debugger/binding-breakpoints.md)」を参照してください。  
  
   ブレークポイントエラーには、エラーまたは警告のいずれかを指定できます。  
  
- は、 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) インターフェイスによって表されます。  
  
## <a name="see-also"></a>参照  
 [プログラム](../../extensibility/debugger/programs.md)   
 [デバッガーの概念](../../extensibility/debugger/debugger-concepts.md)   
 [コードコンテキスト](../../extensibility/debugger/code-context.md)   
 [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)   
 [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)   
 [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
