---
description: 次に示すのは、Visual Studio デバッグ SDK の式評価インターフェイスです。
title: 式の評価インターフェイス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, interfaces
ms.assetid: 2d259f60-2cd7-460e-b02d-24a8fb202850
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d380fcce087fad3dc6b101e78cbc514ba19b1052
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158736"
---
# <a name="expression-evaluation-interfaces"></a>式の評価のインターフェイス
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 デバッグ SDK の式評価インターフェイスを次に示し [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、中断モード中に呼び出し履歴で式を評価するために使用されます。 共通言語ランタイム式エバリュエーター (EE) に対してのみ実装されます。

 表の各インターフェイスには、次の一覧から実装できるコンポーネントが示されています。

- デバッグエンジン (DE)

- 式エバリュエーター (EE)

- Visual Studio (VS)

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)|EE|変数の数値の別名を表します。|
|[IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)|EE|変数の数値の別名を表し、式エバリュエーター (EE) がエイリアスのアプリケーションドメインを取得できるようにします。|
|[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)|EE|配列オブジェクトを表します。|
|[IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)|EE|マネージ配列オブジェクトを表し、式エバリュエーター (EE) が配列のベースインデックス (下限) を決定できるようにします。|
|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)|DE|デバッグシンボルをメモリ内の実際のアドレスにバインドするバインダーを表します。|
|[IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)|DE|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイスと同じですが、型、エイリアス、およびカスタムビジュアライザーへのアクセスを提供します。|
|[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)|EE|式エバリュエーターを表します。|
|[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)|EE|式エバリュエーター (EE) の拡張バージョンを表します。|
|[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)|EE|パーサーツリーが拡張された式エバリュエーター (EE) を表します。|
|[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)|EE|関数を表します。|
|[IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)|EE|関数を表し、 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) インターフェイスを拡張します。|
|[IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)|DE|デバッガーの出力ウィンドウにメッセージを表示する式エバリュエーター (EE) を有効にします。|
|[IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)|EE|マネージコードオブジェクトを表します。|
|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)|EE|メモリアドレスにバインドされている任意のシンボルを表す基本インターフェイス。|
|[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)|EE|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスと同じですが、追加情報へのアクセスを提供します。|
|[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)|EE|評価の準備ができている解析済みの式を表します。|
|[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)|EE|ポインターを表します。|
|[IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)|EE|は、解析ツリー内のポインターを表し、 **IDebugPointerObject** インターフェイスを拡張します。|
|[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)|EE|型ビジュアライザーを使用して型の値を変更する機能を提供します。|
|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)|VS|カスタムビューアーおよび型ビジュアライザーへのアクセスを提供します。|
|[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)|VS|[Ieevisualizerservice](../../../extensibility/debugger/reference/ieevisualizerservice.md)オブジェクトを作成する機能を提供します。|
|[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)|EE|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトのコレクションを表します。|

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [CLR 式エバリュエーターの書き込み](../../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
