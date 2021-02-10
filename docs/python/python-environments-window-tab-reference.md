---
title: '[Python 環境] ウィンドウ リファレンス'
description: Visual Studio の [Python 環境] ウィンドウに表示される各タブの詳細について説明します。
ms.date: 03/18/2019
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: d00f8cc05e4a2a2ce1e947207997cc2e46d9d9f9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912379"
---
# <a name="python-environments-window-tabs-reference"></a>[Python 環境] ウィンドウ タブ リファレンス

**[Python 環境]** ウィンドウを開くには:

- **[表示]**  >  **[その他のウィンドウ]**  >  **[Python 環境]** メニュー コマンドを選びます。
- **ソリューション エクスプローラー** でプロジェクトの **[Python 環境]** ノードを右クリックし、 **[すべての Python 環境の表示]** を選択します。

**[Python 環境]** ウィンドウを大きく広げると、これらのオプションがタブとして表示され、より操作しやすくなります。 わかりやすくするために、この記事ではタブが拡大表示されています。

::: moniker range="vs-2017"
![[Python Environments (Python 環境)] ウィンドウを広げた表示](media/environments/environments-expanded-view.png)
::: moniker-end
::: moniker range=">=vs-2019"
![[Python Environments (Python 環境)] ウィンドウを広げた表示](media/environments/environments-expanded-view-2019.png)
::: moniker-end

## <a name="overview-tab"></a>[Overview (概要)] タブ

環境の基本的な情報とコマンドを提供します。

