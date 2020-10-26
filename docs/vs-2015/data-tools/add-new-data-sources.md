---
title: 新しいデータソースの追加 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.datasource.datasourcefieldspicker
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio], data sources
- data sources
ms.assetid: ed28c625-bb89-4037-bfde-cfa435d182a2
caps.latest.revision: 60
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 85c07ad7995bc614df4b988bb17fa8977452b5d8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673060"
---
# <a name="add-new-data-sources"></a>新しいデータ ソースの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の .NET data tools のコンテキストでは、データ *ソース* という用語は、データストアに接続してデータを .net アプリケーションに公開する .net オブジェクトを指します。 Visual Studio デザイナーは、データソースの出力を使用して、[ **データソース** ] ウィンドウからデータベースオブジェクトをドラッグアンドドロップしたときに、データをフォームにバインドする定型コードを生成できます。 この種類のデータソースは次のようになります。

- 何らかの種類のデータベースに関連付けられている Entity Framework モデルのクラス。

- 何らかの種類のデータベースに関連付けられているデータセット。

- Windows Communication Foundation (WCF) データサービスや REST サービスなどのネットワークサービスを表すクラス。

- SharePoint サービスを表すクラス。

- ソリューション内のクラスまたはコレクション。

> [!NOTE]
> データバインディング機能、データセット、Entity Framework、LINQ to SQL、WCF、または SharePoint を使用していない場合、"データソース" の概念は適用されません。 SQLCommand オブジェクトを使用してデータベースに直接接続し、データベースと直接通信するだけです。

 データソースは、Windows フォームまたは Windows Presentation Foundation アプリケーションの **データソース構成ウィザード** を使用して作成および編集します。 Entity Framework には、まずエンティティクラスを作成してから、[**プロジェクト**] [新しいデータソースの追加] の順に選択してウィザードを開始します (詳細については、  >  **Add New Data Source**この記事で後述します)。

 ![データ ソース構成ウィザード](../data-tools/media/data-source-configuration-wizard.png "データ ソース構成ウィザード")

 作成したデータソースは、[**データソース**] ツールウィンドウに表示されます (Shift + Alt **View**+ D または  >  **その他の Windows**  >  **データソース**を表示)。 データソースは、[ **データソース** ] ウィンドウからフォームデザインサーフェイスまたはコントロールにドラッグできます。 これにより定型コードが生成されます。これは、データストアで発生したデータをユーザーに表示するコードです。 次の図は、Windows フォームにドロップされたデータセットを示しています。 アプリケーションで F5 を選択した場合、基になるデータベースのデータがフォームのコントロールに表示されます。

 ![データソースのドラッグ操作](../data-tools/media/raddata-data-source-drag-operation.png "レーダーデータデータソースのドラッグ操作")

## <a name="data-source-for-a-database-or-a-database-file"></a>データベースまたはデータベースファイルのデータソース

### <a name="dataset"></a>データセット
 データソースとしてデータセットを作成するには、**データソース構成ウィザード**([**プロジェクト**] [  >  **新しいデータ**ソースの追加]) を実行し、**データベース**のデータソースの種類を選択します。 画面の指示に従って、新規または既存のデータベース接続、またはデータベースファイルを指定します。

### <a name="entity-classes"></a>エンティティ クラス
 データソースとして Entity Framework モデルを作成するには、まず**Entity Data Model ウィザード**を実行してエンティティクラスを作成します (**Project**  >  **Add New Item**  >  **ADO.NET Entity Data Model**)。

 ![新しい Entity Framework モデルプロジェクト項目](../data-tools/media/raddata-new-entity-framework-model-project-item.png "レーダーデータの新しい Entity Framework モデルプロジェクト項目")

 モデルを生成する方法を選択します。

 ![エンティティ データ モデル ウィザード](../data-tools/media/raddata-entity-data-model-wizard.png "レーダーデータ Entity Data Model ウィザード")

 モデルをデータソースとして追加します。 生成されたクラスは、[**オブジェクト**] カテゴリを選択すると、**データソース構成ウィザード**に表示されます。

 ![エンティティクラスを使用したデータソース構成ウィザード](../data-tools/media/raddata-data-source-configuration-wizard-with-entity-classes.png "エンティティクラスを使用したレーダーデータデータソース構成ウィザード")

