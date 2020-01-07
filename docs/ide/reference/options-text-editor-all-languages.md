---
title: '[オプション]、[テキスト エディター]、[すべての言語]'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.JavaScript.General
- VS.ToolsOptionsPages.Text_Editor.ResJSON.General
- VS.ToolsOptionsPages.Text_Editor.All_Languages.General
- VS.ToolsOptionsPages.Text_Editor.Basic.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.General
- VS.ToolsOptionsPages.Text_Editor.C/C++.General
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.General
- VS.ToolsOptionsPages.Text_Editor.CSS.General
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.General
- VS.ToolsOptionsPages.Text_Editor.F#.General
- VS.ToolsOptionsPages.Text_Editor.Fsharp.General
- VS.ToolsOptionsPages.Text_Editor.HQL.General
- VS.ToolsOptionsPages.Text_Editor.HTML.General
- VS.ToolsOptionsPages.Text_Editor.HTML_(Web_Forms).General
- VS.ToolsOptionsPages.Text_Editor.JavaScript.General
- VS.ToolsOptionsPages.Text_Editor.TypeScript.General
- VS.ToolsOptionsPages.Text_Editor.JSON.General
- VS.ToolsOptionsPages.Text_Editor.LESS.General
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.General
- VS.ToolsOptionsPages.Text_Editor.SCSS.General
- VS.TOOLSOPTIONSPAGES.TEXT_EDITOR.SQL_SERVER_TOOLS.GENERAL
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.General
- VS.ToolsOptionsPages.Text_Editor.U-SQL.General
- VS.ToolsOptionsPages.Text_Editor.XAML.General
- VS.ToolsOptionsPages.Text_Editor.XML.General
helpviewer_keywords:
- Text Editor Options dialog box
- statement completion
- word wrap
- General dialog box
- line numbers
- virtual space
ms.assetid: 49ee7306-9d46-4170-850f-a1716171752d
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 22ab23911baab30c7617525d318795b1be708bb9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747851"
---
# <a name="options-dialog-box-text-editor--all-languages"></a>[オプション] ダイアログ ボックス:[テキスト エディター] \> [すべての言語]

このダイアログ ボックスでは、コード エディターの既定の動作を変更できます。 設定は、HTML デザイナーのソース ビューなど、コード エディターに基づいて他のエディターにも適用されます。 このダイアログ ボックスを開くには、 **[ツール]** メニューから **[オプション]** を選択します。 **[テキスト エディター]** フォルダー内で **[すべての言語]** サブフォルダーを展開し、 **[全般]** を選択します。

> [!CAUTION]
> このページから、すべての開発言語の既定のオプションが設定されます。 このダイアログでオプションをリセットすると、すべての言語の全般オプションがここで選択されているものにリセットされます。 1 つだけの言語のテキスト エディター オプションを変更にするには、その言語のサブフォルダーを展開し、そのオプション ページを選択します。

全般オプション ページでオプションを選択すると、一部のプログラミング言語で灰色のチェックマークが表示されることがあります。

## <a name="statement-completion"></a>[入力候補]

**自動メンバー表示**

選択すると、エディターに文字を入力すると同時に、利用可能なメンバー、プロパティ、値、メソッドのポップアップ リストが IntelliSense により表示されます。 任意の項目をポップアップ リストから選択し、コードに挿入します。 このオプションを選択すると、 **[メンバーの詳細を非表示]** オプションが有効になります。

**メンバーの詳細を非表示**

選択すると、ステートメント入力候補のポップアップ リストが短くなり、よく使用する項目だけが表示されます。 その他の項目は、リストに表示されません。

**パラメーター ヒント**

選択すると、現在の宣言またはプロシージャの完全な構文と指定可能な全パラメーターがエディター内のカーソル位置の下に表示されます。 次に割り当て可能なパラメーターは、太字で表示されます。

## <a name="settings"></a>設定

**仮想空白を使用**

このオプションがオンで、 **[右端で折り返す]** がオフの場合、コード エディターの行末を越える任意の場所をクリックしてコメントを入力できます。 この機能を使用すると、コードの横の一貫した位置にコメントを配置できます。

**右端で折り返す**

選択すると、表示可能な編集領域を超える行部分 (水平方向) が自動的に次の行に表示されます。 このオプションをオンにすると、 **[右端の折り返しの記号を表示する]** オプションが有効になります。

> [!NOTE]
> **[仮想空白]** 機能は、 **[右端で折り返す]** がオンになっているときはオフになります。

**右端の折り返しの記号を表示する**

選択すると、長い行を折り返したとき、その位置に折り返し矢印インジケーターが表示されます。

![LineBreakSymbol スクリーンショット](../../ide/reference/media/linebreak.gif)

インジケーターを表示しない場合、このオプションをオフにします。

> [!NOTE]
> このような注意を促すための矢印は、コードに追加されたり、印刷されたりすることはありません。 これらは参照専用です。

**行番号**

選択すると、行番号が各コード行の隣に表示されます。

> [!NOTE]
> 行番号がコードに追加されたり、印刷されたりすることはありません。 これらは参照専用です。

**シングル クリックでの URL ナビゲーションを有効にする**

選択すると、エディターの URL にマウス カーソルを置いたときに、マウス カーソルが手の形に変わります。 URL をクリックすると、示されているページが Web ブラウザーに表示されます。

**ナビゲーション バー**

選択すると、コード エディターの上部に**ナビゲーション バー**が表示されます。 そのドロップダウンの **[オブジェクト]** 一覧と **[メンバー]** 一覧では、コードの特定のオブジェクトを選択したり、そのメンバーから選択したり、コード エディターで選択したメンバーの宣言に移動したりできます。

**選択領域がない場合は、切り取りまたはコピー コマンドを空白行に適用する**

このオプションは、空白行に挿入ポインターを置き、何も選択せずにコピーまたは切り取り操作を行った場合のエディターの動作を設定します。

- このオプションを選択した場合、空白行がコピーされるか切り取られます。 その後に貼り付けを行うと、新しい空白行が挿入されます。

- このオプションが選択されていないとき、[切り取り] コマンドを使用すると、空白行が削除されます。 ただし、クリップボードのデータは保持されます。 そのため、その後に貼り付けコマンドを実行すると、最後にクリップボードにコピーされた内容が貼り付けられます。 前にコピーされた内容がない場合、貼り付けは行われません。

この設定は、行が空白でない場合には、コピーや切り取りに何の影響も与えません。 何も選択されていない場合は、行全体のコピーまたは切り取りが行われます。 その後に貼り付けを行うと、行全体のテキストとその行末文字の貼り付けが行われます。

> [!TIP]
> 空白、タブ、および行末のインジケーターを表示し、インデントの設定された行と、空白行とを区別できるようにするには、 **[編集]** メニューの **[詳細]** をクリックし、 **[スペースの表示]** を選択します。

## <a name="see-also"></a>関連項目

- [[オプション]、[テキスト エディター]、[すべての言語]、[タブ]](../../ide/reference/options-text-editor-all-languages-tabs.md)
- [[全般]、[環境]、[オプション] ダイアログ ボックス](../../ide/reference/general-environment-options-dialog-box.md)
- [IntelliSense の使用](../../ide/using-intellisense.md)
