---
title: 式の評価のコンテキスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- expression evaluation, context
ms.assetid: a2fd3758-09bd-45ae-8ecc-2d276c0036ba
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 377609cb9f971b667872c198a53b45a6288f2c15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152780"
---
# <a name="expression-evaluation-context"></a>式の評価のコンテキスト
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

デバッグでは [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 、 **式の評価コンテキスト**:  
  
- 式の評価のコンテキストを表します。 一般に、評価コンテキストは、変数、パラメーター、関数、およびメソッドを評価する構文のスコープに対応します。 たとえば、スタックフレームに関連付けられている式の評価コンテキストでは、ローカル変数、メソッドパラメーター、およびクラスメンバー (該当する場合) を評価するためのコンテキストが提供されます。  
  
- プログラムがブレークポイントで停止したときに存在します。 式自体は、指定されたコンテキスト内でバインドおよび評価できるように準備された解析済みの式を表すデータ構造体です。  
  
     詳細については、 [Parsetext](../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) メソッドを使用して式を作成します。 式が評価されると、変数または引数の名前と型、およびその値を含む印刷可能な文字列が生成されます。 この文字列は、ウォッチウィンドウまたは IDE の [ローカル] ウィンドウに表示されます。  
  
     `BSTR`と[IDebugExpressionContext2](../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスが指定されている場合、デバッグエンジン (DE) は、式を解析することによって[IDebugExpression2](../../extensibility/debugger/reference/idebugexpression2.md)インターフェイスを作成できます。 インターフェイスが指定され `IDebugExpression2` ている場合、DE は、同期または非同期の式の評価によって値を取得できます。 この値は、変数または引数の名前および型と共に IDE に送信され、表示されます。  
  
## <a name="see-also"></a>参照  
 [式の評価インターフェイス](../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [デバッガー コンテキスト](../../extensibility/debugger/debugger-contexts.md)
