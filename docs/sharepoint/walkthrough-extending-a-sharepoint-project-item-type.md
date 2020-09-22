---
title: 'チュートリアル: SharePoint プロジェクト項目の種類の拡張 |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e8186b1a1388745527fbb9f4dd37478942c36e62
ms.sourcegitcommit: 7a46232242783ebe23f2527f91eac8eb84b3ae05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2020
ms.locfileid: "90740007"
---
# <a name="walkthrough-extend-a-sharepoint-project-item-type"></a>チュートリアル: SharePoint プロジェクト項目の種類の拡張
  **ビジネスデータ接続モデル**プロジェクト項目を使用して、SharePoint の Business data CONNECTIVITY (BDC) サービスのモデルを作成できます。 既定では、このプロジェクト項目を使用してモデルを作成しただけでは、モデル内のデータがユーザーに表示されません。 ユーザーがデータを閲覧できるようにするには、それに加えて、SharePoint に外部リストを作成する必要があります。

 このチュートリアルでは、 **ビジネスデータ接続モデル** プロジェクト項目の拡張機能を作成します。 開発者は、この拡張機能を使用することで、BDC モデルのデータを表示するための外部リストを同じプロジェクト内で作成できます。 このチュートリアルでは、次のタスクについて説明します。

- 次の 2 つの主要タスクを実行する Visual Studio の拡張機能を作成する。

  - BDC モデル内のデータを表示するための外部リストを生成する。 拡張機能は、SharePoint プロジェクトシステムのオブジェクトモデルを使用して、リストを定義する *Elements.xml* ファイルを生成します。 さらに、BDC モデルと一緒に配置できるように、このファイルをプロジェクトに追加します。

  - これにより、**ソリューションエクスプローラー**の**ビジネスデータ接続モデル**プロジェクト項目にショートカットメニュー項目が追加されます。 開発者は、このメニュー項目をクリックして、BDC モデル用の外部リストを生成できます。

- 拡張機能のアセンブリを配置するための Visual Studio Extension (VSIX) パッケージを構築する。

- 拡張機能をテストする。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを実行するには、開発コンピューターに次のコンポーネントが必要です。

- サポート対象エディションの Microsoft Windows、SharePoint、および Visual Studio。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]。 このチュートリアルでは、SDK の **Vsix プロジェクト** テンプレートを使用して、プロジェクト項目を配置する vsix パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

  次の概念に関する知識があると役に立ちますが、チュートリアルを実行するうえで必須というわけではありません。

- [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] の BDC サービス。 詳細については、「 [BDC のアーキテクチャ](/previous-versions/office/developer/sharepoint-2010/ee558876(v=office.14))」を参照してください。

- BDC モデルの XML スキーマ。 詳細については、「 [BDC モデルインフラストラクチャ](/previous-versions/office/developer/sharepoint-2010/ee556378(v=office.14))」を参照してください。

## <a name="create-the-projects"></a>プロジェクトを作成する
 このチュートリアルを完了するには、2 つのプロジェクトを作成する必要があります。

- プロジェクト項目の拡張機能を配置するために VSIX パッケージを作成する VSIX プロジェクト。

- プロジェクト項目の拡張機能を実装するクラス ライブラリ プロジェクト。

  この 2 つのプロジェクトを作成することから始めます。

#### <a name="to-create-the-vsix-project"></a>VSIX プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

3. [ **新しいプロジェクト** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **機能拡張** ] ノードを選択します。

    > [!NOTE]
    > **機能拡張**ノードは、VISUAL Studio SDK をインストールした場合にのみ使用できます。 詳細については、このトピックで前に説明した「前提条件」を参照してください。

4. [ **新しいプロジェクト** ] ダイアログボックスの上部にある一覧で、[ **.NET Framework 4.5**] を選択します。

     SharePoint ツールの拡張機能を使用するには、このバージョンの .NET Framework の機能が必要です。

5. [ **VSIX プロジェクト** ] テンプレートを選択します。

6. [ **名前** ] ボックスに「 **GenerateExternalDataLists**」と入力し、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**GenerateExternalDataLists**プロジェクトを**ソリューションエクスプローラー**に追加します。

7. Source.extension.vsixmanifest ファイルが自動的に開かない場合は、GenerateExternalDataLists プロジェクトでそのショートカットメニューを開き、[**開く**] を選択します。

8. source.extension.vsixmanifest ファイルで [作成者] フィールドが空白でないことを確認し (「Contoso」と入力し)、ファイルを保存して閉じます。

#### <a name="to-create-the-extension-project"></a>拡張機能プロジェクトを作成するには

1. **ソリューションエクスプローラー**で、 **GenerateExternalDataLists**ソリューションノードのショートカットメニューを開き、[**追加**]、[**新しいプロジェクト**] の順に選択します。

