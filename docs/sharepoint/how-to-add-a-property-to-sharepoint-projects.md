---
title: '方法: SharePoint プロジェクトにプロパティを追加する |Microsoft Docs'
description: プロジェクト拡張機能を使用して、SharePoint プロジェクトにプロパティを追加します。 ソリューションエクスプローラーでプロジェクトを選択すると、プロパティウィンドウにプロパティが表示されます。
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
ms.openlocfilehash: 7be241dd4a043b8104c628e73f98e8881dc8b88b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215423"
---
# <a name="how-to-add-a-property-to-sharepoint-projects"></a>方法: SharePoint プロジェクトにプロパティを追加する
  プロジェクトの拡張機能を使用して、任意の SharePoint プロジェクトにプロパティを追加できます。 **ソリューションエクスプローラー** でプロジェクトを選択すると、プロパティが [**プロパティ**] ウィンドウに表示されます。

 次の手順では、プロジェクトの拡張機能が既に作成されていることを前提としています。 詳細については、「 [方法: SharePoint プロジェクトの拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-extension.md)する」を参照してください。

### <a name="to-add-a-property-to-a-sharepoint-project"></a>SharePoint プロジェクトにプロパティを追加するには

1. SharePoint プロジェクトに追加するプロパティを表すパブリックプロパティを持つクラスを定義します。 複数のプロパティを追加する場合は、同じクラスまたは異なるクラスのすべてのプロパティを定義できます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A>実装のメソッドで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> 、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> *projectservice* パラメーターのイベントを処理します。

3. イベントのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> 、properties クラスのインスタンスを <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectPropertiesRequestedEventArgs.PropertySources%2A> イベント引数パラメーターのコレクションに追加します。

## <a name="example"></a>例
 次のコード例は、SharePoint プロジェクトに2つのプロパティを追加する方法を示しています。 1つのプロパティは、プロジェクトのユーザーオプションファイル ( *.csproj* ファイルまたは *.vbproj* ファイル) でデータを永続化します。 もう一方のプロパティは、プロジェクトファイル (*.csproj* ファイルまたは *.vbproj* ファイル) でデータを永続化します。

 :::code language="vb" source="../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb" id="Snippet1":::
 :::code language="csharp" source="../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs" id="Snippet1":::

### <a name="understand-the-code"></a>コードの理解
 イベントが発生するたびにクラスの同じインスタンスが使用されるようにするため、 `CustomProjectProperties` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.ProjectPropertiesRequested> このコード例では、 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> このイベントが初めて発生したときに、プロジェクトのプロパティにプロパティオブジェクトを追加します。 このコードは、このイベントが再び発生するたびにこのオブジェクトを取得します。 プロパティを使用してデータをプロジェクトに関連付ける方法の詳細につい <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> ては、「 [SharePoint ツールの拡張機能とカスタムデータの関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

 プロパティ値の変更を保持するために、プロパティの **set** アクセサーは次の api を使用します。

- `CustomUserFileProperty` プロパティを使用して、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> プロジェクトのユーザーオプションファイルに値を保存します。

- `CustomProjectFileProperty` メソッドを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> その値をプロジェクトファイルに保存します。

  これらのファイルにデータを保持する方法の詳細については、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

### <a name="specify-the-behavior-of-custom-properties"></a>カスタムプロパティの動作を指定する
 名前空間からプロパティ定義に属性を適用することによって、[ **プロパティ** ] ウィンドウでカスタムプロパティの表示と動作を定義でき <xref:System.ComponentModel> ます。 次の属性は、多くのシナリオで役立ちます。

- <xref:System.ComponentModel.DisplayNameAttribute>: [ **プロパティ** ] ウィンドウに表示されるプロパティの名前を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>: プロパティが選択されたときに [ **プロパティ** ] ウィンドウの下部に表示される説明文字列を指定します。

- <xref:System.ComponentModel.DefaultValueAttribute>: プロパティの既定値を指定します。

- <xref:System.ComponentModel.TypeConverterAttribute>: [ **プロパティ** ] ウィンドウに表示される文字列と、文字列以外のプロパティ値の間のカスタム変換を指定します。

- <xref:System.ComponentModel.EditorAttribute>: プロパティの変更に使用するカスタムエディターを指定します。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- VisualStudio

- VisualStudio (相互運用)

- VisualStudio のようになります。

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクトの拡張](../sharepoint/extending-sharepoint-projects.md)
- [方法: SharePoint プロジェクトの拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-extension.md)
- [方法: ショートカットメニュー項目を SharePoint プロジェクトに追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-sharepoint-projects.md)
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
