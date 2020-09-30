---
title: メッセージクラスの .ofs ファイルのプロパティが無効です "
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.OFSPropertyError
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 66e8ecacffb58e945a3f80d03f47edc1329668d1
ms.sourcegitcommit: 9d2829dc30b6917e89762d602022915f1ca49089
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2020
ms.locfileid: "91584660"
---
# <a name="invalid-properties-in-the-ofs-file-for-the-message-class"></a>Message クラスの .ofs ファイルのプロパティが無効です。

  Outlook でデザインされたフォーム領域をインポートするときに、フォーム領域の1つ以上のフィールドが、 **新しいフォーム領域** ウィザードの最後のページで選択したメッセージクラスと互換性がない場合、"1 つ以上のプロパティが、選択されたメッセージクラスに対して有効ではありません" というエラーが表示されます。

たとえば、 **新しいフォーム領域** ウィザードの最後のページで **[仕事 (IPM.Task)]** を選択したとします。 フォーム領域に [ **会社住所** ] フィールドがある場合は、このエラーが表示されます。これは、タスクに勤務先住所がないためです。 そのため、[ **ビジネスアドレス** ] フィールドはメッセージクラスと互換性がありません `IPM.Task` 。

 [ **タスク (IPM.タスク)** 。 **新しいフォーム領域** ウィザードの最後のページにあります。 フォーム領域に [ **会社住所** ] フィールドがある場合は、このエラーが表示されます。これは、タスクに勤務先住所がないためです。 そのため、[ **ビジネスアドレス** ] フィールドはメッセージクラスと互換性がありません `IPM.Task` 。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **新しいフォーム領域** ウィザードの最後のページで、フォーム領域のフィールドと互換性のあるメッセージ クラスを選択します。

- Outlook のフォームデザイナーで、メッセージクラスと互換性のないフィールドを削除します。 **新しいフォーム領域**ウィザードの最後のページで選択しようとしているフィールドを削除します。

## <a name="see-also"></a>関連項目
- [チュートリアル: Outlook でデザインされたフォーム領域をインポートする](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
