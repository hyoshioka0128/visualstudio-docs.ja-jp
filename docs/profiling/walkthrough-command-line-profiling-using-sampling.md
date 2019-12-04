---
title: 'チュートリアル: サンプリングを使ったコマンドライン プロファイリング | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, walkthroughs
- performance tools, walkthroughs
- performance tools, command-line tools
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 09272c8cf2dff02d3be024b9c3eeab8b51f56df7
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74777973"
---
# <a name="walkthrough-command-line-profiling-using-sampling"></a>チュートリアル: サンプリングを使ったコマンド ライン プロファイリング

このチュートリアルでは、コマンド ライン ツールを使用したアプリケーションのプロファイリング方法と、パフォーマンス上の問題をサンプリングによって特定する方法について説明します。

このチュートリアルでは、コマンド ライン ツールを使用してマネージド アプリケーションのプロファイリングを行う方法と、サンプリングを使用してアプリケーションのパフォーマンス上の問題を特定および識別する方法の各手順を説明します。

このチュートリアルでは、次の手順を行います。

- コマンド ライン ツールとサンプリングを使用してアプリケーションのプロファイリングを行います。
- サンプリングしたプロファイリング結果を分析して、パフォーマンス上の問題を特定および修正します。

## <a name="prerequisites"></a>必須コンポーネント

- [!INCLUDE[csharp_current_short](../misc/includes/csharp_current_short_md.md)] についての中級レベルの知識
- コマンド ライン ツールの操作についての中級レベルの知識
- [PeopleTrax サンプル](performance-explorer.md)のコピー
- プロファイリングによって得られた情報を操作するには、デバッグ シンボル情報を使用できるようにしておくことをお勧めします。

## <a name="command-line-profiling-using-the-sampling-method"></a>サンプリング メソッドを使用したコマンド ライン プロファイリング

サンプリングとは 1 つのプロファイリング方式で、対象のプロセスを定期的にポーリングしてアクティブな関数を識別します。 結果のデータからは、プロセスがサンプリングされたときに対象の関数が呼び出し履歴の一番上に配置されていた回数がわかります。

> [!NOTE]
> プロファイル ツールへのパスを取得するには、[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)に関する記事をご覧ください。 64 ビット コンピューター上では、64 ビット バージョンのツールと 32 ビット バージョンのツールの両方を使用できます。 プロファイラー コマンド ライン ツールを使用するには、コマンド プロンプト ウィンドウの PATH 環境変数にツールのパスを追加するか、コマンド自体にそれを追加します。

### <a name="to-profile-the-peopletrax-application-by-using-the-sampling-method"></a>サンプリング メソッドを使用して PeopleTrax アプリケーションのプロファイリングを行うには

1. PeopleTrax サンプル アプリケーションをインストールして、リリース バージョンをビルドします。

2. コマンド プロンプト ウィンドウを開いて、ローカル パス環境変数にプロファイリング ツール ディレクトリを追加します。

3. 作業ディレクトリを PeopleTrax バイナリを含むディレクトリに変更します。

4. 次のコマンドを入力し、適切な環境変数を設定します。

    ```cmd
    VSPerfCLREnv /sampleon
    ```

5. *VSPerfCmd.exe* (プロファイラーを制御するコマンド ライン ツール) を実行してプロファイリングを開始します。 次のコマンドにより、アプリケーションとプロファイラーがサンプリング モードで起動します。

    ```cmd
    VsPerfCmd /start:sample /output:PeopleTraxReport.vsp /launch:PeopleTrax.exe
    ```

     プロファイラーのプロセスが開始され、*PeopleTrax.exe* のプロセスにアタッチされます。 プロファイラーのプロセスにより、収集したプロファイリング データのレポート ファイルへの出力が開始されます。

6. **[Get People]** をクリックします。

7. **[ExportData]** をクリックします。

     メモ帳が開かれ、**PeopleTrax** からエクスポートされたデータを含む新しいファイルが表示されます。

8. メモ帳を閉じてから、**PeopleTrax** アプリケーションを閉じます。

9. プロファイラーをシャットダウンします。 次のコマンドを入力します。

    ```cmd
    VSPerfCmd /shutdown
    ```

10. 次のコマンドを使用し、環境変数をリセットします。

    ```cmd
    VSPerfCLREnv /sampleoff
    ```

11. プロファイリング データは .*vsp* ファイルに格納されます。次のいずれかの方法により結果を分析します。

    - Visual Studio IDE で .*vsp* ファイルを開きます。

         または

    - コマンド ライン ツール *VSPerfReport.exe* を使用してコンマ区切り値 (.*csv*) ファイルを生成します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 以外で使用するレポートを生成するには、次のコマンドを使用します。

        ```cmd
        VSPerfReport <dir> PeopleTraxReport.vsp /output:<dir> /summary:all
        ```

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの概要](../profiling/performance-session-overview.md)
[コマンドラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)
[VSPerfCmd](../profiling/vsperfcmd.md)
[サンプリング データ値について](../profiling/understanding-sampling-data-values.md)
[パフォーマンス レポート ビュー](../profiling/performance-report-views.md)
