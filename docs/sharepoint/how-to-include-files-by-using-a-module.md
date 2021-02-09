---
title: '方法: モジュールを使用してファイルを含める | |Microsoft Docs'
description: モジュールを使用してファイルを含める方法を理解します。これは、ASPX マスターページ、テキストファイル、画像などのファイルを SharePoint に配置できるコンテナーです。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, modules
- modules [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e83a1474c7dfe6385c36cc13646bfe40fc897640
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99913625"
---
# <a name="how-to-include-files-by-using-a-module"></a>方法: モジュールを使用してファイルを含める
  *モジュール* (モジュールと混同しないで [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ください) は、ASPX マスターページ、テキストファイル、画像などのファイルを SharePoint に配置できるコンテナーです。

 ドキュメントライブラリの外部にあるファイルをドキュメントライブラリに配置するか、通常のファイル (default.aspx など) として配置するかを選択できます。 ファイルをドキュメントライブラリに追加するには、 `Type="GhostableInLibrary"` **file** 要素の属性としてを指定します。 この設定により、ファイルがライブラリに追加されたときにファイルを使用するためのリスト項目を作成するように SharePoint に指示します。 ドキュメントライブラリの外部にファイルを配置するに `Type="Ghostable"` は、 **Type** 属性を指定するか省略します。

## <a name="add-a-module-to-a-sharepoint-solution"></a>SharePoint ソリューションにモジュールを追加する

#### <a name="to-add-a-module"></a>モジュールを追加するには

1. で [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 、SharePoint プロジェクトを開くか作成します。

     詳細については、「 [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

2. **ソリューションエクスプローラー** で、プロジェクトノードを選択し、メニューバーで [**プロジェクト**] [  >  **新しい項目の追加**] の順に選択します。

     **[新しい項目の追加]** ダイアログ ボックスが開きます。

3. SharePoint テンプレートの一覧で、[ **モジュール** ] テンプレートを選択し、[ **追加** ] をクリックします。

     この手順により、プロジェクト内に Module1 という名前のノードが作成されます。

4. [Module1] の下で、 *Sample.txt* ファイルを削除します。

     Sample.txt は、例としてすべての新しいモジュールに含まれているため、必要ありません。 (ファイルを削除すると、モジュールの *Elements.xml* ファイルからもエントリが削除されることに注意してください)。

5. ファイルを SharePoint の特定のフォルダー構造に配置する場合は、[Module1] ノードを選択し、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] メニューバーで [ **プロジェクト**]、[ **新しいフォルダー**] の順に選択して、これらのフォルダーを module1 の下に作成します。

6. ファイルを追加するフォルダーを選択し、メニューバーで [ **プロジェクト**]、[ **既存項目の追加**] の順に選択します。

7. SharePoint に配置する1つ以上のファイルを選択し、[ **追加** ] ボタンをクリックします。

     プロジェクトにファイルを追加すると、そのファイルのエントリがモジュールの Elements.xml ファイルに自動的に追加されます。 プロジェクトが配置されると、ファイルは、プロジェクトのルートディレクトリを基準として SharePoint サーバーにコピーされます。これは、 **ファイル** 要素の **Url** 属性で指定します (など) `Url="Module1/New Folder/SomeFile.doc` 。 ファイルの配置場所を変更する場合は、ファイルを **ソリューションエクスプローラー** 内の別のフォルダーに移動するか、 **Url** 設定を変更します。

8. ドキュメントライブラリに表示するファイルについては、 `Type="GhostableInLibrary"` *Elements.xml* のエントリに属性を追加します。 たとえば、次のように入力します。

    ```xml
    <File Path="Module1\Some Folder\SomePage.aspx" Url="Module1/Some Folder/SomePage.aspx" Type="GhostableInLibrary" />
    ```

9. プロジェクトを配置する。

     ファイルは、SharePoint 内の指定した場所にコピーされます。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのパッケージ化と配置](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
