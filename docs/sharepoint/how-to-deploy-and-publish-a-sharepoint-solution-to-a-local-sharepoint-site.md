---
title: SharePoint ソリューションをローカルの SharePoint サイトに配置 & 発行する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 59d4fe41565d0aaf0c52cae9434d4a576dc26baa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016815"
---
# <a name="how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site"></a>方法: SharePoint ソリューションをローカルの SharePoint サイトに配置および発行する
  開発用コンピューターのローカル SharePoint サーバーに SharePoint ソリューションを配置したり、発行したりすることができます。 配置プロセスでは、SharePoint サーバーに *.wsp* ファイルがコピーされ、ソリューションがインストールされて、機能がアクティブ化されます。 発行プロセスでは、 *.wsp* ファイルを SharePoint サーバーにコピーしてインストールするだけです。 SharePoint で有効にするには、手動でアクティブ化する必要があります。

## <a name="to-deploy-a-sharepoint-solution-to-the-local-sharepoint-server"></a>SharePoint ソリューションをローカルの SharePoint サーバーに配置するには

1. **ソリューションエクスプローラー**で、配置するプロジェクトを選択します。

2. メニューバーで、[ **ビルド**]、[ **ソリューションの配置**] の順に選択します。

     *.Wsp*ファイルが作成され、ローカルの SharePoint サーバーにインストールされます。 また、機能がアクティブ化されます。

## <a name="to-publish-a-sharepoint-solution-to-a-local-sharepoint-server"></a>SharePoint ソリューションをローカルの SharePoint サーバーにパブリッシュするには

1. **ソリューションエクスプローラー**で、パブリッシュする SharePoint プロジェクトのショートカットメニューを開き、[**発行**] を選択します。

2. [ **発行** ] ダイアログボックスで、[ **ファイルシステムに発行する** ] オプションボタンをクリックします。

3. [ **ターゲットの場所** ] テキストボックスにローカルパスを入力し、[ **発行** ] をクリックします。

     発行の進行状況が Visual Studio の **出力** ウィンドウに表示されます。 プロセスが終了すると、ソリューション (*.wsp*) ファイルがローカルの SharePoint サーバーにインストールされます。 ただし、SharePoint で使用するには、アクティブにする必要があります。 ソリューションファイルが既に存在する場合は、エラーが発生し、既存のファイルを上書きするかどうかを確認するメッセージが表示されます。 パッケージのアップグレードの詳細については、「 [方法: リモートサーバー上で SharePoint ソリューションを配置、発行、およびアップグレード](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)する」の「リモートパッケージのアップグレード」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: リモートサーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)
- [SharePoint ソリューションパッケージの作成](../sharepoint/creating-sharepoint-solution-packages.md)
- [方法: SharePoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージデザイナーを使用してパッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
