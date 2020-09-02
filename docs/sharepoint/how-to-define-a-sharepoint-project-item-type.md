---
title: '方法: SharePoint プロジェクト項目の種類を定義する |Microsoft Docs'
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
ms.openlocfilehash: ae709bf2d81e2b8b00dc984602c0426fdf272ebd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016858"
---
# <a name="how-to-define-a-sharepoint-project-item-type"></a>方法: SharePoint プロジェクト項目の種類を定義する
  カスタム SharePoint プロジェクト項目を作成する場合は、プロジェクト項目の種類を定義します。 詳細については、「 [カスタム SharePoint プロジェクト項目の種類の定義](../sharepoint/defining-custom-sharepoint-project-item-types.md)」を参照してください。

### <a name="to-define-a-project-item-type"></a>プロジェクト項目の種類を定義するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> インターフェイスを実装するクラスを作成します。

4. クラスに次の属性を追加します。

    - <xref:System.ComponentModel.Composition.ExportAttribute>. この属性を使用すると、Visual Studio で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> 属性コンストラクターに渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. プロジェクト項目の種類の定義で、この属性は新しいプロジェクト項目の文字列識別子を指定します。 *会社名*の形式を使用することをお勧めします。すべてのプロジェクトアイテムの名前が一意になるようにするための*機能名*。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>. この属性は、 **ソリューションエクスプローラー**でこのプロジェクト項目に対して表示するアイコンを指定します。 この属性は省略可能です。クラスに適用しない場合、Visual Studio ではプロジェクト項目の既定のアイコンが表示されます。 この属性を設定する場合は、アセンブリに埋め込まれているアイコンまたはビットマップの完全修飾名を渡します。

5. メソッドの実装では、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> *projectItemTypeDefinition* パラメーターのメンバーを使用して、プロジェクト項目の種類の動作を定義します。 このパラメーターは、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> インターフェイスおよびインターフェイスで定義されたイベントへのアクセスを提供するオブジェクトです <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> 。 プロジェクト項目の種類の特定のインスタンスにアクセスするには、やなどのイベントを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> ます。

## <a name="example"></a>例
 単純なプロジェクト項目の種類を定義する方法を次のコード例に示します。 このプロジェクト項目の種類は、ユーザーがこの種類のプロジェクト項目をプロジェクトに追加したときに、メッセージを [ **出力** ] ウィンドウと [ **エラー一覧** ] ウィンドウに書き込みます。

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemtype.vb#2)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#2](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemtype.cs#2)]

 この例では、SharePoint プロジェクトサービスを使用して、メッセージを [ **出力** ] ウィンドウと [ **エラー一覧** ] ウィンドウに書き込みます。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-project-item"></a>プロジェクト項目を配置する
 他の開発者がプロジェクト項目を使用できるようにするには、プロジェクトテンプレートまたはプロジェクト項目テンプレートを作成します。 詳細については、「 [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)」を参照してください。

 プロジェクト項目を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリ、テンプレート、およびプロジェクト項目と共に配布するその他のファイルの拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [カスタム SharePoint プロジェクト項目の種類を定義する](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [SharePoint プロジェクト項目の項目テンプレートとプロジェクトテンプレートを作成する](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [チュートリアル: プロジェクトテンプレートを使用したサイト列プロジェクト項目の作成 (パート 1)](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [方法: プロパティをカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)
- [方法: ショートカットメニュー項目をカスタム SharePoint プロジェクト項目の種類に追加する](../sharepoint/how-to-add-a-shortcut-menu-item-to-a-custom-sharepoint-project-item-type.md)
