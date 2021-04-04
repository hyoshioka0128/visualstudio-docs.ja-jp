---
title: SharePoint プロジェクトのカスタム配置手順の作成
description: このチュートリアルでは、SharePoint を実行しているサーバー上の SharePoint プロジェクトソリューションをアップグレードするためのカスタム配置手順を作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 77c80134ad63346b363c072ef2eff7e49978501f
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217932"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成
  SharePoint プロジェクトを配置すると、Visual Studio は一連の配置手順を特定の順序で実行します。 Visual Studio には多くの組み込みの配置手順が含まれていますが、独自に作成することもできます。

 このチュートリアルでは、SharePoint を実行しているサーバー上のソリューションをアップグレードするためのカスタム配置手順を作成します。 Visual Studio には、ソリューションの取り消しや追加など、多くのタスクに対する組み込みの配置手順が含まれていますが、ソリューションをアップグレードするための配置手順は含まれていません。 既定では、SharePoint ソリューションを配置すると、Visual Studio はまずソリューションを取り消し (既に配置されている場合)、ソリューション全体を再デプロイします。 組み込みの配置手順の詳細については、「 [SharePoint ソリューションパッケージの配置、発行、およびアップグレード](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md)」を参照してください。

 このチュートリアルでは、次のタスクについて説明します。

- 次の 2 つの主要タスクを実行する Visual Studio の拡張機能を作成する。

  - 拡張機能は、SharePoint ソリューションをアップグレードするためのカスタム配置手順を定義します。

  - この拡張機能は、新しい配置構成を定義するプロジェクト拡張機能を作成します。これは、特定のプロジェクトに対して実行される配置手順のセットです。 新しい展開構成には、カスタム配置手順といくつかの組み込みの展開手順が含まれています。

- 拡張機能アセンブリが呼び出す2つのカスタム SharePoint コマンドを作成します。 SharePoint コマンドは、SharePoint のサーバーオブジェクトモデルで Api を使用するために拡張機能アセンブリから呼び出すことができるメソッドです。 詳細については、「 [SharePoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

- 両方のアセンブリを配置するための Visual Studio Extension (VSIX) パッケージをビルドします。

- 新しい配置手順をテストする。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Windows、SharePoint、Visual Studio。

- Visual Studio SDK。 このチュートリアルでは、SDK の **Vsix プロジェクト** テンプレートを使用して、拡張機能を配置する vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- SharePoint のサーバーオブジェクトモデルの使用。 詳細については、「 [SharePoint Foundation Server-Side オブジェクトモデルの使用](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14))」を参照してください。

- SharePoint ソリューション。 詳細については、「 [ソリューションの概要](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))」を参照してください。

- SharePoint ソリューションをアップグレードしています。 詳細については、「 [ソリューションのアップグレード](/previous-versions/office/developer/sharepoint-2010/aa543659(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、次の3つのプロジェクトを作成する必要があります。

- 拡張機能を配置する VSIX パッケージを作成する VSIX プロジェクト。

- 拡張機能を実装するクラスライブラリプロジェクト。 このプロジェクトは、.NET Framework 4.5 をターゲットにする必要があります。

- カスタム SharePoint コマンドを定義するクラスライブラリプロジェクト。 このプロジェクトは、.NET Framework 3.5 をターゲットにする必要があります。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **機能拡張** ] ノードを選択します。

    > [!NOTE]
    > **機能拡張** ノードは、VISUAL Studio SDK をインストールした場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択します。

5. [ **VSIX プロジェクト** ] テンプレートを選択し、「 **upgradedeploymentstep**」という名前を指定して、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**ソリューションエクスプローラー** に **upgradedeploymentstep** プロジェクトを追加します。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューションエクスプローラー** で、UpgradeDeploymentStep ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **Windows** ] ノードをクリックします。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択します。

4. [ **クラスライブラリ** ] プロジェクトテンプレートを選択し、プロジェクトに **deploymentstepextension** という名前を指定して、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**Deploymentstepextension** プロジェクトをソリューションに追加し、既定の Class1 コードファイルを開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

