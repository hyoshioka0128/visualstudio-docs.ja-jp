---
title: '方法: BDC 機能にカスタムアセンブリを含める |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.Add_Assemblies_Dialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], add reference
- Business Data Connectivity service [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], custom assembly
- BDC [SharePoint development in Visual Studio], add reference
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 772cdbaca67cc82fc6b7eb2c5ef5adb6508df34a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "86015262"
---
# <a name="how-to-include-a-custom-assembly-in-a-bdc-feature"></a>方法: BDC 機能にカスタムアセンブリを含める
  プロジェクトは、同じソリューション内の他のプロジェクトのアセンブリを参照できます。 ただし、[参照された **アセンブリを lobsystem に割り当てる** ] ダイアログボックスを使用して、プロジェクトの機能ファイルにこれらのアセンブリを追加する必要があります。

### <a name="to-include-a-custom-assembly-in-a-business-data-connectivity-bdc-feature"></a>Business data connectivity (BDC) 機能にカスタムアセンブリを含めるには

1. **ソリューションエクスプローラー**で、BDC モデルが含まれているフォルダーを選択します。

2. **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。

3. [ **プロパティ** ] ウィンドウで、[ **アセンブリ** ] プロパティを選択し、省略記号ボタン (![ASP.NET Mobile Designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

     [ **参照アセンブリの lobsystem への割り当て** ] ダイアログボックスが表示されます。

4. **[アセンブリの選択**] の一覧で、カスタムアセンブリを選択します。

    > [!NOTE]
    > アセンブリを含むプロジェクトへの参照を追加した場合、アセンブリは [参照された **アセンブリを lobsystem に割り当てる** ] ダイアログボックスにのみ表示されます。 詳細については、「 [方法: [参照の追加] ダイアログボックスを使用して参照を追加または削除](https://msdn.microsoft.com/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)する」を参照してください。

5. [ **参照プロパティ** ] グループで、[ **LobSystem Scope** ] プロパティに対して表示される一覧を開き、カスタムアセンブリを使用するメソッドの LOB システムを選択してから、[ **OK** ] をクリックします。

    > [!NOTE]
    > カスタムアセンブリ内のコードをデバッグするには、ソリューションパッケージにアセンブリを追加する必要があります。 詳細については、「 [方法: 追加のアセンブリを追加および削除](../sharepoint/how-to-add-and-remove-additional-assemblies.md)する」を参照してください。

## <a name="see-also"></a>関連項目
- [方法: リソースファイルを使用してローカライズされた名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [方法: 既存の BDC モデルファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [ビジネスデータを SharePoint に統合する](../sharepoint/integrating-business-data-into-sharepoint.md)
