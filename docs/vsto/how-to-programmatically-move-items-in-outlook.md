---
title: '方法: プログラムによって Outlook で項目を移動する'
description: プログラムを使用して Microsoft Outlook で項目を移動する方法について説明します。 この例では、未読の電子メールメッセージを受信トレイから Test という名前のフォルダーに移動します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], moving items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 770f056dc681e1ee2cd6704f9bd1d42afae4957b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99888863"
---
# <a name="how-to-programmatically-move-items-in-outlook"></a>方法: プログラムによって Outlook で項目を移動する
  この例では、未読の電子メールメッセージを **受信トレイ** から **Test** という名前のフォルダーに移動します。 この例では、フィールドに **Test** という単語が含まれているメッセージのみを移動し `Subject` ます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_MoveItems#1](../vsto/codesnippet/CSharp/Trin_OL_MoveItems/thisaddin.cs#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- **Test** という名前の Outlook mail フォルダー。

- フィールドに **Test** という単語が含まれている電子メールメッセージ `Subject` 。

## <a name="see-also"></a>関連項目
- [フォルダーの操作](../vsto/working-with-folders.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: プログラムによって特定のフォルダー内を検索する](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [方法: 電子メールメッセージを受信したときにプログラムによってアクションを実行する](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
