---
title: 共通言語ランタイムおよび式の評価 |Microsoft Docs
description: 共通言語ランタイムがデバッグエンジンとどのように対話するか、および独自のプログラミング言語を Visual Studio IDE に統合する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], expression evaluation
- expression evaluation, and common language runtime
ms.assetid: b36c1eb5-1aaf-48a6-b287-ee7a273d2b1c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a7c120ac1da59ab86e9419bcb031af46f1b3d900
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96914258"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>共通言語ランタイムおよび式の評価
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 共通言語ランタイム (CLR) を対象とする Visual Basic や C# (C シャープ) などのコンパイラは、後でネイティブコードにコンパイルされる Microsoft 中間言語 (MSIL) を生成します。 CLR には、結果のコードをデバッグするためのデバッグエンジン (DE) が用意されています。 独自のプログラミング言語を Visual Studio IDE に統合する予定がある場合は、MSIL にコンパイルすることを選択できます。そのため、独自の DE を記述する必要はありません。 ただし、プログラミング言語のコンテキスト内で式を評価できる式エバリュエーター (EE) を作成する必要があります。

## <a name="discussion"></a>ディスカッション
 通常、コンピューターの言語式は、データオブジェクトのセットとそれらを操作するために使用される一連の演算子を生成するために解析されます。 たとえば、式 "A + B" を解析して、加算演算子 (+) をデータオブジェクト "A" と "B" に適用すると、別のデータオブジェクトが生成される可能性があります。 データオブジェクト、演算子、およびそれらの関連付けの合計セットは、多くの場合、プログラムではツリーとして表され、ツリーのノードと分岐のデータオブジェクトには演算子があります。 ツリー形式に分類された式は、多くの場合、解析されたツリーと呼ばれます。

 式が解析されると、各データオブジェクトを評価するためにシンボルプロバイダー (SP) が呼び出されます。 たとえば、"A" が2つ以上の方法で定義されている場合、 の値を確かめるする前に、応答する必要があります。 SP によって返される応答は、"5 番目のスタックフレームの3番目の項目" または "このメソッドに割り当てられた静的メモリの先頭を超える50バイトの A" のようになります。

 CLR コンパイラでは、プログラム自体の MSIL を作成するだけでなく、プログラムデータベース (*.pdb*) ファイルに書き込まれる、非常にわかりやすいデバッグ情報を生成することもできます。 独自言語コンパイラが CLR コンパイラと同じ形式でデバッグ情報を生成する限り、CLR の SP はその言語の名前付きデータオブジェクトを識別できます。 名前付きデータオブジェクトが識別されると、EE はバインダーオブジェクトを使用して、そのオブジェクトの値を保持するメモリ領域にデータオブジェクトを関連付け (またはバインド) します。 その後、DE は、データオブジェクトの新しい値を取得または設定できます。

 独自のコンパイラは、 `ISymbolWriter` (名前空間の .NET Framework で定義されている) インターフェイスを呼び出すことによって CLR デバッグ情報を提供でき `System.Diagnostics.SymbolStore` ます。 MSIL にコンパイルし、これらのインターフェイスを使用してデバッグ情報を記述することにより、独自のコンパイラで CLR DE と SP を使用できます。 これにより、独自の言語を Visual Studio IDE に統合する作業が大幅に簡素化されます。

 CLR DE が式を評価するために独自の EE を呼び出すと、DE は、インターフェイスを持つ EE を SP とバインダーオブジェクトに提供します。 したがって、CLR ベースのデバッグエンジンを作成するには、適切な式エバリュエーターインターフェイスを実装するだけで済みます。CLR はバインドとシンボルの処理を自動的に行います。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
