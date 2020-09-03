---
title: N 層データアプリケーションの概要 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- presentation tier
- middle tier
- data tier
- n-tier applications, about n-tier applications
ms.assetid: 1020581d-eaaa-41a2-aca4-bf4c212895f6
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 0f124e997669370e71819cf37423d0c2d6a414d7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658058"
---
# <a name="n-tier-data-applications-overview"></a>n 層データ アプリケーションの概要
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

N 層 * データアプリケーションは、複数の *層*に分割されるデータアプリケーションです。 n 層アプリケーションは、"分散アプリケーション" および "多階層アプリケーション" とも呼ばれ、クライアントとサーバー間に分散された別個の層に処理を分離します。 データにアクセスするアプリケーションを開発する場合は、アプリケーションを構成する各種の層を明確に分離する必要があります。

 一般的な n 層アプリケーションには、プレゼンテーション層、中間層、およびデータ層が含まれます。 n 層アプリケーションで各層を分離する最も簡単な方法は、アプリケーションに組み込む層ごとに別個のプロジェクトを作成することです。 たとえば、プレゼンテーション層を Windows フォーム アプリケーションにする一方で、データ アクセス ロジックを、中間層に配置されるクラス ライブラリにすることができます。 また、プレゼンテーション層では、サービスなどのサービスを通して中間層のデータ アクセス ロジックと通信できます。 アプリケーション コンポーネントを別個の層に分離すると、アプリケーションの保守容易性とスケーラビリティが向上します。 これは、ソリューション全体を再設計しなくても 1 つの層に適用できる、新しい技術を簡単に導入できるようにすることで実現されます。 さらに、通常、n 層アプリケーションでは、機密情報が中間層に格納され、プレゼンテーション層から分離されます。

 Visual Studio には、開発者が n 層アプリケーションを作成するときに役立つ機能がいくつか用意されています。

- データセットデザイナーには、データセット (データエンティティ層) と s (データアクセス層) を個別のプロジェクトに分割できる **データセットプロジェクト** プロパティが用意されて `TableAdapter` います。

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)には、DataContext とデータクラスを別々の名前空間に生成する設定が用意されています。 これにより、データ アクセス層とデータ エンティティ層の論理的な分離が可能になります。

- [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) には、 <xref:System.Data.Linq.Table%601.Attach%2A> アプリケーションのさまざまな層から DataContext をまとめることができるメソッドが用意されています。 詳細については、「 [LINQ to SQL を使用した N 層とリモートアプリケーション](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)」を参照してください。

## <a name="presentation-tier"></a>プレゼンテーション層
 *プレゼンテーション層*は、ユーザーがアプリケーションとやりとりする層です。 多くの場合、追加のアプリケーション ロジックも含まれています。 一般的なプレゼンテーション層のコンポーネントには、次のようなものがあります。

- データ バインディング コンポーネント (<xref:System.Windows.Forms.BindingSource> や <xref:System.Windows.Forms.BindingNavigator> など)

- プレゼンテーション層で使用する [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) エンティティクラスなど、データのオブジェクト表現。

  通常、プレゼンテーション層は、サービス参照 (たとえば、 [Visual Studio アプリケーションの Windows Communication Foundation サービスと WCF Data Services](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) ) を使用して中間層にアクセスします。 プレゼンテーション層からデータ層に直接アクセスすることはありません。 プレゼンテーション層は、中間層のデータ アクセス コンポーネントを通してデータ層と通信します。

## <a name="middle-tier"></a>中間層
 *中間層*は、プレゼンテーション層とデータ層が互いに通信するために使用する層です。 一般的な中間層のコンポーネントには、次のようなものがあります。

- ビジネス ロジック (ビジネス ルールやデータ検証など)

- 次のようなデータ アクセス コンポーネントおよびロジック

  - [Tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364) と [dataadapter と datareader](https://msdn.microsoft.com/library/cc952ca2-ec19-46ab-9189-15174b52cb74)。

  - データのオブジェクト表現 ( [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) エンティティクラスなど)。

  - 共通のアプリケーション サービス (認証、承認、パーソナル化など)

  次の図は、Visual Studio で使用できる機能および技術と、n 層アプリケーションの中間層においてそれらが適合する位置を示しています。

  ![中間層コンポーネント](../data-tools/media/ntiermid.png "NtierMid") 中間層

  通常、中間層は、データ接続を使用してデータ層に接続します。 一般に、このデータ接続はデータ アクセス コンポーネントに格納されます。

## <a name="data-tier"></a>データ層
 *データ層*は基本的に、アプリケーションのデータ (を実行しているサーバーなど) を格納するサーバーです [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 。

 次の図は、Visual Studio で使用できる機能および技術と、n 層アプリケーションのデータ層においてそれらが適合する位置を示しています。

 ![データ層コンポーネント](../data-tools/media/ntierdatatier.png "ntierdatatier") データ層

 プレゼンテーション層のクライアントからデータ層に直接アクセスすることはできません。 代わりに、プレゼンテーション層とデータ層の間の通信では、中間層のデータ アクセス コンポーネントが使用されます。

## <a name="help-for-n-tier-development"></a>n 層開発のためのヘルプ
 n 層アプリケーションを操作するための情報については、次のトピックを参照してください。

 [データセットと Tableadapter を別々のプロジェクトに分離する](../data-tools/separate-datasets-and-tableadapters-into-different-projects.md)

 [チュートリアル : n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md)

 [チュートリアル : n 層データ アプリケーションへの検証の追加](https://msdn.microsoft.com/library/b35d072c-31f0-49ba-a225-69177592c265)

 [LINQ to SQL を使用する n 層アプリケーションとリモート アプリケーション](https://msdn.microsoft.com/library/854a1cdd-53cb-45f5-83ca-63962a9b3598)

## <a name="see-also"></a>参照
 <xref:System.Data.Linq.ITable.Attach%2A>[チュートリアル: N 層データアプリケーション](../data-tools/walkthrough-creating-an-n-tier-data-application.md)[の作成 visual studio の](../data-tools/dataset-tools-in-visual-studio.md)[階層更新](../data-tools/hierarchical-update.md)データセットツール visual studio で[のデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
