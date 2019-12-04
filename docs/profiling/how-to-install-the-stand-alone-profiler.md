---
title: '方法: スタンドアロンのプロファイラーをインストールする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- performance tools, installing stand-alone profiler
- profiling tools, stand-alone profiler
ms.assetid: cae81c95-83cd-4ab6-8a98-84ef977a2f6d
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 05611b74049307fc0d7c038ecdb275f70c983501
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778922"
---
# <a name="how-to-install-the-stand-alone-profiler"></a>方法: スタンドアロンのプロファイラーをインストールする
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE をインストールしなくても実行できるコマンドライン ベースのスタンドアロン プロファイラーを利用できます。 このような状況は、コンピューターに開発環境がインストールされていないときに発生します。 たとえば、本稼働中の Web サーバーには開発環境をインストールするべきではありません。

> [!NOTE]
> スタンドアロン プロファイラーを利用し、ASP.NET Web サイトのパフォーマンス データを集めるときは、[VSPerfCmd](../profiling/vsperfcmd.md) ツールよりも [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) ライン ツールをお勧めします。

### <a name="to-install-the-stand-alone-profiler"></a>スタンドアロンのプロファイラーをインストールするには

1. [Performance Tools for Visual Studio](https://visualstudio.microsoft.com/downloads/?q=performance+tools#performance-tools-for-visual-studio) をダウンロードします。

1. パフォーマンス ツールをダウンロードした場所でスタンドアロン プロファイル インストーラー (*vs_standaloneprofiler.exe*) を探して、それを実行します。

2. *vsintr.exe* と *msdis150.dll* のパスをシステム パスに追加します。

   > [!NOTE]
   > プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

3. コマンド プロンプトで、「**VSInstr**」と入力します。

   > [!NOTE]
   > vsinstr.exe の利用状況情報が表示された場合、すべてが正しく設定されています。 vsinstr.exe またはその依存関係の 1 つが見つからないというエラーが表示された場合、手順 2 のとおりにパスが正しく設定されていることを確認してください。

4. シンボル サーバーを設定します。 **_NT_SYMBOL_PATH** 変数を **symsrv\*symsrv.dll\*c:\localcache\*http://msdl.microsoft.com/download/symbols** に設定してください。

5. システム環境変数を利用してシンボル サーバーを設定したら、新しいコマンド プロンプトでコマンドライン プロファイラー ツールを実行します。 実行後、新しい環境変数が適用されます。 [コマンド プロンプト] ウィンドウで、次のコマンド ラインを入力します。

    **start %COMSPEC%**

   > [!NOTE]
   > シンボル サーバー パッケージの設定方法については、「[方法:Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)」を参照してください。

6. [VSPerfReport](../profiling/vsperfreport.md) ツールを利用し、シンボルをシリアル化してプロファイリング データ ファイル (.vsp) を生成します。 **VSPerfReport /summary:all /packsymbols** スイッチを使用します。 データ ファイルにシンボルが挿入されていない場合、_NT_SYMBOL_PATH 環境変数が設定されていることを確認します。

## <a name="see-also"></a>関連項目
- [コマンド ラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
- [チュートリアル: サンプリングを使ったコマンド ライン プロファイリング](../profiling/walkthrough-command-line-profiling-using-sampling.md)
- [チュートリアル: インストルメンテーションを使ったコマンド ライン プロファイリング](command-line-profiling-of-stand-alone-applications.md)
- [方法: Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)
- [VSPerfReport](../profiling/vsperfreport.md)
