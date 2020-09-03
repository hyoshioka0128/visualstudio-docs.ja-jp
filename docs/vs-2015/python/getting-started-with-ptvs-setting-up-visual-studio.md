---
title: 'PTVS の概要: Visual Studio 2015 のセットアップ | Microsoft Docs'
titleSuffix: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: ec491c1d-bdb2-4c2b-a390-bd808cec635a
caps.latest.revision: 6
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: cf841c181b3a7e0b378e53e3901a079b7136b32c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "82586984"
---
# <a name="getting-started-with-ptvs-setting-up-visual-studio"></a>PTVS の概要: Visual Studio のセットアップ

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

PTVS と関連するライブラリのインストールは、Visual Studio がある場合は簡単です。 Visual Studio がない場合は、プロの品質のバージョンの無償コピーを取得できます。

これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=_okUV47eM5c&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=1)で視聴できます。

ハイレベルな手順は、Visual Studio のインストール、PTVS のインストール、Python とデータ ライブラリ (Anaconda、Canopy) のインストール、そして最後にインストールをチェックすることです。

まず Visual Studio が必要です。 オープン ソースまたは個人の開発者の場合、無料でプロフェッショナル向けの機能を備えた Visual Studio [Community Edition](https://www.visualstudio.com/products/visual-studio-community-vs) を使用できます。 また、クラスルーム学習や学術調査のための使用である場合、またはオープン ソース プロジェクトに参加している場合は、組織でも Community Edition を使用できます。 学生や新規事業者は DreamSpark と BizSpark プログラムを調べて、無料アクセスの条件を満たしているかを確認するか、または MSDN サブスクリプションがあるかを雇用主に確認してくのださい。

Visual Studio をインストールした後に、[PTVS をインストールする](https://archive.codeplex.com/?p=pytools)必要があります。 これは、Microsoft によってフルサポートされ、コミュニティの支援を得てオープンに開発された、無料のスタンドアロン拡張です。

次に、[Python をインストールする](https://www.python.org/download/)必要があります。 Python はコミュニティによって管理されており、そのホームページは python.org です。連続分析では、Python と多くの便利なライブラリ (特にサイエンスとデータ処理) を持つ Anaconda という名前の無料バンドルが作成され、Canopy という名前の類似したバンドルが生成されます。 これらのいずれか 1 つの製品をインストールすれば十分です。 どちらにするか迷う場合には、最新の Python とインストール困難なパッケージのほとんどを提供する [Anaconda](https://www.anaconda.com/products/individual) から始めてください。

Visual Studio を起動して、すべてが動作していることを確認します。 [表示] メニューで、[その他のウィンドウ] を選択します。 Python Environments という項目があります。 このウィンドウには、PTVS が検出したすべての Python インストール環境と、インストールしたすべてのパッケージが表示されます。 ウィンドウは、コードを編集する際に入力候補を表示するための、データベースの更新も制御します。 この更新プロセスには多少時間がかかりますが、完了すれば、PTVS を使用してパッケージに関するより役立つ情報を表示できるようになります。

IPython を PTVS と共に使用する場合、これらの[手順](https://archive.codeplex.com/?p=pytools)に従ってください。

これらの手順は、短い [YouTube ビデオ](https://www.youtube.com/watch?v=_okUV47eM5c&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=1)で視聴できます。

## <a name="see-also"></a>参照

[PTVS の概要と詳細に関するビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
