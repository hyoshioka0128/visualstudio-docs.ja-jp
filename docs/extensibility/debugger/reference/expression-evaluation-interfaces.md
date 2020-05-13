---
title: 式評価インタフェース |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, interfaces
ms.assetid: 2d259f60-2cd7-460e-b02d-24a8fb202850
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: da230a2da87b2dd3e3a85ce3ec6c914e829ccc61
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736945"
---
# <a name="expression-evaluation-interfaces"></a>式の評価のインターフェイス
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 デバッグ SDK の式評価インターフェイスを[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]次に示します。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、中断モード中に呼び出し履歴の式を評価するために使用されます。 共通言語ランタイム式エバリュエーター (EE) に対してのみ実装されます。

 表の各インターフェイスは、次の一覧から実装できるコンポーネントを示しています。

- デバッグ エンジン (DE)

- 式エバリュエーター (EE)

- ビジュアル スタジオ (VS)

|インターフェイス|によって実装される|説明|
|---------------|--------------------|-----------------|
|[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)|EE|変数の数値エイリアスを表します。|
|[IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)|EE|変数の数値エイリアスを表し、式エバリュエーター (EE) がエイリアスのアプリケーション ドメインを取得できるようにします。|
|[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)|EE|配列オブジェクトを表します。|
|[IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)|EE|マネージ配列オブジェクトを表し、式エバリュエーター (EE) が配列のベース インデックス (下限) を決定できるようにします。|
|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)|DE|デバッグ シンボルをメモリ内の実際のアドレスにバインドするバインダーを表します。|
|[IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)|DE|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)インターフェイスと同じですが、型、エイリアス、およびカスタム ビジュアライザーへのアクセスを提供します。|
|[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)|EE|式エバリュエーターを表します。|
|[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)|EE|式エバリュエーター (EE) の拡張バージョンを表します。|
|[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)|EE|拡張パーサー ツリーを使用して式エバリュエーター (EE) を表します。|
|[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)|EE|関数を表します。|
|[IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)|EE|関数を表し、インターフェイスを強化[します](../../../extensibility/debugger/reference/idebugfunctionobject.md)。|
|[IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)|DE|デバッガーの出力ウィンドウにメッセージを表示する式エバリュエーター (EE) を有効にします。|
|[IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)|EE|マネージ コード オブジェクトを表します。|
|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)|EE|メモリ アドレスにバインドされたシンボルを表す基本インターフェイス。|
|[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)|EE|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスと同じですが、追加情報へのアクセスを提供します。|
|[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)|EE|解析済みの式を評価する準備ができていることを表します。|
|[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)|EE|ポインターを表します。|
|[IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)|EE|パース ツリー内のポインターを表し **、IDebugPointerObject**インターフェイスを拡張します。|
|[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)|EE|型ビジュアライザーを使用して型の値を変更する機能を提供します。|
|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)|VS|カスタム ビューアーおよび型ビジュアライザーへのアクセスを提供します。|
|[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)|VS|[IEE ビジュアライザーサービス](../../../extensibility/debugger/reference/ieevisualizerservice.md)オブジェクトを作成する機能を提供します。|
|[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)|EE|オブジェクトのコレクション[を](../../../extensibility/debugger/reference/idebugobject.md)表します。|

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [CLR 式エバリュエーターの書き込み](../../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [型のビジュアライザーとカスタム ビューアー](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
