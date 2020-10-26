---
title: .NET 用 Visual Studio data tools |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9d591595c65f00e0198ded9492ae0b8399e363e5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670099"
---
# <a name="visual-studio-data-tools-for-net"></a>.NET 用の Visual Studio データ ツール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio と .NET Framework は、データベースへの接続、メモリ内のデータのモデル化、ユーザーインターフェイスでのデータの表示など、さまざまな API とツールのサポートを提供します。  データアクセス機能を提供する .NET Framework クラスは、 [ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx)と呼ばれます。 ADO.NET は、Visual Studio のデータツールと共に、主にリレーショナルデータベースと XML をサポートするように設計されています。 これらの日、多くの NoSQL データベースベンダー、またはサードパーティが ADO.NET プロバイダーを提供しています。

 Visual Studio 2015 Update 2 には            [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)の最新の更新プログラムが含まれており、Azure [SQL Database](https://azure.microsoft.com/services/sql-database/) と [SQL Server 2016](https://www.microsoft.com/sql-server/sql-server-2016)の最新機能のサポートが有効になります。 [.Net Core](https://www.dotnetfoundation.org/projects?searchquery=dotnet+core&type=project) は、データセットと関連する型を除き、ADO.NET をサポートしています。 .NET Core を対象としていて、オブジェクトリレーショナルマッピング (ORM) レイヤーが必要な場合は、 [Entity Framework Core](https://msdn.microsoft.com/data/ef.aspx)を使用します。

 次の図は、基本的なアーキテクチャの簡略化されたビューを示しています。

 ![ADO.NET のアーキテクチャ](../data-tools/media/raddata-ado-net-architecture-diagram.png "レーダーデータ ADO.NET のアーキテクチャの図")

 一般的なワークフローは次のとおりです。

1. 開発データベースまたはテストデータベースをローカルコンピューターにインストールします。 「 [データベースシステム、ツール、サンプルのインストール](../data-tools/installing-database-systems-tools-and-samples.md)」を参照してください。 Azure データサービスを使用している場合、この手順は必要ありません。

2. Visual Studio でデータベース (またはサービスまたはローカルファイル) への接続をテストします。 「 [新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

3. Optionalツールを使用して、新しいモデルを生成して構成します。 Entity Framework に基づくモデルは、新しいアプリケーションの既定の推奨事項です。 使用するモデルはいずれも、アプリケーションが操作するデータソースです。 モデルは、データベースまたはサービスとアプリケーションの間で論理的に配置されます。  「 [新しいデータソースの追加](../data-tools/add-new-data-sources.md)」を参照してください。

4. データソースを [ **データソース** ] ウィンドウから Windows フォーム、ASP.NET、または Windows Presentation Foundation デザインサーフェイスにドラッグして、指定した方法でユーザーにデータを表示するデータバインドコードを生成します。 「 [Visual Studio でのデータへのコントロールのバインド」を](../data-tools/bind-controls-to-data-in-visual-studio.md)参照してください。

5. ビジネスルール、検索、データ検証などのカスタムコードを追加したり、基になるデータベースが公開するカスタム機能を利用したりできます。

   モデルを使用するのではなく、手順3をスキップし、.NET アプリケーションをプログラミングして、コマンドをデータベースに直接発行することができます。 この場合は、ここで、関連するドキュメントが表示されます: [ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx)します。 ただし、データソース構成ウィザードとデザイナーを使用して、メモリ内に独自のオブジェクトを設定し、それらのオブジェクトに UI コントロールをデータバインドするときに、データバインディングコードを生成することができます。

## <a name="in-this-section"></a>このセクションの内容

- [ADO.NET を使用した単純なデータ アプリケーションの作成](../data-tools/create-a-simple-data-application-by-using-adonet.md)

- [新しい接続の追加](../data-tools/add-new-connections.md)

- [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)

- [Visual Studio のエンティティ データ モデル ツール](../data-tools/entity-data-model-tools-in-visual-studio.md)

- [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)

- [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)

- [データ アクセス エラーのトラブルシューティングのための追加のリソース](../data-tools/additional-resources-for-troubleshooting-data-access-errors.md)

- [Visual Studio でのサービスと WCF Data Services の Windows Communication Foundation](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

- [Visual Studio でのデータベースおよびデータ層アプリケーションの作成と管理](../data-tools/creating-and-managing-databases-and-data-tier-applications-in-visual-studio.md)

- [データ アクセス エラーのトラブルシューティングのための追加のリソース](../data-tools/additional-resources-for-troubleshooting-data-access-errors.md)

## <a name="see-also"></a>参照
 [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
