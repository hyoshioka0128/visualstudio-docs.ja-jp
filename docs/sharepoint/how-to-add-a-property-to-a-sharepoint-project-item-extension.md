---
title: '方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する |Microsoft Docs'
titleSuffix: ''
description: SharePoint プロジェクト項目の拡張機能を使用して、Visual Studio に既にインストールされている SharePoint プロジェクト項目にプロパティを追加します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: ae43eb1fd2c20fde6e7b1ad503b87a5d1cb367b1
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850170"
---
# <a name="how-to-add-a-property-to-a-sharepoint-project-item-extension"></a>方法: SharePoint プロジェクト項目の拡張機能にプロパティを追加する
  プロジェクト項目の拡張機能を使用して、Visual Studio に既にインストールされている SharePoint プロジェクト項目にプロパティを追加できます。 **ソリューションエクスプローラー** でプロジェクト項目を選択すると、プロパティが [**プロパティ**] ウィンドウに表示されます。

 次の手順では、プロジェクト項目の拡張機能が既に作成されていることを前提としています。 詳細については、「 [方法: SharePoint プロジェクト項目の拡張機能を作成](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)する」を参照してください。

### <a name="to-add-a-property-to-a-project-item-extension"></a>プロジェクト項目の拡張機能にプロパティを追加するには

1. プロジェクト項目の種類に追加するプロパティを表すパブリックプロパティを持つクラスを定義します。 複数のプロパティをプロジェクト項目の種類に追加する場合は、同じクラスまたは異なるクラスのすべてのプロパティを定義できます。

2. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A>実装のメソッドで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> *projectItemType* パラメーターのイベントを処理します。

3. イベントのイベントハンドラーで <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> 、properties クラスのインスタンスを <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemPropertiesRequestedEventArgs.PropertySources%2A> イベント引数パラメーターのコレクションに追加します。

## <a name="example"></a>例
 次のコード例は、" **Example property** " という名前のプロパティをイベントレシーバープロジェクト項目に追加する方法を示しています。

 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemextensionproperty.cs#8)]
 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#8](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemextensionproperty.vb#8)]

### <a name="understand-the-code"></a>コードの理解
 イベントが発生するたびにクラスの同じインスタンスが使用されるようにするため、 `CustomProperties` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemPropertiesRequested> このコード例では、 <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> このイベントが初めて発生したときに、プロジェクト項目のプロパティにプロパティオブジェクトを追加します。 このコードは、このイベントが再び発生するたびにこのオブジェクトを取得します。 プロパティを使用してデータをプロジェクトアイテムに関連付ける方法の詳細につい <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject.Annotations%2A> ては、「 [SharePoint ツールの拡張機能とカスタムデータの関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

 プロパティ値の変更を保持するために、の **set** アクセサーは、 `ExampleProperty` <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> プロパティが関連付けられているオブジェクトのプロパティに新しい値を保存します。 プロパティを使用してプロジェクトアイテムでデータを永続化する方法の詳細につい <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> ては、「 [SharePoint プロジェクトシステムの拡張機能にデータを保存](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)する」を参照してください。

### <a name="specify-the-behavior-of-custom-properties"></a>カスタムプロパティの動作を指定する
 名前空間からプロパティ定義に属性を適用することによって、[ **プロパティ** ] ウィンドウでカスタムプロパティの表示と動作を定義でき <xref:System.ComponentModel> ます。 次の属性は、多くのシナリオで役立ちます。

- <xref:System.ComponentModel.DisplayNameAttribute>: [ **プロパティ** ] ウィンドウに表示されるプロパティの名前を指定します。

- <xref:System.ComponentModel.DescriptionAttribute>: プロパティが選択されたときに [ **プロパティ** ] ウィンドウの下部に表示される説明文字列を指定します。

- <xref:System.ComponentModel.DefaultValueAttribute>: プロパティの既定値を指定します。

- <xref:System.ComponentModel.TypeConverterAttribute>: [ **プロパティ** ] ウィンドウに表示される文字列と、文字列以外のプロパティ値の間のカスタム変換を指定します。

- <xref:System.ComponentModel.EditorAttribute>: プロパティの変更に使用するカスタムエディターを指定します。

## <a name="compile-the-code"></a>コードのコンパイル
 これらの例では、次のアセンブリへの参照を含むクラスライブラリプロジェクトが必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: SharePoint プロジェクト項目の拡張機能を作成する](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)
- [方法: ショートカットメニュー項目を SharePoint プロジェクト項目の拡張機能に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-sharepoint-project-item-extension.md)
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
