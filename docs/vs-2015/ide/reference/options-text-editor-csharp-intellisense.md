---
title: '[オプション]、[テキスト エディター]、[C#]、[IntelliSense] | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Intellisense
- VS.ToolsOptionsPages.Text_Editor.Visual_JSharp.Intellisense
helpviewer_keywords:
- IntelliSense [J#], options
- underlines, wavy
- IntelliSense [C#], options
- IntelliSense [C#], wavy underlines
- wavy underlines
- Text Editor Options dialog box, IntelliSense
ms.assetid: 3466dedb-e5f4-424c-8dd8-e4941b2f4fc2
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1e3f4df9a7a885245e40f7e9fec1b0da207ada39
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662294"
---
# <a name="options-text-editor-c-intellisense"></a>[オプション]、[テキスト エディター]、[C#]、[IntelliSense]
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual C# での IntelliSense の動作設定を変更するには、 **[IntelliSense]** プロパティ ページを使用します。 **[IntelliSense]** プロパティ ページにアクセスするには、 **[ツール]** メニューの **[オプション]** をクリックして、 **[テキスト エディター]** フォルダーで **[C#]** をクリックし、 **[IntelliSense]** をクリックします。

> [!NOTE]
> 実際に画面に表示されるダイアログ ボックスとメニュー コマンドは、アクティブな設定またはエディションによっては、ヘルプの説明と異なる場合があります。 設定を変更するには、 **[ツール]** メニューの **[設定のインポートとエクスポート]** をクリックします。 詳細については、「 [Visual Studio での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)」を参照してください。

 **[IntelliSense]** プロパティ ページには、以下のプロパティがあります。

## <a name="completion-lists"></a>入力候補一覧
 **文字が入力された後に入力候補一覧を表示する**このオプションを選択すると、入力を開始したときに、IntelliSense によって入力候補一覧が自動的に表示されます。 このオプションを選択しない場合でも、IntelliSense の入力候補は **[IntelliSense]** メニューから、または CTRL キーを押しながら SPACE キーを押して使用できます。

 **入力候補一覧にキーワードを配置**するこのオプションを選択すると、IntelliSense C#によって、[クラス](https://msdn.microsoft.com/library/b95d8815-de18-4c3f-a8cc-a0a53bdf8690)などのキーワードがコンプリートリストに追加されます。

 **入力候補一覧にコードスニペットを配置**するこのオプションを選択すると、IntelliSense によっC#て、コードスニペットのエイリアスが入力候補一覧に追加されます。 コード スニペットのエイリアスがキーワードと同じ場合 ([class](https://msdn.microsoft.com/library/b95d8815-de18-4c3f-a8cc-a0a53bdf8690) など)、キーワードは、ショートカットで置き換えられます。 詳細については、「[Visual C# のコード スニペット](../../ide/visual-csharp-code-snippets.md)」を参照してください。

## <a name="selection-in-completion-lists"></a>入力候補一覧からの選択
 **次の文字を入力することでコミットされます。** 入力した後、入力候補一覧で選択された項目に対して IntelliSense のオートコンプリートを実行するすべての文字を指定します。

 **スペースバーを押してコミット**入力候補一覧で選択された項目に対して IntelliSense のオートコンプリートを実行するために、スペースバーを押す操作を含めるように指定します。

 **完全に入力された単語の末尾にある enter キーで新しい行を追加します**入力候補一覧のエントリのすべての文字を入力し、enter キーを押すと、新しい行が自動的に作成され、カーソルが新しい行に移動することを指定します。

 たとえば、`else` を入力し、ENTER キーを押すと、エディターには次のように表示されます。

 `else`

 `|` (カーソルの位置)

 ただし、`el` のみを入力して ENTER キーを押すと、エディターには次のように表示されます。

 `else|` (カーソルの位置)

## <a name="intellisense-member-selection"></a>IntelliSense メンバーの選択
 **直前に使用されたメンバーを事前選択**しますこのオプションを選択すると、統合開発環境 (IDE) の現在のセッション中に、オブジェクト名の自動補完のためにポップアップリストメンバーボックスで最近選択したメンバーが、IntelliSense によって事前に選択されます。 最近使用したメンバーの履歴は、IDE の各セッションの間に消去されます。 詳細については、「[最近使用されたメンバーに対する IntelliSense](../../misc/intellisense-for-most-recently-used-members.md)」を参照してください。

## <a name="see-also"></a>関連項目
 [[全般] ([オプション] ダイアログボックス](../../ide/reference/general-environment-options-dialog-box.md)- [IntelliSense を使用し](../../ide/using-intellisense.md)た[XML ドキュメントコメント](https://msdn.microsoft.com/library/803b7f7b-7428-4725-b5db-9a6cff273199))
