---
title: データへのアクセス
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- "80025080"
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
ms.assetid: 9812a6d5-23d2-4427-8b98-70a2abfec3bc
caps.latest.revision: 103
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: d2b716bb4e6119c76f593ff067784f360cb48187
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75917034"
---
# <a name="accessing-data-in-visual-studio"></a>Visual Studio でのデータへのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、ローカルコンピューター、ローカルエリアネットワーク、パブリッククラウド、プライベートクラウド、またはハイブリッドクラウドで、事実上すべてのデータベース製品またはサービスのデータに接続するアプリケーションを作成できます。

 JavaScript、Python、PHP、Ruby、またはのアプリケーションC++では、ライブラリを入手してコードを記述することで、他の操作と同様にデータに接続できます。 .NET アプリケーションの場合、Visual Studio には、データソースの探索、メモリ内のデータを格納および操作するためのオブジェクトモデルの作成、およびユーザーインターフェイスへのデータのバインドに使用できるツールが用意されています。     Microsoft Azure には、.NET、Java、node.js、PHP、Python、Ruby、およびモバイルアプリ用の Sdk と、Azure Storage に接続するための Visual Studio のツールが用意されています。

 次の一覧は、Visual Studio から使用できる多くのデータベースおよびストレージシステムを示しています。 [Microsoft Azure](https://azure.microsoft.com/)オファリングは、基になるデータストアのすべてのプロビジョニングと管理を含むデータサービスです。  [Azure Tools For Visual studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)は、visual studio から直接 azure データストアを操作できるようにするオプションのコンポーネントです。 ここに記載されている他の SQL および NoSQL データベース製品のほとんどは、ローカルコンピューター、ローカルネットワーク、または仮想マシン上の Microsoft Azure でホストできます。 このシナリオでは、データベース自体を管理する必要があります。

 **Microsoft Azure**

||||
|-|-|-|
|SQL データベース|DocumentDB|ストレージ (blob、テーブル、キュー、ファイル)|
|SQL Data Warehouse|SQL Server Stretch Database|StorSimple|

 その他

 **SQL**

||||
|-|-|-|
|SQL Server 2005 – 2016 (Express と LocalDB を含む)|Firebird|MariaDB|
|MySQL|Oracle|PostgreSQL|
|SQLite|||

 その他

 **NoSQL**

||||
|-|-|-|
|Apache Cassandra|CouchDB|MongoDB|
|NDatabase|OrientDB|RavenDB|
|VelocityDB|||

 その他

 多くのデータベースベンダーとサードパーティは、NuGet パッケージによる Visual Studio の統合をサポートしています。 Nuget.org または Visual Studio の NuGet パッケージマネージャー (**ツール** > **nuget パッケージマネージャー** > **ソリューションの nuget パッケージの管理**) を使用して、オファリングを調べることができます。 その他のデータベース製品は、拡張機能として Visual Studio と統合されます。   これらの製品を Visual Studio ギャラリーで閲覧するには、[**ツール** > の**拡張機能と更新プログラム**] に移動し、ダイアログボックスの左側のウィンドウで **[オンライン]** を選択します。  詳細については、「[データベースシステム、ツール、サンプルのインストール](../data-tools/installing-database-systems-tools-and-samples.md)」を参照してください。

> [!NOTE]
> SQL Server 2005 の延長サポートは 2016 年 4 月 12 日で終了しました。   この日付以降、Visual Studio 2015 以降のデータツールが SQL Server 2005 と引き続き動作することは保証されていません。 詳細については、 [SQL Server 2005 のサポート終了](https://www.microsoft.com/sql-server/sql-server-2005)に関するお知らせを参照してください。

### <a name="net-languages"></a>.NET 言語
 .NET Core を含むすべての .NET データアクセスは、ADO.NET に基づいています。これは、リレーショナルと非リレーショナルの両方の種類のデータソースにアクセスするためのインターフェイスを定義するクラスのセットです。 Visual Studio には、ADO.NET と連携して、データベースに接続し、データを操作し、データをユーザーに提示するのに役立つ、いくつかのツールとデザイナーがあります。 このセクションのドキュメントでは、これらのツールの使用方法について説明します。 ADO.NET command オブジェクトに対して直接プログラムを実行することもできます。 ADO.NET Api を直接呼び出す方法の詳細については、MSDN ライブラリの「 [ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx) 」を参照してください。

 ASP.NET に特化したデータアクセスドキュメントについては、ASP.NET サイトでの[データの操作](/aspnet/web-forms/overview/presenting-and-managing-data/)に関するページを参照してください。 ASP.NET MVC での Entity Framework の使用に関するチュートリアルについては、「 [mvc 5 を使用した Entity Framework 6 Code First のはじめに](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)」を参照してください。

 または Visual Basic のC#ユニバーサル WINDOWS プラットフォーム (UWP) アプリは、Microsoft Azure SDK for .NET を使用して Azure Storage およびその他の Azure サービスにアクセスできます。 Windows の Web. HttpClient クラスは、任意の RESTful サービスとの通信を可能にします。 詳細については、「 [Windows を使用して http サーバーに接続する方法](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx)」を参照してください。

 ローカルコンピューター上のデータストレージの場合、推奨される方法は、アプリケーションと同じプロセスで実行される SQLite を使用することです。 オブジェクトリレーショナルマッピング (ORM) レイヤーが必要な場合は、Entity Framework を使用できます。 詳細については、Windows デベロッパーセンターの「[データアクセス](https://msdn.microsoft.com/windows/uwp/data-access/index)」を参照してください。

 Azure サービスに接続する場合は、最新の[AZURE SDK ツール](https://azure.microsoft.com/downloads/)をダウンロードしてください。

#### <a name="data-providers"></a>データ プロバイダー
 ADO.NET で使用するデータベースには、カスタム*ADO.NET データプロバイダー*が必要です。そうでない場合は、ODBC または OLE DB インターフェイスを公開する必要があります。 Microsoft では、SQL Server 製品の[ADO.NET データプロバイダー](https://msdn.microsoft.com/data/dd363565)と、ODBC および OLE DB プロバイダーの一覧を提供しています。

#### <a name="data-modeling"></a>データ モデリング
 .NET では、データソースからデータを取得した後、メモリ内のデータをモデル化して操作するための3つの選択肢があります。

 お好みの Microsoft ORM テクノロジを Entity Framework します。 これを使用して、ファーストクラスの .NET オブジェクトとしてのリレーショナルデータに対するプログラミングを行うことができます。 新しいアプリケーションの場合、モデルが必要になったときの既定の最初の選択になります。 これには、基になる ADO.NET プロバイダーからのカスタムサポートが必要です。

 以前世代のオブジェクトリレーショナルマッパーを LINQ to SQL します。 これは、より複雑なシナリオに適していますが、アクティブな開発ではなくなりました。

 データセットは、3つのモデリングテクノロジの中で最も古いものです。 これは主に、大量のデータを処理したり、複雑なクエリや変換を実行したりしない "フォームオーバーデータ" アプリケーションを迅速に開発するために設計されています。 DataSet オブジェクトは、.NET オブジェクトよりはるかに多くの SQL database オブジェクトに似た DataTable オブジェクトと DataRow オブジェクトで構成されています。 SQL データソースに基づく比較的単純なアプリケーションの場合でも、データセットが適している可能性があります。

 これらのテクノロジを使用する必要はありません。 特にパフォーマンスが重要な場合には、DataReader オブジェクトを使用してデータベースを読み取り、必要な値を List\<T > などのコレクションオブジェクトにコピーするだけで済みます。

### <a name="native-c"></a>ネイティブ C++
 C++SQL Server に接続するアプリケーションでは、 [SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733.aspx)を使用する必要があります。 [ODBC](https://msdn.microsoft.com/library/ms710252\(v=vs.85\).aspx)または OLE DB ドライバーを直接使用して、他のデータベースにアクセスできます。 ODBC は現在の標準データベースインターフェイスですが、ほとんどのデータベースシステムは、ODBC インターフェイスを使用してアクセスできないカスタム機能を提供しています。  OLE DB は、従来の COM データアクセステクノロジであり、新しいアプリケーションでは引き続きサポートされますが、お勧めできません。  詳細については、「[データアクセス](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)」を参照してください。

 C++rest サービスを使用するプログラムは、 [ C++ rest SDK](https://github.com/Microsoft/cpprestsdk)を使用できます。

 C++Microsoft Azure Storage で動作するプログラムでは、 [Microsoft Azure Storage クライアント](https://www.nuget.org/packages/wastorage)を使用できます。

#### <a name="data-modeling"></a>データ モデリング
 Visual Studio では、のC++ORM レイヤーは提供されていません。  [Odbc](https://www.codesynthesis.com/products/odb/)は、の広く普及してC++いるオープンソースの ORM です。

 レガシビジュアルC++データアクセステクノロジの詳細については、「[データアクセス](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)」を参照してください。

### <a name="javascript"></a>JavaScript
 [Visual Studio の JavaScript](https://msdn.microsoft.com/library/hh334522.aspx)は、クロスプラットフォームアプリ、UWP アプリ、クラウドサービス、web サイト、web アプリを構築するためのファーストクラスの言語です。 Visual Studio 内から Bower、Grunt、Gulp、npm、および NuGet を使用して、お気に入りの JavaScript ライブラリとデータベース製品をインストールできます。 Azure の[web サイト](https://azure.microsoft.com/)から sdk をダウンロードして、azure storage とサービスに接続します。  ADO.NET は、サーバー側の JavaScript (node.js) をデータソースに接続するライブラリです。

### <a name="python"></a>Python
 CPython または IronPython (.NET) アプリケーションを作成するために、お気に入りの Python フレームワークと共に[Python Tools for Visual Studio](http://microsoft.github.io/PTVS/)をインストールします。  Python Tools for Visual Studio の web サイトには、azure での[Django と SQL Database](https://github.com/Microsoft/PTVS/wiki/Django-and-SQL-Database-on-Azure)、azure 上の[Django と MySQL](https://github.com/Microsoft/PTVS/wiki/Django-and-MySQL-on-Azure) 、azure での[瓶と MongoDB](https://github.com/Microsoft/PTVS/wiki/Bottle-and-MongoDB-on-Azure)など、データへの接続に関するいくつかのチュートリアルがあります。

## <a name="in-this-section"></a>このセクションの内容
 [データベースシステム、ツール、およびサンプルのインストール](../data-tools/installing-database-systems-tools-and-samples.md)データベース製品と、それらをサポートする Visual Studio 拡張機能またはドライバーを取得する方法、および実験と学習を目的としたサンプルデータベースの検索場所について説明します。

 [.Net 用 Visual Studio data tools](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1)Visual Studio のツールウィンドウを使用してデータソースに接続する方法、データセットまたは Entity Framework モデルを作成する方法、およびデータをユーザーインターフェイスコントロールにバインドする方法について説明します。

## <a name="related-topics"></a>関連トピック
 [データ、デバイス、および分析](https://msdn.microsoft.com/data-and-devices)Cortana Analytics Suite やモノのインターネットのサポートなど、Microsoft インテリジェントクラウドの概要について説明します。

 [Microsoft Azure Storage](/azure/storage/)Azure Storage について説明します。また、Azure blob、テーブル、キュー、およびファイルを使用してアプリケーションを作成する方法について説明します。

 [Azure SQL Database](https://azure.microsoft.com/documentation/services/sql-database/)サービスとしてのリレーショナルデータベース Azure SQL Database に接続する方法について説明します。

 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)データ接続アプリケーションとデータベースの設計、探索、テスト、および配置を簡略化するツールについて説明します。

 [ADO.NET](https://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)ADO.NET アーキテクチャと、ADO.NET クラスを使用してアプリケーションデータを管理し、データソースと XML を操作する方法について説明します。

 [ADO.NET Entity Framework](https://msdn.microsoft.com/data/ef)開発者がリレーショナルデータベースに対して直接ではなく、概念モデルに対してプログラミングを行うことができるデータアプリケーションを作成する方法について説明します。

 [WCF Data Services 4.5](https://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a)[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] を使用して、web 上または[Open Data Protocol (OData)](https://www.odata.org/)を実装するイントラネットにデータサービスを配置する方法について説明します。

 [Office ソリューションのデータ](https://msdn.microsoft.com/library/8478c095-864b-4ed3-8a70-1fc19b411c6a)Office ソリューションでのデータの動作について説明するトピックへのリンクが含まれています。 スキーマ指向プログラミング、データ キャッシュ、およびサーバー側データ アクセスに関する説明が含まれます。

 [LINQ (統合言語クエリ)](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)および Visual Basic にC#組み込まれているクエリ機能と、リレーショナルデータベース、XML ドキュメント、データセット、およびメモリ内コレクションに対してクエリを実行するための一般的なモデルについて説明します。

 [Visual Studio の XML ツール](../xml-tools/xml-tools-in-visual-studio.md)Xml データの操作、XSLT のデバッグ、XML 機能の .NET Framework、および XML クエリのアーキテクチャについて説明します。

 [XML ドキュメントと XML データ](https://msdn.microsoft.com/library/e695047f-3c0f-4045-8708-5baea91cc380).NET Framework 内の XML ドキュメントとデータを操作する包括的で統合されたクラスのセットについて概要を説明します。
