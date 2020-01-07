---
title: '方法: エディターでフォントと色を変更する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- editors, fonts
- text, color
- text, customizing in editors
- text, fonts
- editors, text color
ms.assetid: 3f7629d1-1cdf-4046-9a31-0632517f234d
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4eca05b76a55fb45539da7bb15479495b8a3449f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661235"
---
# <a name="how-to-change-fonts-and-colors-in-the-editor"></a>方法 : エディターで使用するフォントのフォント フェイス、サイズ、色を変更する
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

コード エディターでは、さまざまなテキスト**表示項目**の既定のフォント フェイスを変更し、フォント サイズを調整し、前景色と背景色を変更することができます。 フォントの設定を変更するときは、次の情報に注意してください。

- **[フォント]** と **[サイズ]** の設定は、すべての [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] エディターのすべてのテキスト要素に対するグローバルな設定です。

- 固定幅フォントの名前は、太字で表示されます。

- **[前景色]** 、 **[背景色]** 、 **[太字]** の各オプションは、テキスト要素の種類ごとに設定できます。 たとえば、 **[コメント]** と **[ブックマーク]** について色を変更して **[太字]** を選んでも、他の種類のテキスト要素は影響を受けません。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、**ヘルプ**の説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「[Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

### <a name="to-change-the-default-font-face-size-and-colors"></a>既定のフォント フェイス、サイズ、色を変更するには

1. **[ツール]** メニューの **[オプション]** を選び、 **[環境]** フォルダーで **[フォントおよび色]** を選びます。

     [[フォントおよび色] ([オプション] ダイアログ ボックス - [環境])](../../ide/reference/fonts-and-colors-environment-options-dialog-box.md) が開きます。

2. **[設定の表示]** の **[テキスト エディター]** を選びます。

3. **[フォント]** および **[サイズ]** オプションで、すべてのエディター内のすべてのテキスト要素のフォント フェイスとサイズを変更します。

4. **[表示項目]** で適切な項目を選択し、 **[前景色]** および **[背景色]** オプションを変更します。

    > [!TIP]
    > 既定の設定にリセットするには、 **[既定値を使用]** をクリックします。

5. **[OK]** をクリックします。

## <a name="see-also"></a>参照
 [エディターの [テキストエディター] の [](../../ide/customizing-the-editor.md) [オプション] ダイアログボックス](../../ide/reference/text-editor-options-dialog-box.md)のカスタマイズ[コードの記述](../../ide/writing-code-in-the-code-and-text-editor.md)[方法: フォントと色を変更する](../../ide/how-to-change-fonts-and-colors-in-visual-studio.md)
