---
title: .ofs ファイルの 1 つ以上のプロパティが、選択されたメッセージ クラスに対して有効ではありません
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
ms.openlocfilehash: d58ad6ff89d8cf41ec60135cfbfe3deac1382f1e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62977862"
---
# <a name="one-or-more-properties-in-the-ofs-file-are-not-valid-for-the-message-class-selected"></a>.ofs ファイルの 1 つ以上のプロパティが、選択されたメッセージ クラスに対して有効ではありません
  このエラーは、Outlook でデザインされたフォーム領域をインポートするときに表示されますが、フォーム領域の1つ以上のフィールドが、 **新しいフォーム領域** ウィザードの最後のページで選択したメッセージクラスと互換性がありません。

たとえば、 **新しいフォーム領域** ウィザードの最後のページで **[仕事 (IPM.Task)]** を選択したとします。 フォーム領域に [ **会社住所** ] フィールドがある場合は、このエラーが表示されます。これは、タスクに勤務先住所がないためです。 そのため、[ **ビジネスアドレス** ] フィールドはメッセージクラスと互換性がありません `IPM.Task` 。

 [ **タスク (IPM.タスク)** 。 **新しいフォーム領域** ウィザードの最後のページにあります。 フォーム領域に [ **会社住所** ] フィールドがある場合は、このエラーが表示されます。これは、タスクに勤務先住所がないためです。 そのため、[ **ビジネスアドレス** ] フィールドはメッセージクラスと互換性がありません `IPM.Task` 。

## <a name="to-correct-this-error"></a>このエラーを解決するには

- **新しいフォーム領域** ウィザードの最後のページで、フォーム領域のフィールドと互換性のあるメッセージ クラスを選択します。

- Outlook のフォームデザイナーで、メッセージクラスと互換性のないフィールドを削除します。 **新しいフォーム領域**ウィザードの最後のページで選択しようとしているフィールドを削除します。

## <a name="see-also"></a>こちらもご覧ください
- [チュートリアル: Outlook でデザインされたフォーム領域をインポートする](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