#### <a name="to-create-the-sharepoint-command-project"></a>SharePoint コマンドプロジェクトを作成するには

1. **ソリューションエクスプローラー** で、UpgradeDeploymentStep ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [ **新しいプロジェクト** ] ダイアログボックスで、 **[Visual C#** ] または [ **Visual Basic**] を展開し、[ **Windows** ] ノードをクリックします。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 3.5** ] を選択します。

4. [ **クラスライブラリ** ] プロジェクトテンプレートを選択し、プロジェクトに **sharepointcommands** という名前を指定して、[ **OK** ] をクリックします。

     Visual Studio によって、 **Sharepointcommands** プロジェクトがソリューションに追加され、既定の Class1 コードファイルが開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-projects"></a>プロジェクトを構成する
 カスタム配置手順を作成するコードを記述する前に、コードファイルとアセンブリ参照を追加し、プロジェクトを構成する必要があります。

#### <a name="to-configure-the-deploymentstepextension-project"></a>DeploymentStepExtension プロジェクトを構成するには

1. **Deploymentstepextension** プロジェクトで、次の名前を持つ2つのコードファイルを追加します。

    - UpgradeStep

    - DeploymentConfigurationExtension

2. DeploymentStepExtension プロジェクトのショートカットメニューを開き、[参照の **追加**] を選択します。

3. [ **Framework** ] タブで、system.componentmodel アセンブリのチェックボックスをオンにします。

4. [ **拡張** ] タブで、VisualStudio アセンブリのチェックボックスをオンにし、[ **OK** ] をクリックします。

#### <a name="to-configure-the-sharepointcommands-project"></a>SharePointCommands プロジェクトを構成するには

1. **Sharepointcommands** プロジェクトで、Commands という名前のコードファイルを追加します。

2. **ソリューションエクスプローラー** で、[ **sharepointcommands** ] プロジェクトノードのショートカットメニューを開き、[**参照の追加**] を選択します。

3. [ **拡張** ] タブで、次のアセンブリのチェックボックスをオンにし、[ **OK** ] をクリックします。

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

## <a name="define-the-custom-deployment-step"></a>カスタム配置手順を定義する
 アップグレードの展開手順を定義するクラスを作成します。 配置手順を定義するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> ます。 カスタム配置手順を定義する場合は、常にこのインターフェイスを実装します。

#### <a name="to-define-the-custom-deployment-step"></a>カスタム配置手順を定義するには

1. **Deploymentstepextension** プロジェクトで、upgradestep コードファイルを開き、次のコードを貼り付けます。

    > [!NOTE]
    > このコードを追加すると、プロジェクトのコンパイルエラーが発生しますが、後の手順でコードを追加したときに、そのエラーが解消されます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs" id="Snippet1":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb" id="Snippet1":::

## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>カスタム展開手順を含む展開構成を作成する
 新しい配置構成のプロジェクト拡張機能を作成します。これには、いくつかの組み込みの配置手順と新しいアップグレード配置手順が含まれます。 この拡張機能を作成することにより、sharepoint 開発者は SharePoint プロジェクトの [配置のアップグレード] 手順を使用することができます。

 配置構成を作成するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ます。 SharePoint プロジェクトの拡張機能を作成する場合は、常にこのインターフェイスを実装します。

#### <a name="to-create-the-deployment-configuration"></a>展開構成を作成するには

1. **Deploymentstepextension** プロジェクトで deploymentstepextension コードファイルを開き、次のコードを貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs" id="Snippet2":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb" id="Snippet2":::

## <a name="create-the-custom-sharepoint-commands"></a>カスタム SharePoint コマンドを作成する
 SharePoint のサーバーオブジェクトモデルを呼び出す2つのカスタムコマンドを作成します。 1つのコマンドは、ソリューションが既にデプロイされているかどうかを判断します。もう1つのコマンドは、ソリューションをアップグレードします。

#### <a name="to-define-the-sharepoint-commands"></a>SharePoint コマンドを定義するには

1. **Sharepointcommands** プロジェクトで Commands コードファイルを開き、次のコードを貼り付けます。

     :::code language="csharp" source="../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs" id="Snippet4":::
     :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb" id="Snippet4":::

## <a name="checkpoint"></a>Checkpoint
 このチュートリアルのこの時点で、カスタム配置手順と SharePoint コマンドのすべてのコードがプロジェクトに含まれるようになりました。 これらをビルドして、エラーが発生せずにコンパイルされるようにします。

#### <a name="to-build-the-projects"></a>プロジェクトをビルドするには

1. **ソリューションエクスプローラー** で、 **deploymentstepextension** プロジェクトのショートカットメニューを開き、[**ビルド**] を選択します。

2. **Sharepointcommands** プロジェクトのショートカットメニューを開き、[**ビルド**] を選択します。

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>拡張機能を配置するための VSIX パッケージの作成
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、vsix プロジェクトの source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューションエクスプローラー** の **upgradedeploymentstep** プロジェクトで、 **source.extension.vsixmanifest** ファイルのショートカットメニューを開き、[**開く**] を選択します。

     Visual Studio によってマニフェスト エディターでファイルが開きます。 source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要になる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. [ **製品名** ] ボックスに、「 **SharePoint プロジェクトのアップグレードの配置手順**」と入力します。

3. [ **作成者** ] ボックスに「 **Contoso**」と入力します。

4. [ **説明** ] ボックスに「」と入力すると、 **SharePoint プロジェクトで使用できるカスタムのアップグレード配置手順が表示さ** れます。

5. エディターの [ **アセット** ] タブで、[ **新規** ] ボタンをクリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

6. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「 [Mefcomponent 要素 (VSX Schema)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト** を選択します。

8. [ **プロジェクト** ] ボックスの一覧で [ **deploymentstepextension**] を選択し、[ **OK** ] をクリックします。

9. マニフェストエディターで、[ **新規作成** ] ボタンをもう一度クリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

10. [種類] ボックスの一覧で、 **「** **SharePoint. コマンド. v4**」と入力します。

    > [!NOTE]
    > この要素は、Visual Studio 拡張機能に追加するカスタム拡張機能を指定します。 詳細については、「 [Asset 要素 (VSX Schema)](/previous-versions/dd393737(v=vs.110))」を参照してください。

11. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト** を選択します。

12. [ **プロジェクト** ] ボックスの一覧で [ **sharepointcommands**] を選択し、[ **OK** ] をクリックします。

13. メニューバーで [ビルド] [ソリューションの **ビルド**] の順に選択し、  >  ソリューションがエラーなしでコンパイルされることを確認します。

14. UpgradeDeploymentStep プロジェクトのビルド出力フォルダーに、UpgradeDeploymentStep .vsix ファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="prepare-to-test-the-upgrade-deployment-step"></a>アップグレードの展開手順をテストする準備をする
 アップグレードの配置手順をテストするには、最初にサンプルソリューションを SharePoint サイトに配置する必要があります。 まず、Visual Studio の実験用インスタンスで拡張機能をデバッグします。 次に、配置手順をテストするために使用するリスト定義とリストインスタンスを作成し、SharePoint サイトに配置します。 次に、リスト定義とリストインスタンスを変更し、それらを再配置して、既定の配置プロセスで SharePoint サイトのソリューションを上書きする方法を示します。

 このチュートリアルの後の方で、リスト定義とリストインスタンスを変更し、SharePoint サイトでアップグレードします。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 管理者資格情報を使用して Visual Studio を再起動し、UpgradeDeploymentStep ソリューションを開きます。

2. DeploymentStepExtension プロジェクトで、UpgradeStep コードファイルを開き、メソッドとメソッドの最初のコード行にブレークポイントを追加し `CanExecute` `Execute` ます。

3. **F5** キーを押すか、メニューバーで [**デバッグ**] [デバッグ開始] の順に選択して、デバッグを開始  >  します。

4. Visual Studio では、SharePoint プロジェクト/1.0 の%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade 配置手順の拡張機能がインストールされ、Visual Studio の実験用インスタンスが開始されます。 この Visual Studio のインスタンスで、アップグレードのデプロイ手順をテストします。

#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>リスト定義とリストインスタンスを使用して SharePoint プロジェクトを作成するには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  ます。

2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **SharePoint** ] ノードを展開して、[ **2010** ] ノードを選択します。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧に **.NET Framework 3.5** が表示されていることを確認します。

    およびのプロジェクトで [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] は、このバージョンの .NET Framework が必要です。

4. プロジェクトテンプレートの一覧で [ **SharePoint 2010 プロジェクト**] を選択し、プロジェクトに **EmployeesListDefinition** という名前を指定して、[ **OK** ] をクリックします。

5. **SharePoint カスタマイズウィザード** で、デバッグに使用するサイトの URL を入力します。

6. [ **この SharePoint ソリューションの信頼レベル** を指定してください] で、[ **ファームソリューションとして配置** する] オプションボタンを選択します。

   > [!NOTE]
   > アップグレードの展開手順では、サンドボックスソリューションはサポートされていません。

7. **[完了]** をクリックします。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] EmployeesListDefinition プロジェクトを作成します。

