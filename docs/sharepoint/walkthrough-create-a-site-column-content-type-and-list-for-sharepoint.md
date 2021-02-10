---
title: SharePoint のサイト列、コンテンツタイプ、およびリストの作成
titleSuffix: ''
description: このチュートリアルでは、カスタムのサイト列 (フィールド)、サイト列を使用するカスタムコンテンツタイプ、SharePoint でコンテンツタイプを使用するリストを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.ListDesigner.GeneralMessageHelp
- Microsoft.VisualStudio.SharePoint.Designers.ListDesigner.ViewModels.ListViewModel.SortingAndGrouping
- VS.SharePointTools.ListDesigner.SortingGrouping
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, list definitions
- SharePoint development in Visual Studio, list instances
- SharePoint development in Visual Studio, fields
- SharePoint development in Visual Studio, content types
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d205203797d8bd50c7b3132df86fbff9dbad1771
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99937694"
---
# <a name="walkthrough-create-a-site-column-content-type-and-list-for-sharepoint"></a>チュートリアル: SharePoint のサイト列、コンテンツ タイプ、リストの作成
  次の手順では、カスタム SharePoint サイトの列 (または *フィールド*) と、サイト列を使用するコンテンツの種類を作成する方法について説明します。 また、新しいコンテンツタイプを使用するリストを作成する方法も示します。

 このチュートリアルでは、次のタスクについて説明します。