2. [ **新しいプロジェクトの追加** ] ダイアログボックスで、[ **Visual C#** ] ノードまたは [ **Visual Basic** ] ノードを展開し、[ **Windows** ] ノードをクリックします。

3. ダイアログボックスの上部にある一覧で、 **.NET Framework 4.5**を選択します。

4. プロジェクトテンプレートの一覧で、[ **クラスライブラリ**] を選択します。

5. [ **名前** ] ボックスに「 **BdcProjectItemExtension**」と入力し、[ **OK** ] をクリックします。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]**BdcProjectItemExtension**プロジェクトをソリューションに追加し、既定の Class1 コードファイルを開きます。

6. Class1 コード ファイルをプロジェクトから削除します。

## <a name="configure-the-extension-project"></a>拡張機能プロジェクトの構成
 プロジェクト項目の拡張機能を作成するためのコードを記述する前に、コード ファイルおよびアセンブリ参照を拡張プロジェクトに追加します。

#### <a name="to-configure-the-project"></a>プロジェクトを構成するには

1. BdcProjectItemExtension プロジェクトに、次の名前を持つ 2 つのコード ファイルを追加します。

    - ProjectItemExtension

    - GenerateExternalDataLists

2. BdcProjectItemExtension プロジェクトを選択し、メニューバーで [**プロジェクト**] [参照の追加] の順に選択し  >  **Add Reference**ます。

3. [ **アセンブリ** ] ノードで、[ **フレームワーク** ] ノードを選択し、次の各アセンブリのチェックボックスをオンにします。

    - System.ComponentModel.Composition

    - WindowsBase

4. [ **アセンブリ** ] ノードで、[ **拡張機能** ] ノードを選択し、次のアセンブリのチェックボックスをオンにします。

    - Microsoft.VisualStudio.SharePoint

5. **[OK]** を選択します。

## <a name="define-the-project-item-extension"></a>プロジェクト項目の拡張機能を定義する
 **ビジネスデータ接続モデル**プロジェクト項目の拡張機能を定義するクラスを作成します。 拡張機能を定義するため、このクラスに <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> インターフェイスを実装します。 このインターフェイスは、既存の種類のプロジェクト項目を拡張する場合に必ず実装します。

#### <a name="to-define-the-project-item-extension"></a>プロジェクト項目の拡張機能を定義するには

1. ProjectItemExtension コードファイルに次のコードを貼り付けます。

    > [!NOTE]
    > このコードを追加した直後は、いくつかのコンパイル エラーが発生します。 これらのエラーは、この後の手順でコードを追加すると解消されます。

     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/projectitemextension.cs#1)]
     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/projectitemextension.vb#1)]

## <a name="create-the-external-data-lists"></a>外部データリストを作成する
 BDC モデル内の各エンティティの外部データ リストを作成する `GenerateExternalDataListsExtension` クラスの部分定義を追加します。 外部データ リストを作成するために、このコードはまず BDC モデル ファイル内の XML データを解析して、BDC モデルのエンティティ データを読み取ります。 次に、BDC モデルに基づくリスト インスタンスを作成し、このリスト インスタンスをプロジェクトに追加します。

#### <a name="to-create-the-external-data-lists"></a>外部データ リストを作成するには

1. 次のコードを GenerateExternalDataLists コード ファイルに貼り付けます。

     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.cs#2)]

## <a name="checkpoint"></a>Checkpoint
 この段階で、プロジェクト項目の拡張機能に必要なすべてのコードがプロジェクトに揃ったことになります。 エラーが発生することなくプロジェクトをコンパイルできるかどうか、ソリューションをビルドして確認してください。

#### <a name="to-build-the-solution"></a>ソリューションをビルドするには

1. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

## <a name="create-a-vsix-package-to-deploy-the-project-item-extension"></a>プロジェクト項目の拡張機能を配置するための VSIX パッケージの作成
 拡張機能を配置するには、ソリューションで VSIX プロジェクトを使用して VSIX パッケージを作成します。 まず、VSIX プロジェクトに含まれている source.extension.vsixmanifest ファイルを変更して、VSIX パッケージを構成します。 次に、ソリューションをビルドして VSIX パッケージを作成します。

#### <a name="to-configure-and-create-the-vsix-package"></a>VSIX パッケージを構成および作成するには

1. **ソリューションエクスプローラー**で、GenerateExternalDataLists プロジェクトの source.extension.vsixmanifest ファイルのショートカットメニューを開き、[**開く**] を選択します。

     Visual Studio によってマニフェスト エディターでファイルが開きます。 source.extension.vsixmanifest ファイルが、すべての VSIX パッケージで必要とされる extension.vsixmanifest ファイルの基礎となります。 このファイルの詳細については、「 [VSIX 拡張機能スキーマ1.0 リファレンス](/previous-versions/dd393700(v=vs.110))」を参照してください。

