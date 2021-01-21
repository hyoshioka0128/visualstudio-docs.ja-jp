---
title: SharePoint へのビジネス データの統合 | Microsoft Docs
description: ビジネス データ接続 (BDC) サービスのモデルを作成してビジネス データを SharePoint に統合する方法の概要を説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: f3156adc286222282ae63f70f70838bc6b7155a8
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96304351"
---
# <a name="integrate-business-data-into-sharepoint"></a>SharePoint へのビジネス データの統合
  ビジネス データを SharePoint に統合できます。 [!INCLUDE[TLA#tla_sqlsvr](../sharepoint/includes/tlasharptla-sqlsvr-md.md)] や Siebel、SAP、または Web サービスなどのバック エンドのサーバー アプリケーションからのビジネス データを使用できます。 ユーザーは、SharePoint の外部リストまたはビジネス データ Web パーツを使用して、ビジネス データの表示、追加、更新、または削除を行うことができます。  また、ユーザーは、Microsoft Outlook などの Microsoft Office アプリケーションで、このデータにオフラインでアクセスすることもできます。 詳細については、「[外部データを表示できる場所](/previous-versions/office/developer/sharepoint-2010/ee558737(v=office.14))」を参照してください。

 データを SharePoint に統合するには、ビジネス データ接続 (BDC) サービスのモデルを作成します。 BDC サービスは、データに関する情報をビジネス アプリケーションに格納する、SharePoint のアプリケーションです。 詳細については、「[Business Data Connectivity (BDC) Service](/previous-versions/office/developer/sharepoint-2010/ee556407(v=office.14))」を参照してください。

## <a name="models-in-visual-studio"></a>Visual Studio のモデル
 Visual Studio のモデルを使用すると、バックエンド データ ソースからデータを取得して更新するためのカスタム コードを記述できます。 複数のデータ ソースからのデータを集計することもできます。 たとえば、[!INCLUDE[ssNoVersion](../sharepoint/includes/ssnoversion-md.md)] データベースと Web サービスからのデータが含まれた、顧客の一覧を表示できます。

 既に SharePoint に配置されているモデルをインポートすることもできます。 モデルをインポートした後、カスタム コードを追加することも、Visual Studio を使用してモデルをパッケージ化し、複数の SharePoint サーバー ファームに配置することもできます。 詳細については、「[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)」を参照してください。

## <a name="design-a-model-in-visual-studio"></a>Visual Studio でモデルをデザインする
 デザイナーといくつかのツール ウィンドウを使用して、モデルをデザインできます。 モデルをデザインすると、Visual Studio によってモデルの XML が生成されます。 詳細については、「[BDC モデルのデザイン ツールの概要](../sharepoint/bdc-model-design-tools-overview.md)」を参照してください。

 モデルにはエンティティとメソッドが含まれます。

### <a name="entities"></a>エンティティ
 エンティティは、フィールドのコレクションを表すものです。 たとえば、エンティティはデータベース内のテーブルを表すことができます。 エンティティは、SharePoint で外部コンテンツ タイプとして表示されます。 外部コンテンツ タイプの詳細については、「[外部コンテンツ タイプとは](/previous-versions/office/developer/sharepoint-2010/ee556391(v=office.14))」を参照してください。

### <a name="methods"></a>メソッド
 メソッドを使用すると、外部コンテンツ タイプのコンシューマーは、エンティティのフィールドに対してアクションを実行できます。 たとえば、Updater メソッドを使用すると、ユーザーは顧客の住所と生年月日を変更できます。この場合、`Address` と `BirthDate` が `Customer` エンティティのフィールドです。

 Visual Studio によって、モデル内の各エンティティに対してサービス コード ファイルが生成されます。 メソッドをモデルに追加すると、Visual Studio によって、対応するメソッドがサービス コード ファイル内に生成されます。 適切なタスクを実行するためのコードを各メソッドに追加します。 たとえば、作成者メソッドをモデルに追加すると、Visual Studio によってサービス コード ファイル内に Creator メソッドが生成されます。 このメソッドは、ユーザーがモデルに基づくリストの **[新しい項目]** ボタンをクリックしたときに、BDC サービスによって呼び出されます。 そのため、データ ソースに新しいデータを追加するコードを Creator メソッドに追加してください。 詳細については、「[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[ビジネス データ接続モデルを作成する](../sharepoint/creating-a-business-data-connectivity-model.md)|新しいモデルを作成する方法、または SharePoint からエクスポートしたモデルをインポートする方法について説明します。|
|[ビジネス データ接続モデルを設計する](../sharepoint/designing-a-business-data-connectivity-model.md)|Visual Studio のデザイン ツールを使用して、モデルの要素をデザインする方法について説明します。|
|[BCS を使用するソリューションをビルドする場合 SharePoint Designer と Visual Studio のどちらを使用するかについて](/previous-versions/office/developer/sharepoint-2010/ee558875(v=office.14))|BDC のモデルを作成するときに、Visual Studio を使用するか、または SharePoint Designer を使用するかを決定するのに役立ちます。|
