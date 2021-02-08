---
title: Cloud Services の使用 (延長サポート) (プレビュー)
description: Azure Resource Manager を Visual Studio と共に使用して Cloud Services (拡張サポート) を作成およびデプロイする方法について説明します
author: ghogen
manager: jmartens
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 01/25/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 39a76f4c76afb2ed0c738adfc477807eebfdbc61
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99841134"
---
# <a name="create-and-deploy-to-cloud-services-extended-support-in-visual-studio-preview"></a>Visual Studio で Cloud Services (拡張サポート) を作成してデプロイする (プレビュー)

[Visual Studio 2019 バージョン 16.9](https://visualstudio.microsoft.com/vs/preview) (現在プレビュー段階) 以降では、Azure Resource Manager を使用してクラウドサービスを操作できます。これにより、Azure リソースのメンテナンスと管理が大幅に簡素化され、港湾ます。 これは、 *Cloud Services (拡張サポート)* と呼ばれる新しい Azure サービスによって有効になります。 既存のクラウド サービスを Cloud Services (延長サポート) に発行することができます。 この Azure サービスの詳細については、[Cloud Services (延長サポート) に関するドキュメント](/azure/cloud-services-extended-support/overview)を参照してください。

## <a name="publish-to-cloud-services-extended-support"></a>Cloud Services に発行 (拡張サポート)

既存の Azure クラウドサービスプロジェクトを Cloud Services (拡張サポート) に発行する場合は、従来の Azure クラウドサービスに発行する機能を引き続き保持します。 Visual Studio 2019 バージョン 16.9 Preview 3 以降では、従来のクラウドサービスプロジェクトには、 **発行** コマンドの特別なバージョンである **publish (拡張サポート)** が含まれています。 このコマンドは、 **ソリューションエクスプローラー** のショートカットメニューに表示されます。

Cloud Services (拡張サポート) に発行する場合、いくつかの違いがあります。 たとえば、 **ステージング** または **運用環境** に発行するかどうかは確認されません。これらのデプロイスロットは、拡張サポート公開モデルには含まれていないためです。 代わりに、Cloud Services (拡張サポート) を使用して、複数のデプロイを設定し、Azure portal でデプロイをスワップすることができます。 Visual Studio ツールでは、16.9 Preview 3 でこの設定を行うことができますが、Cloud Services の今後のリリース (拡張サポート) まではスワップ機能が有効になりません。また、プレビュー期間中はデプロイ時にエラーが発生する可能性があります。

クラシック Azure クラウドサービスを Cloud Services (拡張サポート) に発行する前に、プロジェクトで使用されているストレージアカウントを確認し、ストレージ V1 またはストレージ V2 アカウントであることを確認してください。 クラシックストレージアカウントの種類は、デプロイ時にエラーメッセージで失敗します。 診断で使用されるストレージアカウントを必ず確認してください。 診断ストレージアカウントを確認するには、「 [Azure Cloud Services と仮想マシンの診断を設定](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)する」を参照してください。 サービスが従来のストレージアカウントを使用している場合は、アップグレードすることができます。「 [汎用 v2 ストレージアカウントへのアップグレード」を](/azure/storage/common/storage-account-upgrade?tabs=azure-portal)参照してください。  ストレージアカウントの種類に関する一般的な情報については、「 [ストレージアカウントの概要](/azure/storage/common/storage-account-overview)」を参照してください。

### <a name="to-publish-a-classic-azure-cloud-service-project-to-cloud-services-extended-support"></a>クラシック Azure Cloud Service プロジェクトを Cloud Services に発行するには (拡張サポート)

1. Cloud Services (延長サポート) は現在、プレビュー段階です。 次のようにして、サブスクリプションに機能を登録します。

   ```azurepowershell-interactive
   Register-AzProviderFeature -FeatureName CloudServices -ProviderNamespace Microsoft.Compute
   ```

1. Azure クラウドサービス (クラシック) プロジェクトでプロジェクトノードを右クリックし、[ **発行 (拡張サポート)**] を選択します。最初の画面に **発行ウィザード** が開きます。

   ![メニューから [発行 (拡張サポート)] を選択します。](./media/cloud-services-extended-support/publish-commands-on-menu.png)

   **発行** ウィザードが表示されます。

   ![サインイン ページ](./media/cloud-services-extended-support/publish-step1.png)

1. **アカウント** - アカウント ドロップダウン リストでアカウントを選択するか、**[アカウントの追加]** を選択します。

1. **[サブスクリプションの選択]** - デプロイに使用するサブスクリプションを選択します。

1. **[次へ]** を選択して、 **[設定]** ページに移動します。

   ![[共通設定]](./media/cloud-services-extended-support/publish-settings.png)

1. **クラウドサービス (拡張サポート)** -ドロップダウンを使用して、既存のクラウドサービス (拡張サポート) を選択するか、[ **新規作成**] を選択して作成します。 データセンターは、各クラウドサービス (拡張サポート) に対してかっこで囲まれて表示されます。 クラウドサービスのデータセンターの場所 (拡張サポート) は、ストレージアカウントのデータセンターの場所と同じにすることをお勧めします。

   新しいサービスを作成することを選択した場合は、[ **クラウドサービスの作成 (拡張サポート)** ] ダイアログボックスが表示されます。 クラウドサービスに使用する場所とリソースグループを指定します (拡張サポート)。

   ![クラウドサービスを作成する (拡張サポート)](./media/cloud-services-extended-support/extended-support-dialog.png)

1. **[ビルド構成]** - **[デバッグ]** または **[リリース]** を選択します。

1. **[サービス構成]** - **[クラウド]** または **[ローカル]** を選択します。

1. **[ストレージ アカウント]** - このデプロイに使用するストレージ アカウントを選択するか、 **[新規作成]** を選択してストレージ アカウントを作成します。 ストレージ アカウントごとに、リージョンがかっこ内に表示されます。 ストレージ アカウントのデータ センターの場所は、クラウド サービスのデータ センターの場所 ([共通設定]) と同じであることが推奨されます。

   Azure ストレージ アカウントには、アプリケーション デプロイのパッケージが格納されます。

1. **Key vault** -このクラウドサービス (拡張サポート) のシークレットを含むキーコンテナーを指定します。 これは、リモートデスクトップが有効になっている場合、または証明書が構成に追加されている場合に有効になります。

1. **[すべてのロールのリモート デスクトップを有効にする]** - サービスにリモート接続できるようにする場合は、このオプションを選択します。 資格情報を指定するように求められます。

   ![リモート デスクトップの設定](./media/cloud-services-extended-support/remote-desktop-configuration.png)

1. **[次へ]** を選択して、 **[診断設定]** ページに移動します。

   ![診断設定](./media/cloud-services-extended-support/diagnostics-settings.png)

   診断を使用すると、Azure クラウドサービス (拡張サポート) のトラブルシューティングを行うことができます。 診断については、「[Azure クラウド サービスおよび仮想マシン用の診断の構成](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)」をご覧ください。 Application Insights については、「[Application Insights とは何か?](/azure/application-insights/app-insights-overview)」をご覧ください。

1. **[次へ]** を選択して **[概要]** ページに移動します。

   ![まとめ](./media/cloud-services-extended-support/publish-summary.png)

1. **[ターゲット プロファイル]** - 選択した設定から発行プロファイルを作成できます。 たとえば、テスト環境用と運用環境用に 1 つずつプロファイルを作成できます。 このプロファイルを保存するには、**[保存]** アイコンをクリックします。 ウィザードでプロファイルが作成され、Visual Studio プロジェクトに保存されます。 プロファイル名を変更するには、**[ターゲット プロファイル]** の一覧を開き、[**管理…]** を選択します。

   > [!Note]
   > 発行プロファイルが Visual Studio のソリューションエクスプローラーに表示され、プロファイル設定が *azurepubxml* 拡張機能を持つファイルに書き込まれます。 設定は、XML タグの属性として保存されます。

1. プロジェクトのデプロイのすべての設定を構成したら、ダイアログの下部にある **[発行]** をクリックします。 Visual Studio の **[Azure アクティビティ ログ]** 出力ウィンドウでプロセスの状態を監視できます。 [ **ポータルで開く** ] リンクを選択します。 

お疲れさまでした。 クラウドサービス (拡張サポート) プロジェクトを Azure に発行しました。 同じ設定を使用して再度発行する場合は、発行プロファイルを再利用するか、この手順を繰り返して新しいプロファイルを作成します。 配置に使用される Azure Resource Manager (ARM) テンプレートとパラメーターは、 *bin// \<configuration\> Publish* フォルダーに保存されます。

## <a name="clean-up-azure-resources"></a>Azure リソースをクリーンアップする

このチュートリアルに従って作成した Azure リソースをクリーンアップするには、 [Azure portal](https://portal.azure.com)にアクセスし、[ **リソースグループ**] を選択して、クラウドサービスの作成に使用したリソースグループ (拡張サポート) を探して開き、[ **リソースグループの削除**] を選択します。

## <a name="next-steps"></a>次のステップ

**[発行]** 画面の **[構成]** ボタンを使用して、継続的インテグレーション (CI) を設定します。 詳細については、「[Azure Pipelines のドキュメント](/azure/devops/pipelines/?view=azure-devops&preserve-view=true)」を参照してください。
