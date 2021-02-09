---
title: 'チュートリアル: 既存の SharePoint サイトからのアイテムのインポート |Microsoft Docs'
titleSuffix: ''
description: このチュートリアルでは、既存の SharePoint サイトから Visual Studio SharePoint プロジェクトに項目をインポートします。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 861b6ff20f9ceb73c279e54fa89ee513389b6b91
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900951"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>チュートリアル: 既存の SharePoint サイトからのアイテムのインポート
  このチュートリアルでは、既存の SharePoint サイトから sharepoint プロジェクトに項目をインポートする方法について説明し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。

 このチュートリアルでは、次のタスクについて説明します。

- カスタムサイト列 ( *フィールド* とも呼ばれます) を追加して SharePoint サイトをカスタマイズする。

- SharePoint サイトを .wsp ファイルにエクスポートする。

- .Wsp インポートプロジェクトを使用して、.wsp ファイルを SharePoint にインポートします。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- および SharePoint のサポートされているエディション [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] 。

- 見ることができます。

## <a name="customize-a-sharepoint-site"></a>SharePoint サイトのカスタマイズ
 この例では、SharePoint サブサイトに新しいサイト列を追加し、後で使用するために別のサブサイトを作成することによって、SharePoint サブサイトを作成およびカスタマイズします。 後で、最初のサブサイトを .wsp ファイルにエクスポートし、.wsp インポートプロジェクトを使用して、2番目のサブサイトにカスタムサイト列をインポートします。

### <a name="to-create-and-customize-a-sharepoint-site"></a>SharePoint サイトを作成およびカスタマイズするには

1. Http://<em>system name</em>/SitePages/Home.aspx. などの Web ブラウザーを使用して SharePoint サイトを開きます。

2. メインの SharePoint サイトからサブサイトを作成するには、[ **サイトの操作** ] メニューを開き、[ **新しいサイト**] を選択します。

3. サイトの [ **作成** ] ダイアログボックスで、 **空のサイト** の種類を選択します。

4. [ **タイトル** ] ボックスに「 **Site Column Test 1**;」と入力します。[ **URL name** ] ボックスに、「 **columntest1**;」と入力します。その他の設定は既定値のままにしておきます。次に、[ **作成** ] ボタンをクリックします。

5. サイトが作成されたら、ブラウザーでメインサイト http://<em>system name</em>/SitePages/Home.aspx. に移動します。

6. ここでも、メインの SharePoint サイトから空のサブサイトを作成します。そのためには、[ **サイトの操作** ] メニューを開き、[ **新しいサイト**] を選択して、 **空のサイト** の種類を選択します。

7. [ **タイトル** ] ボックスに「 **Site Column Test 2**;」と入力します。[ **URL name** ] ボックスに、「 **columntest2**;」と入力します。その他の設定は既定値のままにしておきます。次に、[ **作成** ] ボタンをクリックします。

8. 最初のサブサイト、http://<em>SystemName</em>の順に移動します。

9. [ **サイトの操作** ] メニューの [サイトの **設定** ] をクリックして、[サイトの設定] ページを表示します。

10. [ **ギャラリー** ] セクションで、[ **サイト列** ] リンクを選択します。

11. **サイト列ギャラリー** ページの上部にある [**作成**] ボタンをクリックします。

12. [ **列名** ] ボックスに「 **Test Column**」と入力し、その他の既定値はそのままにして、[ **OK** ] をクリックします。

13. [ **テスト列** ] 列は、サイト列ギャラリーの [カスタム列] 見出しの下に表示されます。

## <a name="exporting-the-sharepoint-site"></a>SharePoint サイトのエクスポート
 次に、sharepoint プロジェクトにインポートする sharepoint アイテムと要素を含む SharePoint セットアップ (.wsp) ファイルを取得し [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 .Wsp ファイルをまだ作成していない場合は、既存の SharePoint サイトから作成する必要があります。 この例では、既定の SharePoint サイトを .wsp ファイルにエクスポートします。

> [!IMPORTANT]
> 次の手順を実行する実行時エラーが発生した場合は、SharePoint サイトにアクセスできるシステムでこの手順を実行する必要があります。

### <a name="to-export-an-existing-sharepoint-site"></a>既存の SharePoint サイトをエクスポートするには

1. SharePoint サイトで、[サイトの **操作**] タブの [**サイトの設定**] を選択し、[サイトの設定] ページを表示します。

2. [サイトの設定] ページの [ **サイトの操作** ] セクションで、[ **サイトをテンプレートとして保存** ] リンクを選択します。

3. [ **ファイル名** ] ボックスに「 **Example ite**」と入力し、[ **テンプレート名** ] ボックスに「 **Example Site**」と入力します。

4. この例では、[ **コンテンツを含める** ] チェックボックスをオフのままにします。

     このチェックボックスをオンにすると、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] すべてのリストとドキュメントライブラリとその内容が .wsp ファイルに保存されます。 これは、状況によっては役に立ちますが、この例では必須ではありません。

