---
title: R Tools for Visual Studio
description: R Tools for Visual Studio 2017 (RTVS) は無料のオープンソースの拡張機能で、IntelliSense、デバッグ、リモート ワークスぺースを含む多くの言語機能を提供しています。
ms.date: 11/13/2017
ms.topic: overview
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: 89aa8b9d1b1f288e19252b8a111666f5b4e3e087
ms.sourcegitcommit: d8609a78b460d4783f5d59c0c89454910a4dbd21
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88238713"
---
# <a name="work-with-r-in-visual-studio"></a>Visual Studio での R の使用

R は、高い拡張性を備えた、統計コンピューティングおよびグラフィックス用の言語であり環境です。 R は GNU General Public License に基づき無料配布されており、コミュニティの強力なサポートを受けることができます。また、数学記号と式を含むプロットを出版品質で生成できる機能で知られています。 R の詳細については、[r-project.org](https://www.r-project.org/about.html) と「[An Introduction to R (R の概要)](https://cran.r-project.org/doc/manuals/r-release/R-intro.html)」をご覧ください。

R Tools for Visual Studio (RTVS) は Visual Studio 2017 と Visual Studio 2015 Update 3 以降向けの無料の[オープンソース](https://github.com/microsoft/RTVS)拡張機能であり、MIT ライセンスに基づいてリリースされています (R インタープリターのバイナリとリンクする [RHost](https://github.com/microsoft/R-Host) という名前の 2 番目のオープン ソース コンポーネントは、GNU Public License V2 に基づいてリリースされています)。

> [!Note]
> RTVS は現在、Windows 上の Visual Studio 2017 でのみサポートされています。Visual Studio for Mac ではサポートされていません。 Visual Studio 2019 ではまだご利用いただけません。

Visual Studio で R を使用するには、次の手順を実行します。

- [R Tools をインストールします](installing-r-tools-for-visual-studio.md)。
- [作業の開始](getting-started-with-r.md)ガイドのほか、[サンプル](getting-started-samples.md)や[ヘルプ情報の入手方法](getting-started-help.md)に関する記事をご覧ください。

その後、以下のリンクから、R 関連の機能と Visual Studio 自体の一般的な機能の詳細を確認してください。

| 機能 | 説明 | Visual Studio の一般的なドキュメント |
| --- | --- | --- |
| [Visual Studio のプロジェクト システム](r-projects-in-visual-studio.md) | 関連ファイルを使いやすい構造で整理および管理し、R コード、R ドキュメント、R Markdown、SQL クエリ、ストアド プロシージャなどのアイテムに関する便利なテンプレートを活用できます。 [パッケージ マネージャー](r-package-manager-in-visual-studio.md)や [SQL Server integration](integrating-sql-server-with-r.md) も使用できます。  | [Visual Studio のソリューションおよびプロジェクト](../ide/solutions-and-projects-in-visual-studio.md) |
| [ワークスペース](r-workspaces-in-visual-studio.md) | RTVS は、ローカル ワークスペースとリモート ワークスペースへバインド可能です。これにより、ローカルで小規模なデータ セットを使用して R コードを開発してから、クラウドベースのより強力なコンピューター上で大規模なデータ セットを使用して簡単にコードを実行することができます。 | 該当なし |
| [R Tools オプション](options-for-r-tools-in-visual-studio.md) | RTVS のさまざまな側面を制御します。 | [[オプション] ダイアログ ボックス](../ide/reference/options-dialog-box-visual-studio.md) |
| [豊富な編集、IntelliSense、コード スニペット](editing-r-code-in-visual-studio.md) | 構文の色分け、すべてのコードとライブラリ間での [IntelliSense](r-intellisense.md)、コードのフォーマット、シグネチャ ヘルプ、定義への移動、すべての参照の検索、[コード スニペット](code-snippets-for-r.md)などが含まれます。 | [コード エディターの機能](../ide/writing-code-in-the-code-and-text-editor.md) |
| [R Markdown](rmarkdown-with-r-in-visual-studio.md) | R Markdown ドキュメントを使用すると、マークダウン コード ブロック内の統合された R コードを用いてデータの結果を共有できます。 | 該当なし |
| [対話型ウィンドウ](interactive-repl-for-r-in-visual-studio.md) | R で完全な REPL エクスペリエンスを実現でき、対話型ウィンドウでソース ファイルのコードを簡単に実行可能です。 | 該当なし |
| [データの視覚化](visualizing-data-with-r-in-visual-studio.md) | プロットは R を使用する上で不可欠な部分であるため、RTVS では独立した複数のプロット ウィンドウを利用できます。各ウィンドウには、履歴とウィンドウ間のプロットの移動機能が備わっています。 プロットはビットマップ ファイルと PDF ファイルに保存でき、またビットマップやメタファイルとしてクリップボードにコピーすることもできます。  | 該当なし |
| [変数エクスプローラー](variable-explorer.md) | 並べ替え可能なテーブルを表示する機能と CSV へのエクスポート機能を備えており、グローバル スコープ内やパッケージ固有のスコープ内の変数を調査できます。 | 該当なし |
| [フル機能のデバッグ](debugging-r-in-visual-studio.md) | 対話型ウィンドウとの統合などがあります。 | [Visual Studio でのデバッグ](../debugger/debugger-feature-tour.md) |

「[よく寄せられる質問](faq.md)」もご覧ください。

![ビデオのムービー カメラ アイコン](../install/media/video-icon.png "ビデオを見る") R Tools for Visual Studio (12 分 36 秒) の概要について[ビデオ (Youtube.com) を見てください](https://www.youtube.com/watch?v=dll3IS1bfWQ)。 [その他の R Tools ビデオ](https://www.youtube.com/results?search_query=R+Tools+for+visual+studio)も参照してください。

## <a name="send-us-your-feedback"></a>フィードバックをお寄せください。

1. **Github の問題**: RTVS チームへ問い合わせる場合は、[GitHub 上で問題を報告する](https://github.com/Microsoft/RTVS/issues)か、**[R Tools]** > **[フィードバック]** メニューを使用して行ってください。

1. **気に入った機能の報告や問題点、改善点の報告**: **[R Tools]** > **[フィードバック]** メニューから、フィードバックの送信と、問題の診断に役立つ RTVS ログ ファイルの添付を素早く行えます  (ログは、個別に送信できるように *%temp%/RTVSlogs.zip* に書き込まれています)。 **[ヘルプ]**  >  **[フィードバック]**  >  **[設定]** メニュー コマンドから、またはインストール中に [Visual Studio telemetry]\(Visual Studio テレメトリ\) をオフにした場合は、ログ機能が無効になります。

1. **電子メール**: チーム (*rtvsuserfeedback (at) microsoft.com*) 宛にフィードバックを直接送信できます。
