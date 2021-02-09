---
title: ビジネスデータを使用した SharePoint での外部リストの作成
description: ビジネスデータベースの連絡先に関する情報を返す BDC サービスのモデルを作成し、このモデルを使用して SharePoint に外部リストを作成します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], external list
- Business Data Connectivity service [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a SharePoint list
- BDC [SharePoint development in Visual Studio], business data in a Web Part
- BDC [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], entity backed list
- Business Data Connectivity service [SharePoint development in Visual Studio], external list
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: dbf996a2d44f94e4571a332fa7a86d861d820d45
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99847714"
---
# <a name="walkthrough-create-an-external-list-in-sharepoint-by-using-business-data"></a>チュートリアル: ビジネスデータを使用した SharePoint での外部リストの作成

Business Data Connectivity (BDC) サービスを使用すると、SharePoint で、バックエンドサーバーアプリケーション、Web サービス、およびデータベースのビジネスデータを表示できます。

このチュートリアルでは、サンプルデータベースの連絡先に関する情報を返す BDC サービスのモデルを作成する方法について説明します。 次に、このモデルを使用して、SharePoint に外部リストを作成します。

このチュートリアルでは、次の作業について説明します。

- プロジェクトを作成しています。
- モデルにエンティティを追加します。
- Finder メソッドを追加しています。
- 特定の Finder メソッドを追加します。
- プロジェクトをテストしています。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- サポート対象エディションの Windows と SharePoint

- AdventureWorks サンプルデータベースへのアクセス。 AdventureWorks データベースをインストールする方法の詳細については、「 [SQL Server サンプルデータベース](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)」を参照してください。

## <a name="create-a-project-that-contains-a-bdc-model"></a>BDC モデルを含むプロジェクトを作成する

1. Visual Studio のメニューバーで、[**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >  ます。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. [ **Visual C#** ] または [ **Visual Basic** で、[ **SharePoint** ] ノードを展開し、[ **2010** ] 項目を選択します。

3. [ **テンプレート** ] ペインで、[ **SharePoint 2010 プロジェクト**] を選択し、プロジェクトに **AdventureWorksTest** という名前を指定して、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード** が表示されます。 このウィザードでは、プロジェクトをデバッグし、ソリューションの信頼レベルを設定するために使用するサイトを指定できます。

4. [ **ファームソリューションとして配置** する] オプションボタンをクリックして、信頼レベルを設定します。

5. [ **完了** ] をクリックして、既定のローカル SharePoint サイトを受け入れます。

6. **ソリューションエクスプローラー** で、[SharePoint プロジェクト] ノードを選択します。

7. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが開きます。

8. [ **テンプレート** ] ペインで、[ **ビジネスデータ接続モデル (ファームソリューションのみ)**] を選択し、プロジェクトに **AdventureWorksContacts** という名前を指定して、[ **追加** ] をクリックします。

## <a name="add-data-access-classes-to-the-project"></a>データアクセスクラスをプロジェクトに追加する

1. メニューバーで、[**ツール**] [  >  **データベースへの接続**] の順に選択します。

     **[接続の追加]** ダイアログ ボックスが表示されます。

2. SQL Server AdventureWorks サンプルデータベースへの接続を追加します。

     詳細については、「 [接続の追加/変更 (Microsoft SQL Server)](/previous-versions/dxb6fxah(v=vs.140))」を参照してください。

3. **ソリューション エクスプローラー** で、プロジェクト ノードを選択します。

4. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

5. [ **インストールされたテンプレート** ] ペインで、[ **データ** ] ノードを選択します。

6. [ **テンプレート** ] ペインで、[ **LINQ to SQL クラス**] を選択します。

7. [ **名前** ] ボックスに「 **AdventureWorks**」と入力し、[ **追加** ] をクリックします。

     .Dbml ファイルがプロジェクトに追加され、オブジェクトリレーショナルデザイナー (O/R デザイナー) が開きます。

8. メニューバーで、[サーバーエクスプローラーの **表示**] を選択し  >  ます。

9. **サーバーエクスプローラー** で、AdventureWorks サンプルデータベースを表すノードを展開し、[**テーブル**] ノードを展開します。

10. O/R デザイナーに **Contact (Person)** テーブルを追加します。

     エンティティ クラスが作成され、デザイン サーフェイスに表示されます。 エンティティクラスには、Contact (Person) テーブルの列にマップされるプロパティがあります。

## <a name="remove-the-default-entity-from-the-bdc-model"></a>BDC モデルから既定のエンティティを削除する

**ビジネスデータ接続モデル** プロジェクトによって、Entity1 という名前の既定のエンティティがモデルに追加されます。 このエンティティを削除します。 後で、新しいエンティティを追加します。 空のモデルから開始すると、このチュートリアルを完了するために必要な手順の数が減ります。

1. **ソリューションエクスプローラー** で、[ **BdcModel1** ] ノードを展開し、 *BdcModel1* ファイルを開きます。

2. BDC デザイナーでビジネスデータ接続モデルファイルが開きます。

3. デザイナーで **Entity1** のショートカットメニューを開き、[ **削除**] を選択します。

4. **ソリューションエクスプローラー** で、 *Entity1* (Visual Basic) または *Entity1.cs* (C# の場合) のショートカットメニューを開き、[**削除**] を選択します。

5. *Entity1Service* (Visual Basic) または *Entity1Service.cs* (C# の場合) のショートカットメニューを開き、[**削除**] を選択します。

## <a name="add-an-entity-to-the-model"></a>エンティティをモデルに追加する

エンティティをモデルに追加します。 エンティティは、Visual Studio の **ツールボックス** から BDC デザイナーに追加できます。

1. メニューバーで、[   >  **ツールボックス** の表示] を選択します。

2. **ツールボックス** の [ **BusinessDataConnectivity** ] タブで、BDC デザイナーに **エンティティ** を追加します。

     新しいエンティティがデザイナーに表示されます。 Visual Studio によって、 *Entityservice .vb* という名前のファイル (Visual Basic) または *EntityService.cs* (C# の場合) がプロジェクトに追加されます。

3. メニューバーで、[プロパティウィンドウの **表示**] を選択し  >    >  ます。

4. [ **プロパティ** ] ウィンドウで、[ **名前** ] プロパティの値を「 **Contact**」に設定します。

5. デザイナーで、エンティティのショートカットメニューを開き、[ **追加**] を選択し、[ **識別子**] を選択します。

     エンティティに新しい識別子が表示されます。

6. [ **プロパティ** ] ウィンドウで、識別子の名前を **ContactID** に変更します。

7. [ **型名** ] ボックスの一覧で、[system.string] **を選択し** ます。

## <a name="add-a-specific-finder-method"></a>特定の Finder メソッドを追加する

BDC サービスで特定の連絡先を表示できるようにするには、特定の Finder メソッドを追加する必要があります。 ユーザーがリスト内の項目を選択し、リボンの [ **項目の表示** ] ボタンを選択すると、BDC サービスは特定の Finder メソッドを呼び出します。

[ **BDC メソッドの詳細** ] ウィンドウを使用して、Contact エンティティに特定の Finder メソッドを追加します。 特定のエンティティを返すには、メソッドにコードを追加します。

1. BDC デザイナーで、 **Contact** エンティティを選択します。

2. メニューバーで、[   >  **その他の Windows**  >  **BDC メソッドの詳細** を表示] を選択します。

     [BDC メソッドの詳細] ウィンドウが開きます。

3. [ **メソッドの追加** ] の一覧で、[ **特定の Finder メソッドの作成**] を選択します。

     Visual Studio によって、モデルに次の要素が追加されます。 これらの要素は、[ **BDC メソッドの詳細** ] ウィンドウに表示されます。

    - ReadItem という名前のメソッド。

    - メソッドの入力パラメーター。

    - メソッドの戻りパラメーター。

    - 各パラメーターの型記述子。

    - メソッドのメソッドインスタンス。

4. [ **BDC メソッドの詳細** ] ウィンドウで、 **連絡先** の種類の記述子に対して表示される一覧を開き、[ **編集**] を選択します。

     **BDC エクスプローラー** が開き、モデルの階層ビューが表示されます。

5. [ **プロパティ** ] ウィンドウで、[ **TypeName** ] プロパティの横にある一覧を開き、[ **現在のプロジェクト** ] タブを選択し、[ **Contact** ] プロパティを選択します。

6. **BDC エクスプローラー** で、**連絡先** のショートカットメニューを開き、[**型記述子の追加**] を選択します。

     **TypeDescriptor1** という名前の新しい型記述子が **BDC エクスプローラー** に表示されます。

7. [ **プロパティ** ] ウィンドウで、[ **名前** ] プロパティの値を **ContactID** に設定します。

8. [ **TypeName** ] プロパティの横にある一覧を開き、[ **Int32**] を選択します。

9. **識別子** プロパティの横にある一覧を開き、[ **ContactID**] を選択します。

10. 手順 6. を繰り返して、次の各フィールドの型記述子を作成します。

    |名前|種類名|
    |----------|---------------|
    |FirstName|System.String|
    |LastName|System.String|
    |Phone|System.String|
    |EmailAddress|System.String|
    |EmailPromotion|System.Int32|
    |NameStyle|System.Boolean|
    |PasswordHash|System.String|
    |PasswordSalt|System.String|

11. BDC デザイナーの **Contact** エンティティで、 **ReadItem** メソッドを開きます。

     コードエディターで Contact service コードファイルが開きます。

12. クラスで、 `ContactService` メソッドを `ReadItem` 次のコードに置き換えます。 このコードは、以下のタスクを実行します。

    - AdventureWorks データベースの Contact テーブルからレコードを取得します。

    - BDC サービスに Contact エンティティを返します。

    > [!NOTE]
    > フィールドの値を `ServerName` サーバーの名前に置き換えます。

     [!code-csharp[SP_BDC#3](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#3)]
     [!code-vb[SP_BDC#3](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#3)]

## <a name="add-a-finder-method"></a>Finder メソッドを追加する

BDC サービスが連絡先を一覧に表示できるようにするには、Finder メソッドを追加する必要があります。 [ **BDC メソッドの詳細** ] ウィンドウを使用して、Contact エンティティに Finder メソッドを追加します。 BDC サービスにエンティティのコレクションを返すには、メソッドにコードを追加します。

1. BDC デザイナーで、 **Contact** エンティティを選択します。

2. [ **BDC メソッドの詳細** ] ウィンドウで、[ **ReadItem** ] ノードを折りたたみます。

3. **Readlist** メソッドの下にある [**メソッドの追加**] の一覧で、[ **Finder メソッドの作成**] を選択します。

     Visual Studio によって、メソッド、戻りパラメーター、および型記述子が追加されます。

4. BDC デザイナーの **Contact** エンティティで、 **readlist** メソッドを開きます。

     連絡先サービスのコードファイルがコードエディターで開きます。

5. クラスで、 `ContactService` メソッドを `ReadList` 次のコードに置き換えます。 このコードは、以下のタスクを実行します。

   - AdventureWorks データベースの Contacts テーブルからデータを取得します。

   - BDC サービスに対する連絡先エンティティの一覧を返します。

     > [!NOTE]
     > フィールドの値を `ServerName` サーバーの名前に置き換えます。

     [!code-csharp[SP_BDC#2](../sharepoint/codesnippet/CSharp/SP_BDC/bdcmodel1/contactservice.cs#2)]
     [!code-vb[SP_BDC#2](../sharepoint/codesnippet/VisualBasic/sp_bdc/bdcmodel1/contactservice.vb#2)]

## <a name="test-the-project"></a>プロジェクトをテストする

プロジェクトを実行すると、SharePoint サイトが開き、Visual Studio によってモデルがビジネスデータ接続サービスに追加されます。 連絡先エンティティを参照する外部リストを SharePoint に作成します。 AdventureWorks データベースの連絡先のデータが一覧に表示されます。

> [!NOTE]
> ソリューションをデバッグする前に、SharePoint でセキュリティ設定を変更することが必要になる場合があります。 詳細については、「[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

1. **F5** キーを押します。

     SharePoint サイトが開きます。

2. [ **サイトの操作** ] メニューの [その **他のオプション** ] をクリックします。

3. [ **作成** ] ページで、[ **外部リスト** ] テンプレートを選択し、[ **作成** ] ボタンを選択します。

4. カスタムリストの **連絡先** に名前を指定します。

5. [ **外部コンテンツタイプ** ] フィールドの横にある [参照] ボタンをクリックします。

6. [ **外部コンテンツタイプの選択** ] ダイアログボックスで、 **AdventureWorksContacts** 項目を選択し、[ **作成** ] ボタンをクリックします。

     SharePoint では、AdventureWorks サンプルデータベースの連絡先を含む外部リストが作成されます。

7. 特定の Finder メソッドをテストするには、一覧で連絡先を選択します。

8. リボンで [ **項目** ] タブを選択し、[項目の **表示** ] コマンドを選択します。

     選択した連絡先の詳細がフォームに表示されます。

## <a name="next-steps"></a>次の手順

SharePoint で BDC サービスのモデルを設計する方法の詳細については、次のトピックを参照してください。

- [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)
- [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)
- [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)

## <a name="see-also"></a>関連項目

[ビジネスデータ接続モデル](../sharepoint/designing-a-business-data-connectivity-model.md) 
 を設計する[ビジネスデータ接続モデル](../sharepoint/creating-a-business-data-connectivity-model.md) 
 を作成する[BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md) 
[SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)