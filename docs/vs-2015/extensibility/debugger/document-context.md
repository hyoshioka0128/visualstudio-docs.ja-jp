---
title: ドキュメントコンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 8e8b5702-5c16-4988-953d-69dd807d8b84
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3034c9ca02fca8e91eb1aa5e4d0eb5a2fe1f773f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200583"
---
# <a name="document-context"></a>ドキュメント コンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグでは [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、 **ドキュメントコンテキスト**は次のようになります。  
  
- ソースファイル内の位置を表します。 ソースファイルが存在しない可能性がある言語の場合、ドキュメントコンテキストは、通常、ランタイム環境によって生成されるドキュメント内の位置を識別します。 たとえば、スクリプトエンジンは、スクリプトからドキュメントを生成する場合があります。 詳細については、「 [ドキュメントの位置](../../extensibility/debugger/document-position.md)」を参照してください。  
  
- コードコンテキストに対応するソースドキュメント内の位置を記述します。 シンボルハンドラーは、コンパイラまたはインタープリターによって生成された情報を使用して、コードコンテキストをドキュメントコンテキストにマップします。  
  
- は、 [IDebugDocumentContext2](../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスによって実装されます。  
  
## <a name="see-also"></a>参照  
 [コードコンテキスト](../../extensibility/debugger/code-context.md)   
 [シンボルプロバイダー](../../extensibility/debugger/symbol-provider.md)   
 [シンボルプロバイダーインターフェイス](../../extensibility/debugger/reference/symbol-provider-interfaces.md)   
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