5. 操作が正常に完了したら、[ **ソリューションギャラリー** ] リンクをクリックして、.wsp ファイルを表示します。

     後で [ソリューションギャラリー] ページを表示するには、[サイトの **操作**] メニューを開き、[**サイトの設定**] を選択します。次に、[**サイトコレクションの管理**] セクションの [**最上位レベルのサイト設定にアクセス**] リンクを選択し、[**ギャラリー** ] セクションの [**ソリューション**] リンクを選択します。

6. ソリューションギャラリーで、[の例 **] リンクを** 選択します。

7. [ **ファイルのダウンロード** ] ダイアログボックスで、[ **保存** ] をクリックして、既定でローカルシステムのダウンロードフォルダーにファイルを保存します。

## <a name="import-the-wsp-file"></a>.Wsp ファイルをインポートする
 再利用する項目 ([カスタムサイト] 列の [テスト] 列) を含む *.wsp* ファイルがあるので、それにアクセスするための *.wsp* ファイルをインポートします。

### <a name="to-import-a-wsp-file"></a>.Wsp ファイルをインポートするには

1. の [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] メニューバーで、[**ファイル**] [  >  **新規作成**] [プロジェクト] の順に選択し  >   、[**新しいプロジェクト**] ダイアログボックスを表示します。 IDE が Visual Basic 開発設定を使用するように設定されている場合は、メニューバーで [**ファイル**] [新規作成] [プロジェクト] の順に選択し  >  ます。

2. [ **Visual C#** ] または [ **Visual Basic**] の下にある [ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

3. [**テンプレート**] ペインで [ **SharePoint 2010 ソリューションパッケージのインポート**] テンプレートを選択し、プロジェクトの名前を WspImportProject1 のままにして、[ **OK** ] をクリックします。

    **SharePoint カスタマイズウィザード** が表示されます。

4. [ **デバッグのサイトとセキュリティレベルの指定** ] ページで、前に作成した [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] 2 番目の SharePoint サブサイトのを入力します。 新しいカスタムフィールド項目である http://<em>system name</em>/columntest2 をそのサブサイトに追加します。

5. [ **この SharePoint ソリューションの信頼レベル** を選択してください。] セクションで、[ **サンドボックスソリューションとして配置** する] を選択したままにします。

6. [ **新しいプロジェクトソースの指定** ] ページで、 *.wsp* ファイルを保存したシステム上の場所を参照し、[ **次へ** ] をクリックします。

   > [!NOTE]
   > このページの [ **完了** ] ボタンをクリックすると、 *.wsp* ファイル内の使用可能なすべての項目がインポートされます。

7. [ **インポートする項目の選択** ] ボックスで、[ **テスト列**] 以外の一覧のすべてのチェックボックスをオフにし、[ **完了** ] をクリックします。

    一覧には多くの項目が含まれているので、 **Ctrl** + **A** キーを押して一覧内のすべての項目を選択し、space キーを押してすべてのチェックボックスをオフにして、[**テスト] 列** 項目の横のチェックボックスのみをオンにします。

    インポート操作が完了すると、 **WspImportProject1** という名前の新しいプロジェクトが作成されます。このプロジェクトには、 **フィールド** という名前のフォルダーが含まれています。 このフォルダーには、カスタムサイト列の **テスト列** とその定義ファイル *Elements.xml* ます。

## <a name="deploy-the-project"></a>プロジェクトをデプロイする
 最後に、[カスタムサイト] 列を表示するために、前に作成した2つ目の SharePoint サブサイトに **WspImportProject1** を配置します。

### <a name="to-deploy-the-project"></a>プロジェクトを展開するには

1. で、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] F5 キーを **押し** て、 *.wsp* インポートプロジェクトを配置して実行します。

2. SharePoint サイトで、[サイトの **操作** ] メニューを開き、[サイトの **設定** ] を選択して [サイトの設定] ページを表示します。

3. [ **ギャラリー** ] セクションで、[ **サイト列** ] リンクを選択します。

4. [ **カスタム列** ] セクションまで下にスクロールします。

     最初の SharePoint サイトからインポートしたカスタムサイト列が一覧に表示されます。

## <a name="see-also"></a>関連項目
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
- [Web パーツまたはアプリケーション ページの再利用できるコントロールを作成する](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
