---
title: デバッグ中に .NET コードを逆コンパイルする |マイクロソフトドキュメント
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
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "79508746"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>デバッグ中に .NET アセンブリからソース コードを生成する

NET アプリケーションをデバッグするときに、使用していないソース コードを表示する必要がある場合があります。 たとえば、例外を解除したり、呼び出し履歴を使用してソースの場所に移動したりする場合などです。

> [!NOTE]
> * ソース コードの生成 (逆コンパイル) は、.NET アプリケーションでのみ使用でき、オープンソースの[ILSpy](https://github.com/icsharpcode/ILSpy)プロジェクトに基づいています。
> * 逆コンパイルは、Visual Studio 2019 16.5 以降でのみ使用できます。
> * アセンブリまたはモジュールに[属性を](https://docs.microsoft.com/dotnet/api/system.runtime.compilerservices.suppressildasmattribute)適用すると、Visual Studio が逆コンパイルを試みるのを防ぎます。

## <a name="generate-source-code"></a>ソース コードの生成

デバッグ中にソース コードが使用できない場合、Visual Studio には**ソースが見つかりません**ドキュメントが表示されるか、アセンブリのシンボルがない場合**は、シンボルが読み込まれていません**。 どちらのドキュメントにも、現在の場所の C# コードを生成する **[ソース コードの逆コンパイル**] オプションがあります。 生成された C# コードは、他のソース コードと同様に使用できます。 コードの表示、変数の検査、ブレークポイントの設定などを行うことができます。

### <a name="no-symbols-loaded"></a>シンボルが読み込まれていません

次の図は、**シンボルが読み込まれていないというメッセージを**示しています。

![シンボルが読み込まれていないドキュメントのスクリーンショット](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>ソースが見つかりません

次の図は、**ソースが見つかりません**というメッセージを示しています。

![ソースが見つからないドキュメントのスクリーンショット](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>アセンブリのソースを生成および埋め込む

特定の場所のソース コードを生成するだけでなく、特定の .NET アセンブリのすべてのソース コードを生成できます。 これを行うには、**モジュール**ウィンドウに移動し、.NET アセンブリのコンテキスト メニューから、**ソース コードの逆コンパイル**コマンドを選択します。 Visual Studio は、アセンブリのシンボル ファイルを生成し、ソースをシンボル ファイルに埋め込みます。 後の手順で、埋め込みソース コードを[抽出](#extract-and-view-the-embedded-source-code)できます。

![逆コンパイル ソース コマンドを使用してモジュール ウィンドウでアセンブリコンテキスト メニューのスクリーンショット。](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>埋め込みソース コードを抽出して表示する

シンボル ファイルに埋め込まれたソース ファイルは **、[モジュール]** ウィンドウのコンテキスト メニューの [**ソース コードの抽出**] コマンドを使用して抽出できます。

![ソースの抽出コマンドを使用してモジュール ウィンドウでアセンブリコンテキストメニューのスクリーンショット。](media/decompilation-extract-source-code.png)

抽出されたソース ファイルは、その他の[ファイル](../ide/reference/miscellaneous-files.md)としてソリューションに追加されます。 その他のファイル機能は、Visual Studio では既定でオフになっています。 この機能は、[**ツール** > **オプション** > **環境** > **ドキュメント** > ] ソリューション**エクスプローラーの [その他のファイルを表示**する] チェック ボックスから有効にできます。 この機能を有効にしないと、抽出されたソース コードを開くことができないほどです。

![[その他のファイル] オプションが有効になっているツール オプション ページのスクリーンショット。](media/decompilation-tools-options-misc-files.png)

抽出されたソース ファイルは、**ソリューション エクスプローラー**のその他のファイルに表示されます。

![その他のファイルを含むソリューション エクスプローラーのスクリーンショット。](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>既知の制限事項

### <a name="requires-break-mode"></a>中断モードが必要

逆コンパイルを使用してソース コードを生成できるのは、デバッガーが中断モードで、アプリケーションが一時停止している場合のみです。 たとえば、ブレークポイントまたは例外にヒットすると、Visual Studio は中断モードに入ります。 Visual Studio を起動して、次にコードを実行するときに 、[すべて中断] コマンド![(](media/decompilation-break-all.png) **[すべて壊**す] アイコン ) を使用して、コードを中断することができます。

### <a name="decompilation-limitations"></a>逆コンパイルの制限事項

NET アセンブリで使用される中間形式 (IL) からソース コードを生成する場合は、いくつかの固有の制限があります。 そのため、生成されたソース コードは元のソース コードとは違います。 違いのほとんどは、元のソース コードの情報が実行時に必要とされない場所にあります。 たとえば、空白、コメント、ローカル変数の名前などの情報は実行時に必要ありません。 生成されたソースを使用して、元のソース コードの代わりとしてではなく、プログラムの実行方法を理解することをお勧めします。

### <a name="debug-optimized-or-release-assemblies"></a>デバッグの最適化されたアセンブリまたはリリース アセンブリ

コンパイラの最適化を使用してコンパイルされたアセンブリから逆コンパイルされたコードをデバッグするときに、次の問題が発生する可能性があります。
- ブレークポイントは、一致するソーシング場所に必ずしもバインドされない場合があります。
- ステップ実行は、常に正しい場所にステップインするとは限りません。
- ローカル変数には正確な名前が付いていない可能性があります。
- 一部の変数は、評価に使用できない可能性があります。

詳細については、GitHub の問題を参照してください: [VS デバッガーへの ICSharpCode.デコンパイラの統合](https://github.com/icsharpcode/ILSpy/issues/1901).

### <a name="decompilation-reliability"></a>逆コンパイルの信頼性

逆コンパイルの試行の割合が比較的少ない場合、失敗する可能性があります。 これは、ILSpy のシーケンス ポイントの null 参照エラーが原因です。  これらの問題をキャッチし、デコンパイルの試みを正常に失敗することで、障害を軽減しました。

詳細については、GitHub の問題を参照してください: [VS デバッガーへの ICSharpCode.デコンパイラの統合](https://github.com/icsharpcode/ILSpy/issues/1901).

### <a name="limitations-with-async-code"></a>非同期コードの制限

async/await コード パターンを使用してモジュールを逆コンパイルした結果は、不完全であるか、完全に失敗する可能性があります。 非同期/待機状態マシンと yield 状態マシンの ILSpy 実装は部分的にしか実装されていません。 

詳細については、GitHub の問題を参照してください: [PDB ジェネレーターの状態 。](https://github.com/icsharpcode/ILSpy/issues/1422)

### <a name="just-my-code"></a>マイ コードのみ

[[マイ コードのみの使用] (JMC)](https://docs.microsoft.com/visualstudio/debugger/just-my-code)の設定では、Visual Studio でシステム、フレームワーク、ライブラリ、およびその他の非ユーザー呼び出しをステップ オーバーできます。 デバッグ セッション中に、**モジュール**ウィンドウには、デバッガーがマイ コード (ユーザー コード) として処理しているコード モジュールが表示されます。

最適化モジュールまたはリリースモジュールの逆コンパイルにより、非ユーザー コードが生成されます。 たとえば、逆コンパイルされた非ユーザー コードでデバッガーが中断した場合は、[**ソースなし**] ウィンドウが表示されます。 マイ コードのみを無効にするには、[**ツール** > **オプション]** (または **[デバッグ** > **オプション**] ) > **[デバッグ** > **全般**] に移動し、[マイ**コードのみを有効にする**] の選択を解除します。

### <a name="extracted-sources"></a>抽出されたソース

アセンブリから抽出されたソース コードには、次の制限があります。
- 生成されたファイルの名前と場所は構成できません。
- ファイルは一時的なファイルであり、Visual Studio によって削除されます。
- ファイルは単一のフォルダに配置され、元のソースが持っていたフォルダ階層は使用されません。
- 各ファイルのファイル名には、ファイルのチェックサム ハッシュが含まれています。

### <a name="generated-code-is-c-only"></a>生成されたコードは C# のみです
逆コンパイルでは、C# でソース コード ファイルのみが生成されます。 他の言語でファイルを生成するオプションはありません。
