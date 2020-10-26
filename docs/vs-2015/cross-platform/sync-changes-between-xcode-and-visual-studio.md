---
title: XCode と Visual Studio 2015 の間の変更の同期 |Microsoft Docs
titleSuffix: ''
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c71a4d7c-120e-4559-a114-3a99c4b860a9
caps.latest.revision: 10
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 42352ba4c5260c4b13a4cb3c6875d3469efcf404
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62573386"
---
# <a name="sync-changes-between-xcode-and-visual-studio"></a>XCode と Visual Studio 間の変更の同期
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft Visual C++ for Mobile Development コンポーネントには、PC と Mac 間で作業を同期するリモート機能が含まれます。 Visual Studio と Mac コンピューターがペアになっている場合、Visual Studio の iOS Application プロジェクトで新しいオプションを使用して、プロジェクトを XCode で開いたり、XCode と Visual Studio 間でコードを移動したり、一時 XCode プロジェクト ディレクトリを消去したりできます。

 リモート コンピューターのオプションを使用するには、プロジェクトが iOS Application プロジェクトで、Visual Studio とお使いの Mac がペアになっている必要があります。 Mac とペアにするための前提条件と手順については、「[iOS を使用してビルドするためのツールのインストールおよび構成](../cross-platform/install-and-configure-tools-to-build-using-ios.md)］をご覧ください。

## <a name="the-remote-machine-menu"></a>リモート コンピューターのメニュー
 **ソリューション エクスプローラー**で、iOS Application プロジェクトを右クリックすると、コンテキスト メニューが表示されます。 **[リモート コンピューター]** 項目を選択すると、使用可能なリモート オプションが表示されます。

 ![ソリューション エクスプローラーの [リモート コンピューター] メニュー項目](../cross-platform/media/cppmdd-u2-remotemachine-menu.jpg "CPPMDD_U2_RemoteMachine_Menu")

 これらのコマンドを使用すると、プロジェクトを XCode で開いたり、Visual Studio と XCode 間でローカルの変更やプロジェクト全体を移動したり、リモート コンピューターの一時ファイルを消去したりできます。

### <a name="open-in-xcode"></a>XCode で開く
 Visual Studio から XCode でプロジェクトを開くには、**[リモート コンピューター]** サブメニューで、**[XCode で開く]** を選択して、ペアになっているリモート コンピューターで、選択したプロジェクトを開きます。 vcremote サーバーを使用すると、XCode をお使いの Mac で開いて、プロジェクトのコピーを含む Mac で作成した一時ディレクトリに移動できます。 Visual Studio では、プロジェクトで使用した一時ディレクトリを表示するダイアログが表示されます。 リモート コンピューターで実行されるアクションも Visual Studio の**出力**ウィンドウに表示されます。 これを表示するため、**出力**ウィンドウの上部にある **[出力元の表示]** ドロップダウンで **[Visual C++ リモート コンピューター]** を選択する必要がある場合があります。

 ![出力ウィンドウにリモート コンピューターのアクションが表示される。](../cross-platform/media/cppmdd-u2-remotemachine-output.png "CPPMDD_U2_RemoteMachine_Output")

 Mac では、コードとリソース、ストーリーボード、アクションの編集に XCode のすべてのツールを使用できます。 Visual Studio では、iOS Application プロジェクトに "XCode で開かれました" という注釈が付けられ、リモート コンピューターで変更が加えられた可能性があることを示します。 編集が完了したら、[リモートからのプル] コマンドか [リモートからの増分プル] コマンドを使用して、Visual Studio プロジェクトに変更を適用します。

### <a name="push-to-remote-and-incremental-push-to-remote"></a>[リモートへのプッシュ] と [リモートへの増分プッシュ]
 Visual Studio で iOS Application プロジェクトに変更を加えた場合、[リモートへのプッシュ] コマンドか [リモートへの増分プッシュ] コマンドを使用して、変更したプロジェクト ファイルをペアになっているリモート コンピューターに移動できます。 [リモートへのプッシュ] コマンドは、すべてのプロジェクト ファイルをリモート コンピューターにコピーします。 [リモートへの増分プッシュ] コマンドは、変更したファイルのみをリモート コンピューターにコピーします。 大規模なプロジェクトに小さい変更を加えた場合、増分コマンドを使用すると時間と帯域幅を節約できます。

 プロジェクト ファイルを Mac にコピーするには、Visual Studio の**ソリューション エクスプローラー** ウィンドウで、iOS Application プロジェクトを右クリックしてコンテキスト メニューを開きます。 **[リモート コンピューター]** を選択し、**[リモートへのプッシュ]** か **リモートへの増分プッシュ]** のいずれかを選んで、プロジェクト ファイルを Visual Studio から Mac にコピーします。

### <a name="pull-from-remote-and-incremental-pull-from-remote"></a>[リモートからのプル] と [リモートからの増分プル]
 XCode でプロジェクトを変更した後、変更を Visual Studio に適用し、プロジェクトの同期を保ちます。

 プロジェクト ファイルを Mac からコピーするには、Visual Studio の**ソリューション エクスプローラー** ウィンドウで、iOS Application プロジェクトを右クリックしてコンテキスト メニューを開きます。 **[リモート コンピューター]** を選択し、**[リモートからのプル]** か **[リモートからの増分プル]** のいずれかを選んで、プロジェクト ファイルを Mac から Visual Studio にコピーします。

### <a name="clean-remote"></a>リモートの消去
 リモートの消去コマンドを使用すると、リモート コンピューター上の一時プロジェクト ディレクトリ内にあるファイルを消去できます。 ソース ファイルやビルド製品など、ディレクトリのコンテンツが Mac 上で削除されます。 リモートの消去コマンドを使用する前に、[リモートからのプル] か [リモートからの増分プル] を使用して、Visual Studio に適用する変更が同期されていることをご確認ください。

 一時プロジェクト ディレクトリをリモート コンピューター上で消去するには、Visual Studio の**ソリューション エクスプローラー** ウィンドウで、iOS Application プロジェクトを右クリックしてコンテキスト メニューを開きます。 プロジェクト ディレクトリ ファイルを Mac から削除するには、**[リモート コンピューター]**、**[リモートの消去]** の順に選択します。
