---
title: '[オプション]、[テキスト エディター]、[C#]、[IntelliSense]'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Intellisense
helpviewer_keywords:
- underlines, wavy
- IntelliSense [C#], options
- IntelliSense [C#], wavy underlines
- wavy underlines
- Text Editor Options dialog box, IntelliSense
ms.assetid: 3466dedb-e5f4-424c-8dd8-e4941b2f4fc2
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 87a167a75f3b06522da77d562b0137df89757975
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75596217"
---
# <a name="options-text-editor-c-intellisense"></a>[オプション]、[テキスト エディター]、[C#]、[IntelliSense]

C# での IntelliSense の動作設定を変更するには、 **[IntelliSense]** オプション ページを使用します。 このオプション ページにアクセスするには、 **[ツール]**  >  **[オプション]** を選択し、さらに **[テキスト エディター]**  >  **[C#]**  >  **[IntelliSense]** の順に選択します。

**[IntelliSense]** オプション ページには、以下のオプションがあります。

## <a name="completion-lists"></a>入力候補一覧

- 文字が入力された後に入力候補一覧を表示する*

   このオプションを選択すると、入力を開始したときに IntelliSense によって入力候補一覧が自動的に表示されます。 このオプションを選択しない場合でも、IntelliSense の入力候補は **[IntelliSense]** メニューから、または **Ctrl**+**Space** キーを押して、使うことができます。

- 文字が削除された後に入力候補一覧を表示する

- 入力候補一覧の項目の一致している部分を強調表示する

- 入力候補の項目フィルターを表示する

## <a name="snippets-behavior"></a>スニペットの動作

- スニペットを含めない

   このオプションをオンにすると、IntelliSense は C# コード スニペットのエイリアスを入力候補一覧に追加しません。

- 常にスニペットを含める

   このオプションを選択すると、IntelliSense によって C# コード スニペットのエイリアスが入力候補一覧に追加されます。 コード スニペットのエイリアスがキーワードと同じ場合 ([class](/dotnet/csharp/language-reference/keywords/class) など)、キーワードは、ショートカットで置き換えられます。 詳細については、「[C# Code Snippets](../../ide/visual-csharp-code-snippets.md)」を参照してください。

- 識別子の後に ? Tab を入力したときにスニペットを含める

   このオプションをオンにした場合、識別子の後で **?** +**Tab** キーを押すと、IntelliSense によって C# コード スニペットのエイリアスが入力候補一覧に追加されます。

## <a name="enter-key-behavior"></a>Enter キー入力時動作

- Enter キーで新しい行を追加しない

   入力候補一覧で項目を選んで **Enter** キーを押した後、新しい行が自動的に追加されないようにすることを指定します。

- 単語を完全に入力した後 Enter キーで新しい行のみを追加する

   入力候補一覧内のエントリのすべての文字を入力して **Enter** キーを押すと、新しい行が自動的に追加されて、新しい行にカーソルが移動することを指定します。

   たとえば、「`else`」と入力し、**Enter** キーを押すと、エディターには次のように表示されます。

   `else`

   `|` (カーソルの位置)

   一方、「`el`」のみを入力して **Enter** キーを押すと、エディターには次のように表示されます。

   `else|` (カーソルの位置)

- Enter キーで常に新しい行を追加する

   入力候補一覧内のエントリの "*いずれかの*" 文字を入力して **Enter** キーを押すと、新しい行が自動的に追加されて、新しい行にカーソルが移動することを指定します。

## <a name="show-name-suggestions"></a>名前の提案を表示

最近選択したメンバーのオブジェクト名の自動補完を実行します。

## <a name="see-also"></a>参照

- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
- [IntelliSense の使用](../../ide/using-intellisense.md)
