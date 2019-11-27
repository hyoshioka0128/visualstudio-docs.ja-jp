---
title: データベースおよびデータ層アプリケーションの作成と管理
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
helpviewer_keywords:
- managing change, databases
- database features of Visual Studio, managing change
- databases, managing change
- managing change, database servers
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
caps.latest.revision: 40
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c2b1caf45235f9dd745841cb26a2fa10a148a7b5
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299641"
---
# <a name="creating-and-managing-databases-and-data-tier-applications-in-visual-studio"></a>Visual Studio でのデータベースおよびデータ層アプリケーションの作成と管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

重要]
> 以前のバージョンの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] に含まれていたデータベースプロジェクトは、[!INCLUDE[sql_Denali_long](../includes/sql-denali-long-md.md)] ツールで提供されるようになりました。 詳細については、「 [SQL Server Developer ツール](https://go.microsoft.com/fwlink/?LinkId=228126)」を参照してください。

 データベースプロジェクトを使用して、新しいデータベース、新しいデータ層アプリケーション (Dac) を作成したり、既存のデータベースおよびデータ層アプリケーションを更新したりできます。 データベースプロジェクトと DAC プロジェクトの両方を使用すると、これらの手法をマネージコードまたはネイティブコードに適用するのとほぼ同じ方法で、データベース開発作業にバージョンコントロールおよびプロジェクト管理手法を適用できます。 *DAC プロジェクト*、*データベースプロジェクト*、または*サーバープロジェクト*を作成してバージョン管理することにより、開発チームがデータベースおよびデータベースサーバーの変更を管理するのに役立ちます。 チームのメンバーは、ファイルをチェックアウトして、*分離開発環境*またはサンドボックスで変更を行ってビルドし、テストしてから、チームと共有することができます。 コードの品質を確保するために、チームは、変更を運用環境に配置する前に、ステージング環境でデータベースの特定のリリースに関するすべての変更を完了し、テストすることができます。

 データ層アプリケーションでサポートされているデータベース機能の一覧については、Microsoft web サイトの「[データ層アプリケーションでサポートされる機能](https://go.microsoft.com/fwlink/?LinkId=164239)」を参照してください。 データ層アプリケーションでサポートされていない機能をデータベースで使用する場合は、代わりにデータベースプロジェクトを使用して、データベースへの変更を管理する必要があります。

## <a name="common-high-level-tasks"></a>一般的な概要タスク

|高レベルタスク|関連する参照先|
|----------------------|------------------------|
|**データ層アプリケーションの開発を開始します。** DAC は、[!INCLUDE[sskatmai_r2](../includes/sskatmai-r2-md.md)] で導入された新しい概念で、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースの定義と、クライアント/サーバーまたは3層アプリケーションによって使用されるサポートインスタンスオブジェクトを含みます。 DAC には、テーブルやビューなどのデータベースオブジェクトと共に、ログインなどのインスタンスエンティティが含まれます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用すると、dac プロジェクトを作成し、DAC パッケージファイルを作成し、その DAC パッケージファイルをデータベース管理者に送信して、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースエンジンのインスタンスに配置することができます。|[データ層アプリケーションの作成と管理の](https://go.microsoft.com/fwlink/?LinkId=160741)-   (Microsoft web サイト)<br />-   [SQL Server Management Studio](https://go.microsoft.com/fwlink/?LinkId=227328)|
|**反復的なデータベース開発の実行:** 開発者またはテスト担当者の場合は、プロジェクトの一部をチェックアウトし、分離開発環境で更新します。 この種類の環境を使用すると、チームの他のメンバーに影響を与えることなく、変更をテストできます。 変更が完了したら、ファイルをバージョン管理に戻します。他のチームメンバーが変更を取得して、テストサーバーにビルドして配置することができます。|[クエリおよびテキストエディターの -   (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=227327) (Microsoft web サイト)<br />[Transact-sql デバッガー](https://go.microsoft.com/fwlink/?LinkId=227324)の -   (Microsoft web サイト)|
|**プロトタイプの生成、テスト結果の検証、およびデータベーススクリプトとオブジェクトの変更:** [!INCLUDE[tsql](../includes/tsql-md.md)] エディターを使用して、これらの一般的なタスクのいずれかを実行できます。|[クエリおよびテキストエディターの -   (SQL Server Management Studio)](https://go.microsoft.com/fwlink/?LinkId=227327) (Microsoft web サイト)|

## <a name="see-also"></a>関連項目
 [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
