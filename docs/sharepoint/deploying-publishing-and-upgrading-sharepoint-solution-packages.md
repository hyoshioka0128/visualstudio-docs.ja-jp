---
title: SharePoint ソリューションパッケージの配置、パブリッシュ、& アップグレード
description: SharePoint ソリューションパッケージの配置、発行、およびアップグレードを行います。 デプロイプロセスをカスタマイズします。 リモートまたはローカルサーバーにパッケージを発行します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SharePointProjectPropertyTab
- VS.SharePointTools.Project.Publishing
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: cd0dfa3a12c675463c46e93aa0d5b25e8b4bd4b2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948857"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>SharePoint ソリューションパッケージの配置、発行、およびアップグレード
  Visual Studio で SharePoint ソリューションを開発した後、パッケージ (.wsp) ファイルをローカルの SharePoint サーバーに配置するか、リモートまたはローカルの SharePoint サーバーにパブリッシュすることができます。 ファイルを展開する場合は、パッケージファイル (.wsp) の展開方法をカスタマイズできます。

> [!NOTE]
> 現時点では、リモートの SharePoint サーバーにパブリッシュできるのは、サンドボックス化されたソリューションのみです。 詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

## <a name="deploy-publish-and-upgrade"></a>デプロイ、発行、およびアップグレード
 *配置* とは、Visual Studio の sharepoint プロジェクトからビルドされた sharepoint ソリューションファイルをローカルホストにコピーすることを指します。 配置されたソリューションでは、インターネットインフォメーションサービス (IIS) プールのリサイクル、配置後のソリューションのアクティブ化などの配置手順を構成できます。 配置するには、[**ビルド**] メニューの [**配置**] を使用します。 詳細については、「 [方法: sharepoint の配置構成を編集](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md) する」および「 [方法: Sharepoint ソリューションをローカルの Sharepoint サイトに配置および発行](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)する」を参照してください。

 *発行* とは、リモートの sharepoint サイトにサンドボックス化される sharepoint ソリューションファイルをアップロードすることを指します。つまり、別のシステムに配置されているサイトです。 SharePoint サンドボックスソリューションファイルをローカルの SharePoint サイトに発行することもできますが、に発行されたサイトがローカルかリモートかに関係なく、その配置手順を構成することはできません。

 *アップグレード* とは、既存のリモートまたはローカルにパブリッシュされた SharePoint ソリューションの更新を指します。 Visual Studio で SharePoint ソリューションを変更した後、ソリューションのパッケージファイル名を変更し、ソリューションを再パブリッシュした後、ソリューションを正常に再パブリッシュした後にアップグレードします。 ローカルに発行されたソリューションを再発行する場合は、既存のソリューションファイルを上書きすることができます。

## <a name="deploy-packages"></a>パッケージの配置
 テストおよびデバッグのために、開発用コンピューターの SharePoint サーバーにパッケージファイルを配置できます。 また、[**発行**] ダイアログボックスの [**ファイルシステムに発行**] オプションボタンをクリックして、別のコンピューターにインストールできるパッケージファイルを作成することもできます。 パッケージが作成され、指定されたローカルファイルパスにコピーされます。 SharePoint ソリューションをローカルサーバーに配置するには、[**ビルド**] メニューの [**配置**] を使用します。 詳細については、「 [方法: sharepoint ソリューションをローカルの sharepoint サイトに配置および発行](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)する」を参照してください。

 リスト定義を配置する方法、イベントレシーバーを追加する方法、およびフィーチャーデザイナーとパッケージデザイナーを使用する方法については、「 [チュートリアル: プロジェクトタスクリスト定義の配置](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)」を参照してください。

## <a name="customize-the-deployment-process"></a>展開プロセスをカスタマイズする
 次の表は、SharePoint ソリューションをデバッグおよび配置するときに使用できる2つの配置構成を示しています。

|デプロイの構成|説明|
|------------------------------|-----------------|
|Default|既定の配置構成。 次の配置手順が実行されます。<br /><br /> 1. 配置前コマンドを実行します。<br />2. IIS アプリケーションプールをリサイクルします。<br />3. ソリューションを取り消します。<br />4. ソリューションを追加します。<br />5. 機能をアクティブにします。<br />6. 配置後コマンドを実行します。<br /><br /> パッケージがアンインストールされると、次の取り消し手順が実行されます。<br /><br /> 1. IIS アプリケーションプールをリサイクルします。<br />2. ソリューションを取り消します。|
|アクティブ化なし|この展開構成では、既定の構成と同じ手順が実行されますが、アクティブ化の手順はスキップされます。|

 独自の配置構成を作成して、1つの手順を完了したり、配置プロセスのステップの順序を変更したりすることができます。 詳細については、「[方法:SharePoint の配置構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」を参照してください。

 配置の前後に実行するコマンドを追加することもできます。 詳細については、「 [方法: SharePoint の配置コマンドを設定する](../sharepoint/how-to-set-sharepoint-deployment-commands.md)」を参照してください。

## <a name="publish-packages-to-a-remote-or-local-server"></a>リモートサーバーまたはローカルサーバーにパッケージを発行する
 リモートサーバーにサンドボックス化された SharePoint ソリューションを発行するには、メニューバーで [ **ビルド**]、[ **発行**] の順に選択し、[ **発行** ] ダイアログボックスの [ **SharePoint サイトに発行** ] をクリックして、リモートサーバーの URL (など) を指定し `https://someremoteserver.sharepoint.microsoftonline.com` ます。

 SharePoint ソリューションをローカルサーバーに発行するには、[ **発行** ] ダイアログボックスで、[ **ファイルシステムに発行** ] オプションを選択し、ローカルシステムパスを指定します。

 ソリューションが SharePoint に正常に発行されると、ソリューション **ギャラリー** にソリューションが表示され、アクティブ化できるようになります。 詳細については、「 [方法: リモートサーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」を参照してください。

### <a name="upgrade-published-packages"></a>発行されたパッケージのアップグレード
 発行後に Visual Studio で SharePoint プロジェクトに変更を加えた場合は、発行されたパッケージをアップグレードして変更を含める必要があります。 正常にアップグレードするには、パッケージの名前が一意である必要があります。 既存のアプリケーションを更新するときに発生する可能性のある、SharePoint サイトで同じ名前のパッケージが見つかった場合は、ファイル名の競合を警告するメッセージが表示され、パッケージの名前を変更できます。 再発行されると、SharePoint サイトに新しいパッケージが表示され、アップグレードできます。 アップグレードされたパッケージは、古いパッケージのデータを使用してソリューションを更新し、SharePoint でソリューションをアクティブ化します。 詳細については、「 [方法: リモートサーバー上で SharePoint ソリューションを配置、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
