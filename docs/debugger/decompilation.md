---
title: デバッグ中に .NET コードを逆コンパイルする |Microsoft Docs
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
ms.openlocfilehash: ffd5f2e4bfc13f79b519fbdf9b3cf517793cd324
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091874"
---
# <a name="generate-source-code-from-net-assemblies-while-debugging"></a>デバッグ中に .NET アセンブリからソースコードを生成する

.NET アプリケーションをデバッグするときに、使用していないソースコードを表示することが必要になる場合があります。 たとえば、例外の中断や、呼び出し履歴を使用したソースの場所への移動などです。

> [!NOTE]
> * ソースコードの生成 (ilspy) は .NET アプリケーションでのみ使用でき、オープンソースの[Ilspy](https://github.com/icsharpcode/ILSpy)プロジェクトに基づいています。
> * Ilspy は、Visual Studio 2019 16.5 以降でのみ使用できます。

## <a name="generate-source-code"></a>ソースコードの生成

デバッグ中にソースコードが使用できない場合、Visual Studio では、ソースコードが**見つからない**ことを示すドキュメントが表示されます。また、アセンブリのシンボルがない場合は、[**シンボルが読み込ま**れていません] というドキュメントが表示されます。 どちらのドキュメントにも、現在の場所のC#コードを生成する**逆コンパイルソースコード**オプションがあります。 生成さC#れたコードは、他のソースコードと同様に使用できます。 コードの表示、変数の検査、ブレークポイントの設定などを行うことができます。

### <a name="no-symbols-loaded"></a>シンボルが読み込まれていません

次の図は、**シンボルが読み込まれていない**ことを示しています。

![シンボルが読み込まれていないドキュメントのスクリーンショット](media/decompilation-no-symbol-found.png)

### <a name="source-not-found"></a>ソースが見つかりません

次の図は、"**ソースが見つかりません**" というメッセージを示しています。

![ソースが見つからないドキュメントのスクリーンショット](media/decompilation-no-source-found.png)

## <a name="generate-and-embed-sources-for-an-assembly"></a>アセンブリのソースの生成と埋め込み

特定の場所のソースコードを生成するだけでなく、特定の .NET アセンブリのすべてのソースコードを生成することもできます。 これを行うには、 **[モジュール]** ウィンドウと .net アセンブリのコンテキストメニューから、 **[逆アセンブルソースコード]** コマンドを選択します。 Visual Studio によってアセンブリのシンボルファイルが生成され、そのソースがシンボルファイルに埋め込まれます。 後の手順で、埋め込まれたソースコードを[抽出](#extract-and-view-the-embedded-source-code)できます。

![[モジュール] ウィンドウで、[ソースの逆アセンブル] コマンドを使用してアセンブリコンテキストメニューのスクリーンショットを表示します。](media/decompilation-decompile-source-code.png)

## <a name="extract-and-view-the-embedded-source-code"></a>埋め込みソースコードを抽出して表示する

シンボルファイルに埋め込まれているソースファイルを抽出するには、 **[モジュール]** ウィンドウのコンテキストメニューにある **[ソースコードの抽出]** を使用します。

![[ソースの抽出] コマンドを含む [モジュール] ウィンドウのアセンブリコンテキストメニューのスクリーンショット。](media/decompilation-extract-source-code.png)

抽出されたソースファイルは、[その他のファイル](../ide/reference/miscellaneous-files.md)としてソリューションに追加されます。 その他のファイル機能は、Visual Studio では既定でオフになっています。 この機能を有効にするには、**ツール** > **オプション** > **環境** >  > **ドキュメント** の **ソリューションエクスプローラーのその他のファイルを表示**する チェックボックスをオンにします。 この機能を有効にしないと、抽出されたソースコードを開くことができません。

![[その他のファイル] オプションが有効になっているツールオプションページのスクリーンショット。](media/decompilation-tools-options-misc-files.png)

抽出されたソースファイルは、**ソリューションエクスプローラー**のその他のファイルに表示されます。

![その他のファイルを含むソリューションエクスプローラーのスクリーンショット。](media/decompilation-solution-explorer.png)

## <a name="known-limitations"></a>既知の制限事項

### <a name="requires-break-mode"></a>中断モードが必要です

Ilspy を使用してソースコードを生成することができるのは、デバッガーが中断モードで、アプリケーションが一時停止している場合のみです。 たとえば、ブレークポイントにヒットしたとき、または例外が発生すると、Visual Studio は中断モードに入ります。 **[すべて中断]** コマンドを使用して、次にコードを実行するときに Visual Studio を簡単にトリガーできます (![すべて中断 アイコン](media/decompilation-break-all.png))。

### <a name="decompilation-limitations"></a>Ilspy の制限事項

.NET アセンブリで使用される中間形式 (IL) からソースコードを生成することには、いくつかの固有の制限があります。 そのため、生成されたソースコードは元のソースコードのようには見えません。 ほとんどの相違点は、元のソースコードの情報が実行時に必要ない場所にあります。 たとえば、実行時には、空白、コメント、ローカル変数の名前などの情報は必要ありません。 生成されたソースを使用して、元のソースコードの代わりとしてではなく、プログラムの実行方法を理解することをお勧めします。

### <a name="debug-optimized-or-release-assemblies"></a>最適化またはリリースアセンブリのデバッグ

コンパイラの最適化を使用してコンパイルされたアセンブリからデコンパイルされたコードをデバッグする場合、次の問題が発生する可能性があります。
- ブレークポイントは、常に一致するソーシングの場所にバインドされるとは限りません。
- ステップ実行では、常に正しい場所にステップインするとは限りません。
- ローカル変数の名前が正確でない可能性があります。

詳細については、GitHub の問題に関する IChsarpCompiler を参照してください。[デコンパイラと VS デバッガーの統合](https://github.com/icsharpcode/ILSpy/issues/1901)です。

### <a name="extracted-sources"></a>抽出されたソース

アセンブリから抽出されたソースコードには、次の制限があります。
- 生成されたファイルの名前と場所は構成できません。
- ファイルは一時的なものであり、Visual Studio によって削除されます。
- ファイルは、元のソースが使用されていない1つのフォルダーおよびフォルダー階層に配置されます。
- 各ファイルのファイル名には、ファイルのチェックサムハッシュが含まれています。

### <a name="generated-code-is-c-only"></a>生成されC#たコードのみ
Ilspy では、でC#のみソースコードファイルが生成されます。 他の言語でファイルを生成するオプションはありません。