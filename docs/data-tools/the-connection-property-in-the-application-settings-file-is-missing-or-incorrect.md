---
title: 接続プロパティがありません
description: アプリケーション設定ファイルの接続プロパティが、存在しないか、正しくありません。 この Visual Studio O/R デザイナーのメッセージに関する情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 77724510-ff59-4d43-b933-a0434e1ac597
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 3e1c07424c4d43c9a3f545bd8c4d16ed5de726c1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99866490"
---
# <a name="the-connection-property-in-the-application-settings-file-is-missing-or-incorrect"></a>アプリケーション設定ファイルの接続プロパティが、存在しないか、正しくありません

アプリケーション設定ファイルの接続プロパティが、存在しないか、正しくありません。 *.Dbml* ファイルからの接続文字列が代わりに使用されています。

*.Dbml* ファイルには、見つからないアプリケーション設定ファイル内の接続文字列への参照が含まれています。 このメッセージは情報であり、**[OK]** をクリックすると接続文字列設定が作成されます。

このメッセージに応答するには、[ **OK]** を選択します。 *.Dbml* ファイルに格納されている接続情報は、アプリケーション設定に追加されます。

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
