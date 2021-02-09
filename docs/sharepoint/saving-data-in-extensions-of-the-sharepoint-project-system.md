---
title: SharePoint プロジェクトシステムの拡張機能におけるデータの保存 |Microsoft Docs
titleSuffix: ''
description: 拡張機能を含む SharePoint プロジェクトを終了した後に保持される文字列データを保存する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- SharePoint project items, saving string data
- project items [SharePoint development in Visual Studio], saving string data
- projects [SharePoint development in Visual Studio], saving string data
- SharePoint projects, saving string data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 579289a7ba5afa1eb50bdf5f1dbb105fc2a6b01e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99881569"
---
# <a name="save-data-in-extensions-of-the-sharepoint-project-system"></a>SharePoint プロジェクトシステムの拡張機能にデータを保存する
  SharePoint プロジェクトシステムを拡張すると、SharePoint プロジェクトを閉じた後も保持される文字列データを保存できます。 データは、通常、特定のプロジェクトアイテムまたはプロジェクト自体に関連付けられています。

 保持する必要のないデータがある場合は、インターフェイスを実装する SharePoint ツールオブジェクトモデル内の任意のオブジェクトにデータを追加でき <xref:Microsoft.VisualStudio.SharePoint.IAnnotatedObject> ます。 詳細については、「 [SharePoint ツールの拡張機能とカスタムデータの関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)」を参照してください。

## <a name="save-data-that-is-associated-with-a-project-item"></a>プロジェクト項目に関連付けられているデータを保存する
 特定の SharePoint プロジェクト項目に関連付けられているデータ (プロジェクト項目に追加するプロパティの値など) がある場合は、そのデータをプロジェクト項目の *sharepointprojectitem.spdata* ファイルに保存できます。 これを行うには、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> オブジェクトのプロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem> ます。 このプロパティに追加したデータは、プロジェクト項目の *sharepointprojectitem.spdata* ファイルの **extensiondata** 要素に保存されます。 詳細については、「 [Extensiondata 要素](../sharepoint/extensiondata-element.md)」を参照してください。

 次のコード例は、プロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItem.ExtensionData%2A> て、カスタム SharePoint プロジェクト項目の種類で定義されている文字列プロパティの値を保存する方法を示しています。 大きな例のコンテキストでこの例を確認するには、「 [方法: カスタム SharePoint プロジェクト項目の種類にプロパティを追加](../sharepoint/how-to-add-a-property-to-a-custom-sharepoint-project-item-type.md)する」を参照してください。

 [!code-vb[SPExtensibility.ProjectItemExtension.MenuAndProperty#14](../sharepoint/codesnippet/VisualBasic/projectitemmenuandproperty/extension/projectitemtypeproperty.vb#14)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.MenuAndProperty#14](../sharepoint/codesnippet/CSharp/projectitemmenuandproperty/extension/projectitemtypeproperty.cs#14)]

## <a name="save-data-that-is-associated-with-a-project"></a>プロジェクトに関連付けられているデータを保存する
 SharePoint プロジェクトに追加するプロパティの値などのプロジェクトレベルのデータがある場合は、プロジェクトファイル ( *.csproj* ファイルまたは *.vbproj* ファイル) またはプロジェクトユーザーオプションファイル ( *.csproj* ファイルまたは *.vbproj* ファイル) にデータを保存することができます。このような場合は、 データの保存先として選択するファイルは、データの使用方法によって異なります。

- SharePoint プロジェクトを開いているすべての開発者がデータを使用できるようにするには、データをプロジェクトファイルに保存します。 このファイルは常にソース管理データベースにチェックインされるので、このファイル内のデータは、プロジェクトをチェックアウトする他の開発者が使用できます。

- Visual Studio で SharePoint プロジェクトを開いている現在の開発者のみがデータを使用できるようにするには、データを project ユーザーオプションファイルに保存します。 通常、このファイルはソース管理データベースにチェックインされないため、このファイル内のデータは、プロジェクトをチェックアウトする他の開発者が使用することはできません。

### <a name="save-data-to-the-project-file"></a>データをプロジェクトファイルに保存する
 データをプロジェクトファイルに保存するには、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> オブジェクトをオブジェクトに変換 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> してから、メソッドを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.SetPropertyValue%2A> ます。 次のコード例は、このメソッドを使用してプロジェクトプロパティの値をプロジェクトファイルに保存する方法を示しています。 大規模なサンプルのコンテキストでこの例を確認するには、「 [方法: SharePoint プロジェクトにプロパティを追加](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)する」を参照してください。

 [!code-vb[SpExt_SPCustomPrjProperty#3](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#3)]
 [!code-csharp[SpExt_SPCustomPrjProperty#3](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#3)]

 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject>Visual studio オートメーションオブジェクトモデルまたは統合オブジェクトモデルでオブジェクトを他の型に変換する方法の詳細については、「 [SharePoint プロジェクトシステムの種類とその他の visual studio プロジェクトの種類の間での変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)」を参照してください。

### <a name="save-data-to-the-project-user-option-file"></a>プロジェクトユーザーオプションファイルにデータを保存する
 プロジェクトユーザーオプションファイルにデータを保存するには、 <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectUserFileData%2A> オブジェクトのプロパティを使用し <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> ます。 次のコード例では、このプロパティを使用してプロジェクトのプロパティの値をプロジェクトのユーザーオプションファイルに保存する方法を示します。 大規模なサンプルのコンテキストでこの例を確認するには、「 [方法: SharePoint プロジェクトにプロパティを追加](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)する」を参照してください。

 [!code-vb[SpExt_SPCustomPrjProperty#2](../sharepoint/codesnippet/VisualBasic/customspproperty/customproperty.vb#2)]
 [!code-csharp[SpExt_SPCustomPrjProperty#2](../sharepoint/codesnippet/CSharp/customspproperty/customproperty.cs#2)]

## <a name="see-also"></a>関連項目
- [SharePoint プロジェクト システムを拡張する](../sharepoint/extending-the-sharepoint-project-system.md)
- [カスタムデータと SharePoint ツールの拡張機能の関連付け](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
- [SharePoint プロジェクトシステムの種類とその他の Visual Studio プロジェクトの種類の変換](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