- [カスタムサイト列を作成](#create-custom-site-columns)します。

- [カスタムコンテンツタイプを作成](#create-a-custom-content-type)します。

- [リストを作成](#create-a-list)します。

- [アプリケーションをテスト](#test-the-application)します。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Windows と SharePoint

- [!INCLUDE[vsprvs-current](../sharepoint/includes/vsprvs-current-md.md)]

## <a name="create-custom-site-columns"></a>カスタムサイト列の作成
 この例では、病院で患者を管理するためのリストを作成します。 まず、で SharePoint プロジェクトを作成し、次のように [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] サイト列を追加する必要があります。

#### <a name="to-create-the-project"></a>プロジェクトを作成するには

1. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **[ファイル]** メニューで、 **[新規]**  >  **[プロジェクト]** の順にクリックします。
::: moniker range="=vs-2017"
2. [ **新しいプロジェクト** ] ダイアログボックスの [ **Visual C#** ] または [ **Visual Basic**] で、[ **Office/SharePoint** ] ノードを展開し、[ **sharepoint ソリューション**] を選択します。

3. [ **テンプレート** ] ペインで、インストールした sharepoint の特定のバージョンに対応する **sharepoint の空のプロジェクト** を選択します。 たとえば、SharePoint 2016 がインストールされている場合は、[ **sharepoint 2016-空のプロジェクト** ] テンプレートを選択します。  

4. プロジェクトの名前を「 **クリニック**」に変更し、[ **OK** ] をクリックします。

5. [**デバッグ用のサイトとセキュリティレベルの指定**] ダイアログボックスで、新しいカスタムフィールド項目を追加するローカル SharePoint サイトの URL を入力するか、既定の場所 (SystemName) を使用し `http://<`  `>/)` ます。

6. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、既定値の [ **サンドボックスソリューションとして配置**] を使用します。

     サンドボックスソリューションとファームソリューションの詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

7. **[完了]** をクリックします。 これで、プロジェクトが **ソリューションエクスプローラー** に一覧表示されます。
::: moniker-end
::: moniker range=">=vs-2019"
2.  [ **新しいプロジェクトの作成** ] ダイアログで、インストールした sharepoint の特定のバージョンに対応する **sharepoint の空のプロジェクト** を選択します。 たとえば、SharePoint 2016 がインストールされている場合は、[ **sharepoint 2016-空のプロジェクト** ] テンプレートを選択します。
    [!INCLUDE[new-project-dialog-search](../sharepoint/includes/new-project-dialog-search-md.md)]

3. プロジェクトの名前を「 **クリニック**」に変更し、[ **作成** ] ボタンを選択します。

4. [**デバッグ用のサイトとセキュリティレベルの指定**] ダイアログボックスで、新しいカスタムフィールド項目を追加するローカル SharePoint サイトの URL を入力するか、既定の場所 (SystemName) を使用し `http://<`  `>/)` ます。

5. [ **この SharePoint ソリューションの信頼レベル** を指定してください] セクションで、既定値の [ **サンドボックスソリューションとして配置**] を使用します。

     サンドボックスソリューションとファームソリューションの詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

6. **[完了]** をクリックします。 これで、プロジェクトが **ソリューションエクスプローラー** に一覧表示されます。
::: moniker-end

#### <a name="to-add-site-columns"></a>サイト列を追加するには

1. 新しいサイト列を追加します。 これを行うには、**ソリューションエクスプローラー** で、[**クリニック**] プロジェクトを右クリックし、[新しい項目の **追加**] を選択し  >  ます。

2. [ **新しい項目の追加** ] ダイアログボックスで [ **サイト列**] を選択し、名前を **PatientName** に変更して、[ **追加** ] ボタンをクリックします。

3. サイト列の *Elements.xml* ファイルで、[ **種類** ] の設定を [ **テキスト**] のままにして、 **グループ** 設定を [ **クリニックサイトの列**] に変更します。 完了すると、サイト列の *Elements.xml* ファイルは次の例のようになります。

    ```xml
    <Field
         ID="{f9ba60d1-5631-41fb-b016-a38cf48eef63}"
         Name="PatientName"
         DisplayName="Patient Name"
         Type="Text"
         Required="FALSE"
         Group="Clinic Site Columns">
    </Field>
    ```

    > [!TIP]
    > サイト列の名前に camel 形式の文字種を使用すると、Visual Studio によって自動的に DisplayName にスペースが追加されます。
    > SharePoint にソリューションを配置しようとすると問題が発生する可能性があるため、サイトの列名にスペースを使用しないことをお勧めします。

4. 同じ手順を使用して、2つのサイト列をプロジェクトに追加します。 **患者 id** (type = "Integer") と **DoctorName** (type = "Text") です。 グループの値を「 **クリニックサイトの列**」に設定します。

## <a name="create-a-custom-content-type"></a>カスタムコンテンツタイプを作成する
 次に、前の手順で作成したサイト列を含む、Contacts コンテンツタイプに基づくコンテンツの種類を作成します。 コンテンツの種類を既存のコンテンツの種類に基づいて作成することで、新しいコンテンツの種類で使用する複数のサイト列が基本コンテンツタイプに提供されるため、時間を節約できます。

#### <a name="to-create-a-custom-content-type"></a>カスタムコンテンツタイプを作成するには

1. プロジェクトにコンテンツタイプを追加します。 これを行うには、 **ソリューションエクスプローラー** でプロジェクトノードを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

4. [ **テンプレート** ] ウィンドウで、[ **コンテンツタイプ** ] テンプレートを選択し、名前を「 **患者情報**」に変更して、[ **追加** ] ボタンを選択します。

     **SharePoint カスタマイズウィザード** が開きます。

5. [ **このコンテンツの種類を継承する基本コンテンツ** の種類] で、新しいコンテンツの種類の基になるコンテンツの種類として [ **Contact** ] を選択し、[ **完了** ] をクリックします。

     これにより、以前に定義したサイトの列に加えて、Contact コンテンツの種類の他の便利なサイト列にもアクセスできるようになります。

6. コンテンツタイプデザイナーが表示されたら、[ **列** ] タブで、前に定義した3つのサイト列 ( **患者名**、 **患者 ID**、および **医師名**) を追加します。 これらの列を追加するには、[ **表示名**] の [サイトの列] の一覧で最初のリストボックスを選択し、一覧内の各サイトの列を1つずつ選択します。

    > [!TIP]
    > サイト列をより迅速に選択するには、列名の最初の数文字を入力して一覧をフィルター処理します。

7. 3つのカスタムサイト列に加えて、[サイト列] の一覧から [ **コメント** ] サイト列を追加します。

8. [**患者の名前**] と [**患者 ID** ] のサイト列 **に必須のチェックボックス** をオンにして、必須フィールドにします。

9. [ **コンテンツの種類** ] タブで、[コンテンツの種類] の名前が [ **患者情報**] になっていることを確認し、[説明] を「 **患者情報カード**」に変更します。

10. **グループ名** を「**クリニックコンテンツタイプ**」に変更し、その他の設定は既定値のままにします。

11. メニューバーで、[**ファイル**] [すべて保存] の順に選択し、  >  コンテンツタイプデザイナーを閉じます。

## <a name="create-a-list"></a>リストを作成する
 ここで、新しいコンテンツの種類とサイト列を使用するリストを作成します。

#### <a name="to-create-a-list"></a>リストを作成するには

1. プロジェクトにリストを追加します。 これを行うには、 **ソリューションエクスプローラー** でプロジェクトノードを選択します。

2. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

3. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開します。

4. [ **テンプレート** ] ペインで、[ **リスト** ] テンプレートを選択し、名前を「 **患者**」に変更し、[ **追加** ] ボタンを選択します。

5. [既定値としての設定 **に基づいてリストをカスタマイズ** する **(カスタムリスト)**] のままにして、[ **完了** ] をクリックします。

6. リストデザイナーで [ **コンテンツの種類** ] ボタンをクリックして、[ **コンテンツタイプの設定** ] ダイアログボックスを表示します。

7. 新しい行を選択し、コンテンツの種類の一覧で **患者情報** のコンテンツの種類を選択し、[ **OK** ] をクリックします。

     これにより、 **患者情報** のコンテンツタイプのすべてのサイト列が一覧に追加されます。

8. 次の項目を除く、一覧内のすべてのサイト列を削除します。

    - 患者 ID

    - 患者の名前

    - 自宅電話番号

    - 電子メール

    - 医師名

    - 説明

9. [ **列表示名**] で、空の行を選択し、カスタムリスト列を追加して、「 **病院**」という名前を指定します。 データ型 **は単一行のテキスト** としてそのままにします。

     [カスタムリスト] 列は、この一覧にのみ適用されます。 リストにカスタムリスト列を追加すると、リストに追加されたすべての列を含む新しいリストのコンテンツの種類が作成され、既定の一覧として設定されます。

    > [!TIP]
    > サイト列の一覧から列を選択すると、既存のサイト列が使用されます。 ただし、一覧の列を選択せずに [列名] の値を入力すると、同じ名前の列が既に一覧に存在する場合でも、カスタムリスト列が作成されます。

     必要に応じて、カスタムリストの列のデータ型を **単一行のテキスト** に設定するのではなく、この列のデータ型を Lookup に設定し、その値をテーブルまたは別のリストから取得することもできます。 参照列の詳細については、「 [SharePoint 2010 でのリレーションシップの一覧](/previous-versions/msp-n-p/ff798514(v=pandp.10)) 表示」と「参照 [とリレーションシップの一覧](/previous-versions/office/developer/sharepoint-2010/ff623048(v=office.14))」を参照してください。

10. [患者の **ID** ] ボックスと [ **患者の名前** ] ボックスの横にある [ **必須** ] チェックボックスをオンにします。

11. [ **ビュー** ] タブで、ビューを作成するための空の行を選択します。 [**ビュー名**] 列の下の空白行に **患者の詳細** を入力します。

     [ **表示** ] タブでは、SharePoint リストに表示する列を指定できます。

12. [新しい **患者の詳細** ] 行を選択し、[ **既定値として設定** ] ボタンを選択します。

     新しいビューは、リストの既定のビューになります。

13. 次の列を [ **選択された列** ] の一覧に次の順序で追加します。

    - 患者 ID

    - 患者の名前

    - 自宅電話番号

    - 電子メール

    - 医師名

    - 所在

    - 説明

14. [**プロパティ**] の一覧で、[**並べ替えとグループ化**] プロパティを選択し、省略記号ボタンをクリックして [**並べ替えとグループ化**] ダイアログ ![ボックスを表示](../sharepoint/media/ellipsisicon.gif "省略記号アイコン")します。

15. [ **列名** ] ボックスの一覧で、[ **患者の名前**] を選択し、[ **並べ替え** ] 列が [ **昇順**] に設定されていることを確認してから、[ **OK** ] をクリックします。

## <a name="test-the-application"></a>アプリケーションをテストする
 カスタムサイト列、コンテンツタイプ、およびリストの準備ができたので、SharePoint に配置し、アプリケーションを実行してテストします。

#### <a name="to-test-the-application"></a>アプリケーションをテストするには

1. メニュー バーで、 **[ファイル]**  >  **[すべてを保存]** の順に選択します。

2. F5 キーを **押し** てアプリケーションを実行します。

     アプリケーションがコンパイルされ、その機能が SharePoint に配置され、アクティブ化されます。

3. クイックナビゲーションバーで、[ **患者** ] リンクを選択して、[ **患者** ] の一覧を表示します。

     一覧に表示される列名は、の [ **表示** ] タブで入力したものと一致している必要があり [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

4. [ **新しい項目の追加** ] リンクを選択して、患者情報カードを作成します。

5. フィールドに情報を入力し、[ **保存** ] をクリックします。

     新しいレコードが一覧に表示されます。

## <a name="see-also"></a>関連項目
- [SharePoint のサイト列、コンテンツ タイプ、リストの作成](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [方法: カスタムフィールド型を作成する](/previous-versions/office/developer/sharepoint-2010/bb862248(v=office.14))
- [コンテンツの種類](/previous-versions/office/developer/sharepoint-2010/ms479905(v=office.14))
- [[列]](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14))
