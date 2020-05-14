---
title: '方法 : エディターのワード ラップを管理する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- word wrap
- editors, text viewing
- Code Editor, word wrap
ms.assetid: 442f33ef-9f52-4515-b55f-fb816d664645
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 59cc8536707744543490bc3e91b85545e4cd4007
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668853"
---
# <a name="how-to-manage-word-wrap-in-the-editor"></a>方法 : エディターのワード ラップを管理する
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[右端で折り返す]** オプションを設定および解除できます。 このオプションを設定すると、コード エディター ウィンドウの現在の幅からはみ出した長い行の部分は次の行に表示されます。 たとえば行番号の使用を容易にするためにこのオプションをオフにすると、右にスクロールして長い行の末尾を表示できます。

 詳しくは、「[方法: 一般エディター オプションを設定する](https://msdn.microsoft.com/704e4a7b-2162-4bed-8a47-f4f6ffec98c2)」をご覧ください。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、**ヘルプ**の説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

## <a name="procedure"></a>プロシージャ

#### <a name="to-set-word-wrap-preferences"></a>ワード ラップ オプションを設定するには

1. **[ツール]** メニューの **[オプション]** を選択します。

2. **[テキスト エディター]** フォルダーで、 **[すべての言語]** サブフォルダーの **[全般]** オプションを選択して、このオプションをグローバルに設定します。

     または

     プログラミングしている言語のサブフォルダーの **[全般]** オプションを選択します。

3. **[設定]** で、 **[右端で折り返す]** オプションをオンまたはオフにします。

     **[右端で折り返す]** オプションをオンにすると、 **[右端の折り返しの記号を表示する]** オプションが有効になります。

4. 長い行が 2 行目に折り返される場合に改行インジケーターを表示するには、 **[折り返しの記号を表示する]** オプションをオンにします。 このオプションをオフにすると、インジケーターは表示されません。

    > [!NOTE]
    > 改行インジケーターはコードには追加されません。表示専用です。

## <a name="see-also"></a>参照
 [エディターの [テキストエディター] の [](../../ide/customizing-the-editor.md) [オプション] ダイアログボックス](../../ide/reference/text-editor-options-dialog-box.md)のカスタマイズ[コードの記述](../../ide/writing-code-in-the-code-and-text-editor.md)
