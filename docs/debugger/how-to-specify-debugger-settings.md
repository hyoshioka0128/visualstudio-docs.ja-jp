---
title: デバッガー設定を指定する | Microsoft Docs
description: 変数の表示方法、表示する警告、ブレークポイントの設定方法など、Visual Studio でのデバッガー動作のさまざまな設定を指定します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debug builds, debugger settings
- debugger, setting options
- debugging [Visual Studio], debugger settings
- options, debugging
ms.assetid: ea172841-7fef-47bf-bd02-e7da4c3c7109
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5034fe887ba221106055a928e67e11076167286
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98150770"
---
# <a name="how-to-specify-debugger-settings"></a>方法: デバッガー設定を指定する
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] では、変数の表示方法、特定の警告を表示するかどうか、ブレークポイントの設定方法、実行中のプログラムを中断した場合の影響など、デバッガーの動作のさまざまな設定を指定できます。 デバッガーの設定は **[オプション]** ダイアログ ボックスで指定します。

### <a name="to-set-debugger-options"></a>デバッガー オプションを設定するには

1. **[ツール]** メニューの **[オプション]** をクリックします。

2. **[オプション]** ダイアログ ボックスで、 **[デバッグ]** フォルダーを開きます。

3. **[デバッグ]** フォルダーで、目的のオプションのカテゴリをクリックします。

     最も一般的なオプションは、 **[全般]** カテゴリに配置されています。 詳細については、「 [General, Debugging, Options Dialog Box](../debugger/general-debugging-options-dialog-box.md)」を参照してください。

4. 目的のオプションをオンまたはオフにします。 F1 キーを押すとオプションについてのヘルプが表示されます。

## <a name="see-also"></a>関連項目
- [[全般] ([オプション] ダイアログ ボックス - [デバッグ])](../debugger/general-debugging-options-dialog-box.md)
- [[エディット コンティニュ] ([オプション] ダイアログ ボックス - [デバッグ])](./edit-and-continue.md)
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)
- [ビルドのコマンドとプロパティの共通マクロ](/cpp/build/reference/common-macros-for-build-commands-and-properties)