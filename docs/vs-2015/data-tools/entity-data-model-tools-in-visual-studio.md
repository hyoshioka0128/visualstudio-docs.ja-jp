---
title: Entity Data Model ツール
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 1b06b573-84aa-4458-b3f5-e238df47bf45
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d663b86603145f8a665f189e5abfbfa2b0b360ae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672391"
---
# <a name="entity-data-model-tools-in-visual-studio"></a>Visual Studio の Entity Data Model ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Entity Framework は、.NET 開発者がドメイン固有のオブジェクトを使用してリレーショナルデータを操作できるようにするオブジェクトリレーショナルマッピングテクノロジです。 これにより、開発者が通常は記述する必要のあるデータアクセス コードの大部分が不要になります。 Entity Framework は、新しい .NET アプリケーションに推奨されるオブジェクトリレーショナルマッピング (ORM) モデリングテクノロジです。

 2016年3月の時点で、最新のリリースバージョンは [Entity Framework 6](https://msdn.microsoft.com/data/ef) です。 [Entity Framework 7](https://docs.efproject.net/en/latest/) はプレリリース版です。

 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ツールは、アプリケーションの構築を支援するように設計されてい [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] ます。 ツールの完全なドキュメントについては、「Entity Framework」を参照して [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ください。 [Entity Framework](https://msdn.microsoft.com/data/jj590134)

 ツールを使用 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] すると、既存のデータベースから *概念モデル* を作成し、その概念モデルをグラフィカルに視覚化して編集できます。 また、グラフィカルな概念モデルを作成し、そのモデルをサポートするデータベースを生成することもできます。 いずれの場合も、基になるデータベースの変更時には、モデルを自動的に更新できるだけではなく、アプリケーションのオブジェクトレイヤー コードも自動生成できます。 データベースの生成とオブジェクトレイヤー コードの生成はカスタマイズ可能です。

 これらは、Visual Studio 2015 の Entity Data Model ツールを構成する特定のツールです。

- [!INCLUDE[vstecado](../includes/vstecado-md.md)] ** [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] デザイナー** (**Entity Designer**) を使用して、エンティティ、アソシエーション、マッピング、および継承関係を視覚的に作成および変更できます。 **Entity Designer** [!INCLUDE[TLA#tla_cshrp](../includes/tlasharptla-cshrp-md.md)] はまたは [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] オブジェクトレイヤーコードも生成します。

- ** [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ウィザード**を使用して、既存のデータベースから概念モデルを生成し、データベース接続情報をアプリケーションに追加できます。

- **データベースの作成ウィザード**を使用すると、最初に概念モデルを作成し、そのモデルをサポートするデータベースを作成できます。

- 基になるデータベースに変更が加えられた場合は、 **モデルの更新ウィザード** を使用して、概念モデル、ストレージモデル、およびマッピングを更新できます。

  > [!NOTE]
  > Visual Studio 2010 以降では、 [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] ツールはをサポートしていません [!INCLUDE[ss2k](../includes/ss2k-md.md)] 。

  これらのツールは .edmx ファイルを生成または変更します。 このファイルには、概念モデル、ストレージモデル、およびそれらの間のマッピングについて説明する情報が含まれています。 詳細については、「  [EDMX](https://msdn.microsoft.com/data/jj650889.aspx)」を参照してください。

  Entity Framework パワーツールは、Entity Data Model を使用するアプリケーションを構築するのに役立ちます。 ツールでは、概念モデルの生成、既存のモデルの検証、概念モデルに基づくオブジェクトクラスを含むソースコードファイルの生成、およびモデルによって生成されるビューを含むソースコードファイルの生成を行うことができます。 詳細については、「 [事前に生成されたマッピングビュー](https://msdn.microsoft.com/data/dn469601.aspx)」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[ADO.NET Entity Framework](https://msdn.microsoft.com/library/a437041f-6899-4ae7-96ce-aabf528d7205)|[!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] アプリケーションを作成するために用意されているツールの使用方法について説明します。|
|[Entity Data Model](https://msdn.microsoft.com/library/2dda3d5b-4582-4ba0-a91d-fcd7a1498137)|上に構築されたアプリケーションで使用されるデータを操作するためのリンクと情報を提供 [!INCLUDE[adonet_ef](../includes/adonet-ef-md.md)] します。|
|[完全な .NET (コンソール、WinForms、WPF など) でのはじめに](/ef/ef6/get-started)|Entity Framework 7 を使用する .NET デスクトップアプリケーションを作成する方法についてのチュートリアルを提供します。|
|[ASP.NET 5 アプリケーションを新しいデータベースに](https://docs.efproject.net/en/latest/platforms/aspnetcore/new-db.html)|Entity Framework 7 を使用して新しい ASP.NET 5 アプリケーションを作成する方法について説明します。|

## <a name="see-also"></a>参照
 [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