8. EmployeesListDefinition プロジェクトのショートカットメニューを開き、[ **追加**]、[ **新しい項目**] の順に選択します。

9. [ **新しい項目の追加-EmployeesListDefinition** ] ダイアログボックスで、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

10. **リスト** 項目テンプレートを選択し、[ **Employees] ボックス** に名前を入力して、[**追加**] をクリックします。

     SharePoint カスタマイズウィザードが表示されます。

11. [ **リスト設定の選択** ] ページで、次の設定を確認し、[ **完了** ] をクリックします。

    1. [**一覧に表示する名前を** 指定してください] ボックスに [Employees] の **一覧** が表示されます。

    2. **[次に基づいてカスタマイズ可能なリストを作成する**] オプションボタンが選択されています。

    3. **[次に基づいてカスタマイズ可能なリストを作成する**] の一覧では、**既定 (空白)** が選択されます。

       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] タイトル列と1つの空のインスタンスを含む Employees リストアイテムを作成し、リストデザイナーを開きます。

12. リストデザイナーの [ **列** ] タブで、[ **新規または既存の列名を入力** してください] 行を選択し、[ **列の表示名** ] の一覧に次の列を追加します。

    1. 名

    2. [会社]

    3. Business Phone (勤務先電話番号)

    4. 電子メール

