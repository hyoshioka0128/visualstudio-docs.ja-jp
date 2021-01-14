---
title: デバッグのための言語サービスサポート |Microsoft Docs
description: Visual Studio でのデバッグのサポートを提供する IVsLanguageDebugInfo インターフェイスの言語サービス機能について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c17b11ce3639664a8097abeaa2a2de9a6faaadc7
ms.sourcegitcommit: a436ba564717b992eb1984b28ea0aec801eacaec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2021
ms.locfileid: "98205165"
---
# <a name="language-service-support-for-debugging"></a>デバッグのための言語サービスのサポート
言語サービスは、インターフェイスを介してデバッガーをサポートする機能を提供でき <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo> ます。 これらの機能には、ブレークポイントの検証や、[ **自動変数** ] ウィンドウへの式の一覧の指定が含まれます。

 ただし、言語をデバッグするには、式エバリュエーターが必要です。 式エバリュエーターは、デバッグ中に値を生成する式を評価します。 CLR 式エバリュエーターの実装の詳細については、以下を参照してください。

- [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)

- [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

## <a name="compiler-output"></a>コンパイラの出力
 コンパイラの種類によって、言語のデバッグを実装するために必要なものが決まります。 コンパイラが Windows オペレーティングシステムを対象として .pdb ファイルを書き込む場合は、Visual Studio に統合されているネイティブコードデバッグエンジンを使用してプログラムをデバッグできます。 コンパイラが Microsoft 中間言語 (MSIL) を生成する場合は、マネージコードデバッグエンジンを使用してプログラムをデバッグできます。これは、Visual Studio にも統合されています。 コンパイラが独自のオペレーティングシステムまたは別のランタイム環境を対象としている場合は、独自のデバッグエンジンを作成する必要があります。

 言語のデバッグの実装の詳細については、Visual Studio デバッグ SDK の「 [はじめに](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) 」を参照してください。