2. [ **Product Name** ] ボックスに、「 **External Data List Generator**」と入力します。

3. [ **作成者** ] ボックスに「 **Contoso**」と入力します。

4. [ **説明** ] ボックスに、 **外部データリストを生成するために使用できるビジネスデータ接続モデルのプロジェクト項目の拡張機能**を入力します。

5. エディターの [ **アセット** ] タブで、[ **新規** ] ボタンをクリックします。

     [ **新しい資産の追加** ] ダイアログボックスが表示されます。

6. [ **種類** ] ボックスの一覧で、[ **VisualStudio**] を選択します。

    > [!NOTE]
    > この値は、extension.vsixmanifest ファイル内の `MefComponent` 要素に対応します。 この要素は、VSIX パッケージ内の拡張機能アセンブリの名前を指定します。 詳細については、「 [Mefcomponent 要素 (VSX Schema)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))」を参照してください。

7. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト**を選択します。

8. [ **プロジェクト** ] ボックスの一覧で [ **BdcProjectItemExtension**] を選択し、[ **OK** ] をクリックします。

9. メニュー バーで、 **[ビルド]**  >  **[ソリューションのビルド]** の順にクリックします。

10. エラーが発生することなくプロジェクトがコンパイルされてビルドされたことを確認します。

11. GenerateExternalDataLists プロジェクトのビルド出力フォルダーに GenerateExternalDataLists.vsix ファイルが格納されていることを確認します。

     既定では、ビルド出力フォルダーは ..\bin\Debug で、プロジェクト ファイルが格納されているフォルダーの下にあります。

## <a name="test-the-project-item-extension"></a>プロジェクト項目の拡張機能をテストする
 これで、プロジェクト項目の拡張機能をテストする準備ができました。 まず、Visual Studio の実験用インスタンスで拡張機能プロジェクトのデバッグを開始します。 次に、Visual Studio の実験用インスタンスで拡張機能を使用して、BDC モデルの外部リストを生成します。 最後に、SharePoint サイトで外部リストを開いて正常に動作するかどうかを確認します。

#### <a name="to-start-debugging-the-extension"></a>拡張機能のデバッグを開始するには

1. 必要に応じて、管理者の資格情報を使用して Visual Studio を再起動し、GenerateExternalDataLists ソリューションを開きます。

2. BdcProjectItemExtension プロジェクトで、ProjectItemExtension コード ファイルを開き、`Initialize` メソッド内のコード行にブレークポイントを追加します。

3. GenerateExternalDataLists コード ファイルを開き、`GenerateExternalDataLists_Execute` メソッドのコードの先頭行にブレークポイントを追加します。

4. **F5**キーを押すか、メニューバーで [**デバッグ**] [デバッグ開始] の順に選択して、デバッグを開始  >  **Start Debugging**します。

     Visual Studio によって、拡張機能が %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\External Data List Generator\1.0 にインストールされ、Visual Studio の実験用インスタンスが開始されます。 このインスタンスの Visual Studio でプロジェクト項目をテストします。

#### <a name="to-test-the-extension"></a>拡張機能をテストするには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  **Project**ます。

2. [ **新しいプロジェクト** ] ダイアログボックスで、[ **テンプレート** ] ノードを展開し、[ **Visual C#** ] ノードを展開して、[ **SharePoint** ] ノードを展開し、[ **2010**] を選択します。

3. ダイアログボックスの上部にある一覧で、 **.NET Framework 3.5** が選択されていることを確認します。 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] のプロジェクトには、このバージョンの .NET Framework が必要です。

4. プロジェクトテンプレートの一覧で、[ **SharePoint 2010 プロジェクト**] を選択します。

5. [ **名前** ] ボックスに「 **Sharepointprojecttestbdc**」と入力し、[ **OK** ] をクリックします。

6. SharePoint カスタマイズウィザードで、デバッグに使用するサイトの URL を入力し、[ **ファームソリューションとして配置**] を選択して、[ **完了** ] をクリックします。

7. SharePointProjectTestBDC プロジェクトのショートカットメニューを開き、[ **追加**]、[ **新しい項目**] の順に選択します。

8. [ **NewItem の追加-SharePointProjectTestBDC** ] ダイアログボックスで、[インストールされている言語] ノードを展開し、[ **SharePoint** ] ノードを展開します。

9. [ **2010** ] ノードを選択し、[ **ビジネスデータ接続モデル (ファームソリューションのみ)** ] テンプレートを選択します。