::: moniker range="vs-2017"
![[Python Environments (Python 環境)] の [Overview (概要)] タブ](media/environments/environments-overview-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![[Python Environments (Python 環境)] の [Overview (概要)] タブ](media/environments/environments-overview-tab-2019.png)
::: moniker-end

| コマンド | 説明 |
| --- | --- |
| **Make this environment the default for new projects (この環境を新しいプロジェクトの既定にする)** | アクティブな環境を設定します。これにより、IntelliSense データベースが読み込まれる間、Visual Studio (2017 バージョン 15.5 以前) がしばらく応答しなくなる場合があります。 多くのパッケージがある環境では、長時間応答しなくなる可能性があります。 |
| **ディストリビューターの Web サイトに移動する** | Python のディストリビューションで提供された URL をブラウザーで開きます。 たとえば、Python 3.x では python.org に移動します。 |
| **対話型ウィンドウを開く** | この環境用の[対話型 (REPL) ウィンドウ](python-interactive-repl-in-visual-studio.md)を Visual Studio 内で開き、すべての[スタートアップ スクリプト (後述)](#startup-scripts) を適用します。 |
| **対話型のスクリプトを確認する** | 「[スタートアップ スクリプト](#startup-scripts)」をご覧ください。 |
| **IPython 対話モードを使用する** | 設定すると、IPython では **対話型** ウィンドウが既定で開きます。 インライン プロットや、ヘルプを表示する `name?` やシェル コマンド用の `!command` などの拡張 IPython 構文が有効になります。 Anaconda ディストリビューションを使うときは、追加パッケージが必要なので、このオプションを使うことをお勧めします。 詳しくは、「[対話型ウィンドウで IPython を使用する](interactive-repl-ipython.md)」をご覧ください。 |
| **PowerShell で開く** | PowerShell コマンド ウィンドウでインタープリターを開始します。 |
| (フォルダーとプログラムのリンク) | 環境のインストール フォルダー、*python.exe* インタープリター、*pythonw.exe* インタープリターに簡単にアクセスできます。 インストール フォルダーはエクスプローラーで開き、2 つのインタープリターはコンソール ウィンドウが開きます。 |

### <a name="startup-scripts"></a>スタートアップ スクリプト

日常のワークフローで対話型ウィンドウを使っていると、ヘルパー関数を作成して繰り返し使うことがあります。 たとえば、Excel でデータ フレームを開く関数を作成し、そのコードをスタートアップ スクリプトとして保存して、**対話型** ウィンドウでいつでも使えるようにするといった場合です。

スタートアップ スクリプトにはインポート、関数定義、その他文字どおりどのようなコードでも含めることができ、**対話型** ウィンドウは自動的にそれを読み込んで実行します。 このようなスクリプトは、2 つの方法で参照されます。

1. 環境をインストールすると、Visual Studio によって *Documents\Visual Studio \<version>\Python Scripts\\\<environment>* フォルダーが作成されます。ここで、&lt;version&gt; は Visual Studio バージョン (2017 や 2019 など) であり、&lt;environment&gt; は環境の名前と一致します。 **[対話型のスクリプトを確認する]** コマンドを使って、環境固有のフォルダーに簡単に移動できます。 その環境の **対話型** ウィンドウを開始すると、このフォルダーで見つかったすべての *.py* ファイルがアルファベット順に読み込まれて実行されます。

1. **[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[対話型ウィンドウ]** タブ (「[対話型ウィンドウ オプション](python-support-options-and-settings-in-visual-studio.md#interactive-windows-options)」を参照) の **[スクリプト]** コントロールでは、すべての環境で読み込まれて実行されるスタートアップ スクリプトの追加フォルダーを指定します。 ただし、この機能は現時点では機能しません。

## <a name="configure-tab"></a>[Configure (構成)] タブ

使用可能な場合、 **[構成]** タブには次の表で説明するような詳細が表示されます。 このタブが存在しない場合は、Visual Studio がすべての詳細情報を自動的に管理していることを意味します。

::: moniker range="vs-2017"
![[Python Environments (Python 環境)] の [Configure (構成)] タブ](media/environments/environments-configure-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
![[Python Environments (Python 環境)] の [Configure (構成)] タブ](media/environments/environments-configure-tab-2019.png)
::: moniker-end

| フィールド | 説明 |
| --- | --- |
| **説明** | 環境の名前です。 |
| **Prefix path (プレフィックスのパス)** | インタープリターの基本フォルダーの場所です。 この値を入力して **[自動検出]** をクリックすると、Visual Studio が他のフィールドを設定します。 |
| **Interpreter Path (インタープリターのパス)** | インタープリターの実行可能ファイルへのパスです。通常は、プレフィックスのパスの後に **python.exe** を付けたものです。 |
| **Windowed interpreter (ウィンドウ形式のインタープリター)** | コンソールではない実行可能ファイルへのパスです。多くの場合、プレフィックスのパスの後に **pythonw.exe** を付けたものです。 |
| **Library path (ライブラリのパス)**<br/>(使用可能な場合) | 標準ライブラリのルートを指定します。ただし、Visual Studio がさらに正確なパスをインタープリターに要求できる場合、この値は無視される可能性があります。 |
| **Language version (言語バージョン)** | ドロップダウン メニューから選びます。 |
| **アーキテクチャ** | 通常は自動的に検出されて設定されます。されない場合は **32 ビット** または **64 ビット** を指定します。 |
| **Path environment variable (パス環境変数)** | 検索パスを探すためにインタープリターが使う環境変数です。 Visual Studio は、Python を開始するとき、プロジェクトの検索パスが含まれるように変数の値を変更します。 通常、このプロパティは **PYTHONPATH** に設定する必要がありますが、一部のインタープリターでは別の値が使われます。 |

## <a name="packages-tab"></a>[パッケージ] タブ

*旧バージョンでは "pip" も表示されます。*

pip ( **[パッケージ (PyPI)]** タブ) または Conda ( **[パッケージ (Conda)]** タブ、Visual Studio 2017 バージョン 15.7 以降の Conda 環境の場合) を使用して、環境にインストールされたパッケージを管理します。 このタブでは、新しいパッケージを検索し、その依存関係と共にインストールすることもできます。

既にインストールされているパッケージには、パッケージを更新するためのコントロール (上向き矢印) とアンインストールするためのコントロール (円内の X) が表示されます。

![[Python 環境] の [パッケージ] タブ](media/environments/environments-pip-tab-controls.png)

検索用語を入力すると、インストール済みのパッケージと PyPI からインストールできるパッケージの一覧がフィルター処理されます。

::: moniker range="vs-2017"
!["num" で検索を実行中の [Python 環境] の [パッケージ] タブ](media/environments/environments-pip-tab.png)
::: moniker-end
::: moniker range=">=vs-2019"
!["num" で検索を実行中の [Python 環境] の [パッケージ] タブ](media/environments/environments-pip-tab-2019.png)
::: moniker-end

上の図に示すように、検索結果には、検索用語と一致するパッケージが多数表示されます。しかし、一覧の最初のエントリは、**pip install \<name>** を直接実行するコマンドです。 **[パッケージ (Conda)]** タブを表示している場合、代わりに **conda install \<name>** が表示されます。

::: moniker range="vs-2017"
![conda インストール コマンドを表示している Conda パッケージ タブ](media/environments/environments-conda-tab-install.png)
::: moniker-end
::: moniker range=">=vs-2019"
![conda インストール コマンドを表示している Conda パッケージ タブ](media/environments/environments-conda-tab-install-2019.png)
::: moniker-end

どちらの場合でも、パッケージの名前の後に、検索ボックスに引数を追加してインストールをカスタマイズできます。 引数を含めた場合、検索結果で **pip install** または **conda install** の後に、検索ボックスの内容が表示されます。

::: moniker range="vs-2017"
![pip および conda のインストール コマンドで引数を使用する](media/environments/environments-pip-tab-arguments.png)
::: moniker-end
::: moniker range=">=vs-2019"
![pip および conda のインストール コマンドで引数を使用する](media/environments/environments-pip-tab-arguments-2019.png)
::: moniker-end

パッケージをインストールすると、ファイル システム上の環境の *Lib* フォルダー内にサブフォルダーが作成されます。 たとえば、*c:\Python36* に Python 3.6 をインストールした場合、パッケージは *c:\Python36\Lib* にインストールされます。*c:\Program Files\Anaconda3* に Anaconda3 をインストールした場合は、パッケージは *c:\Program Files\Anaconda3\Lib* にインストールされます。 Conda 環境では、パッケージはその環境のフォルダーにインストールされます。

### <a name="grant-administrator-privileges-for-package-install"></a>パッケージのインストールのための管理者特権を付与する

*c:\Program Files\Anaconda3\Lib* など、ファイル システムの保護された領域に置かれた環境にパッケージをインストールする場合、Visual Studio は、パッケージ サブフォルダーを作成できるように、管理者特権で `pip install` を実行する必要があります。 管理者特権への昇格が必要な場合、Visual Studio により "**この環境でパッケージのインストール、更新、削除を行うには、管理者特権が必要な場合があります**" というプロンプトが表示されます。

![パッケージ インストールのための昇格時のプロンプト](media/environments/environments-pip-elevate.png)

**[今すぐ昇格]** を選ぶと、1 回の操作について pip に管理者特権が付与され、アクセス許可を求めるオペレーティング システムのプロンプトも対象になります。 **[管理者特権なしで続行]** を選ぶと、パッケージのインストールは試みられますが、pip がフォルダーを作成しようとすると、"**エラー: 'C:\Program Files\Anaconda3\Lib\site-packages\png.py' を作成できませんでした: アクセス許可が拒否されました**" のような出力で失敗します。

**[パッケージのインストール時か削除時に必ず昇格]** を選ぶと、対象の環境ではダイアログが表示されなくなります。 再びダイアログが表示されるようにするには、 **[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[全般]** に移動し、 **[永続的に表示されないすべてのダイアログをリセットする]** ボタンを選択します。

同じ **[オプション]** タブでは、 **[常に管理者として pip を実行する]** を選んで、すべての環境でダイアログを非表示にすることもできます。 「[Options - General tab](python-support-options-and-settings-in-visual-studio.md#general-options)」([全般] タブのオプション) をご覧ください。

### <a name="security-restrictions-with-older-versions-of-python"></a>Python の旧バージョンのセキュリティ制限

Python 2.6、3.1、3.2 を使用する場合、Visual Studio には、"**Due to security restrictions, installing from the internet may not work on this version of Python (セキュリティ上の制限により、このバージョンの Python ではインターネットからのインストールが機能しない場合があります)** " という警告が示されます。

![Python の以前のバージョンでの pip インストール制限についてのメッセージ](media/environments/environments-old-version-restriction.png)

警告の理由は、Python の以前のバージョンでは、パッケージ ソース pypi.org からパッケージをダウンロードするために必要な、トランスポート セキュリティ層 (TLS) 1.2 のサポートが `pip install` に含まれていないことです。カスタムの Python ビルドは TLS 1.2 をサポートすることがあります。その場合 `pip install` が動作する可能性があります。

パッケージの適切な *get-pip.py* を [bootstrap.pypa.io](https://bootstrap.pypa.io/) からダウンロードできる場合があります。[pypi.org](https://pypi.org/) からパッケージを手動でダウンロードし、そのローカル コピーからパッケージをインストールします。

ただし、Python 2.7 または 3.3 にアップグレードすることをお勧めします。この場合、警告が表示されません。

::: moniker range="vs-2017"
## <a name="intellisense-tab"></a>[IntelliSense] タブ

IntelliSense 入力候補データベースの現在の状態を示します。

![[Python Environments (Python 環境)] の [IntelliSense] タブ](media/environments/environments-intellisense-tab.png)

- Visual Studio 2017 バージョン 15.5 以前は、IntelliSense による補完は、そのライブラリ用にコンパイルされているデータベースに依存しています。 データベースの構築はライブラリのインストール時にバックグラウンドで実行されますが、時間がかかる可能性があり、コードの記述の開始時には完了していないことがあります。
- Visual Studio 2017 バージョン 15.6 以降は、既定ではデータベースに依存せずに完了する迅速な方法が使用されます。 このため、タブのラベルは **IntelliSense [データベース無効]** になります。 データベースを有効にするには、オプション **[ツール]**  >  **[オプション]**  >  **[Python]**  >  **[試験段階]**  >  **[Use new style IntelliSense for environments]\(環境に対して新しいスタイル IntelliSense を使用する\)** をクリアします。

Visual Studio は新しい環境を検出すると (またはユーザーが追加すると)、ライブラリのソース ファイルを分析することで、データベースのコンパイルを自動的に開始します。 インストールされている内容により、この処理には 1 分から 1 時間以上かかることがあります (たとえば、Anaconda には多くのライブラリが付属しており、データベースのコンパイルに少し時間がかかります)。完了すると、詳細な IntelliSense が提供され、新しいライブラリをインストールするまでデータベースを再度更新する ( **[Refresh DB]\(DB の更新\)** ボタンで) 必要はありません。

データがコンパイルされていないライブラリには、 **!** が表示されます。環境のデータベースが完成していない場合は、 **!** も メイン環境リストのライブラリの横に表示されます。

::: moniker-end

## <a name="see-also"></a>関連項目

- [Visual Studio での Python 環境の管理](managing-python-environments-in-visual-studio.md)
- [プロジェクトのインタープリターの選択](selecting-a-python-environment-for-a-project.md)
- [依存関係の requirements.txt の使用](managing-required-packages-with-requirements-txt.md)
- [検索パス](search-paths.md)
