---
title: 混合モード Python/C++ デバッグのシンボル
description: C++ と Python の完全な混合モード デバッグのために Visual Studio が提供するシンボル読み込み機能について説明します。
ms.date: 11/12/2018
ms.topic: conceptual
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- python
- data-science
ms.openlocfilehash: 77dc73b0be050e5108f73d38dfbbaa763d236995
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "62957612"
---
# <a name="install-debugging-symbols-for-python-interpreters"></a>Python インタープリターのデバッグ シンボルをインストールする

完全なデバッグ エクスペリエンスを提供するため、Visual Studio の[混合モードの Python デバッガー](debugging-mixed-mode-c-cpp-python-in-visual-studio.md)では、多数の内部データ構造を解析するために、Python インタープリターのデバッグ シンボルを使用する必要があります。 たとえば、*python27.dll* の場合、対応するシンボル ファイルは *python27.pdb* です。*python36.dll* の場合、シンボル ファイルは *python36.pdb* です。 また、各バージョンのインタープリターは、多様なモジュールに合わせてシンボル ファイルを用意しています。

Visual Studio 2017 以降では、Python 3 および Anaconda 3 インタープリターによってそれぞれのシンボルが自動的にインストールされ、Visual Studio で自動的に検出されます。 Visual Studio 2015 以前の場合、または他のインタープリターを使用している場合は、シンボルを別にダウンロードし、 **[ツール]**  >  **[オプション]** ダイアログにある **[デバッグ]**  >  **[シンボル]** タブを使用して、Visual Studio にシンボルの場所を設定する必要があります。これらの手順については、以下のセクションで詳しく説明します。

Visual Studio でシンボルが必要なとき、通常は混合モードのデバッグ セッションを開始したときに、プロンプトが表示されることがあります。 この場合、ダイアログで 2 つの選択肢が示されます。

- **[シンボル設定ダイアログを開く]** を選択すると、 **[オプション]** ダイアログが開き、 **[デバッグ]**  >  **[シンボル]** タブが表示されます。
- **[インタープリター用のシンボルをダウンロード]** を選択すると、この現在のドキュメント ページが開きます。この場合は、 **[ツール]**  >  **[オプション]** を選択し、 **[デバッグ]**  >  **[シンボル]** タブに移動して続行します。

    ![混合モード デバッガーのシンボルのプロンプト](media/mixed-mode-debugging-symbols-required.png)

## <a name="download-symbols"></a>シンボルをダウンロードする

- Python 3.5 以前: Python インストーラーでデバッグ シンボルを取得します。 **[カスタム インストール]** を選択し、 **[次へ]** を選択します。 **[詳細設定]** 画面で、 **[Download debugging symbols]** (デバッグ シンボルのダウンロード) と **[Download debug binaries]** (デバッグ バイナリのダウンロード) を選択します。

    ![デバッグ シンボルを含む Python 3.x インストーラー](media/mixed-mode-debugging-symbols-installer35.png)

    シンボル ファイル ( *.pdb*) はルート インストール フォルダーにあります (個々のモジュールのシンボル ファイルも *DLLs* フォルダーにあります)。 そのため、シンボル ファイルは Visual Studio で自動的に検出されます。追加の手順は必要ありません。

