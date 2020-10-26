---
title: サポートされていないデータベースプロバイダー
description: 選択した接続では、サポートされていないデータベース プロバイダーが使用されています
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c8fa073b47927f673914156c586bf27a121e53ea
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037570"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>選択した接続では、サポートされていないデータベース プロバイダーが使用されています

このメッセージは、SQL Server の .NET Framework Data Provider を使用しない項目を **サーバーエクスプローラー** または **データベースエクスプローラー** から [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)にドラッグしたときに表示されます。

**O/R デザイナー**は、SQL Server に .NET Framework プロバイダーを使用するデータ接続のみをサポートしています。 有効な接続は、Microsoft SQL Server または Microsoft SQL Server データベース ファイルへの接続だけです。

このエラーを修正するには、SQL Server の .NET Framework Data Provider を使用するデータ接続から、 **O/R デザイナー**に項目のみを追加します。

## <a name="see-also"></a>参照

- <xref:System.Data.SqlClient>
- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
