---
title: サポートされていないプロバイダーからのオブジェクト
description: サポートされていないデータベースプロバイダーのデータベースオブジェクトを選択しました。 この Visual Studio (O/R デザイナー) メッセージに関する情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: c0f1298e-31aa-471e-ae19-1bafffd2ae40
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c3ccd477882382962efcc2f87c5dc99f59c14be1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858047"
---
# <a name="you-have-selected-a-database-object-from-an-unsupported-database-provider"></a>サポートされていないデータベース プロバイダーのデータベース オブジェクトが選択されています

**O/R デザイナー** では、SQL Server () の .NET Framework Data Provider のみがサポートされてい <xref:System.Data.SqlClient> ます。 **[OK]** をクリックし、サポートされないデータベース プロバイダーからオブジェクトの処理を続けることもできますが、実行時に予期しない動作が発生することがあります。

> [!NOTE]
> .NET Framework Data Provider for SQL Server を使用するデータ接続のみがサポートされます。

## <a name="options"></a>オプション

- **[OK]** をクリックして、サポートされないデータベース プロバイダーを使用する接続にマップされるエンティティ クラスのデザインを続行します。 サポートされないデータベース プロバイダーを使用すると、予期しない動作が発生することがあります。

- [ **キャンセル** ] をクリックして、操作を停止します。 SQL Server に .NET Framework Provider を使用する別のデータ接続を作成または使用します。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
