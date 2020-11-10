---
title: データセットを XML として保存する
description: データセットを XML として保存します。 GetXml や WriteXml など、データセットの使用可能な XML メソッドを呼び出すことによって、データセット内の XML データにアクセスします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e454aca47f9bf6425ef2dfd98747869c27523f2c
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434624"
---
# <a name="save-a-dataset-as-xml"></a>データセットを XML として保存する

データセットの使用可能な XML メソッドを呼び出すことによって、データセット内の XML データにアクセスします。 XML 形式でデータを保存するには、のメソッドまたはメソッドのいずれかを呼び出すことができ <xref:System.Data.DataSet.GetXml%2A> <xref:System.Data.DataSet.WriteXml%2A> <xref:System.Data.DataSet> ます。

メソッドを呼び出すと、 <xref:System.Data.DataSet.GetXml%2A> XML として書式設定されたデータセット内のすべてのデータテーブルのデータを含む文字列が返されます。

メソッドを呼び出すと、指定した <xref:System.Data.DataSet.WriteXml%2A> ファイルに XML 形式のデータが送信されます。

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>データセットのデータを XML として変数に保存するには

- <xref:System.Data.DataSet.GetXml%2A> メソッドが <xref:System.String> を返します。 型の変数を宣言 <xref:System.String> し、メソッドの結果を代入し <xref:System.Data.DataSet.GetXml%2A> ます。

     [!code-vb[VbRaddataSaving#12](../data-tools/codesnippet/VisualBasic/save-a-dataset-as-xml_1.vb)]
     [!code-csharp[VbRaddataSaving#12](../data-tools/codesnippet/CSharp/save-a-dataset-as-xml_1.cs)]

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>データセットのデータを XML としてファイルに保存するには

- <xref:System.Data.DataSet.WriteXml%2A>メソッドには複数のオーバーロードがあります。 変数を宣言し、ファイルを保存する有効なパスを割り当てます。 次のコードは、データをファイルに保存する方法を示しています。

     [!code-vb[VbRaddataSaving#13](../data-tools/codesnippet/VisualBasic/save-a-dataset-as-xml_2.vb)]
     [!code-csharp[VbRaddataSaving#13](../data-tools/codesnippet/CSharp/save-a-dataset-as-xml_2.cs)]

## <a name="see-also"></a>関連項目

- [データをデータベースに保存する](../data-tools/save-data-back-to-the-database.md)