13. すべてのファイルを保存し、リストデザイナーを閉じます。

14. **ソリューションエクスプローラー** で、[ **employees list** ] ノードを展開し、[ **employees] リストインスタンス** の子ノードを展開します。

15. *Elements.xml* ファイルで、このファイルの既定の xml を次の xml に置き換えます。 この XML は、リストの名前を **Employees** に変更し、Jim という名前の従業員に関する情報を追加します。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
        <Data>
          <Rows>
            <Row>
              <Field Name="Title">Hance</Field>
              <Field Name="FirstName">Jim</Field>
              <Field Name="Company">Contoso</Field>
              <Field Name="Business Phone">555-555-5555</Field>
              <Field Name="E-Mail">jim@contoso.com</Field>
            </Row>
          </Rows>
        </Data>
      </ListInstance>
    </Elements>
    ```

16. *Elements.xml* ファイルを保存して閉じます。

17. EmployeesListDefinition プロジェクトのショートカットメニューを開き、[ **開く** ] または [ **プロパティ**] を選択します。

     プロパティデザイナーが開きます。

18. [ **SharePoint** ] タブで、[ **デバッグ後に自動取り消し** ] チェックボックスをオフにし、プロパティを保存します。

#### <a name="to-deploy-the-list-definition-and-list-instance"></a>リスト定義とリストインスタンスを展開するには

1. **ソリューションエクスプローラー** で、 **EmployeesListDefinition** プロジェクトノードを選択します。

2. [ **プロパティ** ] ウィンドウで、[ **アクティブな配置構成** ] プロパティが [ **既定**] に設定されていることを確認します。

3. **F5** キーを押すか、メニューバーで [**デバッグ**] [  >  **デバッグの開始**] の順に選択します。

4. プロジェクトが正常にビルドされたこと、web ブラウザーが SharePoint サイトを開き、[クイック起動] バーの [ **リスト** ] 項目に [新しい **従業員** ] の一覧が含まれていること、および [ **従業員** ] の一覧に Jim hance エントリが含まれていることを確認します。

5. Web ブラウザーを閉じます。

#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>リスト定義とリストインスタンスを変更して再展開するには

1. EmployeesListDefinition プロジェクトで、 **Employee List Instance** プロジェクト項目の子である *Elements.xml* ファイルを開きます。

2. `Data`リストから Jim hance エントリを削除するには、要素とその子を削除します。

     完了すると、ファイルには次の XML が含まれます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <ListInstance Title="Employees"
                    OnQuickLaunch="TRUE"
                    TemplateType="10000"
                    Url="Lists/Employees"
                    Description="Simple list to test upgrade deployment step">
      </ListInstance>
    </Elements>
    ```

