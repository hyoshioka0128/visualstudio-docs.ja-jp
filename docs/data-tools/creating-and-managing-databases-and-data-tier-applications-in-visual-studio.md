---
title: データベースプロジェクトと DAC プロジェクト
description: 詳細については、「データベースプロジェクトとデータ層アプリケーション」 (Dac) を参照してください。 DB プロジェクトを使用して、新しいデータベースを作成し、新しい Dac を作成して、既存の db と Dac を更新します。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
helpviewer_keywords:
- databases, managing change
ms.assetid: 40b51f5a-d52c-44ac-8f84-037a0917af33
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 8ed1dc21d0029dc8939c540d33d0743c81db93fc
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99867088"
---
# <a name="database-projects-and-data-tier-applications"></a>データベースプロジェクトとデータ層アプリケーション

データベースプロジェクトを使用して、新しいデータベース、新しいデータ層アプリケーション (Dac) を作成したり、既存のデータベースおよびデータ層アプリケーションを更新したりできます。 データベースプロジェクトと DAC プロジェクトの両方を使用すると、これらの手法をマネージコードまたはネイティブコードに適用するのとほぼ同じ方法で、データベース開発作業にバージョンコントロールおよびプロジェクト管理手法を適用できます。 DAC プロジェクト、データベースプロジェクト、またはサーバープロジェクトを作成してバージョン管理することにより、開発チームがデータベースおよびデータベースサーバーの変更を管理するのに役立ちます。 チームのメンバーは、ファイルをチェックアウトして、分離開発環境またはサンドボックスで変更を行ってビルドし、テストしてから、チームと共有することができます。 コードの品質を確保するために、チームは、変更を運用環境に配置する前に、ステージング環境でデータベースの特定のリリースに関するすべての変更を完了し、テストすることができます。

データ層アプリケーションでサポートされているデータベース機能の一覧については、「 [SQL Server オブジェクトの DAC サポート](/sql/relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions)」を参照してください。 データ層アプリケーションでサポートされていない機能をデータベースで使用する場合は、代わりにデータベースプロジェクトを使用して、データベースへの変更を管理する必要があります。

## <a name="common-high-level-tasks"></a>一般的な概要タスク

| High-Level タスク | 関連する参照先 |
| - | - |
| **データ層アプリケーションの開発を開始します。** データ層アプリケーション (DAC) の概念は、SQL Server 2008 で導入されました。 DAC には、SQL Server データベースの定義と、クライアント/サーバーまたは3層アプリケーションによって使用されるサポートインスタンスオブジェクトの定義が含まれています。 DAC には、テーブルやビューなどのデータベースオブジェクトと共に、ログインなどのインスタンスエンティティが含まれます。 Visual Studio を使用して、dac プロジェクトを作成し、DAC パッケージファイルをビルドし、SQL Server データベースエンジンのインスタンスに配置するためのデータベース管理者に DAC パッケージファイルを送信できます。 | - [データ層アプリケーション](/sql/relational-databases/data-tier-applications/data-tier-applications)<br />- [SQL Server Management Studio](/sql/ssms/sql-server-management-studio-ssms) |
| **反復的なデータベース開発の実行:** 開発者は、プロジェクトの一部をチェックアウトして、分離開発環境で更新できます。 この種類の環境を使用すると、チームの他のメンバーに影響を与えることなく、変更をテストできます。 変更が完了したら、ファイルをバージョン管理に戻します。他のチームメンバーが変更を取得して、テストサーバーにビルドして配置することができます。 | - [プロジェクト指向のオフラインデータベース開発 (SQL Server Data Tools)](/sql/ssdt/project-oriented-offline-database-development)<br />- [Transact-sql デバッガー (SQL Server Management Studio)](/sql/ssms/scripting/transact-sql-debugger) |
| **プロトタイプの生成、テスト結果の検証、およびデータベーススクリプトとオブジェクトの変更:** Transact-sql エディターを使用して、次のいずれかの一般的なタスクを実行できます。 | - [クエリエディターとテキストエディター (SQL Server Management Studio)](/sql/ssms/scripting/query-and-text-editors-sql-server-management-studio) |

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
