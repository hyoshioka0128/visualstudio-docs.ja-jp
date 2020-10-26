---
title: エディターのフォントと色を変更する
ms.date: 06/01/2020
ms.topic: how-to
helpviewer_keywords:
- editors, fonts
- text, color
- text, customizing in editors
- text, fonts
- editors, text color
ms.assetid: 3f7629d1-1cdf-4046-9a31-0632517f234d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa56a7ab8b3147cc3e8fbb784211d9a34536189d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85770420"
---
# <a name="how-to-change-fonts-and-colors-for-the-editor-in-visual-studio"></a>方法: Visual Studio でエディターのフォントと色を変更する

コード エディターでは、さまざまなテキスト**表示項目**に対して既定のフォント フェイスを変更したり、フォント サイズを調整したり、前景色と背景色を変更したりできます。 フォントの設定を変更するときは、次のことにご注意ください。

- **[フォント]** と **[サイズ]** の設定は、すべての Visual Studio エディターのすべてのテキスト要素に対するグローバルな設定です。

- 固定幅フォントの名前は、太字で表示されます。

- **[前景色]** 、 **[背景色]** 、 **[太字]** の各オプションは、テキスト要素の種類ごとに設定できます。 たとえば、 **[コメント]** と **[ブックマーク]** について色を変更して **[太字]** を選んでも、他の種類のテキスト要素は影響を受けません。

> [!IMPORTANT]
> コード エディターだけでなく、IDE のフォントと色をカスタマイズする方法については、「 **[方法:Visual Studio で使用するフォントと色を変更する](../../ide/how-to-change-fonts-and-colors-in-visual-studio.md)** 」のページを参照してください。

## <a name="change-the-default-font-face-size-and-colors"></a>既定のフォント フェイス、サイズ、色を変更する

1. **[ツール]** メニューの **[オプション]** を選択します。 **[環境]** で、 **[フォントおよび色]** を選択します。

1. **[設定の表示]** の **[テキスト エディター]** を選びます。

   ![エディター内のフォントと色を変更するための [オプション] ダイアログ ボックスのスクリーンショット](../../ide/media/fonts-colors-text-editor.png "エディター内のフォントと色を変更するための [オプション] ダイアログ ボックスのスクリーンショット")

1. **[フォント]** および **[サイズ]** オプションで、すべてのエディター内のすべてのテキスト要素のフォント フェイスとサイズを変更します。

1. **[表示項目]** で適切な項目を選択し、 **[前景色]** および **[背景色]** オプションを変更します。

    > [!TIP]
    > 既定の設定にリセットするには、 **[既定値を使用]** をクリックします。

1. **[OK]** をクリックします。

## <a name="next-steps"></a>次の手順

**[オプション]** ダイアログ ボックスを使用して IDE に対して行うことができるフォントおよび色の変更の詳細については、「[[フォントおよび色] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/fonts-and-colors-environment-options-dialog-box.md)」のページを参照してください。

## <a name="see-also"></a>関連項目

- [コード エディターの機能](../../ide/writing-code-in-the-code-and-text-editor.md)
- [方法: Visual Studio で使用するフォントと色を変更する](../../ide/how-to-change-fonts-and-colors-in-visual-studio.md)
