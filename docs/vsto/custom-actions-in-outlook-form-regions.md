---
title: Outlook フォーム領域のカスタムアクション
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], custom actions
- custom actions [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 817cf9fe8698c2908e873246a8971f90fe72b460
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "71254439"
---
# <a name="custom-actions-in-outlook-form-regions"></a>Outlook フォーム領域のカスタムアクション
  アクションには、ユーザーが Microsoft Office Outlook アイテムに応答できるようにするボタンが表示されます。 たとえば、メールアイテムに応答するには、[ **返信**]、[ **全員に返信**]、または [ **転送** ] アクションボタンをクリックします。 これらの各アクションは、新しいメールアイテムを作成し、元のアイテムの情報を使用してアイテムのフィールドを設定します。

 任意の種類の Outlook アイテムを開くカスタムアクションを作成できます。 たとえば、新しい予定またはタスク項目を開くカスタムアクションを追加できます。 カスタムアクションのプロパティを設定するか、カスタムコードを使用して新しい項目のフィールドを設定します。 カスタムアクションは、Outlook インスペクターウィンドウで開かれているアイテムの [ **カスタムアクション** ] ドロップダウンに表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-custom-actions-to-a-form-region"></a>フォーム領域にカスタムアクションを追加する
 カスタムアクションをフォーム領域に追加するには、[ **カスタムアクション** ] ダイアログボックスを使用します。 [**カスタムアクション**] ダイアログボックスを開くには、**ソリューションエクスプローラー**でフォーム領域を選択し、[**プロパティ] ウィンドウ**で [**マニフェスト**] ノードを展開します。次に、[ **customactions** ] プロパティを選択し、省略記号ボタン (![ASP.NET mobile designer 楕円](../sharepoint/media/mwellipsis.gif "ASP.NET モバイル デザイナー楕円")) をクリックします。

 [ **カスタムアクション** ] ダイアログボックスを使用すると、 *ターゲットフォーム*を指定できます。 ターゲットフォームは、ユーザーがカスタム動作を実行したときに表示されるフォームです。

 また、[ **カスタム動作** ] ダイアログボックスを使用して、元の項目の情報をターゲットフォームに表示する方法を指定することもできます。

 次の表では、[ **カスタムアクション** ] ダイアログボックスで使用できるプロパティについて説明します。

|プロパティ|説明|
|--------------|-----------------|
|**AddressLike**|ターゲットフォームのアドレス指定方法を指定します。|
|**本文**|元の項目の本文をターゲットフォームに追加する方法を指定します。|
|**Enabled**|カスタム動作が有効かどうかを示します。 このプロパティが **false**に設定されている場合、カスタム動作は無効になります。|
|**方法**|カスタムアクションの実行時に使用可能な応答の種類を指定します。 カスタムアクションでは、フォームを送信したり、フォームを開いたりすることができます。また、フォームを送信するか開くかをユーザーに確認することもできます。|
|**名前**|コード内でこのカスタム動作を参照するために使用できる内部名を指定します。|
|**ShowOnRibbon**|元の項目のリボンにカスタム動作を表示するかどうかを示します。|
|**SubjectPrefix**|ターゲットフォームの件名行の先頭に挿入されるテキストを指定します。|
|**TargetForm**|ターゲットフォームのメッセージクラス名を指定します。 たとえば、「IPM」と入力し **ます。タスクフォーム** を開きます。|
|**タイトル**|カスタム動作ボタンのラベルを指定します。|

## <a name="customize-a-custom-action-at-run-time"></a>実行時にカスタムアクションをカスタマイズする
 コードを使用して、カスタム動作に動作を追加することもできます。 たとえば、電子メールの受信者の名前を取得し、それらの名前を出席者として新しい予定項目に追加するコードを追加できます。 これを行うには、 [MailItem オブジェクト](/office/vba/api/Outlook.MailItem)の[CustomAction](/office/vba/api/Outlook.MailItem.CustomAction)イベントを処理します。

## <a name="see-also"></a>関連項目
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [フォーム領域を Outlook メッセージクラスに関連付ける](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
