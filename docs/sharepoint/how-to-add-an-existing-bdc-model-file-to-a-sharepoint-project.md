---
title: '方法: 既存の BDC モデルファイルを SharePoint プロジェクトに追加する |Microsoft Docs'
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.BDC.ImportDialog
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], import a model
- Business Data Connectivity service [SharePoint development in Visual Studio], reuse a model
- BDC [SharePoint development in Visual Studio], import a model
- BDC [SharePoint development in Visual Studio], remove a model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: fbfbd4e485a359b7e760188217326d23d3b0aa47
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584621"
---
# <a name="how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project"></a>方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する
  Visual Studio を使用して、モデルファイル (*bdcm*) を任意の SharePoint ファームプロジェクトに追加することにより、ビジネスデータ接続 (BDC) モデルをカスタマイズ、パッケージ化、および再配置できます。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

### <a name="to-add-a-bdc-model-file-to-a-sharepoint-project"></a>BDC モデルファイルを SharePoint プロジェクトに追加するには

1. **ソリューションエクスプローラー**で、SharePoint プロジェクトのフォルダーを選択します。

2. メニューバーで、[**プロジェクト**] [既存の項目の追加] の順に選択し  >  **Add Existing Item**ます。

3. [ **既存項目の追加** ] ダイアログボックスで、プロジェクトに追加するモデル定義ファイルの場所を参照し、ファイルを選択して、[ **追加** ] ボタンをクリックします。

    モデルで、 *.net アセンブリ型の基幹業務 (LOB) システム*が定義されていない場合は、[ **.Net アセンブリの追加** ] ダイアログボックスが表示されます。

4. ダイアログボックスが表示されたら、次のいずれかの手順を実行します。

   - カスタムコードを記述し、デザイナーを使用してインポートしたモデルのメタデータを定義する場合は、[ **はい** ] をクリックし、システムに名前を指定して、[ **OK** ] をクリックします。

   - それ以外の場合は、[ **いいえ** ] ボタンをクリックし、[ **OK** ] をクリックします。

     **ビジネスデータ接続モデル**項目がプロジェクトに追加されます。

## <a name="see-also"></a>関連項目
- [ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)
- [方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)
- [方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)
- [方法: BDC 機能にカスタムアセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)
- [SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)
