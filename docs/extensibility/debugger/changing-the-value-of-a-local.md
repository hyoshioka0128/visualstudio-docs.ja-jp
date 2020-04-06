---
title: ローカルの値を変更する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 98e40e4b6ea10bb6ff1242f23f1b6dd83ce0c0cd
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739136"
---
# <a name="change-the-value-of-a-local"></a>ローカルの値を変更する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 **[ローカル**] ウィンドウの値フィールドに新しい値を入力すると、デバッグ パッケージは、型指定された文字列を式エバリュエーター (EE) に渡します。 EE は、単純な値または式を含むことができるこの文字列を評価し、結果の値を関連付けられたローカルに格納します。

 ローカルの値を変更するプロセスの概要を次に示します。

1. ユーザーが新しい値を入力すると、ローカルに関連付けられている[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトで[SetValueAsString](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)を呼び出します。

2. `IDebugProperty2::SetValueAsString` は、以下のタスクを実行します。

   1. 文字列を評価して値を生成します。

   2. 関連付けられた[IDebugField](../../extensibility/debugger/reference/idebugfield.md)オブジェクトをバインドして、[オブジェクト](../../extensibility/debugger/reference/idebugobject.md)を取得します。

   3. 値を一連のバイトに変換します。

   4. [SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md)を呼び出して、デバッグ中のプログラムがアクセスできるように、値のバイト数をメモリに入れます。

3. Visual Studio は **、ローカル**表示を更新します (詳細については、「[ローカルの表示](../../extensibility/debugger/displaying-locals.md)」を参照してください)。

   このプロシージャは、[**ウォッチ]** ウィンドウの変数の値を変更する場合にも使用しますが、`IDebugProperty2`ローカル自体に関連付けられた`IDebugProperty2`オブジェクトの代わりに使用されるローカルの値に関連付けられたオブジェクトです。

## <a name="in-this-section"></a>このセクションの内容
 [変更値の実装例](../../extensibility/debugger/sample-implementation-of-changing-values.md)MyCEE サンプルを使用して、値を変更するプロセスを段階的に実行します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [ローカルの表示](../../extensibility/debugger/displaying-locals.md)
