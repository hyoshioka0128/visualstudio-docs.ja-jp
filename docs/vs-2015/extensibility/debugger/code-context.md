---
title: コードコンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d59a4c79cb21386fa6f6e7031404aeb0b435b3b9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197374"
---
# <a name="code-context"></a>コード コンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグでは [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、 **コードコンテキスト**は次のようになります。  
  
- デバッグエンジン (DE) に知られているコード内の位置を抽象化します。 現在、ほとんどのランタイムアーキテクチャでは、コードコンテキストはプログラムの命令ストリームのアドレスと考えることができます。 コードが命令によって表されない nontraditional 言語の場合、コードコンテキストは他の方法で表すことができます。  
  
- デバッグ中のプログラムの実行ストリーム内の現在の位置を記述します。  
  
- プログラムがブレークポイントで停止した場合にのみ存在します。  
  
- ドキュメントコンテキストが関連付けられています。  
  
- は、 [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) インターフェイスによって実装されます。  
  
## <a name="see-also"></a>参照  
 [ドキュメントのコンテキスト](../../extensibility/debugger/document-context.md)   
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
