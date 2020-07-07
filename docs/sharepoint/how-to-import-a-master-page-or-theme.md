---
title: '方法: マスターページまたはテーマをインポートする |Microsoft Docs'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7abca9e9141fdc8d4540e8a38e9579862fc540f1
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015297"
---
# <a name="how-to-import-a-master-page-or-theme"></a>方法: マスターページまたはテーマをインポートする
  マスターページとテーマを作成して使用することで、SharePoint サイトのページに一貫した外観を与えることができます。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]では、これらの要素のテンプレートは提供されませんが、SharePoint デザイナーで作成してにインポートすることができ [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 詳細については、Microsoft web サイトの「[ビルディングブロック: Pages And User Interface](/previous-versions/office/developer/sharepoint-2010/ee539040(v=office.14)) 」を参照してください。

### <a name="to-import-a-master-page-or-theme"></a>マスターページまたはテーマをインポートするには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、SharePoint プロジェクトを作成するか開きます。

     SharePoint プロジェクトを作成する方法の詳細については、「 [sharepoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. メニューバーで、[**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

3. [**新しい項目の追加**] ダイアログボックスで、[ **SharePoint** ] ノードを展開し、[ **2010** ] ノードを選択します。

4. SharePoint テンプレートの一覧で、**モジュール**テンプレートを選択し、モジュールの名前を指定します。

     モジュールには、SharePoint で指定した場所に配置するためのファイル (マスターページやテーマファイルなど) が含まれています。

5. モジュールで、 *Sample.txt*という名前の既定のファイルを削除します。

6. モジュールノードを選択します。

7. メニューバーで、[**プロジェクト**] [既存の項目の追加] の順に選択し、  >  **Add Existing Item**マスターページまたはテーマファイルを選択します。

     マスターページファイルの拡張子は .master で、テーマファイルの拡張子は thmx です。

8. マスターページを追加した場合は、モジュールのプロパティで、**配置競合の解決**設定を**自動**に変更します。

    > [!NOTE]
    > マスターページの名前が、既定のマスターページまたはカスタムマスターページとしてマークされている既存のマスターページの名前と同じである場合に、エラーが発生することがあります。 この問題を解決する方法の詳細については、「[チュートリアル: イメージを使用したカスタムマスターページおよびサイトページのインポート](../sharepoint/walkthrough-import-a-custom-master-page-and-site-page-with-an-image.md)」を参照してください。

9. モジュールで*Elements.xml*を開きます。

     追加したマスターページまたはテーマを参照するように*Elements.xml*ファイルを更新する必要があります。

10. マスターページの場合は、既存のモジュールマークアップを次のマークアップに置き換えます。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/masterpage">
        <File Path="[Module Name]\[Master Page Name].master"
          Url="[Master Page Name].master" Type="GhostableInLibrary" />
    </Module>
    ```

     テーマの場合は、既存のモジュールマークアップを次のマークアップに置き換えます。

    ```xml
    <Module Name="[Module Name]" Url="_catalogs/theme"
        <File Path="[Module Name]\[Theme Name].thmx" Url="[Theme
          Name].thmx" Type="GhostableInLibrary" />
    </Module>
    ```

     プレースホルダーの値は、モジュールの実際の名前とマスターページまたはテーマに置き換えてください。

     属性は、 `Type="GhostableInLibrary"` アイテムがコンテンツデータベースに追加されることを示し、 `Url` モジュールの属性は、SharePoint コンテンツデータベース内のファイルを格納する場所を指定します。

11. マスターページの配置スコープを変更するには、**ソリューションエクスプローラー**で、機能デザイナーで機能ファイルを開き、[**スコープ**] ボックスの一覧から新しい展開スコープを選択します。

     値が**Web**の場合は、プロジェクトで現在指定されている web サイトにのみマスターページが適用されることを意味します。 **Site**の値は、すべてのサブサイトとルート web を含む、現在のサイトコレクションにマスターページが適用されることを意味します。 その他の値は適用されません。

    > [!NOTE]
    > テーマはサイトコレクションレベルにのみ適用されるため、テーマのスコープを [**サイト**] 以外に設定しないことをお勧めします。 テーマがサブサイトで使用されている場合、エラーが発生することがあります。

12. メニューバーで、[**ビルド**] [ソリューションの配置] の順に選択し  >  **Deploy Solution**ます。

13. ファイルが正しく配置されているかどうかを確認するには、SharePoint サイトを開き、[**サイトの操作**] メニューを選択し、[**サイトの設定**] コマンドを選択して、[**マスターページ**] リンクまたは [**テーマ**] リンクを選択します。

     マスターページまたはテーマの一覧が表示され、インポートしたマスターページまたはテーマのいずれかが含まれます。

## <a name="see-also"></a>関連項目
- [マスター ページ](/previous-versions/office/developer/sharepoint-2010/ms443795(v=office.14))
- [既存の SharePoint サイトからのアイテムのインポート](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [SharePoint のページを作成する](../sharepoint/creating-pages-for-sharepoint.md)
- [モジュールを使用してソリューションにファイルを含める](../sharepoint/using-modules-to-include-files-in-the-solution.md)