3. *Elements.xml* ファイルを保存して閉じます。

4. **Employees List** プロジェクト項目のショートカットメニューを開き、[**開く**] または [**プロパティ**] を選択します。

5. リストデザイナーで [ **ビュー** ] タブを選択します。

6. [ **選択された列** ] ボックスの一覧で [ **添付ファイル**] を選択し、< キーを選択して、その列を [ **使用できる列** ] ボックスの一覧に移動します。

7. 前の手順を繰り返して、[**選択した列**] ボックスの一覧から [**使用できる列**] の一覧に [勤務先の **電話**] 列を移動します。

     この操作により、SharePoint サイトの **従業員** リストの既定のビューからこれらのフィールドが削除されます。

8. **F5** キーを押すか、メニューバーで [**デバッグ**] [デバッグ開始] の順に選択して、デバッグを開始  >  します。

9. [展開の **競合** ] ダイアログボックスが表示されていることを確認します。

     ソリューションが既に配置されている SharePoint サイトにソリューション (リストインスタンス) を配置しようとすると、このダイアログボックスが表示されます。 このダイアログボックスは、このチュートリアルの後の手順でアップグレードの配置手順を実行するときには表示されません。

10. [ **配置の競合** ] ダイアログボックスで、[ **自動的に解決** する] オプションを選択します。

     Visual Studio によって SharePoint サイトのリストインスタンスが削除され、プロジェクトにリストアイテムが配置されて、SharePoint サイトが開きます。

11. クイック起動バーの [ **リスト** ] セクションで、[ **従業員** ] の一覧を選択し、次の詳細を確認します。

    - **添付ファイル** と **自宅電話** の列は、一覧のこのビューに表示されません。

    - リストが空です。 **既定** の配置構成を使用してソリューションを再配置すると、 **employee** リストがプロジェクトの新しい空のリストに置き換えられました。

## <a name="test-the-deployment-step"></a>配置手順をテストする
 これで、アップグレードのデプロイ手順をテストする準備ができました。 まず、SharePoint のリストインスタンスに項目を追加します。 次に、リスト定義とリストインスタンスを変更し、SharePoint サイトでアップグレードします。また、[アップグレード] 配置手順で新しい項目が上書きされないことを確認します。

#### <a name="to-manually-add-an-item-to-the-list"></a>項目を一覧に手動で追加するには

1. SharePoint サイトのリボンの [ **リストツール** ] タブで、[ **アイテム** ] タブを選択します。

2. **新しい** グループで、[**新しい項目**] を選択します。

     別の方法として、項目リスト内の [ **新しい項目の追加** ] リンクを選択することもできます。

3. [ **従業員-新しい項目** ] ウィンドウの [ **タイトル** ] ボックスに、「 **ファシリティマネージャー**」と入力します。

4. [ **名** ] ボックスに、「 **Andy**」と入力します。

5. [ **会社** ] ボックスに「 **Contoso**」と入力します。

6. [ **保存** ] ボタンをクリックし、一覧に新しい項目が表示されていることを確認して、web ブラウザーを閉じます。

     このチュートリアルの後半では、この項目を使用して、アップグレードの展開手順でこの一覧の内容が上書きされないことを確認します。

#### <a name="to-test-the-upgrade-deployment-step"></a>アップグレードの展開手順をテストするには

