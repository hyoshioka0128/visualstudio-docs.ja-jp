---
title: Python でのはじめに |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 33f4f6fb-0ae4-4234-9df2-531f2d3af17f
caps.latest.revision: 13
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 21e724e585f2a5bf0e1fe2a6b70f89c1bd5f5eec
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74298194"
---
# <a name="getting-started-with-python"></a>Python の概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Python Tools for Visual Studio (PTVS) は、強力な Python 開発エクスペリエンスを備えた Visual Studio 用の無料の[オープンソース](https://github.com/Microsoft/ptvs)プラグインです。  
  
## <a name="python-the-language"></a>言語としての Python
  
Python は一般的なプログラミング言語であり、多くの大学、科学者、アプリのスクリプトスクリプト、カジュアル開発者、プロフェッショナル開発者、アプリケーション、web サイト、およびクラウドサービスでの作業に使用されます。

プログラミング言語として、Python は次のようになります。
  
- 信頼性が高い。
- 一般に、クイックプログラム、アプリスクリプト、デスクトップアプリ、web サーバー、web サービス、および科学計算のスクリプト作成に役立ちます。
- 簡単に学ぶことができ、正しくコーディングできるように適切に設計されている (多くの大学でプログラミングの入門コースに使用される)。
- 柔軟で、命令型、機能的、およびオブジェクト指向のプログラミングスタイルをサポートします。
- 無料かつオープン ソース。
- は、すべての主要なオペレーティングシステムで正常に動作します。  
- 多くの無料、便利で適切に設計されたライブラリでサポートされています。  
- 多くのドキュメント、サンプル、および強力な開発者コミュニティでサポートされています。  

言語の詳細については、python.org の[初心者向け Python](https://www.python.org/about/gettingstarted/)を開始してください。

Python 自体をインストールするには、 [https://www.python.org/download/](https://www.python.org/download/)にアクセスしてください。

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
  
[Visualstudio.com](https://www.visualstudio.com/explore/python-vs)からインストールできる Python Tools for Visual Studio には、次の機能が用意されています。  
  
- さまざまなバージョンの CPython、IronPython、IPython など、複数のインタープリターのサポート  
- Python コードのフォルダー構造を暗黙的に取得し、またアプリ コード、テスト コード、Web ページ、JavaScript、ビルド スクリプトなどを識別できるように、明示的な制御も可能にするプロジェクト システム。  
- コンソール、Web、Azure、データ サイエンスおよび他の種類のプロジェクト用のプロジェクト テンプレート。    
- Azure SDK for Python (下記参照)    
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
- インストールと機能のデモ (27 分)] (https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [ドキュメント](https://github.com/Microsoft/PTVS/wiki)  

Visual Studio では、Python を使用してスタンドアロンの実行可能ファイルを作成する手段が提供されていることに注意してください。基本的には、Python インタープリターが埋め込まれたプログラムを意味します。 ただし、[StackOverflow](https://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency)で説明されているように、Python コミュニティでは、多様な実行方法が紹介されています。 また、CPython はネイティブ アプリケーション内への埋め込みをサポートしています。詳細については、ブログの投稿「[Using CPython's Embeddable Zip File](https://devblogs.microsoft.com/python/cpython-embeddable-zip-file/)」(CPython の埋め込み可能な Zip ファイルの使用方法) を参照してください。
  
## <a name="building-ui-with-python"></a>Python を使用した UI の構築  

Python を使用した UI 構築の主要なオファリングは[Qt プロジェクト](https://www.qt.io/qt-for-application-development/)であり、 [PySide (正式なバインド)](https://wiki.qt.io/PySide)と呼ばれる python (公式のバインド) と[PyQt](https://wiki.python.org/moin/PyQt)がバインドさ[れてい](https://download.qt.io/official_releases/pyside/.)ます。 現在のところ、Visual Studio の Python のサポートには、UI 開発用のツールは含まれていません。

## <a name="azure-sdk-for-python"></a>Azure SDK for Python
  
Windows、Mac、および Linux をサポートしている Azure SDK for Python を使用すると、Microsoft Azure サービスの使用と管理が簡単になります。 詳細については、次のリソースを参照してください。 

- SDK をインストールするには、「[Python Package Index (Python パッケージ インデックス)](https://pypi.python.org/pypi/azure)」を使用するか、Azure ドキュメントの 「[Python と SDK のインストール](https://docs.microsoft.com/azure/python/python-sdk-azure-install)」の手順に従ってください。 
- [Azure SDK for Python デベロッパー センター](https://azure.microsoft.com/develop/python/)には、チュートリアルによるインストールからドキュメント化までの多数のヘルプがあります。  いくつかの要点を以下に示します。  
- 使い方ガイド:
  - [Python から Azure BLOB ストレージを使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/blob-service/)  
  - [Python から Queue ストレージを使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/queue-service/)  
  - [Python から Table ストレージを使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/table-service/)  
  - [Service Bus キューの使用方法](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-queues/)
  - [Service Bus のトピックとサブスクリプションの使用方法](https://azure.microsoft.com/develop/python/how-to-guides/service-bus-topics/) 
  - [Python からサービス管理を使用する方法](https://azure.microsoft.com/develop/python/how-to-guides/service-management/)  

## <a name="scientific-computing"></a>科学技術計算

すべての Python データ科学ライブラリに加えて、Python Tools for Visual Studio は、Azure でホスト可能な IPython と IPython Notebooks をサポートしています。

IPython と科学技術計算のライブラリ (matplotlib、scipy、numpy など) を[カリフォルニア大学アーバイン校](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy-stack)から入手することをお勧めします。  
  
## <a name="see-also"></a>関連項目  

[PTVS の概要: Visual Studio のセットアップ](../python/getting-started-with-ptvs-setting-up-visual-studio.md)
[PTVS の概要: コーディングの開始 (プロジェクト)](../python/getting-started-with-ptvs-start-coding-projects.md)
[PTVS の概要: コードの編集](../python/getting-started-with-ptvs-editing-code.md)
[PTVS の概要: デバッグ](../python/getting-started-with-ptvs-debugging.md)
[PTVS の概要: 対話型の Python](../python/getting-started-with-ptvs-interactive-python.md)
[PTVS の概要: Azure での Web サイトの作成](../python/getting-started-with-ptvs-building-a-website-in-azure.md)
