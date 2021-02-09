---
title: '方法: BDC モデルを作成する |Microsoft Docs'
description: その種類の項目に対して Visual Studio テンプレートを使用してビジネスデータ接続 (BDC) モデルを作成し、そのモデルを任意の SharePoint プロジェクトに追加します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 77ffd8b6cd913b79249862a875b6267848a131af
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99923361"
---
# <a name="how-to-create-a-bdc-model"></a>方法: BDC モデルを作成する
  ビジネス データ接続 (BDC: Business Data Connectivity) モデルを作成するには、アイテムの種類に対応するテンプレートを使用し、モデルを任意の SharePoint プロジェクトに追加します。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。 モデルのデザイン方法の詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-create-a-bdc-project"></a>BDC プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

    > [!NOTE]
    > IDE が Visual Basic 開発設定を使用するように設定されている場合は、[**ファイル**] [新規作成] [プロジェクト] を選択し  >  ます。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

2. **Visual Basic** または **Visual C#** のいずれかで、[ **Office/Sharepoint**]、[ **sharepoint ソリューション**] の順に選択します。

3. [ **テンプレート** ] ペインで、[ **SharePoint 2013-空のプロジェクト** ] 項目を選択し、[ **OK** ] をクリックします。

     **SharePoint カスタマイズウィザード** が開きます。

4. [ **デバッグ用のサイトとセキュリティレベルの指定** ] ページで、ローカルコンピューター上の SharePoint サイトの URL を指定し、[ **ファームソリューションとして配置** ] オプションを選択して [ **完了** ] をクリックします。

     指定した SharePoint サイトでモデルをテストします。

    > [!IMPORTANT]
    > BDC モデルはファーム ソリューションのみサポートするため、プロジェクトはファーム ソリューションとして配置する必要があります。

     空の SharePoint プロジェクトが作成されます。

5. メニュー バーで **[プロジェクト]**  >  **[新しい項目の追加]** の順に選択します。

6. [ **新しい項目の追加** ] ダイアログボックスで、[ **Office/SharePoint** ] ノードを選択します。

7. SharePoint テンプレートの一覧で、[ **ビジネスデータ接続モデル (ファームソリューションのみ)**] を選択します。

8. [ **名前** ] ボックスで、BDC モデルの名前を指定し、[ **追加** ] をクリックします。

     **ビジネスデータ接続モデル** 項目がプロジェクトに追加されます。 既定で、BDC デザイナーにモデルが表示されます。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)
- [方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [方法: BDC 機能にカスタムアセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
