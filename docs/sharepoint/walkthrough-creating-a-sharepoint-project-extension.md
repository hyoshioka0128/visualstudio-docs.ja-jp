---
title: 'チュートリアル: SharePoint プロジェクト拡張機能の作成 |Microsoft Docs'
description: SharePoint プロジェクトの拡張機能を作成します。この拡張機能を使用して、プロジェクトが追加、削除、または名前変更されたときなど、プロジェクトレベルのイベントに応答できます。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 378e839ea5f4223873fbbeec8d7b401ae0b16fc0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99918758"
---
# <a name="walkthrough-create-a-sharepoint-project-extension"></a>チュートリアル: SharePoint プロジェクト拡張機能の作成
  このチュートリアルでは、SharePoint プロジェクトの拡張機能を作成する方法について説明します。 プロジェクト拡張機能を使用して、プロジェクトが追加、削除、または名前変更されたときなどのプロジェクトレベルのイベントに応答できます。 また、カスタムプロパティを追加したり、プロパティ値が変更したときに応答したりすることもできます。 プロジェクト項目の拡張機能とは異なり、プロジェクトの拡張機能を特定の SharePoint プロジェクトの種類に関連付けることはできません。 プロジェクト拡張機能を作成すると、で任意の種類の SharePoint プロジェクトが開かれたときに、拡張機能が読み込まれ [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

 このチュートリアルでは、「」で作成した任意の SharePoint プロジェクトに追加されるカスタムのブール型プロパティを作成し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 **True** に設定すると、新しいプロパティによって、Images リソースフォルダーがプロジェクトに追加またはマップされます。 **False** に設定すると、Images フォルダーが存在する場合は削除されます。 詳細については、「 [方法: マップされたフォルダーを追加および削除](../sharepoint/how-to-add-and-remove-mapped-folders.md)する」を参照してください。

 このチュートリアルでは、次のタスクについて説明します。

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint プロジェクト用の拡張機能を作成し、次の手順を実行します。

  - カスタムプロジェクトプロパティをプロパティウィンドウに追加します。 プロパティは、任意の SharePoint プロジェクトに適用されます。

  - は、SharePoint プロジェクトオブジェクトモデルを使用して、マップされたフォルダーをプロジェクトに追加します。

  - は、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] オートメーションオブジェクトモデル (DTE) を使用して、マップされたフォルダーをプロジェクトから削除します。

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]プロジェクトプロパティの拡張機能アセンブリを配置するための拡張機能 (VSIX) パッケージをビルドする。

- プロジェクトプロパティのデバッグとテスト。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- 、SharePoint、およびのサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 このチュートリアルでは、の **Vsix プロジェクト** テンプレートを使用して、 [!INCLUDE[TLA2#tla_sdk](../sharepoint/includes/tla2sharptla-sdk-md.md)] プロジェクトのプロパティ拡張機能を配置するための vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、次の2つのプロジェクトを作成する必要があります。

- プロジェクト拡張機能を配置する VSIX パッケージを作成するための VSIX プロジェクト。

- プロジェクト拡張機能を実装するクラスライブラリプロジェクト。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **機能拡張** ] ノードを選択します。

    > [!NOTE]
    > このノードは、Visual Studio SDK をインストールした場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択し、[ **VSIX プロジェクト** ] テンプレートを選択します。

5. [ **名前** ] ボックスに「 **projectextensionpackage**」と入力し、[ **OK** ] をクリックします。

     **Projectextensionpackage** プロジェクトが **ソリューションエクスプローラー** に表示されます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューションエクスプローラー** で、ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **Windows**] を選択します。

3. ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 4.5** ] を選択し、[ **クラスライブラリ** ] プロジェクトテンプレートを選択します。

4. [ **名前** ] ボックスに「 **projectextension**」と入力し、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**Projectextension** プロジェクトをソリューションに追加し、既定の Class1 コードファイルを開きます。

5. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-project"></a>プロジェクトを構成する
 プロジェクト拡張機能を作成するコードを記述する前に、コードファイルとアセンブリ参照を拡張機能プロジェクトに追加します。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. **Customproperty** という名前のコードファイルを projectextension プロジェクトに追加します。

2. **Projectextension** プロジェクトのショートカットメニューを開き、[参照の **追加**] を選択します。

3. [ **参照マネージャー-CustomProperty** ] ダイアログボックスで、[ **Framework** ] ノードを選択し、system.componentmodel アセンブリおよび system.string アセンブリの横にあるチェックボックスをオンにします。

4. [ **拡張機能** ] ノードを選択し、VisualStudio アセンブリと EnvDTE アセンブリの横にあるチェックボックスをオンにして、[ **OK** ] をクリックします。

5. **ソリューションエクスプローラー** で、 **projectextension** プロジェクトの [**参照**] フォルダーの下にある [ **EnvDTE**] を選択します。

6. [ **プロパティ** ] ウィンドウで、[ **相互運用機能型の埋め込み** ] プロパティを **False** に変更します。

## <a name="define-the-new-sharepoint-project-property"></a>新しい SharePoint プロジェクトプロパティの定義
 プロジェクトの拡張機能と新しいプロジェクトプロパティの動作を定義するクラスを作成します。 新しいプロジェクトの拡張機能を定義するために、クラスはインターフェイスを実装し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ます。 SharePoint プロジェクトの拡張機能を定義する場合は、常にこのインターフェイスを実装します。 また、を <xref:System.ComponentModel.Composition.ExportAttribute> クラスに追加します。 この属性 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用すると、で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 属性のコンストラクターに渡します。

