---
title: R Tools のインストール
description: オフライン インストールなど、Visual Studio 2017 および Visual Studio 2015 に R Tools をインストールする方法について説明します。
ms.date: 01/24/2018
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
monikerRange: vs-2017
ms.openlocfilehash: 5a09b3f78b929fd60764be36f56c0b580c7a42d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75843731"
---
# <a name="how-to-install-r-tools-for-visual-studio"></a>R Tools for Visual Studio のインストール方法

この記事の内容:

- [サポートされている Visual Studio のバージョン](#supported-versions-of-visual-studio)
- [Visual Studio 2017 で RTVS をインストールする](#install-rtvs-in-visual-studio-2017)
- [Visual Studio 2015 で RTVS をインストールする](#install-rtvs-in-visual-studio-2015)
- [オフライン インストール](#offline-installation-of-visual-studio-and-rtvs)

> [!Note]
> R Tools をインストールすると、「[オプション](options-for-r-tools-in-visual-studio.md)」記事で説明したように、最適化されたデータ科学レイアウト用に Visual Studio を構成できます。

## <a name="supported-versions-of-visual-studio"></a>サポートされている Visual Studio のバージョン

Windows では R Tools for Visual Studio (RTVS) は、[Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) および [Visual Studio 2015 Update 3 (以降)](http://htmlpreview.github.io/?https://github.com/lixzhang/R-MRO-MRS/blob/master/Introduction_to_MRO_and_MRS.html) (直接ダウンロード) の両方の Community (無料)、Professional、Enterprise の各エディションでサポートされています。

現在、Visual Studio for Mac では RTVS はサポートされていません。

Visual Studio Test Professional や SQL Server Management Studio などの製品に含まれている Visual Studio Shell しかない場合、RTVS はインストールされません。 Visual Studio Shell には RTVS に必要なコンポーネントがありません。

## <a name="install-rtvs-in-visual-studio-2017"></a>Visual Studio 2017 で RTVS をインストールする

1. Visual Studio インストーラーを実行して、 **[変更]** オプションを選びます (詳しくは、[Visual Studio の変更](../install/modify-visual-studio.md)に関するページをご覧ください)。 Visual Studio をまだインストールしていない場合は、[Visual Studio のインストール](../install/install-visual-studio.md)に関するページをご覧ください。 Windows 7 の場合、Visual Studio 2017 バージョン *15.2 ビルド 26430.12* 以降を表示するには、インストーラーを更新する必要があります。

1. **[データ サイエンスと分析のアプリケーション]** ワークロードを選択します。

    ![VS2017 の [データ サイエンスと分析のアプリケーション] ワークロード](media/installation-data-science-workload.png)

1. 同じワークロード名で、右側にその他のオプションを設定します。 既定では、このワークロードには F# と Python のサポートが含まれていることに注意してください。 R の場合、少なくとも **[R 言語サポート]** 、 **[R 開発ツールのランタイム サポート]** 、および **[Microsoft R クライアント]** を選択する必要があります。

RTVS は次の場所にインストールされます: *%ProgramFiles(x86)%\Microsoft Visual Studio\<version>\<edition>Common7\IDE\Extensions\Microsoft\R Tools for Visual Studio* ここで *\<version>* は通常、`2017` であり、 *\<edition>* は `Community`、`Professional`、または `Enterprise` です。

## <a name="install-rtvs-in-visual-studio-2015"></a>Visual Studio 2015 で RTVS をインストールする

Visual Studio 2015 では、R インタープリターと R Tools を個別にインストールする必要があります。

### <a name="install-an-r-interpreter"></a>R インタープリターをインストールする

RTVS には、次の 1 つ以上のソースから R 3.2.1 以降のバージョンの 64 ビット版のインストールが必要です。

- [Microsoft R Open](https://mran.microsoft.com/download/)
- [Microsoft R Client](/machine-learning-server/r-client/what-is-microsoft-r-client)
- [CRAN R](https://cran.r-project.org/bin/windows/base/)

Microsoft R Open と CRAN R はどちらも複数の side-by-side バージョンを許可しています。 ただし、Microsoft R Client は、1 つのバージョンのみをサポートし、インストールされている最新バージョンを常に使用します。

### <a name="install-the-r-tools"></a>R Tools のインストール

[https://rtvs.blob.core.windows.net/download/RTVS_2017-12-18.1.exe](https://rtvs.blob.core.windows.net/download/RTVS_2017-12-18.1.exe) から最新の R Tools for Visual Studio 2015 をダウンロードします。 RTVS は Visual Studio の適切なバージョンを確認し、R インタープリターがまだインストールされていない場合は、インストールの支援も行います。

> [!Note]
> スタンドアロンの RTVS インストーラーは Visual Studio 2015 でのみ機能します。Visual Studio 2017 の場合は、既に説明した、「[データ サイエンスと分析のアプリケーション ワークロード](#install-rtvs-in-visual-studio-2017)」の手順で R のサポートをインストールします。

RTVS for Visual Studio 2015 は、`%ProgramFiles(x86)%\Microsoft Visual Studio 14\Common7\IDE\Extensions\Microsoft\R Tools for Visual Studio` にインストールされます。

## <a name="offline-installation-of-visual-studio-and-rtvs"></a>Visual Studio と RTVS のオフライン インストール

オフライン インストールは、インターネットに接続されていないコンピューターに適しています。

1. 「[Visual Studio 2017 のオフライン インストールを作成する](../install/create-an-offline-installation-of-visual-studio.md)」に進みます。

1. Visual Studio 2015 を使用している場合、目次の上にあるセレクターで **2015** を選択します。

1. Web ページにあるオフライン インストールを作成する方法に従います。

1. Visual Studio 2015 の場合は、R Tools for Visual Studio のオフライン インストーラーを [https://rtvs.blob.core.windows.net/download/RTVS_2017-12-18.1.zip](https://rtvs.blob.core.windows.net/download/RTVS_2017-12-18.1.zip) および [https://rtvs.blob.core.windows.net/download/RTVS_Remote_2017-12-12.1.zip](https://rtvs.blob.core.windows.net/download/RTVS_Remote_2017-12-12.1.zip) からダウンロードします。

1. オフライン インストーラーから Visual Studio と RTVS をインストールします。

## <a name="see-also"></a>関連項目

- [R の使用を開始する](getting-started-with-r.md)
- [R Tools のサンプル プロジェクト](getting-started-samples.md)
- [R Tools のヘルプ](getting-started-help.md)
- [R Tools オプション](options-for-r-tools-in-visual-studio.md)
- [Microsoft Machine Learning Server (旧称 R Server)](/machine-learning-server/)
