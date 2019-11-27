---
title: 'PTVS の概要: Azure での Web サイトの作成 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-python
ms.topic: conceptual
ms.assetid: 3bdbda36-14d2-4fde-ba42-d91042777ff6
caps.latest.revision: 5
author: kraigb
ms.author: kraigb
manager: jillfra
ms.openlocfilehash: 288fb24c9c1c4ddee1cb59a968e717531e274af1
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300586"
---
# <a name="getting-started-with-ptvs-building-a-website-in-azure"></a>PTVS の概要: Azure での Web サイトの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Azure での Python Web サイトの構築をすばやく開始できます。  
  
 これらの手順は、非常に短い [youtube ビデオ](https://www.youtube.com/watch?v=FJx5mutt1uk&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=6)で視聴できます。  
  
 [新しいプロジェクト] ダイアログ ボックスから開始して、Python プロジェクトの下にある Bottle Web プロジェクトを選択します。  この [Bottle](http://bottlepy.org/docs/dev/index.html) テンプレートは、[Bootstrap フレームワーク](https://getbootstrap.com/) に基づくスターター サイトです。  プロジェクトを作成するとき、Visual Studio は、依存関係 (この場合は Bottle) を仮想環境にインストールすることを求めるプロンプトを出します。  Azure Web サイトを配置しているので、サイトの操作に必要なビットを展開するために、依存関係を仮想環境に追加する必要があります。  また、環境を Python 2.7 または 3.4 32 ビットに基づくものにする必要もあります。  プロジェクトを作成した後に、F5 キーを押して、サイトの実行をローカルで開始します。  
  
 Azure では、サイトの試行が簡単です。  Azure サブスクリプションがない場合は、[try.azurewebsites.net](https://trywebsites.azurewebsites.net/) を使用できます。  このサイトは、ソーシャル ログインのみを使用して、Azure Web サイトを一度に 1 時間だけ試行するための簡単な方法を提供します。  クレジット カードは必要ありません。  [Change Language] ドロップダウンで [Empty Site] テンプレートを選択し、[Create] を選択します。  [Work with your web application] の下の [Download Publishing Profile] を選択して、Visual Studio で使用するファイルを保存します。  また、任意のオペレーティング システムから Git を使用して展開することもできます。  
  
 Visual Studio および作成したプロジェクトに戻ります。  ソリューション エクスプローラーでプロジェクト ノードを選択して、右のポインター ボタンを選択してから、[発行] を選択します。  Azure サブスクリプションがあれば、ダイアログで Microsoft Azure の Web サイトをクリックして、ここからサイトを管理できます。  このチュートリアルでは、[インポート] を選択して、ダウンロードした発行プロファイルをインポートします。  発行プロファイルには必要なすべての情報が含まれているので、[発行] を選択できます。  数秒で、新しいブラウザー ウィンドウが開き、サイトは Azure クラウドでライブ ホストされます。  
  
 単純な Web サイトであれば簡単ですが、Azure でのより重要な Web アプリケーションについては、[deep dive](https://www.youtube.com/watch?v=WG3pGmoo8nE&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=10) でのビデオ、およびこのチャネル内の他のビデオを参照してください (getting started や deep dive のビデオ ページの右上にリンクがあります)。さらに、以下も参照してください。  
  
 これらの手順は、非常に短い [youtube ビデオ](https://www.youtube.com/watch?v=FJx5mutt1uk&list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff&index=6)で視聴できます。  
  
## <a name="see-also"></a>関連項目  
 [Wiki ドキュメント](https://github.com/Microsoft/PTVS/wiki/Web-Project)   
 [PTVS の概要と詳細に関するビデオ](https://www.youtube.com/playlist?list=PLReL099Y5nRdLgGAdrb_YeTdEnd23s6Ff)
