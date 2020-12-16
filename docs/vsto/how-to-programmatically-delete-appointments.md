---
title: '方法: プログラムによって予定を削除する'
description: Microsoft Outlook でプログラムを使用して apppointments 削除する方法について説明します。 この例では、定期的な予定の 1 つのインスタンスを削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- calendars [Office development in Visual Studio], deleting appointments
- deleting appointments
- appointments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 56bd9876fa24610412d66e71800a24b413dac576
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97526803"
---
# <a name="how-to-programmatically-delete-appointments"></a>方法: プログラムによって予定を削除する
  この例では、定期的な予定の 1 つのインスタンスを削除します。 定期的な予定のインスタンスが 2006 年 6 月 28 日 8:00 に発生することを想定しています。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-vb[Trin_Outlook_RL_DeleteAppointment#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_DeleteAppointment/thisaddin.vb#1)]
 [!code-csharp[Trin_Outlook_RL_DeleteAppointment#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_DeleteAppointment/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [予定表アイテムの操作](../vsto/working-with-calendar-items.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
- [方法: プログラムによって予定を作成する](../vsto/how-to-programmatically-create-appointments.md)
- [方法: プログラムによってカスタムカレンダーを作成する](../vsto/how-to-programmatically-create-a-custom-calendar.md)
- [方法: プログラムによって会議出席依頼を作成する](../vsto/how-to-programmatically-create-a-meeting-request.md)
