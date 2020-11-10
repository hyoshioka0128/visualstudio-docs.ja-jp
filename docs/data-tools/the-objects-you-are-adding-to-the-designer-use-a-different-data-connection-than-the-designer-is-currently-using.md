---
title: オブジェクトは別の接続を使用する
description: デザイナーに追加しようとしているオブジェクトは、デザイナーとは異なるデータ接続を使用しています。 この Visual Studio O/R デザイナーのメッセージに関する情報を表示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 332ed2f3-3377-4d51-8e3b-fdb98231978e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: eaae3cd82868a769ec15904fcddcb668c9ef2f5a
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94435952"
---
# <a name="the-objects-you-are-adding-to-the-designer-use-a-different-data-connection-than-the-designer"></a>デザイナーに追加しようとしているオブジェクトは、デザイナーとは異なるデータ接続を使用しています

デザイナーに追加する対象のオブジェクトは、デザイナーが現在使用しているのとは異なるデータ接続を使用しています。 デザイナーが使用している接続に置き換えますか?

**オブジェクトリレーショナルデザイナー** ( **O/R デザイナー** ) に項目を追加すると、すべての項目が1つの共有データ接続を使用します。 (デザインサーフェイスは、 <xref:System.Data.Linq.DataContext> サーフェイス上のすべてのオブジェクトに対して単一の接続を使用するを表します)。デザイナーによって現在使用されているデータ接続とは異なるデータ接続を使用するオブジェクトをデザイナーに追加すると、このメッセージが表示されます。 このエラーを解決するために、既存の接続を維持するように選択できます。 その場合、選択したオブジェクトは追加されません。 別の方法として、オブジェクトを追加し、<xref:System.Data.Linq.DataContext> 接続を新しい接続にリセットすることもできます。

## <a name="connection-options"></a>接続オプション

- 既存の接続を、選択したオブジェクトによって使用されている接続に置き換えるには、[ **はい]** をクリックします。

   選択したオブジェクトが **O/R デザイナー** に追加され、 *DataContext 接続* が新しい接続に設定されます。

   > [!NOTE]
   > [ **はい** ] をクリックすると、 **O/R デザイナー** のすべてのエンティティクラスが新しい接続にマップされます。

- 既存の接続を引き続き使用して、選択したオブジェクトの追加をキャンセルするには、[ **いいえ** ] をクリックします。

   操作がキャンセルされます。 DataContext. 接続は、既存の接続に設定されたままに *なります。*

## <a name="see-also"></a>関連項目

- [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