1. Visual Studio の実験用インスタンスの **ソリューションエクスプローラー** で、[ **EmployeesListDefinition** ] プロジェクトノードのショートカットメニューを開き、[ **プロパティ**] を選択します。

    プロパティエディターまたはデザイナーが開きます。

2. [ **SharePoint** ] タブで、[ **アクティブな配置] 構成** プロパティを [ **アップグレード**] に設定します。

    このカスタム展開構成には、新しいアップグレードの展開手順が含まれています。

3. **Employees List** プロジェクト項目のショートカットメニューを開き、[**プロパティ**] を選択するか、[**開く**] をクリックします。

    プロパティエディターまたはデザイナーが開きます。

4. [ **表示** ] タブの [ **電子メール** ] 列を選択し、キーを選択して [ **<** **選択し** た列] ボックスの一覧から [ **使用できる列** ] ボックスの一覧に移動します。

    この操作により、SharePoint サイトの **従業員** リストの既定のビューからこれらのフィールドが削除されます。

5. **F5** キーを押すか、メニューバーで [**デバッグ**] [デバッグ開始] の順に選択して、デバッグを開始  >  します。

6. Visual Studio のもう一方のインスタンスで、先ほど `CanExecute` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

7. F5 キーをもう一度 **押す** か、メニューバーで [**デバッグ**] [続行] を選択し  >  ます。

8. メソッドで前に設定したブレークポイントでコードが停止していることを確認し `Execute` ます。

9. F5 キーを **押す** か、メニューバーで [**デバッグ**] [最終時間] の順に選択し  >  ます。

     Web ブラウザーで SharePoint サイトが開きます。

10. [クイック起動] 領域の [ **リスト** ] セクションで、[ **従業員** ] の一覧を選択し、次の詳細を確認します。

    - 前に手動で追加した項目 (Andy の場合は、ファシリティマネージャー) が一覧に表示されます。

    - [ **勤務先電話番号** ] 列と [ **電子メールアドレス** ] 列は、一覧のこのビューに表示されません。

      **アップグレード** の配置構成によって、SharePoint サイト上の既存の **Employees** リストインスタンスが変更されます。 **アップグレード** 構成ではなく **既定** の配置構成を使用した場合は、配置の競合が発生します。 Visual Studio は、 **Employees** リストを置き換えることで競合を解決します。 Andy の項目 (ファシリティマネージャー) は削除されます。

## <a name="clean-up-the-development-computer"></a>開発用コンピューターのクリーンアップ
 アップグレードの展開手順のテストが完了したら、SharePoint サイトからリストインスタンスとリストの定義を削除し、Visual Studio から配置手順拡張機能を削除します。

#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>SharePoint サイトからリストインスタンスを削除するには

1. リストがまだ開いていない場合は、SharePoint サイトの **従業員** リストを開きます。

2. SharePoint サイトのリボンで、[ **リストツール** ] タブを選択し、[ **リスト** ] タブを選択します。

3. [ **設定** ] グループで、[ **リストの設定** ] 項目を選択します。

4. [ **アクセス許可と管理**] で、[ **このリストを削除** する] コマンドを選択し、[ **OK]** を選択して、リストをごみ箱に送信することを確認してから、web ブラウザーを閉じます。

#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>SharePoint サイトからリスト定義を削除するには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ビルド** の取り消し] を選択し  >  ます。

     Visual Studio では、SharePoint サイトからリスト定義が取り消されます。

#### <a name="to-uninstall-the-extension"></a>拡張機能をアンインストールするには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ツール**] [  >  **拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、 **SharePoint プロジェクトの [配置のアップグレード] ステップ** を選択し、[ **アンインストール** ] をクリックします。

3. 表示されるダイアログボックスで、[ **はい]** を選択して拡張機能をアンインストールすることを確認し、[ **今すぐ再起動** ] を選択してアンインストールを完了します。

4. Visual Studio の両方のインスタンス (実験的なインスタンスと、UpgradeDeploymentStep ソリューションが開いている Visual Studio のインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint のパッケージ化と配置の拡張](../sharepoint/extending-sharepoint-packaging-and-deployment.md)