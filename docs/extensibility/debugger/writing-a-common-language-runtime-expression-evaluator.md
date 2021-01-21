---
title: 共通言語ランタイム式エバリュエーター | を記述するMicrosoft Docs
description: デバッグ対象のコード言語で式を評価する共通言語ランタイムの式エバリュエーターの記述について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- expression evaluators, tutorial
- expression evaluation, samples
- debugging [Debugging SDK], expression evaluators tutorial
ms.assetid: bd79d57f-8e0a-4e14-a417-0b1de28fa1b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1674ae8345873ede5d1b4afb04774d6ed0469b4c
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996319"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>共通言語ランタイムの式エバリュエーターの記述
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) は、デバッグ対象のコードを生成したプログラミング言語の構文とセマンティクスを処理する、デバッグエンジン (DE) の一部です。 式は、プログラミング言語のコンテキスト内で評価される必要があります。 たとえば、一部の言語では、"A + B" という式は "A と B の合計" を意味します。 他の言語では、同じ式が "A または B" を意味する場合があります。 そのため、Visual Studio IDE でデバッグするオブジェクトコードを生成するプログラミング言語ごとに、別の EE を記述する必要があります。

 Visual Studio デバッグパッケージの一部の側面は、プログラミング言語のコンテキストでコードを解釈する必要があります。 たとえば、ブレークポイントで実行が停止した場合、ユーザーが **ウォッチ** ウィンドウに入力したすべての式が評価され、表示される必要があります。 ユーザーは、 **ウォッチ** ウィンドウまたは [ **イミディエイト** ] ウィンドウに式を入力することによって、ローカル変数の値を変更できます。

## <a name="in-this-section"></a>このセクションの内容
 [共通言語ランタイムおよび式の評価](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md) 独自のプログラミング言語を Visual Studio IDE に統合する場合、独自の言語のコンテキスト内で式を評価できる EE を記述することで、デバッグエンジンを記述せずに Microsoft 中間言語 (MSIL) にコンパイルできることについて説明します。

 [式エバリュエーターのアーキテクチャ](../../extensibility/debugger/expression-evaluator-architecture.md) 必須の EE インターフェイスを実装し、共通言語ランタイムシンボルプロバイダー (SP) とバインダーインターフェイスを呼び出す方法について説明します。

 [式エバリュエーターの登録](../../extensibility/debugger/registering-an-expression-evaluator.md) EE が、共通言語ランタイム環境と Visual Studio ランタイム環境の両方を備えたクラスファクトリとして登録する必要があることに注意してください。

 [式エバリュエーターを実装する](../../extensibility/debugger/implementing-an-expression-evaluator.md) 式を評価するプロセスについて説明します。これには、デバッグエンジン (DE)、シンボルプロバイダー (SP)、バインダーオブジェクト、および式エバリュエーター (EE) が含まれます。

 [ローカルの表示](../../extensibility/debugger/displaying-locals.md) 実行が一時停止したときに、デバッグパッケージが DE を呼び出してローカル変数と引数の一覧を取得する方法について説明します。

 [ウォッチウィンドウの式の評価](../../extensibility/debugger/evaluating-a-watch-window-expression.md) Visual Studio のデバッグパッケージが、ウォッチリスト内の各式の現在の値を確認するために DE を呼び出す方法を文書化します。

 [ローカルの値を変更する](../../extensibility/debugger/changing-the-value-of-a-local.md) ローカルのの値を変更するときに、ローカルウィンドウの各行に、ローカルのの名前、型、および現在の値を提供するオブジェクトが関連付けられていることについて説明します。

 [型ビジュアライザーとカスタムビューアーを実装](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md) する型ビジュアライザーおよびカスタムビューアーをサポートするコンポーネントによって実装する必要があるインターフェイスについて説明します。

## <a name="see-also"></a>こちらもご覧ください
 [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
