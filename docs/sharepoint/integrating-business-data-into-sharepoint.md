---
title: SharePoint へのビジネスデータの統合 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Business Data Connectivity service [SharePoint development in Visual Studio], business data
- BDC [SharePoint development in Visual Studio], aggregating data
- BDC [SharePoint development in Visual Studio], business data
- Business Data Connectivity service [SharePoint development in Visual Studio], aggregating data
- BDC [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], creating a model
- Business Data Connectivity service [SharePoint development in Visual Studio], data
- BDC [SharePoint development in Visual Studio], data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b4bbfb681a0dac0825bf7af4f1f27ab1c1b50053
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016307"
---
# <a name="integrate-business-data-into-sharepoint"></a>SharePoint へのビジネスデータの統合
  ビジネスデータを SharePoint に統合できます。 ビジネスデータは、、Siebel、SAP などのバックエンドサーバーアプリケーション [!INCLUDE[TLA#tla_sqlsvr](../sharepoint/includes/tlasharptla-sqlsvr-md.md)] や Web サービスから取得できます。 ユーザーは、SharePoint の外部リストまたはビジネスデータ Web パーツを使用して、ビジネスデータの表示、追加、更新、または削除を行うことができます。  また、ユーザーは、Microsoft Outlook などの Microsoft Office アプリケーションで、このデータにオフラインでアクセスすることもできます。 詳細については、「[どこで外部データを表示できるか](/previous-versions/office/developer/sharepoint-2010/ee558737(v=office.14))」を参照してください。

 データを SharePoint に統合するには、Business Data Connectivity (BDC) サービスのモデルを作成します。 BDC サービスは、データに関する情報をビジネスアプリケーションに格納する、SharePoint のアプリケーションです。 詳細については、「 [Business Data Connectivity (BDC) サービス](/previous-versions/office/developer/sharepoint-2010/ee556407(v=office.14))」を参照してください。

## <a name="models-in-visual-studio"></a>Visual Studio のモデル
 Visual Studio のモデルを使用すると、バックエンドデータソースからデータを取得および更新するためのカスタムコードを記述できます。 複数のデータソースからデータを集計することもできます。 たとえば、データベースと Web サービスのデータを含む顧客の一覧を表示でき [!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)] ます。

 既に SharePoint に配置されているモデルをインポートすることもできます。 モデルをインポートした後、カスタムコードを追加することも、Visual Studio を使用してモデルをパッケージ化し、複数の SharePoint サーバーファームに配置することもできます。 詳細については、「[ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

## <a name="design-a-model-in-visual-studio"></a>Visual Studio でのモデルのデザイン
 デザイナーといくつかのツールウィンドウを使用して、モデルをデザインできます。 モデルをデザインすると、Visual Studio によってモデル XML が生成されます。 詳細については、「 [BDC モデルデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

 モデルには、エンティティとメソッドが含まれています。

### <a name="entities"></a>エンティティ
 エンティティは、フィールドのコレクションを記述します。 たとえば、エンティティはデータベース内のテーブルを表すことができます。 エンティティは、SharePoint の外部コンテンツタイプとして表示されます。 外部コンテンツタイプの詳細については、「[外部コンテンツタイプとは](/previous-versions/office/developer/sharepoint-2010/ee556391(v=office.14))」を参照してください。

### <a name="methods"></a>メソッド
 メソッドを使用すると、外部コンテンツ型のコンシューマーは、エンティティのフィールドに対してアクションを実行できます。 たとえば、Updater メソッドを使用すると、ユーザーがアドレスを変更したり、 `Address` とがエンティティのフィールドである顧客の生年月日を変更したりでき `BirthDate` `Customer` ます。

 Visual Studio は、モデル内の各エンティティに対してサービスコードファイルを生成します。 メソッドをモデルに追加すると、Visual Studio によって、対応するメソッドがサービスコードファイルに生成されます。 各メソッドにコードを追加して、適切なタスクを実行します。 たとえば、作成者メソッドをモデルに追加すると、Visual Studio によってサービスコードファイルに Creator メソッドが生成されます。 このメソッドは、ユーザーがモデルに基づくリストの [**新しい項目**] ボタンをクリックしたときに、BDC サービスによって呼び出されます。 そのため、データソースに新しいデータを追加するコードを Creator メソッドに追加します。 詳細については、「[ビジネスデータ接続モデルの設計](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[ビジネスデータ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)|新しいモデルを作成する方法、または SharePoint からエクスポートするモデルをインポートする方法について説明します。|
|[ビジネスデータ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)|Visual Studio のデザインツールを使用して、モデルの要素をデザインする方法について説明します。|
|[BCS を使用してソリューションをビルドするときに SharePoint デザイナーと Visual Studio のどちらを使用するか](/previous-versions/office/developer/sharepoint-2010/ee558875(v=office.14))|Visual Studio を使用するか、SharePoint デザイナーを使用して BDC のモデルを作成するかを決定します。|
