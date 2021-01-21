---
title: フォーム領域を Outlook メッセージクラスに関連付ける
description: フォーム領域を各項目のメッセージクラスに関連付けることによって、どの Microsoft Office Outlook アイテムにフォーム領域を表示するかを指定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.InvalidMessageClassName
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FormRegionMessageClassAttribute
- form regions [Office development in Visual Studio], message classes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 213b167bf7fe10c83b028fce2d97c67cd837d272
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/08/2020
ms.locfileid: "96847001"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>フォーム領域を Outlook メッセージクラスに関連付ける
  フォーム領域を各項目のメッセージクラスに関連付けることによって、フォーム領域を表示する Outlook アイテム Microsoft Office を指定できます。 たとえば、メールアイテムの下部にフォーム領域を追加する場合は、フォーム領域を message クラスに関連付けることができ `IPM.Note` ます。

 フォーム領域をメッセージクラスに関連付けるには、 **新しい Outlook フォーム領域** ウィザードでメッセージクラス名を指定するか、フォーム領域ファクトリクラスに属性を適用します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="understand-outlook-message-classes"></a>Outlook メッセージクラスについて
 Outlook メッセージクラスは、Outlook アイテムの種類を識別します。 次の表に、これら8種類の標準の項目とそのメッセージクラス名を示します。

|Outlook アイテムの種類|メッセージクラス名|
|-----------------------|------------------------|
|AppointmentItem|`IPM.Appointment`|
|ContactItem|`IPM.Contact`|
|DistListItem|`IPM.DistList`|
|JournalItem|`IPM.Activity`|
|MailItem|`IPM.Note`|
|PostItem|`IPM.Post` または `IPM.Post.RSS`|
|TaskItem|`IPM.Task`|

 カスタムメッセージクラスの名前を指定することもできます。 カスタムメッセージクラスは、Outlook で定義するカスタムフォームを識別します。

> [!NOTE]
> 置換フォーム領域およびすべて置換フォーム領域では、新しいカスタムメッセージクラス名を指定できます。 既存のカスタムフォームのメッセージクラス名を使用する必要はありません。 カスタムメッセージクラスの名前は一意である必要があります。 名前が一意であることを確認する方法の1つは、次のような名前付け規則を使用すること \<*StandardMessageClassName*> です。 \<*Company*>\<*MessageClassName*> (例: `IPM.Note.Contoso.MyMessageClass` )。

## <a name="associate-a-form-region-with-an-outlook-message-class"></a>フォーム領域を Outlook メッセージクラスに関連付ける
 フォーム領域とメッセージクラスを関連付けるには、次の2つの方法があります。

- **新しい Outlook フォーム領域** ウィザードを使用します。

- クラス属性を適用します。

### <a name="use-the-new-outlook-form-region-wizard"></a>新しい Outlook フォーム領域ウィザードの使用
 **新しい Outlook フォーム領域** ウィザードの最後のページでは、標準のメッセージクラスを選択し、フォーム領域に関連付けるカスタムメッセージクラスの名前を入力できます。

 フォーム領域がフォーム全体またはフォームの既定のページを置き換えるように設計されている場合、標準のメッセージクラスは使用できません。 標準のメッセージクラス名は、フォームに新しいページを追加したり、フォームの下部に追加したりするフォームに対してのみ指定できます。 詳細については、「 [方法: フォーム領域を Outlook アドインプロジェクトに追加](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)する」を参照してください。

 1つ以上のカスタムメッセージクラスを含めるには、[ **このフォーム領域を表示するカスタムメッセージクラス** ] ボックスに名前を入力します。

 入力する名前は、次のガイドラインに準拠している必要があります。

- 完全修飾メッセージクラス名を使用します (例: "IPM.注: Contoso ")。

- 複数のメッセージクラス名を区切るには、セミコロンを使用します。

- "IPM" などの標準の Outlook メッセージクラスは含めないでください。注 "または" IPM.連絡先」にアクセスしてください。 "IPM" などのカスタムメッセージクラスのみを含めます。注: Contoso ".

- 基本メッセージクラスを単独で指定しないでください (例: "IPM")。

- メッセージクラス名ごとに256文字を超えないようにしてください。

  [**完了**] をクリックすると、**新しい Outlook フォーム領域** ウィザードによって入力の形式が検証されます。

> [!NOTE]
> **新しい Outlook フォーム領域** ウィザードでは、指定したメッセージクラス名が正しいか有効であるかは検証されません。

 ウィザードを完了すると、 **新しい Outlook フォーム領域** ウィザードによって、指定したメッセージクラス名を含むフォーム領域クラスに属性が適用されます。 これらの属性は手動で適用することもできます。

### <a name="apply-class-attributes"></a>クラス属性の適用
 **新しい Outlook フォーム領域** ウィザードを完了した後で、フォーム領域を outlook メッセージクラスに関連付けることができます。 これを行うには、フォーム領域ファクトリクラスに属性を適用します。

 次の例は、 <xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute> という名前のフォーム領域ファクトリクラスに適用されている2つの属性を示して `myFormRegion` います。 最初の属性は、フォーム領域をメールメッセージフォームの標準のメッセージクラスに関連付けます。 2番目の属性は、フォーム領域をという名前のカスタムメッセージクラスに関連付け `IPM.Task.Contoso` ます。

 [!code-vb[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb#1)]
 [!code-csharp[Trin_Outlook_FR_Attributes#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs#1)]

 属性は、次のガイドラインに従う必要があります。

- カスタムメッセージクラスの場合は、完全修飾メッセージクラス名を使用します (例: "IPM.注: Contoso ")。

- 基本メッセージクラスを単独で指定しないでください (例: "IPM")。

- メッセージクラス名ごとに256文字を超えないようにしてください。

- フォーム領域がフォーム全体またはフォームの既定のページに置き換わる場合は、標準のメッセージクラスの名前を含めないでください。 標準のメッセージクラス名は、フォームに新しいページを追加したり、フォームの下部に追加したりするフォームに対してのみ指定できます。 詳細については、「 [方法: フォーム領域を Outlook アドインプロジェクトに追加](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)する」を参照してください。

  プロジェクトをビルドすると、Visual Studio によってメッセージクラス名の形式が検証されます。

> [!NOTE]
> Visual Studio では、指定したメッセージクラス名が正しいか、有効であるかは検証されません。

## <a name="see-also"></a>関連項目
- [実行時のフォーム領域へのアクセス](../vsto/accessing-a-form-region-at-run-time.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [Outlook フォーム領域を作成するためのガイドライン](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [フォーム名とメッセージクラスの概要](/office/vba/outlook/Concepts/Forms/form-name-and-message-class-overview)
- [Outlook フォームとアイテムの連携のしくみ](/office/vba/outlook/Concepts/Forms/how-outlook-forms-and-items-work-together)
