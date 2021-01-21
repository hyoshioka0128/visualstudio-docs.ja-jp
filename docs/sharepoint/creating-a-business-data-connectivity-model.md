---
title: ビジネスデータ接続モデルを作成する |Microsoft Docs
description: Business Data Connectivity (BDC) モデルを作成するか、Visual Studio を使用して既存の BDC モデルをカスタマイズします。 各 SharePoint プロジェクトに含めることができるモデルは1つだけです。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], model
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- SharePoint development in Visual Studio, Business Data Connectivity service
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0486ce6ac53850b1b607f9e7f859806cdc3ef8fe
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850469"
---
# <a name="create-a-business-data-connectivity-model"></a>ビジネス データ接続モデルを作成する
  Business Data Connectivity (BDC) モデルを作成することも、Visual Studio を使用して既存の BDC モデルをカスタマイズすることもできます。 各 SharePoint プロジェクトに含めることができるモデルは1つだけです。 詳細については、「 [SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)」を参照してください。

## <a name="create-a-new-model"></a>新しいモデルを作成する
 新しいモデルを作成するには、**ビジネスデータ接続モデル** プロジェクトを作成するか、**空の SharePoint プロジェクト** に **ビジネスデータ接続モデル** アイテムを追加します。

> [!NOTE]
> コンピューターにがインストールされている必要があり [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] ます。

 Visual Studio によってフォルダーがプロジェクトに追加されます。 このフォルダーには、[**新しい項目の追加**] ダイアログボックスの [**ビジネスデータ接続モデル**] 項目に指定した名前が表示されます。 新しい **ビジネスデータ接続モデル** プロジェクトを作成すると、Visual Studio によってフォルダーに **BdcModel1** という名前が付いています。

 Visual Studio は、次のファイルを新しいフォルダーに追加します。

|ファイル|説明|
|----------|-----------------|
|モデル定義ファイル|エンティティ、メソッド、基幹業務 (LOB) システムオブジェクト、およびモデルを記述するその他のメタデータを定義する XML が含まれています。<br /><br /> BDC デザイナー、 **Bdc エクスプローラー**、[ **Bdc メソッドの詳細** ] ウィンドウ、および [ **プロパティ** ] ウィンドウを使用して、このファイル内のメタデータを変更します。|
|エンティティサービスコードファイル|既定のエンティティのインスタンスを取得、更新、および削除するメソッドが含まれています。|

 エンティティのプロパティを定義するには、エンティティコードファイルを編集します。 詳細については、「 [方法: モデルにエンティティを追加](../sharepoint/how-to-add-an-entity-to-a-model.md)する」を参照してください。

 エンティティのインスタンスを取得、更新、および削除するには、entity service コードファイルにコードを追加します。 詳細については、「 [ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

 プロジェクトをコンパイルすると、Visual Studio によってアセンブリが作成されます。 プロジェクトアセンブリにコードを追加する他の項目 (例: **シーケンシャルワークフロー** 項目または **Web パーツ** 項目) をプロジェクトに追加しないようにします。 ソリューションパッケージでは、アセンブリがグローバルアセンブリキャッシュにコピーされないため、ソリューションを配置するときにその項目のコードは実行されません。  ソリューションパッケージでは、アセンブリは SharePoint の BDC データベースにのみ配置されます。

> [!NOTE]
> Visual Studio は、プロジェクトをデバッグするときに、ローカルコンピューター上の両方の場所にアセンブリをコピーします。

## <a name="add-an-existing-model"></a>既存のモデルを追加する
 SharePoint デザイナーなどの他のツールを使用して作成されたモデルをインポートできます。 次の状況では、既存のモデルをプロジェクトにインポートすることを選択できます。

- SharePoint サーバーファームに既に配置されているモデルをカスタマイズするには

- 既存のモデルをパッケージ化して複数の SharePoint サーバーファームに配置すること。

  どちらの場合も、インポートするモデルで定義されている LOB システムは影響を受けず、期待どおりに機能し続けます。 既存のモデルを SharePoint プロジェクトに追加するには、Visual Studio の [ **既存項目の追加** ] ダイアログボックスを使用します。 詳細については、「 [方法: 既存の BDC モデルファイルを SharePoint プロジェクトに追加](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)する」を参照してください。

  [ **.Net アセンブリの追加**] [LobSystem] のオプションを選択すると、インポートしたモデルに .NET Framework アセンブリ型の LOB システムを追加できます。 これにより、カスタムコードを記述し、デザイナーを使用してインポートされたモデルのメタデータを定義できます。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[方法: BDC モデルを作成する](../sharepoint/how-to-create-a-bdc-model.md)|新しい BDC モデルを作成する方法について説明します。|
|[方法: 既存の BDC モデル ファイルを SharePoint プロジェクトに追加する](../sharepoint/how-to-add-an-existing-bdc-model-file-to-a-sharepoint-project.md)|既存のモデルを SharePoint プロジェクトにインポートする方法について説明します。|
|[方法: リソース ファイルを使用して、ローカライズした名前、プロパティ、およびアクセス許可を指定する](../sharepoint/how-to-use-a-resource-file-to-specify-localized-names-properties-and-permissions.md)|モデルが Web パーツまたは Web ページによって使用される場合に、モデルメタデータとマージされる文字列を指定する方法について説明します。|
|[方法: BDC 機能にカスタムアセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)|機能にカスタムアセンブリを含める方法について説明します。|
