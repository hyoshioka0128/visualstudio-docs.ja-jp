---
title: JavaScript IntelliSense の拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- JavaScript, intellisense object
- extending JavaScript IntelliSense
- customizing JavaScript IntelliSense
- JavaScript, extending IntelliSense
- IntelliSense [JavaScript], extending
ms.assetid: 004e1ab6-bd7a-4327-9e01-89b9be96ba2f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bf16b6fdc307e11875f30cfad6e4bb35580b0b04
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665753"
---
# <a name="extending-javascript-intellisense"></a>JavaScript IntelliSense の拡張
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

JavaScript IntelliSense の機能拡張機能を使用すると、サードパーティのライブラリの JavaScript エディターで IntelliSense の結果をカスタマイズできます。 これにより、これらのライブラリを使用する開発者のエクスペリエンスが向上します。

 JavaScript 言語サービスは、プロジェクトに追加されるサードパーティ製の JavaScript ライブラリに IntelliSense 機能を提供します。 ほとんどのライブラリでは、言語サービスによってステートメント入力候補が自動的に提供されます。 次の図は、ステートメント入力候補の例を示しています。

 ![ステートメント入力候補の例](../ide/media/js-intellisense-completion.png "js_intellisense_completion")

 ライブラリに、標準的な JavaScript コメントタグ (//) の変数、関数、およびオブジェクトの説明が含まれている場合、既定では IntelliSense 機能拡張機能によって自動的に恩恵を受けることができます。これにより、入力候補一覧の要素の右側に表示されるか、関数呼び出しに左かっこを入力したときに表示されます。 ポップアップボックスのコメントには、メンバーの説明が含まれています。 次の例は、入力候補一覧のポップアップボックスを示しています。

 ![クイックヒントポップアップ&#45;ボックスの例](../ide/media/js-intellisense-quickinfo.png "js_intellisense_quickinfo")

 開発者のエクスペリエンスをさらに向上させるために、ポップアップボックスで開発者に型情報を提供することが必要になる場合があります。 標準のコメントタグの代わりに JavaScript [XML ドキュメントのコメント](../ide/xml-documentation-comments-javascript.md)を使用して、型情報を指定できます。 XML ドキュメントコメントを追加するには、トリプルスラッシュコメントタグ (///) と XML 要素の定義済みセットを使用します。

 または、JavaScript IntelliSense の機能拡張を使用して型情報を指定することもできます。 この機能を使用すると、JavaScript 拡張を作成してスクリプトコンテキストに追加することで、IntelliSense の結果をカスタマイズできます。 JavaScript ファイルである拡張機能では、言語サービスの `intellisense` オブジェクトによって公開されるイベントをサブスクライブします。 JavaScript IntelliSense の拡張機能は、ライブラリの動作パターンによって JavaScript 言語サービスが必要なレベルの IntelliSense サポートを提供できない場合、また宣言型 XML の代わりに使用できる場合に推奨されるソリューションです。ドキュメントコメントも必要です。 IntelliSense の結果をカスタマイズすることで、言語サービスの既定の機能を制限する可能性のある動作パターンに関係なく、最初のクラスの IntelliSense を作成できます。 詳細については、「[Statement Completion for Identifiers (識別子の入力候補)](../ide/statement-completion-for-identifiers.md)」をご覧ください。

## <a name="adding-an-extension-to-the-script-context"></a>スクリプトコンテキストへの拡張機能の追加
 IntelliSense 拡張を実行するには、現在のスクリプトコンテキストに追加する必要があります。 拡張機能は自動検出メカニズムによってスクリプトコンテキストに自動的に追加されます。また、参照グループまたは参照ディレクティブを使用して、手動でスクリプトコンテキストに拡張機能を追加することもできます。

 自動検出メカニズムを使用すると、言語サービスは、ファイル*の名前付け規則に*従った拡張子を自動的に検索できます。拡張子は、拡張子が付いているライブラリと同じディレクトリに配置されます。当て. たとえば、jQuery ライブラリの有効な拡張子は jQuery. js です。 より制限の厳しい jQuery 拡張機能については、jQuery-1.7.1 (バージョン固有の拡張機能) や jQuery. ui. node.js (スコープ付き jQuery ライブラリの拡張機能) などのファイル名を使用できます。 特定のライブラリの拡張機能が複数見つかった場合は、最も制限の厳しいバージョンが使用されます。

 すべての JavaScript プロジェクトファイルに拡張機能を使用する場合は、その拡張機能を参照グループに追加することを選択できます。 参照グループにはいくつかの種類があり、暗黙的な参照を含むものと、専用のワーカー参照を含むものがあります。 拡張機能を追加するには、通常、暗黙的な参照グループ (暗黙 **(Windows)** 、暗黙的 **(Web))** としてファイルを追加する必要があります。 暗黙の参照は、コードエディターで開かれたすべての .js ファイルのスコープ内にあります。 このメソッドを使用する場合は、拡張機能によって補完される拡張子とファイルの両方を追加する必要があります。

 **[オプション]** ダイアログボックスの **[IntelliSense]** ページを使用すると、拡張機能を参照グループとして追加できます。 **IntelliSense**ページにアクセスするには、メニューバーの **[ツール]** 、 **[オプション]** の順に選択し、 **[テキストエディター]** 、 **[JavaScript]** 、 **[IntelliSense]** 、 **[参照]** の順にクリックします。 参照グループの詳細については、「 [Javascript intellisense](../ide/javascript-intellisense.md)と[オプション、テキストエディター、javascript、intellisense](../ide/reference/options-text-editor-javascript-intellisense.md)」を参照してください。

 特定のファイルセットに拡張機能を使用する場合は、参照ディレクティブを使用します。 このメソッドを使用する場合は、拡張機能が補完するファイルと拡張機能の両方を参照する必要があります。 Reference ディレクティブの使用の詳細については、「 [JavaScript IntelliSense](../ide/javascript-intellisense.md)」を参照してください。

## <a name="handling-intellisense-events"></a>IntelliSense イベントの処理
 拡張機能を使用すると、言語サービス `intellisense` オブジェクトの `statementcompletion` イベントなどのイベントをサブスクライブすることで、IntelliSense の結果をカスタマイズできます。 次の例は、アンダースコアで始まるメンバーを非表示にするために言語サービスによって使用される単純な拡張機能を示しています。 このコードは underscorefilter に含まれており、\\ \\*Visual Studio インストールパス*\JavaScript\References フォルダーにあります。

```javascript
intellisense.addEventListener('statementcompletion', function (event) {
    if (event.targetName === "this") return;

    var filterRegex;

    if (event.target === undefined || event.target === window)
        filterRegex = /^_.*\d{2,}/;
    else
        filterRegex = /^_.*/;

    event.items = event.items.filter(function (item) {
        return !filterRegex.test(item.name);
    });
});
```

 前のコードでは、拡張機能によって、`statementcompletion` イベントオブジェクトの[TargetName プロパティ](#TargetName)と[target プロパティ](#Target)プロパティが確認され、`this` や `window` などのオブジェクトが除外され、有効なステートメント入力候補リストを使用できるようになります。明確. コンプリートリストを識別できる場合は、アンダースコアで始まるメンバーを除外することにより、拡張機能によってステートメント完了[項目のプロパティ](#Items)コレクションが更新されます。

 その他の例については、\\ \\*Visual Studio のインストールパス*\JavaScript\References フォルダーを参照してください。 このフォルダーの showPlainComments ファイルは、他のイベントを使用して、標準の JavaScript コメントタグ (//) の既定の IntelliSense サポートを提供する例を示しています。 Underscorefilter と同様、showPlainComments は動作拡張として既に使用可能であり、コード内で変数、関数、およびオブジェクトのコメントタグを使用すると、結果として得られる IntelliSense 情報を確認できます。 その他の例については、「[コード例](#CodeExamples)」を参照してください。

> [!WARNING]
> Visual Studio に含まれる拡張ファイルを変更する場合は、JavaScript IntelliSense または拡張機能でサポートされている機能を無効にすることができます。

 拡張コードでは、`addEventListener` を使用して、次のイベントの種類のハンドラーを作成できます。

- `statementcompletion`、ステートメント完了イベントのハンドラーを追加します。 ステートメント入力候補には、ピリオド (.) などの特殊文字を入力した後に表示される特定の型のメンバーの一覧、またはの入力時または CTRL + J キーを押したときに表示される識別子の一覧が表示されます。ハンドラーは `CompletionEvent` 型のイベントオブジェクトを受け取ります。このオブジェクトは、 [Items プロパティ](#Items)、 [target Property](#Target)、 [TargetName property](#TargetName)、および[scope プロパティ](#Scope)をサポートしています。

- `signaturehelp`、IntelliSense パラメーターヒントのハンドラーを追加します。 パラメーター情報は、関数に必要なパラメーターの数、名前、および型に関する情報を提供します。 ハンドラーは `SignatureHelpEvent` 型のイベントオブジェクトを受け取ります。このオブジェクトは、 [Target プロパティ](#Target)、 [parentObject Property](#ParentObject)、 [functioncomments プロパティ](#FunctionComments)、 [functioncomments プロパティ](#FunctionHelp)の各メンバーをサポートしています。

- `statementcompletionhint`、IntelliSense のクイックヒント用のハンドラーを追加します。 [クイックヒント] ポップアップボックスには、コード内の識別子の完全な宣言が表示されます。 このハンドラーは、`CompletionHintEvent` 型のイベントオブジェクトを受け取ります。このオブジェクトは、次のメンバーをサポートしています: ["補完 Item" プロパティ](#CompletionItem)と["シンボルヘルプ" プロパティ](#SymbolHelp)。

  ステートメント入力候補、パラメーター情報、クイックヒントなどの IntelliSense 機能を示す例については、「 [intellisense の使用](../ide/using-intellisense.md)」を参照してください。

> [!NOTE]
> JavaScript では、クイックヒントは、入力候補一覧の右側に表示されるポップアップボックスを示します。 クイックヒントを手動で呼び出すことはできません。

## <a name="intellisenseObject"></a> IntelliSense オブジェクト
 次の表は、`intellisense` オブジェクトで使用できる関数を示しています。 @No__t_0 オブジェクトは、デザイン時にのみ使用できます。

|機能|説明|
|--------------|-----------------|
|`addEventListener(type, handler);`|IntelliSense イベントのイベントハンドラーを追加します。<br /><br /> `type` は文字列値です。 有効な値は、`statementcompletion`、`signaturehelp`、および `statementcompletionhint` です。<br /><br /> `handler` は、次のいずれかの型のイベントオブジェクトを受け取るイベントハンドラー関数です。<br /><br /> -    `CompletionEvent`。 `statementcompletion` イベントに使用されます。<br />-    `SignatureHelpEvent`。 `signaturehelp` イベントに使用されます。<br />-    `CompletionHintEvent`。 `statementcompletionhint` イベントに使用されます。<br /><br /> この関数を使用する例については、「[コード例](#CodeExamples)」を参照してください。|
|`annotate(obj, doc);`|1つのオブジェクトから別のオブジェクトにドキュメントコメントをコピーすることによって、オブジェクトのドキュメントを指定します。<br /><br /> `obj` ドキュメントのコピー先のオブジェクトを指定します。<br /><br /> `doc` ドキュメントのコピー元のオブジェクトを指定します。<br /><br /> この関数の使用方法を示す例については、「 [IntelliSense 注釈の追加](#Annotations)」を参照してください。|
|`getFunctionComments(func);`|指定された関数のコメントを返します。<br /><br /> `func` は、コメントが返される関数を指定します。<br /><br /> @No__t_0 パラメーターを設定するには `completionItem.value` を使用します。<br /><br /> 返される `functionComments` オブジェクトには、`above`、`inside`、および `paramComment` の各メンバーが含まれます。 詳細については、「 [Functioncomments プロパティ](#FunctionComments)」プロパティを参照してください。<br /><br /> `getFunctionComments` を呼び出すことができるのは、`addEventListener` によって登録されているいずれかのイベントハンドラー内からだけです。<br /><br /> この関数の使用方法を示す例については、「\\ \\*Visual Studio のインストールパス*\JavaScript\References\showPlainComments.js.」を参照してください。|
|`logMessage(msg);`|診断メッセージを出力ウィンドウに送信します。<br /><br /> `msg` は、メッセージを含む文字列です。<br /><br /> この関数の使用方法を示す例については、「[出力ウィンドウへのメッセージの送信](#Logging)」を参照してください。|
|`nullWithCompletionsOf(value);`|@No__t_0 パラメーターで渡されたオブジェクトによって、コンプリートリストが決定される特殊な null 値を返します。<br /><br /> `value` は、戻り値の入力候補一覧を決定します。 `value` には任意の型を指定できます。<br /><br /> Null 値はデザイン時に null として扱われますが、戻り値のコンプリートリストは `value` パラメーターのコンプリートリストと同じです。<br /><br /> この関数の1つの用途は、戻り値の型が実行時に予測可能な場合に、戻り値に IntelliSense を提供することですが、戻り値はデザイン時に `null` ます。|
|`redirectDefinition(func, definition);`|パラメーターヘルプまたは **[定義へ移動**] が要求されたときに、元の func 関数の代わりに指定された定義関数を使用するように IntelliSense に指示します。<br /><br /> `func` 対象の関数を指定します。<br /><br /> `definition` パラメーター情報の対象の関数の代わりに使用する関数を指定し、 **[定義へ移動**] を指定します。|
|`setCallContext(func, thisArg);`|指定された関数の呼び出しコンテキスト (スコープ) を設定します。<br /><br /> `func` スコープを設定する関数を指定します。<br /><br /> `thisArg` は、`this` キーワードが参照できるオブジェクトリテラルです。これは、メンバーの新しいスコープを指定します。 このパラメーターに渡す引数を含めることができます (例 `intellisense.setCallContext(func, { thisArg: "", args: [23,2] });`<br /><br /> `setCallContext` は `Function.prototype.bind` と同様の動作を提供しますが、デザイン時の IntelliSense サポートにのみ使用される点が異なります。 @No__t_0 を使用すると、他に到達できないコードの呼び出しをシミュレートする必要がある場合に、関数のスコープを設定できます。これにより、関数を呼び出すと、関数の呼び出しに正しいスコープと引数が含まれるようになります。|
|`undefinedWithCompletionsOf(value);`|@No__t_0 パラメーターで渡されたオブジェクトによって入力候補一覧が決定される特別な未定義値を返します。<br /><br /> `value` は、戻り値の入力候補一覧を決定します。 `value` には任意の型を指定できます。<br /><br /> 未定義の戻り値はデザイン時に未定義として扱われますが、戻り値のコンプリートリストは `value` パラメーターのコンプリートリストと同じです。<br /><br /> この関数の1つの用途は、戻り値の型が実行時に予測可能な場合に、戻り値として IntelliSense を提供することですが、戻り値はデザイン時には定義されません。|
|`version()`|Visual Studio のバージョンを返します。|

## <a name="event-members"></a>イベントメンバー
 次のセクションでは、`statementcompletion`、`signaturehelp`、および `statementcompletionhint` イベントのイベントオブジェクトで公開されるメンバーについて説明します。

### <a name="CompletionItem"></a>"項目のプロパティ" プロパティ
 クイックヒントポップアップボックスが要求される、完了項目と呼ばれる識別子を返します。 このプロパティは、`statementcompletionhint` イベントオブジェクトおよび `statementcompletion` イベントオブジェクトの[Items プロパティ](#Items)プロパティで使用できます。

 戻り値: `completionItem` オブジェクト

 @No__t_0 オブジェクトのメンバーを次に示します。

- `name`. @No__t_0 コレクションで使用した場合の読み取り/書き込み。それ以外の場合は読み取り専用です。 完了項目を識別する文字列を返します。

- `kind`. @No__t_0 コレクションで使用した場合の読み取り/書き込み。それ以外の場合は読み取り専用です。 完了項目の種類を表す文字列を返します。 使用可能な値は、メソッド、フィールド、プロパティ、パラメーター、変数、および予約済みです。

- `glyph`. @No__t_0 コレクションで使用した場合の読み取り/書き込み。それ以外の場合は読み取り専用です。 入力候補一覧に表示されるアイコンを表す文字列を返します。 @No__t_0 に使用できる値は、次の形式を使用します。 vs:*glyphType*, *glyphType*は、言語に依存しない、<xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup> 列挙のメンバーに対応します。 たとえば、`vs:GlyphGroupMethod` は `glyph` で使用できる値の1つです。 @No__t_0 が設定されていない場合、`kind` プロパティによって既定のアイコンが決まります。

- `parentObject`. 読み取り専用。 親オブジェクトを返します。

- `value`. 読み取り専用。 完了項目の値を表すオブジェクトを返します。

- `comments`. 読み取り専用。 フィールドまたは変数の上にあるコメントを含む文字列を返します。

- `scope`. 読み取り専用。 完了項目のスコープを返します。 指定できる値は、global、local、parameter、および member です。

### <a name="Items"></a>items プロパティ
 ステートメント完了項目の配列を取得または設定します。 配列の各要素は、[補完項目プロパティ](#CompletionItem)オブジェクトです。 @No__t_0 プロパティは、`statementcompletion` イベントオブジェクトで使用できます。

 戻り値: 配列

### <a name="FunctionComments"></a>functionComments プロパティ
 関数のコメントを返します。 このプロパティは、`signaturehelp` イベントオブジェクトで使用できます。

 戻り値: `comments` オブジェクト

 @No__t_0 オブジェクトのメンバーを次に示します。

- `above`. 関数の上にあるコメントを返します。

- `inside`. 関数内のコメントを返します (通常は VSDoc 形式)。

- `paramComments`. 関数内の各パラメーターのコメントを表す配列を返します。 配列のメンバーは次のとおりです。

  - `name`. パラメーター名を表す文字列を返します。

  - `comment`. パラメーターコメントを含む文字列を返します。

### <a name="FunctionHelp"></a>functionHelp プロパティ
 関数のヘルプを返します。 このプロパティは、`signaturehelp` イベントオブジェクトで使用できます。

 戻り値: `functionHelp` オブジェクト

 @No__t_0 オブジェクトのメンバーを次に示します。

- `functionName`. 読み取り/書き込み。 関数名を含む文字列を返します。

- `signatures`. 読み取り/書き込み。 関数シグネチャの配列を取得または設定します。 配列の各要素は `signature` オブジェクトです。 @No__t_1 などの一部の `signature` プロパティは、一般的な[XML ドキュメントコメント](../ide/xml-documentation-comments-javascript.md)の属性に対応しています。

  @No__t_0 オブジェクトのメンバーは次のとおりです。

  - `description`. 読み取り/書き込み。 関数を説明する文字列を返します。

  - `locid`. 読み取り/書き込み。 関数に関するローカライズ情報を含む文字列識別子を返します。

  - `helpKeyword`. 読み取り/書き込み。 ヘルプキーワードを含む文字列を返します。

  - `externalFile`. 読み取り/書き込み。 メンバー ID を含むファイルを表す文字列を返します。

  - `externalid`. 読み取り/書き込み。 関数のメンバー ID を表す文字列を返します。

  - `params`. 読み取り/書き込み。 関数のパラメーターの配列を取得または設定します。 Parameters 配列の各要素は、 [\<param >](../ide/param-javascript.md)要素の次の属性に対応するプロパティを持つ `parameter` オブジェクトです。

    - `name`. 読み取り/書き込み。 パラメーター名を表す文字列を返します。

    - `type`. 読み取り/書き込み。 パラメーターの型を表す文字列を返します。

    - `elementType`. 読み取り/書き込み。 型が `Array` 場合、は配列内の要素の型を表す文字列を返します。

    - `description`. 読み取り/書き込み。 パラメーターを説明する文字列を返します。

    - `locid`. 読み取り/書き込み。 関数に関するローカライズ情報を含む文字列識別子を返します。

    - `optional`. 読み取り/書き込み。 パラメーターが省略可能かどうかを示す文字列を返します。 `true` は、パラメーターが省略可能であることを示します。 `false` は、そうでないことを示します。

  - `returnValue`. 読み取り/書き込み。 [@No__t_1returns >](../ide/returns-javascript.md)要素の次の属性に対応するプロパティを持つ戻り値オブジェクトを取得または設定します。

    - `type`. 読み取り/書き込み。 戻り値の型を表す文字列を返します。

    - `elementType`. 読み取り/書き込み。 型が `Array` 場合、は配列内の要素の型を表す文字列を返します。

    - `description`. 読み取り/書き込み。 戻り値を説明する文字列を返します。

    - `locid`. 読み取り/書き込み。 関数に関するローカライズ情報を含む文字列識別子を返します。

    - `helpKeyword`. 読み取り/書き込み。 ヘルプキーワードを含む文字列を返します。

    - `externalFile`. 読み取り/書き込み。 メンバー ID を含むファイルを表す文字列を返します。

    - `externalid`. 読み取り/書き込み。 関数のメンバー ID を表す文字列を返します。

### <a name="ParentObject"></a>parentObject プロパティ
 メンバー関数の親オブジェクトを返します。 たとえば、`document.getElementByID` の場合、`parentObject` は `document` オブジェクトを返します。 このプロパティは、`signaturehelp` イベントオブジェクトで使用できます。

 戻り値: オブジェクト

### <a name="Target"></a> target プロパティ
 トリガー文字の左側の項目 (ピリオド (.)) を表すオブジェクトを返します。 関数の場合、`target` は、パラメーター情報が要求される関数を返します。 このプロパティは、`statementcompletion` イベントオブジェクトと `signaturehelp` イベントオブジェクトで使用できます。

 戻り値: オブジェクト

### <a name="TargetName"></a>targetName プロパティ
 ターゲットを表す文字列を返します。 たとえば、"this." の場合、`targetName` は "this" を返します。 "A. B" (カーソルが "B" の後にある場合) の場合、`targetName` は "B" を返します。 このプロパティは、`statementcompletion` イベントオブジェクトで使用できます。

 戻り値: string

### <a name="SymbolHelp"></a>シンボルのヘルププロパティ
 クイックヒントポップアップボックスが要求される完了項目を返します。 このプロパティは、`statementcompletionhint` イベントオブジェクトで使用できます。

 戻り値: `symbolHelp` オブジェクト。

 @No__t_1 などの `symbolHelp` オブジェクトの一部のプロパティは、一般的な[XML ドキュメントコメント](../ide/xml-documentation-comments-javascript.md)の属性に対応しています。

 @No__t_0 オブジェクトのメンバーを次に示します。

- `name`. 読み取り/書き込み。 識別子名を含む文字列を返します。

- `symbolType`. 読み取り/書き込み。 シンボルの種類を表す文字列を返します。 指定できる値は、Unknown、Boolean、Number、String、Object、Function、Array、Date、および Regex です。

- `symbolDisplayType`. 読み取り/書き込み。 表示する型名を含む文字列を返します。 @No__t_0 が設定されていない場合は、`symbolType` が使用されます。

- `elementType`. 読み取り/書き込み。 @No__t_0 が `Array` の場合、は配列内の要素の型を表す文字列を返します。

- `scope`. 読み取り/書き込み。 記号のスコープを表す文字列を返します。 指定できる値は、global、local、parameter、および member です。

- `description`. 読み取り/書き込み。 記号の説明を含む文字列を返します。

- `locid`. 読み取り/書き込み。 シンボルに関するローカライズ情報を含む文字列識別子を返します。

- `helpKeyword`. 読み取り/書き込み。 ヘルプキーワードを含む文字列を返します。

- `externalFile`. 読み取り/書き込み。 メンバー ID を含むファイルを表す文字列を返します。

- `externalid`. 読み取り/書き込み。 シンボルのメンバー ID を表す文字列を返します。

- `functionHelp`. 読み取り/書き込み。 [Functionhelp プロパティ](#FunctionHelp)を返します。このプロパティには、`symbolType` が機能しているときに情報が含まれている場合があります。

### <a name="Scope"></a>scope プロパティ
 イベントの完了スコープを返します。 完了スコープに指定できる値は、グローバルとメンバーです。 このプロパティは、`statementcompletion` イベントオブジェクトで使用できます。

 戻り値: string

## <a name="debugging-intellisense-extensions"></a>デバッグ (IntelliSense 拡張機能を)
 拡張機能をデバッグすることはできませんが、 [Intellisense オブジェクト](#intellisenseObject)関数を使用すると、Visual Studio の出力ウィンドウに情報を送信できます。 この関数の使用方法を示す例については、このトピックで後述[する「出力ウィンドウへのメッセージの送信](#Logging)」を参照してください。 @No__t_0 を機能させるには、少なくとも1つのイベントハンドラーが拡張機能に登録されている必要があります。

## <a name="CodeExamples"></a> コード例
 このセクションには、IntelliSense 機能拡張 Api の使用方法を示すコード例が含まれています。 これらの Api を使用する他の方法もあります。 その他の例については、\\ \\*Visual Studio のインストールパス*\JavaScript\References フォルダーにある次のファイルを参照してください。 JavaScript 言語サービスで使用される実際の例を次に示します。

- underscoreFilter。 このコードは、IntelliSense のプライベートメンバーを非表示にします。 これには、`statementcompletion` イベントのイベントハンドラーが含まれます。

- showPlainComments。 このコードでは、標準のコメントに対して IntelliSense がサポートされています。 これには、`signaturehelp` イベントと `statementcompletionhint` イベントのイベントハンドラーが含まれます。

### <a name="Annotations"></a>IntelliSense 注釈の追加
 次の手順は、ライブラリを直接変更することなく、サードパーティ製ライブラリの IntelliSense ドキュメントサポートを提供する方法を示しています。 これを行うには、拡張機能で `intellisense.annotate` を使用します。

 この例を実行するには、プロジェクトに次の JavaScript ファイルが必要です。

- demoLib は、サードパーティのライブラリを表すプロジェクトファイルです。

- IntelliSense の拡張機能である demoLib。 このファイルは、プロジェクトに含める必要はありませんが、exampleLib.js と同じフォルダーに含める必要があります。

- appCode.js (アプリケーション コードを表すプロジェクト ファイル)。

##### <a name="to-add-an-intellisense-annotation"></a>IntelliSense 注釈を追加するには

1. DemoLib に次のコードを追加します。

    ```javascript
    function someFunc(a) { };
    var rectangle;

    ```

2. DemoLib に次のコードを追加します。

    ```javascript
    intellisense.annotate(someFunc, function (a) {
        /// <signature>
        /// <summary>Description of someFunc</summary>
        /// <param name="a">Param a</param>
        /// </signature>
    });

    intellisense.annotate(window, {
        // This is a comment on a global variable named rectangle.
        rectangle: undefined
    });
    ```

3. 次の reference ディレクティブを appCode.js の最初の行として追加します。 ここで使用するパスは、JavaScript ファイルが同じフォルダーにあることを示しています。

    ```javascript
    /// <reference path="demoLib.js" />

    ```

4. appCode.js で、次のコードを入力します。 IntelliSense のパラメーター情報として表示される拡張機能に XML ドキュメントのコメントが表示されます。

     ![Intellisense の使用例を示します。注釈](../ide/media/js-intellisense-annotate-paraminfo.png "js_intellisense_annotate_paraminfo")

5. appCode.js で、次のコードを入力します。 「」と入力すると、IntelliSense クイックヒントとして表示される拡張機能に標準のコメントが表示されます。

     ![Intellisense の使用例を示します。注釈](../ide/media/js-intellisense-annotations.png "js_intellisense_annotations")

### <a name="Logging"></a>出力ウィンドウへのメッセージの送信
 次の手順は、[出力] ウィンドウにメッセージを送信する方法を示しています。 IntelliSense 拡張機能のデバッグに役立つメッセージを送信できます。

 この例を実行するには、プロジェクトに次の JavaScript ファイルが必要です。

- 例: Lib は、サードパーティのライブラリを表すプロジェクトファイルです。

- 例では、IntelliSense 拡張機能であるを使用します。 このファイルは、プロジェクトに含める必要はありませんが、exampleLib.js と同じフォルダーに含める必要があります。

- appCode.js (アプリケーション コードを表すプロジェクト ファイル)。

##### <a name="to-send-a-message-to-the-output-window"></a>[出力] ウィンドウにメッセージを送信するには

1. 次のコードを例の Lib に追加します。

    ```javascript
    var someVar = {
        a: 1,
        b: 'hello'
    };
    ```

2. 次のコードを追加します。

    ```javascript
    intellisense.addEventListener('statementcompletion', function (e) {
        // Prints out statement completion info: Either (1) the member
        // list, if the trigger character was typed, or (2) the
        // statement completion identifiers.
        // e.target represents the object left of the trigger character.
        intellisense.logMessage(
            e.target ? 'member list requested, target: ' + e.targetName : 'statement completion for current scope requested');

        // Prints out all statement completion items.
        e.items.forEach(function (item) {
            intellisense.logMessage('[completion item] ' + item.name + ', kind:' + item.kind + ', scope:' + item.scope + ', value:' + item.value);
        });
    });
    ```

3. 次の reference ディレクティブを appCode.js の最初の行として追加します。 ここで使用するパスは、JavaScript ファイルが同じフォルダーにあることを示しています。

    ```javascript
    /// <reference path="exampleLib.js" />

    ```

4. 出力ウィンドウで、 **[出力元の表示]** ボックスの一覧の **[JavaScript Language Service]** を選択します。 (出力 ウィンドウを表示するには、表示 メニューの **出力** を選択します)。

5. appCode.js で、次のコードを入力します。 「」と入力すると、[出力] ウィンドウに言語サービスからのメッセージが表示されます。 [出力] ウィンドウの最初のメッセージは、現在のスコープのステートメント補完が要求されたことを示しています。

    ```javascript
    some
    ```

     表示される出力の一部を次に示します。

    ```scr
    03:16:14.3113: statement completion for current scope requested
    03:16:14.3113: [completion item] break, kind:reserved, scope:undefined, value:undefined
    03:16:14.3113: [completion item] case, kind:reserved, scope:undefined, value:undefined
    03:16:14.3113: [completion item] catch, kind:reserved, scope:undefined, value:undefined

    …
    ```

6. 出力 ウィンドウの **すべてクリア** ボタンをクリックします。

7. 次のコードを入力します。 [出力] ウィンドウの最初のメッセージは、メンバーリストが要求されたことを示しています。

    ```javascript
    someVar.
    ```

     表示される出力の部分的なビューを次に示します。

    ```scr
    03:17:43.4032: member list requested, target: someVar
    03:17:43.4032: [completion item] a, kind:field, scope:member, value:1
    03:17:43.4032: [completion item] b, kind:field, scope:member, value:hello
    03:17:43.4032: [completion item] constructor, kind:method, scope:member, value:

    …
    ```

### <a name="Icons"></a>IntelliSense アイコンの変更
 次の手順は、既定で IntelliSense によって表示されるアイコンを変更する方法を示しています。 これは、名前空間、クラス、インターフェイス、列挙などのライブラリ固有の概念に関する IntelliSense 情報を提供する場合に便利です。

 使用可能なアイコンの値については、「<xref:Microsoft.VisualStudio.Language.Intellisense.StandardGlyphGroup>」を参照してください。

 この例を実行するには、プロジェクトに次の JavaScript ファイルが必要です。

- 例: Lib は、サードパーティ製のライブラリを represens するプロジェクトファイルです。

- 例では、IntelliSense 拡張機能であるを使用します。 このファイルは、プロジェクトに含める必要はありませんが、exampleLib.js と同じフォルダーに含める必要があります。

- appCode.js (アプリケーション コードを表すプロジェクト ファイル)。

##### <a name="to-change-the-icons"></a>アイコンを変更するには

1. 次のコードを例の Lib に追加します。

    ```javascript
    function Namespace(name) {
        this._isNamespace = true;
        window[name] = this;
    };

    function Enum(values) {
        var e = Object.create(values);
        e._isEnum = true;
        return e;
    };

    var SomeNamespace = new Namespace('SomeNamespace');
    // A constructor function is considered a class.
    SomeNamespace.SomeClass1 = function () { }
    SomeNamespace.Enum1 = new Enum({ VALUE1: 0, VALUE2: 1 });
    ```

2. 次のコードを追加します。

    ```javascript
    intellisense.addEventListener('statementcompletion', function (e) {
        e.items.forEach(function (item) {
            // Detect a namespace by using the _isNamespace flag.
            if (item.value && item.value._isNamespace) {
                item.glyph = 'vs:GlyphGroupNamespace';
                }

            if (item.parentObject && item.parentObject._isNamespace) {
                // The item is a member of a namespace.

                // All constructor functions that are part of a namespace
                // are considered classes.
                // A constructor function starts with
                // an uppercase letter by convention.
                if (typeof item.value == 'function' && (item.name[0].toUpperCase()
                    == item.name[0])) {
                    item.glyph = 'vs:GlyphGroupClass';
                }

                // Detect an enumeration by using the _isEnum flag.
                if (item.value && item.value._isEnum) {
                    item.glyph = 'vs:GlyphGroupEnum';
                }
            }
        });
    });

    intellisense.addEventListener('statementcompletionhint', function (e) {
        if (e.completionItem.value) {
            if (e.completionItem.value._isNamespace) {
                e.symbolHelp.symbolDisplayType = 'Namespace';
            }
            if (e.completionItem.value._isEnum) {
                e.symbolHelp.symbolDisplayType = 'Enum';
            }
        }
    });
    ```

3. 次の reference ディレクティブを appCode.js の最初の行として追加します。 ここで使用するパスは、JavaScript ファイルが同じフォルダーにあることを示しています。

    ```javascript
    /// <reference path="exampleLib.js" />

    ```

4. appCode.js で、次のコードを入力します。 「」と入力すると、でC#使用されているように、名前空間のアイコンが "{}" に変更されていることがわかります。

     ![グリフのプロパティの使用方法を示す例](../ide/media/js-intellisense-glyph-namespace.png "js_intellisense_glyph_namespace")

5. appCode.js で、次のコードを入力します。 「」と入力すると、Enum1 メンバーの新しい列挙アイコンと、SomeClass1 メンバーの新しいクラスアイコンが表示されます。

     ![グリフプロパティの使用方法を示す例](../ide/media/js-intellisense-glyph-class-enum.png "js_intellisense_glyph_class_enum")

### <a name="Overriding"></a>IntelliSense の結果に対する実行時の影響を回避する
 JavaScript 言語サービスは、IntelliSense 情報を動的に提供するコードを実行します。 結果として、実行時の動作が必要な結果に干渉することがあります。 次の手順は、実行時の動作によって IntelliSense が正しく動作しない場合に IntelliSense の結果をオーバーライドする方法を示しています。

 この例を実行するには、プロジェクトに次の JavaScript ファイルが必要です。

- 例: Lib は、サードパーティのライブラリを表すプロジェクトファイルです。

- 例では、IntelliSense 拡張機能であるを使用します。 このファイルは、プロジェクトに含める必要はありませんが、exampleLib.js と同じフォルダーに含める必要があります。

- appCode.js (アプリケーション コードを表すプロジェクト ファイル)。

##### <a name="to-avoid-run-time-effects-on-intellisense-results"></a>IntelliSense の結果に対して実行時の影響を回避するには

1. 次のコードを例の Lib に追加します。

    ```javascript
    function after(count, func) {
        return function () {
            if (--times < 1) {
                return func.apply(this, arguments);
            }
        };
    };
    ```

     前のコードでは、ラップされた関数は `count` の値に基づいて初期呼び出しを無視し、結果は返しません。

2. 次の reference ディレクティブを appCode.js の最初の行として追加します。 ここで使用するパスは、JavaScript ファイルが同じフォルダーにあることを示しています。

    ```javascript
    /// <reference path="exampleLib.js" />

    ```

3. appCode.js で、次のコードを入力します。 ラップされた関数が呼び出されないため、IntelliSense ではなく識別子の一覧が表示されます。つまり、`throttled` 関数が結果を返さないことを意味します。

     ![Intellisense の結果をオーバーライドする例](../ide/media/js-intellisense-override.png "js_intellisense_override")

4. 次のコードを追加します。 これにより、ラップされた関数の IntelliSense が想定どおりに表示されるように、デザイン時の動作が変更されます。

    ```javascript
    window.after = function (count, func) {
        // Just return func.
        return func;
    };
    ```

5. AppCode .js で、前に入力したものと同じコードを入力して結果をテストします。 今回は、IntelliSense によって必要な情報が提供されます。

     ![IntelliSense の結果をオーバーライドする例](../ide/media/js-intellisense-override-fixed.png "js_intellisense_override_fixed")

## <a name="see-also"></a>参照
 識別子の[JavaScript IntelliSense](../ide/javascript-intellisense.md) [ステートメント入力候補](../ide/statement-completion-for-identifiers.md)
