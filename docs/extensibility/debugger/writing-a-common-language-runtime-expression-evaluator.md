---
title: 共通言語ランタイム式エバリュエーターの作成 |マイクロソフトドキュメント
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
ms.openlocfilehash: 4e46eaef395a7c66792662b3c5d4b9fbad419dfb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712321"
---
# <a name="writing-a-common-language-runtime-expression-evaluator"></a>共通言語ランタイム式エバリュエーターの作成
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については[、「CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 式エバリュエーター (EE) は、デバッグ対象のコードを生成したプログラミング言語の構文とセマンティクスを処理するデバッグ エンジン (DE) の一部です。 式は、プログラミング言語のコンテキスト内で評価する必要があります。 たとえば、一部の言語では、"A+B" という表現は "A と B の和" を意味します。 他の言語では、同じ表現が "A または B" を意味する場合があります。 したがって、Visual Studio IDE でデバッグするオブジェクト コードを生成するプログラミング言語ごとに、個別の EE を記述する必要があります。

 Visual Studio デバッグ パッケージの一部の側面では、プログラミング言語のコンテキストでコードを解釈する必要があります。 たとえば、ブレークポイントで実行が停止した場合、ユーザーが**ウォッチ**ウィンドウに入力した式を評価して表示する必要があります。 ユーザーは、**ウォッチ**ウィンドウまたは**イミディエイト**ウィンドウに式を入力して、ローカル変数の値を変更できます。

## <a name="in-this-section"></a>このセクションの内容
 [共通言語ランタイムと式の評価](../../extensibility/debugger/common-language-runtime-and-expression-evaluation.md)独自のプログラミング言語を Visual Studio IDE に統合する場合、独自の言語のコンテキスト内で式を評価できる EE を記述すると、デバッグ エンジンを作成せずに Microsoft 中間言語 (MSIL) にコンパイルできることを説明します。

 [式エバリュエーター アーキテクチャ](../../extensibility/debugger/expression-evaluator-architecture.md)必要な EE インターフェイスを実装し、共通言語ランタイム シンボル プロバイダー (SP) とバインダー インターフェイスを呼び出す方法について説明します。

 [式エバリュエーターの登録](../../extensibility/debugger/registering-an-expression-evaluator.md)EE は、共通言語ランタイムと Visual Studio ランタイム環境の両方でクラス ファクトリとして登録する必要があります。

 [式エバリュエーターの実装](../../extensibility/debugger/implementing-an-expression-evaluator.md)式を評価するプロセスにデバッグ エンジン (DE)、シンボル プロバイダー (SP)、バインダー オブジェクト、および式エバリュエーター (EE) が含まれる方法について説明します。

 [ローカル表示](../../extensibility/debugger/displaying-locals.md)実行が一時停止すると、デバッグ パッケージが DE を呼び出してローカル変数と引数の一覧を取得する方法について説明します。

 [ウォッチ ウィンドウ式を評価する](../../extensibility/debugger/evaluating-a-watch-window-expression.md)Visual Studio デバッグ パッケージが DE を呼び出して、ウォッチ リスト内の各式の現在の値を確認する方法について説明します。

 [ローカルの値を変更する](../../extensibility/debugger/changing-the-value-of-a-local.md)ローカルの値を変更する際に、ローカル ウィンドウの各行に、ローカルの名前、型、および現在の値を提供する関連付けられたオブジェクトがあることを説明します。

 [型ビジュアライザーとカスタム ビューアーを実装する](../../extensibility/debugger/implementing-type-visualizers-and-custom-viewers.md)型ビジュアライザーとカスタム ビューアーをサポートするコンポーネントによって実装する必要があるインターフェイスについて説明します。

## <a name="see-also"></a>関連項目
 [デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
