---
title: デバッグのための言語サービスサポート |マイクロソフトドキュメント
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
ms.openlocfilehash: 8c80e8e1f584b1728f342cb596b689f6a22c9297
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707428"
---
# <a name="language-service-support-for-debugging"></a>デバッグのための言語サービスのサポート
言語サービスは、インターフェイスを介してデバッガーをサポートする<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo>機能を提供できます。 これらの機能には、ブレークポイントの検証と**Autos**ウィンドウへの式の一覧の指定が含まれます。

 ただし、言語をデバッグするには、式エバリュエーターが必要です。 式エバリュエーターは、デバッグ中に値を生成する式を評価します。 CLR 式エバリュエーターの実装については、次の Web サイトを参照してください。

- [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)

- [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)

## <a name="compiler-output"></a>コンパイラの出力
 コンパイラの種類によって、言語のデバッグを実装するために必要な処理が決まります。 コンパイラが Windows オペレーティング システムを対象とし、.pdb ファイルを書き込む場合は、Visual Studio に統合されたネイティブ コード デバッグ エンジンを使用してプログラムをデバッグできます。 コンパイラが Microsoft 中間言語 (MSIL) を生成する場合は、マネージ コード デバッグ エンジンを使用してプログラムをデバッグできます。 コンパイラが独自のオペレーティング システムまたは別のランタイム環境を対象とする場合は、独自のデバッグ エンジンを記述する必要があります。

 使用言語のデバッグの実装の詳細については、「Visual Studio デバッグ SDK の[概要](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)」を参照してください。
