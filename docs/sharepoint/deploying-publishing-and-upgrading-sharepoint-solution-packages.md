---
title: SharePoint ソリューション パッケージの展開、発行、&アップグレード
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d8e55b01173e749395f60d189366a08907bdaccd
ms.sourcegitcommit: 7b60e81414a82c6d34f6de1a1f56115c9cd26943
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2020
ms.locfileid: "81444971"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>SharePoint ソリューション パッケージの展開、発行、およびアップグレード
  Visual Studio で SharePoint ソリューションを開発した後、そのパッケージ (.wsp) ファイルをローカル SharePoint サーバーに配置するか、リモートまたはローカルの SharePoint サーバーに発行することができます。 ファイルを展開する場合は、パッケージ ファイル (.wsp) の展開方法をカスタマイズできます。

> [!NOTE]
> 現在、リモートの SharePoint サーバーに発行できるのは、サンドボックス ソリューションのみです。 詳細については、「[サンドボックス ソリューションに関する考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

## <a name="deploy-publish-and-upgrade"></a>展開、発行、およびアップグレード
 *配置*とは、Visual Studio の SharePoint プロジェクトからローカル ホストにビルドされた SharePoint ソリューション ファイルをコピーすることを指します。 展開されたソリューションでは、インターネット インフォメーション サービス (IIS) プールのリサイクル、配置後のソリューションのアクティブ化などの展開手順を構成できます。 配置するには、[**ビルド**] メニューの [**配置**] コマンドを使用します。 詳細については[、「[方法] SharePoint 展開構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」および[「SharePoint ソリューションをローカル SharePoint サイトに展開および発行する方法](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)」を参照してください。

 *発行*とは、サンドボックス化された SharePoint ソリューション ファイルをリモート SharePoint サイトにアップロードすることです。つまり、別のシステム上にあるサイトです。 SharePoint サンドボックス ソリューション ファイルをローカル SharePoint サイトに発行することもできますが、発行先のサイトがローカルまたはリモートのどちらであるかに関係なく、展開手順を構成することはできません。

 *アップグレードと*は、既存のリモートまたはローカルに発行された SharePoint ソリューションを更新することです。 Visual Studio で SharePoint ソリューションに変更が加えられた後、ソリューションのパッケージ ファイル名を変更し、ソリューションを再発行し、ソリューションが正常に再発行された後にソリューションをアップグレードします。 ローカルに発行されたソリューションを再発行する場合は、既存のソリューション ファイルを上書きできます。

## <a name="deploy-packages"></a>パッケージの配置
 テストとデバッグのために、開発用コンピューター上の SharePoint サーバーにパッケージ ファイルを展開できます。 [**発行**] ダイアログ ボックスの [**ファイル システムに発行**] オプション ボタンを選択して、別のコンピューターにインストールできるパッケージ ファイルを作成することもできます。 パッケージが作成され、指定したローカル ファイル パスにコピーされます。 SharePoint ソリューションをローカル サーバーに展開するには、[**ビルド**] メニューの [**配置**] コマンドを使用します。 詳細については、「 [[方法] SharePoint ソリューションをローカル SharePoint サイトに展開して発行する](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)」を参照してください。

 リスト定義を配置する方法、イベント レシーバーを追加する方法、およびフィーチャー デザイナーとパッケージ デザイナーの使用方法については、「[チュートリアル: プロジェクト タスク リスト定義を配置する](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)」を参照してください。

## <a name="customize-the-deployment-process"></a>展開プロセスのカスタマイズ
 次の表は、SharePoint ソリューションをデバッグおよび展開するときに使用できる 2 つの展開構成を示しています。

|展開構成|説明|
|------------------------------|-----------------|
|Default|既定の展開構成。 次の展開手順が実行されます。<br /><br /> 1. 配置前コマンドを実行します。<br />2. IIS アプリケーション プールをリサイクルします。<br />3. リトラクト溶液。<br />4. ソリューションを追加します。<br />5. 機能をアクティブにします。<br />6. 配置後コマンドを実行します。<br /><br /> パッケージをアンインストールすると、次の取り消し手順が実行されます。<br /><br /> 1. IIS アプリケーション プールをリサイクルします。<br />2. リトラクト溶液。|
|ライセンス認証なし|この展開構成は、既定の構成と同じ手順を実行しますが、アクティブ化の手順はスキップされます。|

 独自の展開構成を作成して、1 つの手順を完了したり、展開プロセスの手順の順序を変更したりできます。 詳細については、「[方法 : SharePoint 展開構成を編集する](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)」を参照してください。

 配置の前後に実行するコマンドを追加することもできます。 詳細については、「[方法 : SharePoint 展開コマンドを設定する](../sharepoint/how-to-set-sharepoint-deployment-commands.md)」を参照してください。

## <a name="publish-packages-to-a-remote-or-local-server"></a>リモート サーバーまたはローカル サーバーにパッケージを発行する
 サンドボックス化された SharePoint ソリューションをリモート サーバーに発行するには、メニュー バーで [**ビルド**] メニューの [**発行**] をクリックし、[**発行**] ダイアログ ボックスで **[SharePoint サイトに発行**]`https://someremoteserver.sharepoint.microsoftonline.com`オプション ボタンを選択し、リモート サーバーの URL を指定します。

 SharePoint ソリューションをローカル サーバーに発行するには、[**発行**] ダイアログ ボックスで[**ファイル システムに発行**] オプション ボタンを選択し、ローカル システム パスを指定します。

 ソリューションが SharePoint に正常に発行されると、ソリューションがソリューション**ギャラリー**に表示され、アクティブ化できます。 詳細については、「[方法 : リモート サーバー上で SharePoint ソリューションを展開、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」を参照してください。

### <a name="upgrade-published-packages"></a>発行済みパッケージのアップグレード
 発行後に Visual Studio で SharePoint プロジェクトに変更を加えた場合、発行済みパッケージをアップグレードして変更を反映させる必要があります。 正常にアップグレードするには、パッケージに一意の名前が必要です。 SharePoint サイトで同じ名前のパッケージが見つかった場合 (既存のアプリケーションを更新するときに発生する可能性があります)、エラーメッセージがファイル名の競合を通知し、パッケージの名前を変更できます。 再発行後、新しいパッケージは SharePoint サイトに表示され、アップグレードできます。 アップグレードされたパッケージは、古いパッケージのデータを使用してソリューションを更新し、SharePoint でソリューションをアクティブ化します。 詳細については、「[方法 : リモート サーバー上で SharePoint ソリューションを展開、発行、およびアップグレードする](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と展開](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
