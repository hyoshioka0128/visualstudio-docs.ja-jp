---
title: Office Excel キーボード、[設定]、[オプション] ダイアログボックス
description: '[動的キーボードスキーム] を選択して、ドキュメントにフォーカスがあるときに Microsoft Excel がショートカットキーコマンドを受け取る方法について説明します。'
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ExcelOptions.KeyboardMappingScheme
- VS.ToolsOptionsPages.Microsoft_Office_Keyboard_Settings.Microsoft_Office_Excel_Keyboard
- VS.ToolsOptionsPages.Microsoft_Office_Tools.Microsoft_Office_Excel.Keyboard
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- keyboard shortcuts, Office development in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b3422cb53fb454b3585e0b8ba936ce692dfc68a4
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97525314"
---
# <a name="microsoft-office-excel-keyboard-settings-options-dialog-box"></a>Microsoft Office Excel キーボード、[設定]、[オプション] ダイアログボックス
  Microsoft Office Excel と Visual Studio の両方で、ショートカットキーが処理されます。 同じショートカットキーの組み合わせは、Excel や Visual Studio のさまざまなコマンドに使用できます。 Excel が Visual Studio のドキュメントレベルのプロジェクトで開かれている場合、一度に1つのアプリケーションだけがショートカットキーコマンドを受け取ります。 既定では、Visual Studio はすべてのショートカットキーコマンドを受け取りますが、[ **動的キーボードスキーム**] を選択して、ドキュメントにフォーカスがあるときに Excel を受け取るようにすることができます。

 現在ショートカットキーを処理しているアプリケーションのコマンドに割り当てられていないショートカットキーを使用すると、ショートカットキーが他のアプリケーションに渡されます。

 選択したオプションは、Excel プロジェクトが変更されるまで有効なままになります。 選択内容は Microsoft Office Word プロジェクトには影響しません。word の Microsoft Office Word のキーボードオプションを使用して、すべての変更を行う必要があります。

## <a name="uielement-list"></a>UIElement の一覧
 **Visual Studio キーボードスキーム** Excel にフォーカスがある場合でも、Visual Studio はすべてのショートカットキーコマンドを受け取ります。 たとえば、Excel にフォーカスがあるときにファンクションキー **F5** キーを押すと、Visual Studio によってソリューションのデバッグが開始されます。

 **動的キーボードスキーム** Visual Studio は、フォーカスがあるときにのみショートカットキーコマンドを受け取ります。 Excel にフォーカスがある場合、Excel はすべてのショートカットキーコマンドを受け取ります。 たとえば、Excel にフォーカスがあるときにファンクションキー **F5** キーを押すと、[ **ジャンプ** ] ダイアログボックスが表示されます。 Visual Studio にフォーカスがあるときに **F5** キーを押すと、ソリューションのデバッグが開始されます。

## <a name="see-also"></a>関連項目
- [Microsoft Office Word キーボード、Microsoft Office キーボード設定、[オプション] ダイアログボックス](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)
