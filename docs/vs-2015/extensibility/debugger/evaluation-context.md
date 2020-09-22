---
title: 評価コンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, context
ms.assetid: 008a20c7-1b27-4013-bf96-d6a3f510da02
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7dae6ddcb0c75f0dcbc2207465aed522a4210159
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842225"
---
# <a name="evaluation-context"></a>評価コンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。  
  
 デバッグエンジン (DE) が式エバリュエーター (EE) を呼び出すと、次の表に示すように、 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md) に渡される3つの引数によって、シンボルを検索して評価するためのコンテキストが決定されます。  
  
## <a name="arguments"></a>引数  
  
|引数|説明|  
|--------------|-----------------|  
|`pSymbolProvider`|シンボルを識別するために使用するシンボルハンドラー (SH) を指定する [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) インターフェイス。|  
|`pAddress`|現在の実行ポイントを指定する [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) インターフェイス。 これを使用すると、実行されているコードを含むメソッドを見つけることができます。|  
|`pBinder`|名前を指定してシンボルの値と型を検索するために使用できる [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) インターフェイス。|  
  
 `IDebugParsedExpression::EvaluateSync` 結果の値とその型を表す [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスを返します。  
  
## <a name="see-also"></a>参照  
 [キー式エバリュエーターインターフェイス](../../extensibility/debugger/key-expression-evaluator-interfaces.md)   
 [表示 (ローカルを)](../../extensibility/debugger/displaying-locals.md)   
 [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)   
 [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)   
 [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)
