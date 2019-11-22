---
title: Getting Started with Python | Microsoft Docs
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

The Python Tools for Visual Studio (PTVS), is a free, [open-source](https://github.com/Microsoft/ptvs) plug-in for Visual Studio that a powerful Python development experience.  
  
## <a name="python-the-language"></a>言語としての Python
  
Python is a popular programming language that is used by many universities, scientists, app scripters, casual developers, and professional developers, working on applications, web sites, and cloud services.

As a programming language, Python is:
  
- 信頼性が高い。
- Generally useful for scripting quick programs, app scripting, desktop apps, web servers, web services, and scientific computing.
- 簡単に学ぶことができ、正しくコーディングできるように適切に設計されている (多くの大学でプログラミングの入門コースに使用される)。
- Flexible, supporting imperative, functional, and object-oriented programming styles.
- 無料かつオープン ソース。
- Runs well on all major operating systems.  
- Supported by many free, useful, and well-designed libraries.  
- Supported by lots of documentation, samples, and a strong developer community.  

To learn more about the language, start with [Python for Beginners](https://www.python.org/about/gettingstarted/) on python.org.

To install Python itself, visit [https://www.python.org/download/](https://www.python.org/download/).

## <a name="python-tools-for-visual-studio"></a>Python Tools for Visual Studio
  
The Python Tools for Visual Studio, which you can install from [visualstudio.com](https://www.visualstudio.com/explore/python-vs), provide the following features:  
  
- さまざまなバージョンの CPython、IronPython、IPython など、複数のインタープリターのサポート  
- Python コードのフォルダー構造を暗黙的に取得し、またアプリ コード、テスト コード、Web ページ、JavaScript、ビルド スクリプトなどを識別できるように、明示的な制御も可能にするプロジェクト システム。  
- コンソール、Web、Azure、データ サイエンスおよび他の種類のプロジェクト用のプロジェクト テンプレート。    
- The Azure SDK for Python (see below)    
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
- Installation and features demo (27 min)](https://www.youtube.com/watch?v=JNNAOypc6Ek)  
- [ドキュメント](https://github.com/Microsoft/PTVS/wiki)  

Note that Visual Studio does not at present provide the means to create a stand-alone executable using Python, which essentially means a program with an embedded Python interpreter. ただし、[StackOverflow](https://stackoverflow.com/questions/5458048/how-to-make-a-python-script-standalone-executable-to-run-without-any-dependency)で説明されているように、Python コミュニティでは、多様な実行方法が紹介されています。 また、CPython はネイティブ アプリケーション内への埋め込みをサポートしています。詳細については、ブログの投稿「[Using CPython's Embeddable Zip File](https://devblogs.microsoft.com/python/cpython-embeddable-zip-file/)」(CPython の埋め込み可能な Zip ファイルの使用方法) を参照してください。
  
## <a name="building-ui-with-python"></a>Building UI with Python  

The main offering for building a UI with Python is the [Qt Project](https://www.qt.io/qt-for-application-development/), with bindings for Python known as [PySide (the official binding)](https://wiki.qt.io/PySide) (also see [PySide downloads](https://download.qt.io/official_releases/pyside/.))and [PyQt](https://wiki.python.org/moin/PyQt). 現在のところ、Visual Studio の Python のサポートには、UI 開発用のツールは含まれていません。

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
  
## <a name="see-also"></a>参照  

[PTVS の概要: Visual Studio のセットアップ](../python/getting-started-with-ptvs-setting-up-visual-studio.md)
[PTVS の概要: コーディングの開始 (プロジェクト)](../python/getting-started-with-ptvs-start-coding-projects.md)
[PTVS の概要: コードの編集](../python/getting-started-with-ptvs-editing-code.md)
[PTVS の概要: デバッグ](../python/getting-started-with-ptvs-debugging.md)
[PTVS の概要: 対話型の Python](../python/getting-started-with-ptvs-interactive-python.md)
[PTVS の概要: Azure での Web サイトの作成](../python/getting-started-with-ptvs-building-a-website-in-azure.md)
