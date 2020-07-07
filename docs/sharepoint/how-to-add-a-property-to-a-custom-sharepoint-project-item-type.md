---
title: カスタム SharePoint プロジェクト項目の種類へのプロパティの追加
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 54765b9b6b82214a7deccaee4f9ee671a72dd40d
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015993"
---
# <a name="how-to-add-a-property-to-a-custom-sharepoint-project-item-type"></a>方法: プロパティをカスタム SharePoint プロジェクト項目の種類に追加する
  カスタム SharePoint プロジェクト項目の種類を定義するときに、プロパティをプロジェクト項目に追加できます。 **ソリューションエクスプローラー**でプロジェクト項目を選択すると、プロパティが [**プロパティ**] ウィンドウに表示されます。

 次の手順では、独自の SharePoint プロジェクトアイテムの種類が既に定義されていることを前提としています。 詳細については、「[方法: SharePoint プロジェクト項目の種類を定義](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)する」を参照してください。

### <a name="to-add-a-property-to-a-definition-of-a-project-item-type"></a>プロジェクト項目の種類の定義にプロパティを追加するには

1. カスタムプロジェクト項目の種類に追加するプロパティを表すパブリックプロパティを持つクラスを定義します。 カスタムプロジェクト項目の種類に複数のプロパティを追加する場合は、同じクラスまたは異なるクラスのすべてのプロパティを定義できます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A>実装のメソッドで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> *projectItemTypeDefinition*パラメーターのイベントを処理します。

3. イベントのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 、カスタムプロパティクラスのインスタンスを <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> イベント引数パラメーターのコレクションに追加します。

## <a name="example"></a>例
 次のコード例は、" **Example property** " という名前のプロパティをカスタムプロジェクト項目の種類に追加する方法を示しています。

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#11](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#11)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#11](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#11)]

### <a name="understand-the-code"></a>コードの理解
 イベントが発生するたびにクラスの同じインスタンスが使用されるように、 `CustomProperties` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> このコード例では、 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> このイベントが初めて発生したときに、プロジェクト項目のプロパティにプロパティオブジェクトを保存します。 このコードは、このイベントが再び発生するたびにこのオブジェクトを取得します。 プロパティを使用して <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> プロジェクトアイテムでデータを保存する方法の詳細については、「 [SharePoint ツールの拡張機能とカスタムデータの関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

 プロパティ値の変更を保持するために、の**set**アクセサーは、 `ExampleProperty` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> プロパティが関連付けられているオブジェクトのプロパティに新しい値を保存します。 プロパティを使用してプロジェクトアイテムでデータを永続化する方法の詳細につい <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> ては、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

### <a name="specify-the-behavior-of-custom-properties"></a>カスタムプロパティの動作を指定する
 名前空間からプロパティ定義に属性を適用することによって、[**プロパティ**] ウィンドウでカスタムプロパティの表示と動作を定義でき <xref:System.ComponentModel> ます。 次の属性は、多くのシナリオで役立ちます。

- <xref:System.ComponentModel.DisplayNameAttribute>: [**プロパティ**] ウィンドウに表示されるプロパティの名前を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>: プロパティが選択されたときに [**プロパティ**] ウィンドウの下部に表示される説明文字列を指定します。

- <xref:System.ComponentModel.DefaultValueAttribute>: プロパティの既定値を指定します。

- <xref:System.ComponentModel.TypeConverterAttribute>: [**プロパティ**] ウィンドウに表示される文字列と、文字列以外のプロパティ値の間のカスタム変換を指定します。

- <xref:System.ComponentModel.EditorAttribute>: プロパティの変更に使用するカスタムエディターを指定します。

## <a name="compile-the-code"></a>コードのコンパイル
 これらのコード例では、次のアセンブリへの参照を含むクラスライブラリプロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>プロジェクト項目を配置する
 他の開発者がプロジェクト項目を使用できるようにするには、プロジェクトテンプレートまたはプロジェクト項目テンプレートを作成します。 詳細については、「 [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」を参照してください。

 プロジェクト項目を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリ、テンプレート、およびプロジェクト項目と共に配布するその他のファイルの拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の種類を定義する](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)
- [方法: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
- [カスタム SharePoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)
