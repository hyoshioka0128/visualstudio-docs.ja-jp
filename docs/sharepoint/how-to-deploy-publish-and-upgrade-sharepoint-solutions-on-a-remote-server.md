---
title: SharePoint ソリューションをリモートで配置、パブリッシュ、& アップグレードする
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- remote deployment [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, remote deployment
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5de5128ff19472390e65aa5d9a437aee269ff897
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91585785"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>方法: リモートサーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする
  SharePoint ソリューションをローカルシステムに配置するだけでなく、リモートサイトまたはローカル SharePoint サイトに対して、サンドボックス化された SharePoint ソリューションを発行できます。 リモート発行プロセスでは、SharePoint サーバーに *.wsp* ファイルがコピーされ、ソリューションがインストールされて、ソリューションのアクティブ化が可能になります。 リモート SharePoint ソリューションを変更した後に、そのインストールをアップグレードすることもできます。

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>サンドボックス化される SharePoint ソリューションをリモート SharePoint サーバーに発行するには

1. **ソリューションエクスプローラー**で、発行するサンドボックス化された SharePoint プロジェクトのショートカットメニューを開き、[**発行**] を選択します。

2. [ **発行** ] ダイアログボックスで、[ **SharePoint サイトに発行する** ] オプションを選択し、オンライン発行サイトの URL (など) を入力し `https://mytestsite.sharepoint.microsoftonline.com` ます。

3. 発行後にソリューション**ギャラリー**ページにソリューションの一覧を表示するには、[**発行後にブラウザーでソリューションギャラリーを開く**] をクリックします。

4. **[発行]** をクリックします。

5. ユーザー認証が必要な場合は、リモートサーバーにサインインします。

     発行の進行状況が Visual Studio の **出力** ウィンドウに表示されます。 プロセスが終了すると、ソリューション (*.wsp*) ファイルがリモート SharePoint サーバーにインストールされます。 ただし、SharePoint で使用するには、アクティブにしておく必要があります。

6. [ **ソリューションギャラリー** ] ページで SharePoint アプリケーションを選択し、リボンの [ **アクティブ化** ] ボタンをクリックします。

7. [ **ソリューションのアクティブ化** ] ダイアログボックスのリボンで、[ **アクティブ化** ] ボタンをもう一度クリックします。

     **ソリューションギャラリー**ページの [**状態**] 列には、アプリケーションがアクティブであることが示されます。

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>リモートの SharePoint サーバーで、サンドボックス化される SharePoint ソリューションをアップグレードするには
 セキュリティで保護された SharePoint ソリューションがリモートサーバーで既にパブリッシュされている場合、次のプロセスを使用すると、でアプリケーションを変更した後で、そのソリューションをアップグレードでき [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

1. で SharePoint パッケージの名前を変更 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] します。 これを行うには、でパッケージを **ソリューションエクスプローラー** 開きます。 **パッケージエクスプローラー**に表示されます。

2. **パッケージエクスプローラー**の [**名前**] ボックスで、パッケージ名を一意の名前に変更します。

3. プロジェクトを保存します。

4. **ソリューションエクスプローラー**で、プロジェクトのショートカットメニューを開き、[**発行**] を選択します。

5. [ **発行** ] ダイアログボックスで、[ **SharePoint サイトに発行する** ] オプションボタンをクリックし、ソリューションが保存されているリモートサーバーの URL がない場合は、それを入力します。

6. 発行後にソリューション**ギャラリー**ページにソリューションの一覧を表示するには、[**発行後にブラウザーでソリューションギャラリーを開く**] をクリックします。

7. **[発行]** をクリックします。

8. ユーザー認証が必要な場合は、リモートサーバーにサインインします。

     最近リモートサーバーにログインした場合、認証は必要ありません。

     同じ名前を持つ古いバージョンのアプリケーションが SharePoint サーバーにまだ存在している場合は、同じ名前のパッケージが SharePoint サーバーに既に存在するというエラーが表示されます。 発行する前に、パッケージ名を一意の名前に変更する必要があります。

9. SharePoint で新しいアプリケーションを選択し、リボンの [ **アップグレード** ] ボタンをクリックします。

10. [ **ソリューションのアップグレード** ] ダイアログボックスのリボンで、[ **アップグレード** ] ボタンをもう一度クリックします。 **ソリューションギャラリー**ページの [**状態**] 列に、アプリケーションがアクティブであることが表示されます。

     以前のバージョンのソリューションは非アクティブ化されています。新しいバージョンのソリューションは、古いソリューションから保持されているデータでアップグレードされ、新しいソリューションは SharePoint でアクティブ化されます。

## <a name="see-also"></a>関連項目
- [方法: SharePoint ソリューションをローカルの SharePoint サイトに配置および発行する](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [SharePoint ソリューションパッケージの作成](../sharepoint/creating-sharepoint-solution-packages.md)
- [方法: SharePoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージデザイナーを使用してパッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