## <a name="data-source-for-a-service"></a>サービスのデータソース
 サービスからデータソースを作成するには、 **データソース構成ウィザード** を実行し、 **サービス** データソースの種類を選択します。 これは、[ **サービス参照の追加** ] ダイアログボックスへのショートカットにすぎません。これは、 **ソリューションエクスプローラー** でプロジェクトを右クリックし、[ **サービス参照の追加**] を選択してアクセスすることもできます。

 サービスからデータ ソースを作成すると、Visual Studio によりサービス参照がプロジェクトに追加されます。 また、Visual Studio では、サービスから返されるオブジェクトに対応するプロキシオブジェクトも作成されます。 たとえば、データセットを返すサービスは、プロジェクト内でデータセットとして表現され、特定の型を返すサービスは、プロジェクト内で、返される型として表現されます。

 次の種類のサービスからデータ ソースを作成できます。

- WCF Data Services。 詳細については、[概要](https://msdn.microsoft.com/library/7924cf94-c9a6-4015-afc9-f5d22b1743bb)に関するページを参照してください。

- WCF data services。 詳細については、「 [Visual Studio でのサービスと WCF Data Services の Windows Communication Foundation](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)」を参照してください。

- Web サービス

    > [!NOTE]
    > [ **データソース** ] ウィンドウに表示される項目は、サービスから返されるデータによって異なります。 サービスによっては、**データ ソース構成ウィザード**でバインドできるオブジェクトを作成するための十分な情報を提供しないものもあります。 たとえば、サービスが型指定されていないデータセットを返す場合、ウィザードを完了しても [ **データソース** ] ウィンドウに項目は表示されません。 これは、型指定されていないデータセットからはスキーマが提供されず、したがってウィザードでデータ ソースを作成するための十分な情報が得られないためです。

## <a name="data-source-for-an-object"></a>オブジェクトのデータソース
 1 つ以上のパブリック プロパティを公開する任意のオブジェクトからデータ ソースを作成できます。それには、**データ ソース構成ウィザード**を実行し、データ ソースの種類として **[オブジェクト]** を選択します。 オブジェクトのすべてのパブリック プロパティは、**[データ ソース]** ウィンドウに表示されます。   Entity Framework を使用し、モデルを生成した場合、アプリケーションのデータソースとなるエンティティクラスがここに表示されます。

 [ **データオブジェクトの選択** ] ページで、ツリービューのノードを展開して、バインド先のオブジェクトを指定します。 ツリービューには、プロジェクトのノードと、プロジェクトによって参照されるアセンブリおよびその他のプロジェクトのノードが含まれます。

 ツリービューに表示されないアセンブリまたはプロジェクトのオブジェクトにバインドする場合は、[参照の **追加** ] をクリックし、[ **参照の追加] ダイアログボックス** を使用して、アセンブリまたはプロジェクトへの参照を追加します。 参照を追加すると、アセンブリまたはプロジェクトがツリービューに追加されます。

> [!NOTE]
> オブジェクトがツリービューに表示される前に、オブジェクトを含むプロジェクトをビルドする必要がある場合があります。

> [!NOTE]
> ドラッグアンドドロップのデータバインディングをサポートするには、インターフェイスまたはインターフェイスを実装するオブジェクトに <xref:System.ComponentModel.ITypedList> <xref:System.ComponentModel.IListSource> 既定のコンストラクターが必要です。 そうしないと、Visual Studio はデータソースオブジェクトをインスタンス化できず、アイテムをデザイン画面にドラッグしたときにエラーが表示されます。

## <a name="data-source-for-a-sharepoint-list"></a>SharePoint リストのデータソース
 **データ ソース構成ウィザード**を実行し、データ ソースの種類として **[SharePoint]** を選択すると、SharePoint リストからデータ ソースを作成できます。 SharePoint はを通じてデータを公開する [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] ため、sharepoint データソースの作成は、サービスからデータソースを作成する場合と同じです。 **データ ソース構成ウィザード**で **[SharePoint]** 項目をクリックすると、**[サービス参照の追加]** ダイアログ ボックスが表示されます。このダイアログ ボックスで、SharePoint サーバーを指定することにより SharePoint データ サービスに接続します。  これには、SharePoint SDK が必要です。

## <a name="see-also"></a>参照
 [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
