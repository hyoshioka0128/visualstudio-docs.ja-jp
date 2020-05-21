---
title: デバッグ中に .NET コードを逆コンパイルする | Microsoft Docs
ms.date: 2/2/2020
ms.topic: conceptual
dev_langs:
- CSharp
helpviewer_keywords:
- decompilation, debugger, exception
- debugging [Visual Studio], decompilation, source not found
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.openlocfilehash: d63c05120842d52dd54359e128d0cc5f2a195817
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508746"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>デバッグ中に .NET アセンブリからソース コードを生成する

.NET アプリケーションをデバッグするときに、自分が持っていないソース コードを見たくなる場合があります。 たとえば、例外で中断したときや、呼び出し履歴を使用してソースの場所に移動するときなどです。

> [!NOTE]
> * ソース コードの生成 (逆コンパイル) は、.NET アプリケーションでのみ使用でき、オープンソースの [ILSpy](https://github.com/icsharpcode/ILSpy) プロジェクトに基づいています。
> * 逆コンパイルは、Visual Studio 2019 16.5 以降でのみ使用できます。
> * アセンブリまたはモジュールに [SuppressIldasmAttribute](https://docs.microsoft.com/dotnet/api/system.runtime.compilerservices.suppressildasmattribute) 属性を適用すると、Visual Studio で逆コンパイルが試みられなくなります。

## <a name="generate-source-code"></a>ソース コードを生成する

デバッグを行っていて、ソース コードが使用できない場合、Visual Studio では、"**ソースが見つからない**" というドキュメントが表示されるか、またはアセンブリのシンボルがない場合は "**シンボルが読み込まれていない**" というドキュメントが表示されます。 どちらのドキュメントにも、現在の場所に対する C# のコードを生成する **[Decompile source code]\(ソース コードを逆コンパイルする\)** オプションがあります。 生成された C# のコードは、他のソース コードと同様に使用できます。 コードの表示、変数の検査、ブレークポイントの設定などを行うことができます。

### <a name="no-symbols-loaded"></a>シンボルが読み込まれていない

次の図は、**シンボルが読み込まれていない**というメッセージです。

![シンボルが読み込まれていないドキュメントのスクリーンショット](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>ソースが見つからない

次の図は、**ソースが見つからない**というメッセージです。

![ソースが見つからないドキュメントのスクリーンショット](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>アセンブリのソースを生成して埋め込む

特定の場所に対するソース コードを生成するだけでなく、特定の .NET アセンブリに対するすべてのソース コードを生成することもできます。 これを行うには、 **[モジュール]** ウィンドウに移動し、.NET アセンブリのコンテキスト メニューから、 **[Decompile source code]\(ソース コードを逆コンパイルする\)** コマンドを選択します。 Visual Studio によってアセンブリのシンボル ファイルが生成され、ソースがシンボル ファイルに埋め込まれます。 後のステップで、埋め込まれたソース コードを[抽出する](#extract-and-view-the-embedded-source-code)ことができます。

![ソースの逆コンパイル コマンドが含まれる、[モジュール] ウィンドウでのアセンブリのコンテキスト メニューのスクリーンショット。](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>埋め込まれたソース コードを抽出して表示する

**[モジュール]** ウィンドウのコンテキスト メニューにある **[Extract Source Code]\(ソース コードの抽出\)** コマンドを使用して、シンボル ファイルに埋め込まれたソース ファイルを抽出できます。

![ソースの抽出コマンドが含まれる、[モジュール] ウィンドウでのアセンブリのコンテキスト メニューのスクリーンショット。](media/decompilation-extract-source-code.png)

抽出されたソース ファイルは、[その他のファイル](../ide/reference/miscellaneous-files.md)としてソリューションに追加されます。 Visual Studio のその他のファイル機能は、既定ではオフになっています。 この機能を有効にするには、 **[ツール]**  >  **[オプション]**  >  **[環境]**  >  **[ドキュメント]**  >  **[その他のファイルをソリューション エクスプローラーに表示する]** チェック ボックスをオンにします。 この機能を有効にしないと、抽出されたソース コードを開くことはできません。

![その他のファイル オプションが有効になっているツールのオプション ページのスクリーンショット。](media/decompilation-tools-options-misc-files.png)

抽出されたソース ファイルは、**ソリューション エクスプローラー**の [その他のファイル] に表示されます。

![[その他のファイル] が含まれるソリューション エクスプローラーのスクリーンショット。](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>既知の制限事項

### <a name="requires-break-mode"></a>中断モードが必要である

逆コンパイルを使用してソース コードを生成できるのは、デバッガーが中断モードになっていて、アプリケーションが一時停止されている場合だけです。 Visual Studio が中断モードになるのは、たとえば、ブレークポイントにヒットしたときや、例外が発生したときです。 **[すべて中断]** コマンド (![[すべて中断] アイコン](media/decompilation-break-all.png)) を使用することで、次のコード実行時に Visual Studio で中断を簡単にトリガーできます。

### <a name="decompilation-limitations"></a>逆コンパイルに関する制限事項

.NET アセンブリで使用される中間形式 (IL) からソース コードを生成するときは、固有の制限がいくつかあります。 そのため、生成されたソース コードは元のソース コードのようには見えません。 異なっているのは、ほとんどが、元のソース コードの情報が実行時に必要のない箇所です。 たとえば、空白文字、コメント、ローカル変数の名前などの情報は、実行時には必要ありません。 生成されたソースは、元のソース コードの代わりとしてではなく、プログラムの実行方法を理解するために使用することをお勧めします。

### <a name="debug-optimized-or-release-assemblies"></a>最適化されたアセンブリまたはリリース アセンブリをデバッグする

コンパイラの最適化を使用してコンパイルされたアセンブリから逆コンパイルされたコードをデバッグする場合、次の問題が発生する可能性があります。
- ブレークポイントは、一致するソースの場所に常にバインドされるとは限りません。
- ステップ実行では、正しい場所に常にステップするとは限りません。
- ローカル変数の名前が正確ではない可能性があります。
- 一部の変数は、評価に使用できない場合があります。

詳細については、GitHub の次のイシューを参照してください: 「[ICSharpCode.Decompiler の VS デバッガーへの統合](https://github.com/icsharpcode/ILSpy/issues/1901)」。

### <a name="decompilation-reliability"></a>逆コンパイルの信頼性

比較的低い割合ではありますが、逆コンパイルの試みが失敗する可能性があります。 これは、ILSpy でのシーケンス ポイントの null 参照エラーが原因です。  これらの問題をキャッチし、逆コンパイルの試行を適切に失敗させることによって、この障害は軽減されています。

詳細については、GitHub の次のイシューを参照してください: 「[ICSharpCode.Decompiler の VS デバッガーへの統合](https://github.com/icsharpcode/ILSpy/issues/1901)」。

### <a name="limitations-with-async-code"></a>非同期コードに関する制限事項

非同期/待機コード パターンが使用されているモジュールの逆コンパイルの結果は、不完全であるか、完全に失敗する可能性があります。 非同期/待機および一時停止ステート マシンの ILSpy による実装は、部分的にのみ実装されています。 

詳細については、GitHub の次のイシューを参照してください: 「[PDB ジェネレーターの状態](https://github.com/icsharpcode/ILSpy/issues/1422)」。

### <a name="just-my-code"></a>マイ コードのみ

[マイ コードのみ (JMC)](https://docs.microsoft.com/visualstudio/debugger/just-my-code) の設定を使用すると、システム、フレームワーク、ライブラリ、その他の非ユーザーの呼び出しを、Visual Studio にステップオーバーさせることができます。 デバッグ セッション中、 **[モジュール]** ウィンドウには、デバッガーでマイ コード (ユーザー コード) として扱われているコード モジュールが表示されます。

最適化されたモジュールまたはリリース モジュールを逆コンパイルすると、非ユーザー コードが生成されます。 たとえば、逆コンパイルされた非ユーザー コードでデバッガーが中断した場合、**ソースなし**ウィンドウが表示されます。 "マイ コードのみ" を無効にするには、 **[ツール]**  >  **[オプション]** (または **[デバッグ]**  >  **[オプション]** ) > **[デバッグ]**  >  **[全般]** に移動し、 **[マイ コードのみを有効にする]** をオフにします。

### <a name="extracted-sources"></a>抽出されたソース

アセンブリから抽出されたソース コードには、次の制限があります。
- 生成されるファイルの名前と場所は構成できません。
- ファイルは一時的なものであり、Visual Studio によって削除されます。
- ファイルは単一のフォルダーに配置され、元のソースで使用されていたフォルダー階層は使用されません。
- 各ファイルのファイル名には、ファイルのチェックサム ハッシュが含まれます。

### <a name="generated-code-is-c-only"></a>C# のコードのみが生成される
逆コンパイルでは、C# のソース コード ファイルのみが生成されます。 他の言語でファイルを生成するオプションはありません。
