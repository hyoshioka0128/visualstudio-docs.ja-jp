---
title: '[オプション]、[テキスト エディター]、[U-SQL]、[IntelliSense]'
ms.date: 01/17/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.U-SQL.IntelliSense
- VS.ToolsOptionsPages.Text_Editor.HQL.IntelliSense
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91d2af8bfcd8c9d80b589e01aedd535afbd1a913
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85769466"
---
# <a name="options-text-editor-u-sql-intellisense"></a>[オプション]、[テキスト エディター]、[U-SQL]、[IntelliSense]

**[IntelliSense]** オプション ページを使用して、テキスト エディターでの U-SQL 用のいくつかの設定を変更します。 このオプション ページにアクセスするには、 **[ツール]**  >  **[オプション]** を選択し、さらに **[テキスト エディター]**  >  **[U-SQL]**  >  **[IntelliSense]** の順に選択します。

## <a name="intellisense-settings"></a>IntelliSense 設定

チェック ボックスをオンにして、 **[クイック ヒント]** または **[Intellisense]** を有効にします。 クイック ヒントでは、変数の上にマウス カーソルを合わせるとその宣言全体が表示されます。

## <a name="completion-lists"></a>入力候補一覧

- **文字が入力された後に入力候補一覧を表示する**

   このオプションを選択すると、入力を開始したときに IntelliSense によって入力候補一覧が自動的に表示されます。 このオプションを選択しない場合でも、IntelliSense の入力候補は、[IntelliSense] メニューから、または **Ctrl** + **Space** キーを押すことで使用できます。

- **入力候補一覧にキーワードを配置する**

   このオプションを選択すると、IntelliSense によってキーワードが入力候補一覧に追加されます。

- **入力候補一覧にコード スニペットを配置する**

   このオプションを選択すると、IntelliSense によってコード スニペットが入力候補一覧に追加されます。

## <a name="selection-in-completion-list"></a>入力候補一覧からの選択

- **次の文字を入力してコミットする**

   このフィールドでは、現在強調表示されている入力候補一覧の提案をコミットする文字が表示されます。 この一覧の文字を追加または削除できます。

- **Space キーを押してコミットする**

   このオプションを選択した場合、Space キーを押すことで強調表示されている入力候補一覧の提案をコミットできます。

- **単語を完全に入力した後に Enter キーを押したら改行する**

   選択した場合、入力候補一覧の提案のすべての文字を入力すると、新しい行が自動的に追加されて、新しい行にカーソルが移動します。

## <a name="see-also"></a>参照

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
- [IntelliSense の使用](../../ide/using-intellisense.md)