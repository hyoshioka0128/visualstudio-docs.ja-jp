---
title: サポートされていないデータベースプロバイダー
description: 選択した接続では、サポートされていないデータベース プロバイダーが使用されています
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9ff4120796a40da00e258026d8db84ba6e9dbb21
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2020
ms.locfileid: "89743271"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>選択した接続では、サポートされていないデータベース プロバイダーが使用されています

このメッセージは、SQL Server の .NET Framework Data Provider を使用しない項目を **サーバーエクスプローラー** または **データベースエクスプローラー** から [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)にドラッグしたときに表示されます。

**O/R デザイナー**は、SQL Server に .NET Framework プロバイダーを使用するデータ接続のみをサポートしています。 有効な接続は、Microsoft SQL Server または Microsoft SQL Server データベース ファイルへの接続だけです。

このエラーを修正するには、SQL Server の .NET Framework Data Provider を使用するデータ接続から、 **O/R デザイナー**に項目のみを追加します。

## <a name="see-also"></a>関連項目

- <xref:System.Data.SqlClient>
- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
