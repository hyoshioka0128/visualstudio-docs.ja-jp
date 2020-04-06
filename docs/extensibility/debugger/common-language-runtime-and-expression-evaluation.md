---
title: 共通言語ランタイムと式の評価 |マイクロソフトドキュメント
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
ms.openlocfilehash: 013579473189dd9310501b76d2de0d5cf6fa5822
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739113"
---
# <a name="common-language-runtime-and-expression-evaluation"></a>共通言語ランタイムと式の評価
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 」および「[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 共通言語ランタイム (CLR) を対象とする Visual Basic や C# (C-sharp と発音) などのコンパイラは、後でネイティブ コードにコンパイルされる Microsoft 中間言語 (MSIL) を生成します。 CLR には、結果のコードをデバッグするためのデバッグ エンジン (DE) が用意されています。 独自のプログラミング言語を Visual Studio IDE に統合する場合は、MSIL にコンパイルすることを選択できるため、独自の DE を記述する必要はありません。 ただし、プログラミング言語のコンテキスト内で式を評価できる式エバリュエーター (EE) を記述する必要があります。

## <a name="discussion"></a>ディスカッション
 コンピュータ言語の式は、一般に解析されて、データ オブジェクトのセットと、それらを操作するために使用される一連の演算子を生成します。 たとえば、式 "A+B" を解析して、加算演算子 (+) をデータ オブジェクト "A" と "B" に適用すると、別のデータ オブジェクトが生成される可能性があります。 データ オブジェクト、演算子、およびそれらの関連付けの集合の合計は、ツリーのノードの演算子と分岐のデータ オブジェクトを使用して、プログラムでツリーとして表されることがよくあります。 ツリー形式に分割された式は、解析されたツリーと呼ばれることがよくあります。

 式が解析されると、各データ オブジェクトを評価するためにシンボル プロバイダー (SP) が呼び出されます。 たとえば、"A" が複数のメソッドで定義されている場合、"A" という質問は"A" と表示されます。 A の値を確認する前に、回答を得る必要があります。 SP が返す答えは、「5 番目のスタック フレームの 3 番目の項目」または"A は、このメソッドに割り当てられた静的メモリの先頭を 50 バイト超えています" などのものです。

 CLR コンパイラは、プログラム自体の MSIL を生成するだけでなく、プログラム の DataBase (*.pdb*) ファイルに書き込まれる非常に記述的なデバッグ情報を生成することもできます。 独自言語コンパイラが CLR コンパイラと同じ形式でデバッグ情報を生成する限り、CLR の SP はその言語の名前付きデータ オブジェクトを識別できます。 名前付きデータ オブジェクトが識別されると、EE はバインダー オブジェクトを使用して、そのオブジェクトの値を保持するメモリ領域にデータ オブジェクトを関連付ける (またはバインド) します。 DE は、データ オブジェクトの新しい値を取得または設定できます。

 独自のコンパイラは、`ISymbolWriter`インターフェイス ( 名前空間`System.Diagnostics.SymbolStore`の .NET Framework で定義されている ) を呼び出すことによって、CLR デバッグ情報を提供できます。 MSIL にコンパイルし、これらのインターフェイスを通じてデバッグ情報を書き込むと、独自のコンパイラは CLR DE と SP を使用できます。 これにより、独自の言語を Visual Studio IDE に統合する作業が大幅に簡略化されます。

 CLR DE が式を評価するために独自の EE を呼び出すと、DE は SP とバインダー オブジェクトへのインターフェイスを EE に提供します。 したがって、CLR ベースのデバッグ エンジンを記述すると、適切な式エバリュエーター インターフェイスを実装するだけで済みます。CLR がバインディングとシンボル処理を処理します。

## <a name="see-also"></a>関連項目
- [CLR 式エバリュエーターを記述する](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
