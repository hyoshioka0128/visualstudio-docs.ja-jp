---
title: Python の使用開始 |マイクロソフトドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 33f4f6fb-0ae4-4234-9df2-531f2d3af17f
caps.latest.revision: 13
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 97d60fe31f838c4cc497701f4560dc426ebc1cc9
ms.sourcegitcommit: 054815dc9821c3ea219ae6f31ebd9cd2dc8f6af5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2020
ms.locfileid: "80543973"
---
# <a name="getting-started-with-python"></a>Python の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 用の Python ツール (PTVS) は、強力な Python 開発エクスペリエンスを実現する、Visual Studio 用[の無料のオープン ソース](https://github.com/Microsoft/ptvs)プラグインです。  
  
## <a name="python-the-language"></a>言語としての Python
  
Python は、多くの大学、科学者、アプリ スクリプター、カジュアル開発者、およびプロの開発者がアプリケーション、Web サイト、クラウド サービスに取り組んでいる一般的なプログラミング言語です。

プログラミング言語として、Pythonは次のとおりです。
  
- 信頼性が高い。
- 一般に、クイック プログラム、アプリ スクリプト、デスクトップ アプリ、Web サーバー、Web サービス、および科学コンピューティングのスクリプト作成に役立ちます。
- 簡単に学ぶことができ、正しくコーディングできるように適切に設計されている (多くの大学でプログラミングの入門コースに使用される)。
- 柔軟で、命令型、機能的、オブジェクト指向のプログラミング スタイルをサポートします。
- 無料かつオープン ソース。
- すべての主要なオペレーティング システムでうまく動作します。  
- 多くの無料で便利で、適切に設計されたライブラリでサポートされています。  
- 多くのドキュメント、サンプル、および強力な開発者コミュニティによってサポートされています。  

言語の詳細については、[初心者向](https://www.python.org/about/gettingstarted/)け Python のpython.orgから始めます。

Python 自体をインストールするには[https://www.python.org/download/](https://www.python.org/download/)、 をご覧ください。

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
  
visualstudio.com[からインストール](https://www.visualstudio.com/explore/python-vs)できる Visual Studio 用の Python ツールには、次の機能があります。  
  
- さまざまなバージョンの CPython、IronPython、IPython など、複数のインタープリターのサポート  
- Python コードのフォルダー構造を暗黙的に取得し、またアプリ コード、テスト コード、Web ページ、JavaScript、ビルド スクリプトなどを識別できるように、明示的な制御も可能にするプロジェクト システム。  
- コンソール、Web、Azure、データ サイエンスおよび他の種類のプロジェクト用のプロジェクト テンプレート。    
- Python 用 Azure SDK (下記を参照)    
- 構文の色分け、すべてのコードとライブラリ間でのオートコンプリート、シグネチャ ヘルプ、クラス ビュー、定義への移動、すべての参照の検索、リファクタリングなどを含む、豊富な編集とコード読解の機能。    
- 対話型 (REPL) ウィンドウ
- データ可視化を備えた IPython。
- IronPython および .NET/WPF のサポート。    
- Visual Studio プロジェクトを使用しない機能豊富なデバッグ、既存の実行可能ファイルに対する機能、混合モードのデバッグ、Windows/Linux/Mac へのリモート デバッグ、および対話型ウィンドウ内でのデバッグ。   
- プロファイル ツール。  
- テスト用ツール。  
  
使い始めるにあたり、次のリソースを参考にしてください。

- [インストール ガイド](https://github.com/Microsoft/PTVS/wiki/PTVS-Installation)    
- [概要および詳細情報の短いビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)  
- インストールと機能のデモ(27分))https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [ドキュメント](https://github.com/Microsoft/PTVS/wiki)  

Visual Studio には、Python を使用してスタンドアロンの実行可能ファイルを作成する手段は、基本的に Python インタプリタが埋め込まれたプログラムを意味する手段が用意されていません。 ただし、[StackOverflow](https://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency)で説明されているように、Python コミュニティでは、多様な実行方法が紹介されています。 また、CPython はネイティブ アプリケーション内への埋め込みをサポートしています。詳細については、ブログの投稿「[Using CPython's Embeddable Zip File](https://devblogs.microsoft.com/python/cpython-embeddable-zip-file/)」(CPython の埋め込み可能な Zip ファイルの使用方法) を参照してください。
  
## <a name="building-ui-with-python"></a>Python を使用した UI の構築  

Python で UI を構築するための主な提供は[、PySide](https://www.qt.io/qt-for-application-development/) [(公式バインディング)](https://wiki.qt.io/PySide)と呼ばれる Python のバインディングを持つ Qt プロジェクトです[(PySide ダウンロード](https://download.qt.io/official_releases/pyside/.)を参照してください) と[PyQt](https://wiki.python.org/moin/PyQt). 現在のところ、Visual Studio の Python のサポートには、UI 開発用のツールは含まれていません。

## <a name="azure-sdk-for-python"></a>Azure SDK for Python
  
Windows、Mac、および Linux をサポートしている Azure SDK for Python を使用すると、Microsoft Azure サービスの使用と管理が簡単になります。 詳細については、次のリソースを参照してください。 

- SDK をインストールするには、「[Python Package Index (Python パッケージ インデックス)](https://pypi.python.org/pypi/azure)」を使用するか、Azure ドキュメントの 「[Python と SDK のインストール](/azure/developer/python/azure-sdk-install)」の手順に従ってください。 
- [Azure SDK for Python デベロッパー センター](https://azure.microsoft.com/develop/python/)には、チュートリアルによるインストールからドキュメント化までの多数のヘルプがあります。  いくつかの要点を以下に示します。  
- 使い方ガイド:
  - [ストレージ BLOB](https://azure.microsoft.com/develop/python/how-to-guides/blob-service/)  
  - [ストレージ キュー](https://azure.microsoft.com/develop/python/how-to-guides/queue-service/)  
  - [ストレージテーブル](https://azure.microsoft.com/develop/python/how-to-guides/table-service/)  
  - [Service Bus キュー](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-queues/)
  - [サービス バスのトピック/サブスクリプション](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-topics/) 
  - [サービス管理](https://azure.microsoft.com/develop/python/how-to-guides/service-management/)  

## <a name="scientific-computing"></a>科学技術計算

すべての Python データ科学ライブラリに加えて、Python Tools for Visual Studio は、Azure でホスト可能な IPython と IPython Notebooks をサポートしています。

IPython と科学技術計算のライブラリ (matplotlib、scipy、numpy など) を[カリフォルニア大学アーバイン校](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy-stack)から入手することをお勧めします。  
  
## <a name="see-also"></a>参照  

[PTVS の概要: PTVS](../python/getting-started-with-ptvs-setting-up-visual-studio.md)
の Visual Studio のセットアップ[: PTVS のコーディングの開始 (プロジェクト)](../python/getting-started-with-ptvs-start-coding-projects.md)
[: PTVS](../python/getting-started-with-ptvs-editing-code.md)
のコードの編集[: PTVS](../python/getting-started-with-ptvs-debugging.md)
のデバッグ[の開始: PTVS](../python/getting-started-with-ptvs-interactive-python.md)
の対話型 Python の[概要: PTVS の Web サイトの構築](../python/getting-started-with-ptvs-building-a-website-in-azure.md)
