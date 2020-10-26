---
title: サポートされていないプロバイダーからのオブジェクト
description: サポートされていないデータベース プロバイダーのデータベース オブジェクトが選択されています
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: c0f1298e-31aa-471e-ae19-1bafffd2ae40
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 84841c5e0759618430f9c2e4f0146cbc2d21fae9
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036718"
---
# <a name="you-have-selected-a-database-object-from-an-unsupported-database-provider"></a>サポートされていないデータベース プロバイダーのデータベース オブジェクトが選択されています

**O/R デザイナー**では、SQL Server () の .NET Framework Data Provider のみがサポートされてい <xref:System.Data.SqlClient> ます。 **[OK]** をクリックし、サポートされないデータベース プロバイダーからオブジェクトの処理を続けることもできますが、実行時に予期しない動作が発生することがあります。

> [!NOTE]
> .NET Framework Data Provider for SQL Server を使用するデータ接続のみがサポートされます。

## <a name="options"></a>オプション

- **[OK]** をクリックして、サポートされないデータベース プロバイダーを使用する接続にマップされるエンティティ クラスのデザインを続行します。 サポートされないデータベース プロバイダーを使用すると、予期しない動作が発生することがあります。

- [ **キャンセル** ] をクリックして、操作を停止します。 SQL Server に .NET Framework Provider を使用する別のデータ接続を作成または使用します。

## <a name="see-also"></a>参照

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
