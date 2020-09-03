---
title: デザイナーに追加しようとしているオブジェクトは、デザイナーが現在使用しているものとは異なるデータ接続を使用しています。Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d9ec76446aff930475ea5e3ca0133e11b3798b0c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672302"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer-is-currently-using"></a>デザイナーに追加する対象のオブジェクトは、デザイナーが現在使用しているのとは異なるデータ接続を使用しています
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

デザイナーに追加する対象のオブジェクトは、デザイナーが現在使用しているのとは異なるデータ接続を使用しています。 デザイナーが使用している接続に置き換えますか?

 () に項目を追加すると [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 、すべての項目が1つの共有データ接続を使用します。 (デザインサーフェイスは、 <xref:System.Data.Linq.DataContext> サーフェイス上のすべてのオブジェクトに対して単一の接続を使用するを表します)。デザイナーによって現在使用されているデータ接続とは異なるデータ接続を使用するオブジェクトをデザイナーに追加すると、このメッセージが表示されます。 このエラーを解決するために、既存の接続を維持するように選択できます。 その場合、選択したオブジェクトは追加されません。 別の方法として、オブジェクトを追加し、<xref:System.Data.Linq.DataContext> 接続を新しい接続にリセットすることもできます。

> [!NOTE]
> [ **はい**] をクリックすると、のすべてのエンティティクラス [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] が新しい接続にマップされます。

### <a name="to-replace-the-existing-connection-with-the-connection-used-by-the-selected-object"></a>選択したオブジェクトで使用されている接続で既存の接続を置換するには

- **[はい]** をクリックします。

     選択したオブジェクトが [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]に追加され、DataContext.Connection が新しい接続に設定されます。

### <a name="to-continue-to-use-the-existing-connection-and-cancel-adding-the-selected-object"></a>既存の接続を引き続き使用し、選択したオブジェクトの追加を取り消すには

- **[いいえ]** をクリックします。

     操作がキャンセルされます。 DataContext.Connection は、既存の接続に設定されたままになります。

## <a name="see-also"></a>参照
 [Visual Studio LINQ to SQL の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)