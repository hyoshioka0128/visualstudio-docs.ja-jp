---
title: 電子メールメッセージを受信したときにプログラムによってアクションを実行する
description: Microsoft Outlook で電子メールを受信した場合に、Visual Studio を使用してプログラムでカスタムアクションを実行する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], actions when e-mail is received
- NewMail event
- mail items [Office development in Visual Studio], custom actions
- e-mail [Office development in Visual Studio], custom actions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 22dbd3ae72ac8c269de603ce22bbfebef669be08
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97523886"
---
# <a name="how-to-programmatically-perform-actions-when-an-email-message-is-received"></a>方法: 電子メールメッセージを受信したときにプログラムによってアクションを実行する
  この例では、ユーザーが電子メールメッセージを受信したときにカスタムアクションを実行します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-vb[Trin_Outlook_RL_PerformActions#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_PerformActions/thisaddin.vb#1)]
 [!code-csharp[Trin_Outlook_RL_PerformActions#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_PerformActions/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [方法: Office プロジェクトでイベントハンドラーを作成する](../vsto/how-to-create-event-handlers-in-office-projects.md)
- [メールアイテムの操作](../vsto/working-with-mail-items.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
