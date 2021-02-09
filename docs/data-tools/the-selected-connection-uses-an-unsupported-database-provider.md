---
title: サポートされていないデータベースプロバイダー
description: 選択した接続はサポートされていないデータベースプロバイダーを使用しています。 この Visual Studio オブジェクトリレーショナルデザイナー (O/R デザイナー) メッセージに関する情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 246559abc0d1cbc12754b708bbc5938e9e190ddd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858306"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>選択した接続では、サポートされていないデータベース プロバイダーが使用されています

このメッセージは、SQL Server の .NET Framework Data Provider を使用しない項目を **サーバーエクスプローラー** または **データベースエクスプローラー** から [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)にドラッグしたときに表示されます。

**O/R デザイナー** は、SQL Server に .NET Framework プロバイダーを使用するデータ接続のみをサポートしています。 有効な接続は、Microsoft SQL Server または Microsoft SQL Server データベース ファイルへの接続だけです。

このエラーを修正するには、SQL Server の .NET Framework Data Provider を使用するデータ接続から、 **O/R デザイナー** に項目のみを追加します。

## <a name="see-also"></a>関連項目

- <xref:System.Data.SqlClient>
- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
