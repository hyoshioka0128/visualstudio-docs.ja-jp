---
title: プログラムによって Outlook の電子メールアイテムから添付ファイルを保存する
description: Visual Studio を使用して、Microsoft Outlook の電子メールアイテムから添付ファイルをプログラムで保存する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], attachments
- e-mail [Office development in Visual Studio], attachments
- saving e-mail attachments
- mail items [Office development in Visual Studio], attachments
- attachments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d33c2c820f03d7fb40c953165f62943e44648082
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528252"
---
# <a name="how-to-programmatically-save-attachments-from-outlook-email-items"></a>方法: プログラムによって Outlook の電子メールアイテムから添付ファイルを保存する

この例では、メールを受信トレイで受け取ったときに、電子メールの添付ファイルを指定されたフォルダーに保存します。

> [!IMPORTANT]
> この例は、C ディレクトリのルートに **TestFileSave** という名前のフォルダーを追加した場合にのみ機能します。

[!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例

[!code-csharp[Trin_OL_SaveAttachments#1](../vsto/codesnippet/CSharp/Trin_OL_SaveAttachments/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目

- [メールアイテムの操作](../vsto/working-with-mail-items.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: 電子メールメッセージを受信したときにプログラムによってアクションを実行する](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
- [方法: プログラムによって特定のフォルダー内を検索する](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
