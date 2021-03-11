---
description: Visual Studio 統合開発環境 は、コードの編集、デバッグ、テストを行ってから、アプリを発行するために使用できる、Python (およびその他の言語) 用のクリエイティブなランチパッドです。
title: Python 開発者向けの Visual Studio の概要
titleSuffix: ''
ms.date: 03/13/2019
ms.topic: overview
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
dev_langs:
- Python
ms.workload:
- python
- data-science
ms.openlocfilehash: 7e4a0c227f8c833febf20ed4e8dba82b814e3223
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223785"
---
# <a name="welcome-to-the-visual-studio-ide--python"></a>Visual Studio IDE へようこそ | Python

Visual Studio *統合開発環境* は、コードの編集、デバッグ、テストを行ってから、アプリを発行するために使用できる、Python (およびその他の言語) 用のクリエイティブなランチパッドです。 統合開発環境 (IDE) は、ソフトウェア開発の多くの側面で使用できる機能を豊富に備えたプログラムです。 大部分の IDE が備える標準的なエディターおよびデバッガーに加え、Visual Studio にはコード補完ツール、対話型 REPL 環境など、ソフトウェア開発プロセスを容易にする機能が含まれています。

[![Python プロジェクトを示す Visual Studio](media/tour-ide-overview.png)](media/tour-ide-overview.png#lightbox)

これは Python プロジェクトを開いている状態の Visual Studio の画像です。使用頻度の高い主なツール ウィンドウがいくつか開かれています。

- [**ソリューション エクスプローラー**](../ide/solutions-and-projects-in-visual-studio.md) (右上) では、コード ファイルを表示、移動、および管理できます。 **ソリューション エクスプローラー** では、ファイルを [ソリューションやプロジェクト](../get-started/tutorial-projects-solutions.md)にまとめ、コードを整理できます。
  - **ソリューション エクスプローラー** と共に [**Python 環境**](managing-python-environments-in-visual-studio.md)を使用することで、コンピューター上にインストールされているさまざまな Python インタープリターを管理することができます。

  ::: moniker range=">=vs-2019"
  - Visual Studio のプロジェクト ファイルとソリューション ファイルを作成することなく、フォルダー内の Python コードを開いて実行することもできます。 詳細については、[クイック スタート:フォルダー内の Python コードを開いて実行する](quickstart-05-python-visual-studio-open-folder.md)」をご覧ください。
  ::: moniker-end

- 大部分の時間を費やすことになる[エディター ウィンドウ](../ide/writing-code-in-the-code-and-text-editor.md) (中央) にはファイルの内容が表示されます。 これは、[Python コードを編集](editing-python-code-in-visual-studio.md)し、コードの構造内を移動し、デバッグ セッション中にブレークポイントを設定する場所です。 Python では、コードを選択し、Ctrl + Enter キーを押して[対話型 REPL ウィンドウ](python-interactive-repl-in-visual-studio.md)でそのコードを実行することもできます。

- [[出力] ウィンドウ](../ide/reference/output-window.md) (下中央) には、デバッグ メッセージ、エラー メッセージ、警告、公開状態メッセージなど、Visual Studio の通知が出力されます。 メッセージ ソースごとに独自のタブがあります。
  - [Python の対話型 REPL ウィンドウ](python-interactive-repl-in-visual-studio.md)は、[出力] ウィンドウと同じ領域に表示されます。

- [チーム エクスプローラー](/azure/devops/user-guide/work-team-explorer?view=vsts&preserve-view=true) (右下) では、[Git](https://git-scm.com/) や [Team Foundation バージョン管理 (TFVC)](/azure/devops/repos/tfvc/overview?view=vsts&preserve-view=true) などのバージョン管理テクノロジを使用して、作業項目を追跡し、コードを他のユーザーと共有できます。

## <a name="editions"></a>エディション

Visual Studio は Windows と Mac で使用できますが、Python のサポートを利用できるのは Visual Studio for Windows でのみとなります。

Windows 向けには、Community、Professional、Enterprise という 3 つのエディションの Visual Studio 2017 があります。 各エディションでサポートされている機能については、[Visual Studio IDE の比較](https://visualstudio.microsoft.com/vs/compare/)に関するページを参照してください。

## <a name="popular-productivity-features"></a>よく使われる生産性機能

ソフトウェアを開発する際に、生産性を高めるために Visual Studio でよく使われる機能のいくつかを以下に示します。

- [IntelliSense](editing-python-code-in-visual-studio.md#intellisense)

   IntelliSense は、コードに関する情報をエディターに直接表示したり、場合によっては、ちょっとしたコードを自動的に作成したりする機能のセットを表す用語です。 エディター内のインラインに基本ドキュメントがあるようなもので、これによって、他の場所で型情報を検索する手間が省けます。 IntelliSense 機能は言語によって異なります。[Python コードの編集](editing-python-code-in-visual-studio.md#intellisense)に関する記事に Python の詳細が示されています。 次の図は、IntelliSense によって型のメンバー リストがどのように表示されるかを示したものです。

   ![Visual Studio IntelliSense のメンバー入力候補](media/code-editing-completions-simple.png)

- [リファクタリング](refactoring-python-code.md)

   コードの一部を右クリックし、 **[クイック アクションとリファクタリング]** を選択すると、Visual Studio で、変数の名前をインテリジェントに変更する、1 つまたは複数のコード行を新しいメソッドに抽出する、メソッド パラメーターを並べ替える、などの操作が提供されます。

   ![Visual Studio でのリファクタリング](media/tour-ide-refactor-extract-method.png)

- [Lint](refactoring-python-code.md)

   lint では、Python コードでエラーおよび一般的な問題が確認され、適切な Python コード パターンが推奨されます。

   ![Python プロジェクトのコンテキスト メニューに表示された PyLint コマンド](media/code-pylint-command.png)

- 検索ボックス

   Visual Studio には非常に多くのメニュー、オプション、およびプロパティがあるため、手に負えないもののように思える場合があるかもしれません。 検索ボックスは、Visual Studio 内で必要な情報を迅速に見つけるのに役立ちます。 探しているものを表す名前の入力を開始すると、Visual Studio に結果がリストされ、目的の場所に正確に移動できます。 Visual Studio に機能を追加する必要がある場合 (追加のプログラミング言語に対してサポートを追加するなど)、検索ボックスの結果として、ワークロードまたは個々のコンポーネントをインストールするための Visual Studio インストーラーが開かれます。

   ![Visual Studio 内の検索ボックス](media/tour-ide-quick-launch.png)

- 波線と[クイック アクション](../ide/quick-actions.md)

   波線は波打った下線で、コード入力時にエラーや潜在的な問題を警告します。 このような視覚的な手がかりを利用することにより、ビルド中またはプロフラム実行時にエラーが検出されるのを待たなくても問題をすぐに修正することができます。 波線の上に移動すると、エラーに関する追加情報が表示されます。 電球とエラーを修正する方法 (クイック アクションとして知られている) が左余白に表示される場合もあります。

   ![Visual Studio での波線](media/tour-ide-squiggles.png)

- [[定義に移動] と [定義をここに表示]](../ide/go-to-and-peek-definition.md)

   **[定義に移動]** 機能では、関数または型が定義されている場所に直接移動できます。 **[定義をここに表示]** コマンドでは、別のファイルを開かずに、ウィンドウに定義が表示されます。 **[すべての参照の検索]** コマンドでは、特定の識別子の定義場所と使用場所の両方を検出するのに役立つ方法も提供されます。

   ![コード ナビゲーション コマンド](media/tour-ide-navigation-commands.png)

## <a name="powerful-features-for-python"></a>Python 用の強力な機能

::: moniker range=">=vs-2019"
- [プロジェクトを使わないでコードを実行する](quickstart-05-python-visual-studio-open-folder.md)

    Visual Studio 2019 以降では、コードに対する Visual Studio プロジェクトを作成しなくても、Python コードが含まれるフォルダーを開き、IntelliSense やデバッグなどの機能を利用することができます。
::: moniker-end

- [Visual Studio を使用して共同作業する](/visualstudio/liveshare/)

    Visual Studio Live Share を使うと、使っているプログラミング言語や構築しているアプリの種類に関係なく、リアルタイムで他のユーザーと共同で編集したりデバッグしたりできます。

- [Python 対話型 REPL](python-interactive-repl-in-visual-studio.md)

    Visual Studio では、各 Python 環境に向けて対話型の read-evaluate-print loop (REPL) ウィンドウが用意されています。これにより、コマンド ライン上の *python.exe* で得られる REPL が改善されます。 **対話型** ウィンドウで、任意の Python コードを入力し、結果をすぐに確認することができます。

    ![Python Interactive ウィンドウ](media/interactive-window.png)

- [デバッグ](debugging-python-in-visual-studio.md)

    Visual Studio は、実行中のプロセスへのアタッチ、**ウォッチ** ウィンドウや **イミディエイト** ウィンドウでの式の評価、ローカル変数の調査、ブレークポイントの設定、ステートメントのステップ イン/ステップ アウト/ステップ オーバー、**次のステートメントの設定** など、Python 向けの総合的なデバッグ機能を提供します。 Linux コンピューターで実行されているリモートの Python コードをデバッグすることもできます。

    ![Visual Studio での Python のデバッグ](media/remote-debugging-breakpoint-hit.png)

- [C++ の操作](working-with-c-cpp-python-in-visual-studio.md)

    Python 用に作成された多くのライブラリは、最適なパフォーマンスを得るために C++ で記述されています。 Visual Studio では、[混合モード デバッグ](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)を含む、C++ の拡張機能を開発するための豊富な機能が提供されます。

    ![Python と C++ を一緒に使用する混合モードのデバッグ](media/mixed-mode-debugging.png)

- [プロファイル](profiling-python-code-in-visual-studio.md)

    CPython ベースのインタープリターを使用する場合は、Visual Studio 内で Python コードのパフォーマンスを評価できます。

    ![プロファイリング パフォーマンス レポート](media/profiling-results.png)

- [単体テスト](unit-testing-python-in-visual-studio.md)

    Visual Studio では、IDE のコンテキストにおけるすべての単体テストの検出、実行、デバッグのための統合サポートが提供されます。

    ![テストの失敗状態を示す単体テスト](media/unit-test-A-fail.png)

## <a name="next-steps"></a>次の手順

次のクイック スタートまたはチュートリアルのいずれかに従って、Visual Studio での Python についてさらに詳しく調べます。

> [!div class="nextstepaction"]
> [クイック スタート:Flask での Web アプリの作成](../ide/quickstart-python.md?toc=/visualstudio/python/toc.json&bc=/visualstudio/python/_breadcrumb/toc.json)

> [!div class="nextstepaction"]
> [Visual Studio での Python の使用](tutorial-working-with-python-in-visual-studio-step-01-create-project.md)

> [!div class="nextstepaction"]
> [Visual Studio での Django Web フレームワークの概要](learn-django-in-visual-studio-step-01-project-and-solution.md)

> [!div class="nextstepaction"]
> [Visual Studio での Flask Web フレームワークの概要](learn-flask-visual-studio-step-01-project-solution.md)

## <a name="see-also"></a>関連項目

- [Visual Studio のその他の機能](../ide/advanced-feature-overview.md)を確認します
- [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/) にアクセスします
- [Visual Studio ブログ](https://devblogs.microsoft.com/visualstudio/)を参照します
