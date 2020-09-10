---
title: n 層データ アプリケーションの概要
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- presentation tier
- middle tier
- data tier
- n-tier applications, about n-tier applications
ms.assetid: 1020581d-eaaa-41a2-aca4-bf4c212895f6
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 445826a2ada7b22201b7dd82948bc8bd5dd3d296
ms.sourcegitcommit: a3edc753c951f317b67ce294cd2fc74f0c45390c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2020
ms.locfileid: "89426864"
---
# <a name="n-tier-data-applications-overview"></a>n 層データ アプリケーションの概要
"*n 層*" データ アプリケーションは、複数の "*層*" に分けられたデータ アプリケーションです。 n 層アプリケーションは、"分散型アプリケーション" または "多層アプリケーション" とも呼ばれ、処理を別個の層に分け、クライアントとサーバー間に分散します。 データにアクセスするアプリケーションを開発する場合は、アプリケーションを構成する各種の層を明確に分離する必要があります。

一般的な n 層アプリケーションには、プレゼンテーション層、中間層、およびデータ層が含まれます。 n 層アプリケーションで各層を分離する最も簡単な方法は、アプリケーションに組み込む層ごとに別個のプロジェクトを作成することです。 たとえば、プレゼンテーション層を Windows フォーム アプリケーションにする一方で、データ アクセス ロジックを、中間層に配置されるクラス ライブラリにすることができます。 また、プレゼンテーション層では、Web サービスなどのサービスを通して中間層のデータ アクセス ロジックと通信できます。 アプリケーション コンポーネントを別個の層に分離すると、アプリケーションの保守容易性とスケーラビリティが向上します。 これは、ソリューション全体を再設計しなくても 1 つの層に適用できる、新しい技術を簡単に導入できるようにすることで実現されます。 さらに、通常、n 層アプリケーションでは、機密情報が中間層に格納され、プレゼンテーション層から分離されます。

Visual Studio には、開発者が n 層アプリケーションを作成するときに役立つ機能がいくつか用意されています。

- データセットには、データセット (データ エンティティ層) と TableAdapters (データ アクセス層) を別個のプロジェクトに分離できるようにする **DataSet Project** プロパティが用意されています。

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)には、DataContext とデータ クラスを別個の名前空間に生成する設定が用意されています。 これにより、データ アクセス層とデータ エンティティ層の論理的な分離が可能になります。

- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) には、アプリケーションのさまざまな層から DataContext をまとめることができる <xref:System.Data.Linq.Table%601.Attach%2A> メソッドが用意されています。 詳細については、「[LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)」を参照してください。

## <a name="presentation-tier"></a>プレゼンテーション層
*プレゼンテーション層*は、ユーザーがアプリケーションとやりとりする層です。 多くの場合、追加のアプリケーション ロジックも含まれています。 一般的なプレゼンテーション層のコンポーネントには、次のようなものがあります。

- データ バインディング コンポーネント (<xref:System.Windows.Forms.BindingSource> や <xref:System.Windows.Forms.BindingNavigator> など)

- データのオブジェクト表現 (プレゼンテーション層で使用する [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) エンティティ クラスなど)

通常、プレゼンテーション層は、サービス参照 (たとえば、[Visual Studio アプリケーションでの Windows Communication Foundation サービスと WCF Data Services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)) を使用して中間層にアクセスします。 プレゼンテーション層からデータ層に直接アクセスすることはありません。 プレゼンテーション層は、中間層のデータ アクセス コンポーネントを通してデータ層と通信します。

## <a name="middle-tier"></a>中間層
*中間層*は、プレゼンテーション層とデータ層が互いに通信するために使用する層です。 一般的な中間層のコンポーネントには、次のようなものがあります。

- ビジネス ロジック (ビジネス ルールやデータ検証など)

- 次のようなデータ アクセス コンポーネントおよびロジック

  - [TableAdapters](create-and-configure-tableadapters.md)、[DataAdapters と DataReaders](/dotnet/framework/data/adonet/dataadapters-and-datareaders)

  - データのオブジェクト表現 ([LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) エンティティ クラスなど)

  - 共通のアプリケーション サービス (認証、承認、パーソナル化など)

次の図は、Visual Studio で使用できる機能および技術と、n 層アプリケーションの中間層においてそれらが適合する位置を示しています。

![中間層コンポーネント](../data-tools/media/ntiermid.png) 中間層

通常、中間層は、データ接続を使用してデータ層に接続します。 一般に、このデータ接続はデータ アクセス コンポーネントに格納されます。

## <a name="data-tier"></a>データ層
*データ層* は、基本的に、アプリケーションのデータを格納するサーバー (たとえば、SQL Server を実行するサーバー) です。

次の図は、Visual Studio で使用できる機能および技術と、n 層アプリケーションのデータ層においてそれらが適合する位置を示しています。

![データ層コンポーネント](../data-tools/media/ntierdatatier.png) データ層

プレゼンテーション層のクライアントからデータ層に直接アクセスすることはできません。 代わりに、プレゼンテーション層とデータ層の間の通信では、中間層のデータ アクセス コンポーネントが使用されます。

## <a name="help-for-n-tier-development"></a>n 層開発のためのヘルプ
n 層アプリケーションを操作するための情報については、次のトピックを参照してください。

[データセットと TableAdapters を別々のプロジェクトに分離する](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)

[チュートリアル: n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)

[LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション](/dotnet/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql)

## <a name="see-also"></a>関連項目

- [チュートリアル: n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [階層更新](../data-tools/hierarchical-update.md)
- [Visual Studio のデータセット ツール](../data-tools/dataset-tools-in-visual-studio.md)
- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
