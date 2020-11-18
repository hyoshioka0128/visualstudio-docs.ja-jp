---
title: '方法: SharePoint プロジェクト項目の拡張機能を作成する |Microsoft Docs'
description: Visual Studio に既にインストールされている SharePoint プロジェクト項目に機能を追加する場合は、「プロジェクト項目の拡張機能を作成する方法」を参照してください。
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
ms.openlocfilehash: 6ad0befdfc656233373e8c79d14495aa3f7fa21e
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850651"
---
# <a name="how-to-create-a-sharepoint-project-item-extension"></a>方法: SharePoint プロジェクト項目の拡張機能を作成する
  Visual Studio に既にインストールされている SharePoint プロジェクト項目に機能を追加する場合は、プロジェクト項目の拡張機能を作成します。 詳細については、「 [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。

### <a name="to-create-a-project-item-extension"></a>プロジェクト項目の拡張機能を作成するには

1. クラス ライブラリ プロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - Microsoft.VisualStudio.SharePoint

    - System.ComponentModel.Composition

3. <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> インターフェイスを実装するクラスを作成します。

4. クラスに次の属性を追加します。

    - <xref:System.ComponentModel.Composition.ExportAttribute>. この属性を使用すると、Visual Studio で実装を検出して読み込むことができ <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> ます。 型を <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> 属性コンストラクターに渡します。

    - <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. プロジェクト項目の拡張機能では、この属性によって、拡張するプロジェクト項目が識別されます。 プロジェクト項目の ID を属性コンストラクターに渡します。 Visual Studio に含まれているプロジェクト項目の Id の一覧については、「 [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)」を参照してください。

5. メソッドの実装では、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> *projectItemType* パラメーターのメンバーを使用して、拡張機能の動作を定義します。 このパラメーターは、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> インターフェイスおよびインターフェイスで定義されたイベントへのアクセスを提供するオブジェクトです <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemFileEvents> 。 拡張するプロジェクト項目の種類の特定のインスタンスにアクセスするには、やなどのイベントを処理し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemAdded> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemInitialized> ます。

## <a name="example"></a>例
 次のコード例は、イベントレシーバープロジェクト項目の単純な拡張機能を作成する方法を示しています。 ユーザーがイベントレシーバープロジェクト項目を SharePoint プロジェクトに追加するたびに、この拡張機能によって、[ **出力** ] ウィンドウと [ **エラー一覧** ] ウィンドウにメッセージが書き込まれます。

 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/projectitemextension.cs#1)]
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#1](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/projectitemextension.vb#1)]

 この例では、SharePoint プロジェクトサービスを使用して、メッセージを [ **出力** ] ウィンドウと [ **エラー一覧** ] ウィンドウに書き込みます。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル
 この例では、次のアセンブリへの参照が必要です。

- Microsoft.VisualStudio.SharePoint

- System.ComponentModel.Composition

## <a name="deploy-the-extension"></a>拡張機能のデプロイ
 拡張機能を配置するには、 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] アセンブリおよび拡張機能と共に配布するその他のファイル用の拡張機能 (VSIX) パッケージを作成します。 詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト項目の拡張](../sharepoint/extending-sharepoint-project-items.md)
- [チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)