#### <a name="to-define-the-new-sharepoint-project-property"></a>新しい SharePoint プロジェクトプロパティを定義するには

1. 次のコードを CustomProperty コードファイルに貼り付けます。

     [!code-vb[SPExt_ProjectExtension#1](../sharepoint/codesnippet/VisualBasic/projectextension/customproperty.vb#1)]
     [!code-csharp[SPExt_ProjectExtension#1](../sharepoint/codesnippet/CSharp/projectextension/customproperty.cs#1)]

## <a name="build-the-solution"></a>ソリューションをビルドする
 次に、ソリューションをビルドして、エラーを発生させずにコンパイルされるようにします。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="create-a-vsix-package-to-deploy-the-project-property-extension"></a>プロジェクトプロパティ拡張機能を配置するための VSIX パッケージの作成
 プロジェクト拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューションエクスプローラー** で、source.extension.vsixmanifest ファイルのショートカットメニューを開き、[**開く**] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] マニフェストデザイナーでファイルを開きます。 [ **メタデータ** ] タブに表示される情報は、 **拡張機能と更新プログラム** にも表示されます。 すべての VSIX パッケージには source.extension.vsixmanifest ファイルが必要です。 このファイルの詳細については、「 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. [ **製品名** ] ボックスに、「 **カスタムプロジェクトプロパティ**」と入力します。

3. [ **作成者** ] ボックスに「 **Contoso**」と入力します。

4. [ **説明** ] ボックスに、 **Images リソースフォルダーのプロジェクトへのマッピングを切り替えるカスタム SharePoint プロジェクトプロパティ** を入力します。

5. [ **アセット** ] タブを選択し、[ **新規作成** ] をクリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

6. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MEFComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「 [Mefcomponent 要素 (VSX Schema)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. [ **ソース** ] ボックスの一覧で、[ **現在のソリューション内のプロジェクトを表示する** ] オプションボタンをクリックします。

8. [ **プロジェクト** ] ボックスの一覧で、[ **projectextension**] を選択します。

     この値は、プロジェクトでビルドしているアセンブリの名前を識別します。

9. [ **OK]** を選択して [ **新しい資産の追加** ] ダイアログボックスを閉じます。

10. メニューバーで、[**ファイル**] [すべてを保存] の順に選択し、完了したら  >  マニフェストデザイナーを閉じます。

11. メニューバーで [ビルド] [ソリューションの **ビルド**] の順に選択し、  >  プロジェクトがエラーなしでコンパイルされることを確認します。

12. **ソリューションエクスプローラー** で、 **projectextensionpackage** プロジェクトのショートカットメニューを開き、[**エクスプローラーでフォルダーを開く**] ボタンをクリックします。

13. **ファイルエクスプローラー** で、projectextensionpackage プロジェクトのビルド出力フォルダーを開き、フォルダーに projectextensionpackage .vsix という名前のファイルが含まれていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-project-property"></a>プロジェクトプロパティのテスト
 これで、カスタムプロジェクトのプロパティをテストする準備ができました。 の実験用インスタンスで、新しいプロジェクトプロパティ拡張機能のデバッグとテストを行うのが最も簡単です [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 こののインスタンス [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] は、VSIX または他の機能拡張プロジェクトを実行すると作成されます。 プロジェクトをデバッグした後、拡張機能をシステムにインストールし、の通常のインスタンスでデバッグとテストを続行でき [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

#### <a name="to-debug-and-test-the-extension-in-an-experimental-instance-of-visual-studio"></a>Visual Studio の実験用インスタンスで拡張機能をデバッグおよびテストするには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]管理者資格情報で再起動し、ProjectExtensionPackage ソリューションを開きます。

2. **F5** キーを押すか、メニューバーで [**デバッグ**] [  >  **デバッグの開始**] の順に選択して、プロジェクトのデバッグビルドを開始します。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom プロジェクトの Property/1.0 に拡張機能をインストールし、の実験用インスタンスを開始し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

3. の実験用インスタンスで、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ファームソリューション用の SharePoint プロジェクトを作成し、ウィザードのその他の値に既定値を使用します。

    1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

    2. [ **新しいプロジェクト** ] ダイアログボックスの上部にある .NET Framework のバージョンの一覧で [ **.NET Framework 3.5** ] を選択します。

         SharePoint ツール拡張機能には、このバージョンのの機能が必要 [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] です。

    3. [ **テンプレート** ] ノードで、[ **Visual C#** ] または [ **Visual Basic** ] ノードを展開し、[ **SharePoint** ] ノードを選択してから、[ **2010** ] ノードを選択します。

    4. [ **SharePoint 2010] プロジェクト** テンプレートを選択し、プロジェクトの名前として「 **moduletest** 」と入力します。

4. **ソリューションエクスプローラー** で、 **moduletest** プロジェクトノードを選択します。

     新しいカスタムプロパティ **マップイメージフォルダー** が [ **プロパティ** ] ウィンドウに表示され、既定値は **False** になります。

5. そのプロパティの値を **True** に変更します。

     Images リソースフォルダーが SharePoint プロジェクトに追加されます。

6. そのプロパティの値を **False** に戻します。

     [**画像フォルダーを削除しますか?** ] ダイアログボックスの **[はい**] をクリックすると、Images リソースフォルダーが SharePoint プロジェクトから削除されます。

7. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の実験用インスタンスを閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトの拡張](../sharepoint/extending-sharepoint-projects.md)
- [方法: SharePoint プロジェクトにプロパティを追加する](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [SharePoint プロジェクトシステムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [SharePoint プロジェクトシステムの拡張機能にデータを保存する](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [カスタムデータと SharePoint ツールの拡張機能の関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)