10. [ **名前** ] ボックスに「 **TestBDCModel**」と入力し、[ **追加** ] をクリックします。

11. Visual Studio のもう一方のインスタンスで、ProjectItemExtension コード ファイルの `Initialize` メソッドに設定したブレークポイントで、コードが停止していることを確認します。

12. 停止した Visual Studio のインスタンスで、F5 キーを**押す**か、メニューバーで [**デバッグ**] [続行] を選択して、  >  **Continue**プロジェクトのデバッグを続行します。

13. Visual Studio の実験用インスタンスで、 **F5**キーを押すか、メニューバーで [**デバッグ**] [デバッグ開始] の順に選択して、  >  **Start Debugging** **TestBDCModel**プロジェクトをビルド、配置、実行します。

     デバッグ用に指定した SharePoint サイトの既定のページが Web ブラウザーに表示されます。

14. [クイック起動] 領域の [ **リスト** ] セクションに、プロジェクトの既定の BDC モデルに基づくリストがまだ含まれていないことを確認します。 まず、SharePoint のユーザー インターフェイスを使用するか、プロジェクト項目の拡張機能を使用して、外部データ リストを作成する必要があります。

15. Web ブラウザーを閉じます。

16. TestBDCModel プロジェクトが開かれている Visual Studio のインスタンスで、**ソリューションエクスプローラー**の [ **TestBDCModel** ] ノードのショートカットメニューを開き、[**外部データの一覧の生成**] をクリックします。

17. Visual Studio のもう一方のインスタンスで、`GenerateExternalDataLists_Execute` メソッドに設定したブレークポイントで、コードが停止していることを確認します。 F5 キーを**押す**か、メニューバーで [**デバッグ**] [続行] の順に選択して、  >  **Continue**プロジェクトのデバッグを続行します。

18. Visual Studio の実験用インスタンスによって、 **[entity1datalist]** という名前のリストインスタンスが TestBDCModel プロジェクトに追加され、インスタンスによってリストインスタンスの **Feature2** という名前の機能も生成されます。

19. **F5**キーを押すか、メニューバーで [**デバッグ**] [デバッグ開始] の順に選択して、  >  **Start Debugging** TestBDCModel プロジェクトをビルド、配置、実行します。

     デバッグに使用する SharePoint サイトの既定のページが Web ブラウザーに表示されます。

20. [クイック起動] 領域の [ **リスト** ] セクションで、[ **[entity1datalist]** ] の一覧を選択します。

21. リストに Identifier1 および Message という名前の列が存在し、項目 (Identifier1 の値は 0 で、Message の値は Hello World) が 1 つ含まれていることを確認します。

     **ビジネスデータ接続モデル**プロジェクトテンプレートでは、すべてのデータを提供する既定の BDC モデルが生成されます。

22. Web ブラウザーを閉じます。

## <a name="clean-up-the-development-computer"></a>開発用コンピューターのクリーンアップ
 プロジェクト項目の拡張機能のテストが終わったら、外部リストおよび BDC モデルを SharePoint サイトから削除し、さらにプロジェクト項目の拡張機能を Visual Studio から削除します。

#### <a name="to-remove-the-external-data-list-from-the-sharepoint-site"></a>SharePoint サイトから外部データ リストを削除するには

1. SharePoint サイトの [クイック起動] 領域で、[ **[entity1datalist]** ] の一覧を選択します。

2. SharePoint サイトのリボンで、[ **リスト** ] タブを選択します。

3. [ **一覧** ] タブの [ **設定** ] グループで、[ **リストの設定**] を選択します。

4. [ **アクセス許可と管理**] で、[ **この一覧を削除**する] を選択し、[ **OK** ] をクリックして、リストをごみ箱に送信することを確認します。

5. Web ブラウザーを閉じます。

#### <a name="to-remove-the-bdc-model-from-the-sharepoint-site"></a>BDC モデルを SharePoint サイトから削除するには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ビルド**の取り消し] を選択し  >  **Retract**ます。

     Visual Studio によって BDC モデルが SharePoint サイトから削除されます。

#### <a name="to-remove-the-project-item-extension-from-visual-studio"></a>プロジェクト項目の拡張機能を Visual Studio から削除するには

1. Visual Studio の実験用インスタンスのメニューバーで、[**ツール**] [  >  **拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で [ **外部データリストジェネレーター**] を選択し、[ **アンインストール** ] をクリックします。

3. 表示されるダイアログボックスで、[ **はい]** を選択して、拡張機能をアンインストールすることを確認します。

4. [ **今すぐ再起動** ] を選択して、アンインストールを完了します。

5. Visual Studio の両方のインスタンス (実験用インスタンスと、GenerateExternalDataLists ソリューションを開いたインスタンス) を閉じます。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)