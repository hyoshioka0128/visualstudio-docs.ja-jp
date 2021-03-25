---
title: ローカル | の値を変更するMicrosoft Docs
description: '[ローカル] ウィンドウの [値] フィールドに新しい値が入力されたときに、ローカルの値を変更するプロセスについて説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, changing values programmatically
ms.assetid: 8407d3df-d38a-4328-82d1-98084bef43ec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d8baac2f0e288e9bde1288ed72e43d7f1d150d04
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055077"
---
# <a name="change-the-value-of-a-local"></a>ローカルの値を変更する
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 [ **ローカル** ] ウィンドウの [値] フィールドに新しい値が入力されると、デバッグパッケージは、式エバリュエーター (EE) に文字列を渡します。 EE はこの文字列を評価します。この文字列には、単純な値または式のいずれかを含めることができ、結果の値は、関連付けられたローカルに格納されます。

 次に、ローカルのの値を変更するプロセスの概要を示します。

1. ユーザーが新しい値を入力すると、Visual Studio はローカルに関連付けられている[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトで[Setvalueasstring](../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)を呼び出します。

2. `IDebugProperty2::SetValueAsString` では次のタスクを実行します。

   1. 文字列を評価して値を生成します。

   2. 関連付けられている [IDebugField](../../extensibility/debugger/reference/idebugfield.md) オブジェクトをバインドして、 [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) オブジェクトを取得します。

   3. 値を一連のバイトに変換します。

   4. は [SetValue](../../extensibility/debugger/reference/idebugobject-setvalue.md) を呼び出して値のバイトをメモリに格納し、デバッグ中のプログラムがアクセスできるようにします。

3. Visual Studio は **ローカル** 表示を更新します (詳細については、「 [ローカル](../../extensibility/debugger/displaying-locals.md) の表示」を参照してください)。

   このプロシージャは、 **ウォッチ** ウィンドウで変数の値を変更するためにも使用され `IDebugProperty2` ます。ただし、ローカルに関連付けられているオブジェクトの代わりに使用されるローカルの値に関連付けられたオブジェクトである点が異なり `IDebugProperty2` ます。

## <a name="in-this-section"></a>このセクションの内容
 [値の変更の実装例](../../extensibility/debugger/sample-implementation-of-changing-values.md) MyCEE サンプルを使用して、値を変更するプロセスを段階的に実行します。

## <a name="see-also"></a>こちらもご覧ください
- [CLR 式エバリュエーターの記述](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [表示 (ローカルを)](../../extensibility/debugger/displaying-locals.md)