- Python 3.4.x 以前: シンボルは、[公式のディストリビューション](#official-distributions)または [Enthought Canopy](#enthought-canopy) から、ダウンロード可能な *.zip* ファイルとして入手できます。 ダウンロード後は、Python フォルダー内の *Symbols* などのローカル フォルダーにファイルを展開して続行します。

    > [!Important]
    > Python のマイナー ビルド間や 32 ビット ビルドと 64 ビット ビルド間でもシンボルは異なるため、バージョンを完全に一致させることをお勧めします。 使用するインタープリターを確認するには、**ソリューション エクスプローラー**でプロジェクトの **[Python 環境]** *ノード*を展開し、環境名をメモします。 次に **[Python 環境]** *ウィンドウ*に切り替え、インストール場所をメモします。 次に、その場所でコマンド ウィンドウを開き、*python.exe* を起動します。正確なバージョンと 32 ビットか 64 ビットかが表示されます。

- ActiveState Python などのサードパーティの Python ディストリビューションを使用している場合は、そのディストリビューションの作成者に連絡して、シンボルの提供を依頼する必要があります。 WinPython には、標準の Python インタープリターが変更なしで組み込まれているため、対応するバージョン番号用の公式ディストリビューションのシンボルを使用できます。

## <a name="point-visual-studio-to-the-symbols"></a>Visual Studio にシンボルの場所を設定する

シンボルを別にダウンロードした場合は、以下の手順に従って、Visual Studio にシンボルを認識させます。 Python 3.5 以降のインストーラーでシンボルをインストールした場合、Visual Studio で自動的に検出されます。

1. **[ツール]**  >  **[オプション]** メニューを選択し、 **[デバッグ]**  >  **[シンボル]** に移動します。

1. ツールバーの **[追加]** ボタン (下図の線で囲まれたボタン) を選択し、ダウンロードしたシンボルを展開したフォルダー (下図のように、*c:\python34\Symbols* など、*python.pdb* がある場所) を入力し、 **[OK]** を選びます。

    ![混合モードのデバッグでのシンボルのオプション](media/mixed-mode-debugging-symbols.png)

1. Visual Studio のデバッグ セッション中に、Python インタープリターのソース ファイルの場所を入力するように求められることもあります。 ソース ファイルを ([python.org/downloads/](https://www.python.org/downloads/) などから) ダウンロードした場合は、その場所を設定することもできます。

> [!Note]
> ダイアログに表示されているシンボルのキャッシュ機能は、オンライン ソースから取得したシンボルのローカル キャッシュを作成するときに使用します。 Python インタープリターのシンボルの場合、既にローカルに存在するので、これらの機能は必要ありません。 いずれの場合も、詳細については、「[Specify Symbols and Source Files in the Visual Studio Debugger](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)」 (Visual Studio デバッガーでシンボルとソース ファイルを指定する) を参照してください。

## <a name="official-distributions"></a>公式ディストリビューション

| Python のバージョン | ダウンロード |
| --- | --- |
| 3.5 以降 | Python インストーラーでシンボルをインストールします。 |
| 3.4.4 | [32 ビット](https://www.python.org/ftp/python/3.4.4/python-3.4.4-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.4.4/python-3.4.4.amd64-pdb.zip) |
| 3.4.3 | [32 ビット](https://www.python.org/ftp/python/3.4.3/python-3.4.3-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.4.3/python-3.4.3.amd64-pdb.zip) |
| 3.4.2 | [32 ビット](https://www.python.org/ftp/python/3.4.2/python-3.4.2-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.4.2/python-3.4.2.amd64-pdb.zip) |
| 3.4.1 | [32 ビット](https://www.python.org/ftp/python/3.4.1/python-3.4.1-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.4.1/python-3.4.1.amd64-pdb.zip) |
| 3.4.0 | [32 ビット](https://www.python.org/ftp/python/3.4.0/python-3.4.0-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.4.0/python-3.4.0.amd64-pdb.zip) |
| 3.3.5 | [32 ビット](https://www.python.org/ftp/python/3.3.5/python-3.3.5-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.3.5/python-3.3.5.amd64-pdb.zip) |
| 3.3.4 | [32 ビット](https://www.python.org/ftp/python/3.3.4/python-3.3.4-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.3.4/python-3.3.4.amd64-pdb.zip) |
| 3.3.3 | [32 ビット](https://www.python.org/ftp/python/3.3.3/python-3.3.3-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.3.3/python-3.3.3.amd64-pdb.zip) |
| 3.3.2 | [32 ビット](https://www.python.org/ftp/python/3.3.2/python-3.3.2-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.3.2/python-3.3.2.amd64-pdb.zip) |
| 3.3.1 | [32 ビット](https://www.python.org/ftp/python/3.3.1/python-3.3.1-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.3.1/python-3.3.1.amd64-pdb.zip) |
| 3.3.0 | [32 ビット](https://www.python.org/ftp/python/3.3.0/python-3.3.0-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/3.3.0/python-3.3.0.amd64-pdb.zip) |
| 2.7.15 | [32 ビット](https://www.python.org/ftp/python/2.7.15/python-2.7.15-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.15/python-2.7.15.amd64-pdb.zip) |
| 2.7.14 | [32 ビット](https://www.python.org/ftp/python/2.7.14/python-2.7.14-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.14/python-2.7.14.amd64-pdb.zip) |
| 2.7.13 | [32 ビット](https://www.python.org/ftp/python/2.7.13/python-2.7.13-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.13/python-2.7.13.amd64-pdb.zip) |
| 2.7.12 | [32 ビット](https://www.python.org/ftp/python/2.7.12/python-2.7.12-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.12/python-2.7.12.amd64-pdb.zip) |
| 2.7.11 | [32 ビット](https://www.python.org/ftp/python/2.7.11/python-2.7.11-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.11/python-2.7.11.amd64-pdb.zip) |
| 2.7.10 | [32 ビット](https://www.python.org/ftp/python/2.7.10/python-2.7.10-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.10/python-2.7.10.amd64-pdb.zip) |
| 2.7.9 | [32 ビット](https://www.python.org/ftp/python/2.7.9/python-2.7.9-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.9/python-2.7.9.amd64-pdb.zip) |
| 2.7.8 | [32 ビット](https://www.python.org/ftp/python/2.7.8/python-2.7.8-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.8/python-2.7.8.amd64-pdb.zip) |
| 2.7.7 | [32 ビット](https://www.python.org/ftp/python/2.7.7/python-2.7.7-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.7/python-2.7.7.amd64-pdb.zip) |
| 2.7.6 | [32 ビット](https://www.python.org/ftp/python/2.7.6/python-2.7.6-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.6/python-2.7.6.amd64-pdb.zip) |
| 2.7.5 | [32 ビット](https://www.python.org/ftp/python/2.7.5/python-2.7.5-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.5/python-2.7.5.amd64-pdb.zip) |
| 2.7.4 | [32 ビット](https://www.python.org/ftp/python/2.7.4/python-2.7.4-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.4/python-2.7.4.amd64-pdb.zip) |
| 2.7.3 | [32 ビット](https://www.python.org/ftp/python/2.7.3/python-2.7.3-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.3/python-2.7.3.amd64-pdb.zip) |
| 2.7.2 | [32 ビット](https://www.python.org/ftp/python/2.7.2/python-2.7.2-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.2/python-2.7.2.amd64-pdb.zip) |
| 2.7.1 | [32 ビット](https://www.python.org/ftp/python/2.7.1/python-2.7.1-pdb.zip) - [64 ビット](https://www.python.org/ftp/python/2.7.1/python-2.7.1.amd64-pdb.zip) |

## <a name="enthought-canopy"></a>Enthought Canopy

Enthought Canopy は、バージョン 1.2 以降、バイナリのシンボルを提供します。 それらはディストリビューションと共に自動的にインストールされますが、それらが格納されたフォルダーをシンボル パスに追加する操作は手動で実行する必要があります。 Canopy の一般的なユーザーごとのインストールでは、シンボルは *%UserProfile%\AppData\Local\Enthought\Canopy\User\Scripts* (64 ビット バージョンの場合) および *%UserProfile%\AppData\Local\Enthought\Canopy32\User\Scripts* (32 ビット バージョンの場合) に配置されます。

Enthought Canopy 1.1 以前と Enthought Python Distribution (EPD) はインタープリター シンボルの提供がないため、混合モードのデバッグには対応できません。
