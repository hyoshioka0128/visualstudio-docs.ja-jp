---
title: Office プロジェクトのユーザー補助機能
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, accessibility
- shortcut keys [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], shortcut keys
- accessibility [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8bd74f4d61c74a4dc348f7a615e103b283a15fc0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "73189624"
---
# <a name="accessibility-in-office-projects"></a>Office プロジェクトのユーザー補助機能

Microsoft Visual Studio と Microsoft Office には、標準的なアクセシビリティ要件を満たすカスタムソリューションを構築するためのユーザー補助機能が多数含まれています。 Microsoft では、Web 上のアクセシビリティに関するガイドラインを公開しています。 詳細については、 [アクセシビリティ web サイト](https://www.microsoft.com/accessibility/)を参照してください。

ほとんどの場合、Visual Studio の Office プロジェクトはアクセシビリティ標準を満たしているか、ソリューションにアクセスできるように設定できるプロパティを公開します。 ただし、アクセシビリティが制限されている機能がいくつかあります。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="accessibility-at-design-time"></a>デザイン時のアクセシビリティ

### <a name="use-shortcut-keys-in-document-level-projects"></a>ドキュメントレベルのプロジェクトでショートカットキーを使用する
 Visual Studio で Microsoft Office Word 文書または Microsoft Office Excel ブックが開いている場合、ショートカットキーコマンドを受け取るアプリケーションは一度に1つだけです。 既定では、Visual Studio はすべてのショートカットキーコマンドを受け取りますが、[**オプション**] ダイアログボックスの [**キーボード設定**] ページで [**動的キーボードスキーム**] を選択して、ドキュメントにフォーカスがあるときに Word または Excel を受け取るようにすることができます。 詳細については、「Microsoft Office Word のキーボード」、「Microsoft Office キーボードの設定」、「[ [オプション] ダイアログボックス](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md) 」、Microsoft Office および「[ [Microsoft Office キーボードの設定] ([オプション] ダイアログボックス](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md))」を参照してください。

### <a name="display-shortcut-keys-for-the-ribbon-in-document-level-projects"></a>ドキュメントレベルのプロジェクトでリボンのショートカットキーを表示する
 Word 文書または Excel ブックが Visual Studio で開かれている場合は、 **Alt** キーを押して、リボン上のタブとコントロールのショートカットキーを表示することはできません。 デザイナーで文書またはブックを開いているときにショートカットキーを表示するには、次の手順を実行します。

#### <a name="to-view-shortcut-keys-for-ribbon-tabs-and-controls-in-the-designer"></a>デザイナーのリボンタブおよびコントロールのショートカットキーを表示するには

1. Visual Studio で、[ **ツール** ] メニューの [ **オプション**] をクリックします。

2. [ **Office ツール** ] ノードを展開し、必要に応じて [ **Microsoft Office Excel キーボード** ] または [ **Microsoft Office Word キーボード**] を選択します。

3. [ **動的キーボードスキーム**] を選択します。

     変更を有効にするために Visual Studio を再起動する必要があることを示すメッセージが表示されます。

4. **[OK]** をクリックします。

5. Visual Studio を再起動し、プロジェクトを再度開きます。

6. プロジェクトのドキュメントデザイナーまたはブックデザイナーを開きます。

7. **F6**キーを押して、リボンのショートカットキーを表示します。

## <a name="accessibility-at-run-time"></a>実行時のアクセシビリティ

### <a name="windows-forms-controls-on-office-documents"></a>Office ドキュメントのコントロールの Windows フォーム
 Windows フォームコントロールは、スクリーンリーダーなどのユーザー補助機能にコントロールに関する情報を提供するアクセシビリティプロパティを公開します。 ドキュメントレベルのカスタマイズで Office ドキュメントにコントロールがある場合は、これらのアクセシビリティプロパティを利用できます。 詳細については、「 [Windows フォーム上のコントロールのユーザー補助情報の提供](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)」を参照してください。

 ただし、Windows フォームコントロールが Excel ブックまたは Word 文書でホストされている場合、実行時にユーザー補助の制限がいくつかあります。

- 1つのコントロールから別のコントロールにタブを作成することはできません。

- ドキュメントのズーム設定を100% 以外のものに変更すると、ドキュメントのコントロールは無効になります。

  ドキュメントの Windows フォームコントロールの制限事項については、「 [Office ドキュメントの Windows フォームコントロールの制限事項](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)」を参照してください。

### <a name="actions-panes-and-custom-task-panes"></a>操作ウィンドウとカスタム作業ウィンドウ
 操作ウィンドウまたはカスタム作業ウィンドウにフォーカスがある場合は、Windows フォームアプリケーション上のコントロールにアクセスするのと同じ方法でコントロールにアクセスします。 操作ウィンドウとドキュメントの間でカーソルを移動するには、 **F6**キーを押します。

 操作ウィンドウとカスタム作業ウィンドウの詳細については、「 [操作ウィンドウの概要](../vsto/actions-pane-overview.md) 」および「 [カスタム作業](../vsto/custom-task-panes.md)ウィンドウ」を参照してください。

### <a name="display-modes"></a>表示モード

Visual Studio には、表示モードに関連する次の制限事項があります。

- Word 文書または Excel ワークシートのコントロールは、ドキュメントのズーム設定を100% 以外のものに変更すると無効になります。

- ユーザーが**ハイコントラストを使用**するようにコンピューターのユーザー補助オプションを変更した場合、[**新しいプロジェクト**] ダイアログボックスにコントロールが正しく表示されません。

拡大鏡を使用すると、これらの制限を克服できます。 拡大鏡は、ウィンドウの表示ユーティリティで、画面の拡大部分を表示するウィンドウを別に作成します。

## <a name="see-also"></a>関連項目

- [Office ソリューションの開発](../vsto/developing-office-solutions.md)
- [Office ドキュメントのコントロール](../vsto/controls-on-office-documents.md)
- [障碍のある方のためのユーザー補助機能](../ide/reference/accessibility-features-of-visual-studio.md)
- [Visual Studio のユーザー補助機能](../ide/reference/accessibility-features-of-visual-studio.md)