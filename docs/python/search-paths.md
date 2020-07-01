---
title: Python 検索パスの適用方法
description: Visual Studio では、システム全体の変数使用を回避する目的で、環境やプロジェクトの検索パスを指定するための特別な方法が用意されています。
ms.date: 03/13/2019
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.custom: seodec18
ms.workload:
- python
- data-science
ms.openlocfilehash: 3a23afff970405bf7ae1bbd1c8aad326eb133780
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520381"
---
# <a name="how-visual-studio-uses-python-search-paths"></a>Visual Studio による Python 検索パスの使用方法

通常の Python の使用方法では、`PYTHONPATH` 環境変数 (または `IRONPYTHONPATH` など) がモジュール ファイルの既定の検索パスを提供します。 つまり、`from <name> import...` または `import <name>` ステートメントを使うと、Python は次の場所を順に検索して、一致する名前を探します。

1. Python の組み込みモジュール
1. 実行している Python コードが含まれるフォルダー
1. 該当する環境変数によって定義された "モジュール検索パス" (Python のコア ドキュメントの「[The Module Search Path](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)」(モジュール検索パス) および「[Environment variables](https://docs.python.org/2/using/cmdline.html#envvar-PYTHONPATH)」(環境変数) をご覧ください)。

ただし、検索パス環境変数がシステム全体に対して設定されている場合でも、Visual Studio はこの変数を無視します。 実際はまさにシステム全体が設定されている*ために*無視されるので、自動的には答えられないようなある種の疑問が発生します。参照されているモジュールは Python 2.7 または Python 3.6 以降のどちらか。 標準ライブラリ モジュールをオーバーライドするのか。 開発者はこの動作を認識しているのか、それとも悪意のあるハイジャックの試みか。

そのため Visual Studio では、環境とプロジェクトの両方で検索パスを直接指定するための手段が用意されています。 Visual Studio で実行またはデバッグするコードは、検索パスを `PYTHONPATH` (およびその他の同等の変数) の値で受け取ります。 検索パスを追加すると、Visual Studio はそれらの場所でライブラリを検査し、必要に応じて IntelliSense データベースを構築します (Visual Studio 2017 バージョン 15.5 以前、ライブラリの数によっては時間がかかります)。

検索パスを追加するには、**ソリューション エクスプローラー**に移動し、プロジェクト ノードを展開し、 **[検索パス]** を右クリックして **[フォルダーを検索パスに追加]** を選択します。

::: moniker range="vs-2017"
![ソリューション エクスプローラーの [検索パス] 上の [フォルダーを検索パスに追加] コマンド](media/search-paths-command.png)
::: moniker-end
::: moniker range=">=vs-2019"
![ソリューション エクスプローラーの [検索パス] 上の [フォルダーを検索パスに追加] コマンド](media/search-paths-command-2019.png)
::: moniker-end

このコマンドでブラウザーが表示されます。ここで、含めるフォルダーを選択します。

`PYTHONPATH` 環境変数に必要なフォルダーが既に含まれている場合は、便利なショートカットとして **[PYTHONPATH を検索パスに追加]** を使用してください。

フォルダーが検索パスに追加されると、Visual Studio ではプロジェクトに関連付けられているすべての環境にそれらのパスが使用されます。 (環境が Python 3 ベースの場合に、検索パスを Python 2.7 モジュールに追加しようとすると、エラーが発生することがあります。)

**[Zip アーカイブを検索パスに追加]** コマンドを選択することで、拡張子が *.zip* または *.egg* のファイルを検索パスとして追加することもできます。 フォルダーと同様に、これらのファイルの内容もスキャンされて、IntelliSense に利用されます。

## <a name="see-also"></a>参照

- [Visual Studio での Python 環境の管理](managing-python-environments-in-visual-studio.md)
- [プロジェクトのインタープリターの選択](selecting-a-python-environment-for-a-project.md)
- [依存関係の requirements.txt の使用](managing-required-packages-with-requirements-txt.md)
- [[Python 環境] ウィンドウ リファレンス](python-environments-window-tab-reference.md)
