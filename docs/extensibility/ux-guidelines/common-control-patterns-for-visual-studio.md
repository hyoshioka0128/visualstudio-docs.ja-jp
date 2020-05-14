---
title: Visual Studio の共通のコントロール パターン |マイクロソフトドキュメント
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b0b5a1904c01f5688a00e45de7feed7ae326d9b3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698710"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio の コモン コントロール パターン
## <a name="common-controls"></a><a name="BKMK_CommonControls"></a>一般的なコントロール

### <a name="overview"></a>概要
コモン コントロールは、Visual Studio のユーザー インターフェイスの大部分を占めています。 Visual Studio インターフェイスで使用される最も一般的なコントロールは[、Windows デスクトップの操作に関するガイドライン](/windows/desktop/uxguide/controls)に従う必要があります。 このトピックは Visual Studio に固有のものであり、Windows のガイドラインを強化する特殊な状況や詳細について説明します。

#### <a name="common-controls-in-this-topic"></a>このトピックの一般的なコントロール

- [スクロールバー](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [入力フィールド](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [コンボ ボックスとドロップダウン リスト](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [チェック ボックス](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [ラジオボタン](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [グループ フレーム](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [テキスト コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [ボタンとハイパーリンク](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [ツリー ビュー](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>視覚スタイル
コントロールのスタイル設定を行うときに最初に考慮すべき点は、テーマにした UI でコントロールを使用するかどうかです。 標準 UI のコントロールはテーマを設定しない UI であり、通常の[Windows デスクトップ スタイル](/windows/desktop/uxguide/controls)に従う必要があります。

- **標準(ユーティリティ)ダイアログ:** テーマではありません。 再テンプレートを使用しないでください。 基本的なコントロール スタイルの既定値を使用します。

- **ツール ウィンドウ、ドキュメント エディタ、デザイン 画面、テーマダイアログ:** カラーサービスを使用して、特殊なテーマの外観を使用します。

### <a name="scroll-bars"></a><a name="BKMK_Scrollbars"></a>スクロールバー
 スクロール バーは、コード エディターのように、コンテンツ情報で拡張されていない限り[、Windows スクロール バーの一般的な相互作用パターン](/windows/desktop/Controls/about-scroll-bars)に従う必要があります。

### <a name="input-fields"></a><a name="BKMK_InputFields"></a>入力フィールド
 一般的な対話動作については、[テキスト ボックスの Windows デスクトップ のガイドラインに](/windows/desktop/uxguide/ctrl-text-boxes)従ってください。

#### <a name="visual-style"></a>視覚スタイル

- 入力フィールドは、ユーティリティ ダイアログでスタイルを設定しないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ入力フィールドは、テーマを適用したダイアログやツールウィンドウでのみ使用してください。

#### <a name="specialized-interactions"></a>特殊な相互作用

- 読み取り専用フィールドには、背景が灰色 (無効) ですが、既定の (アクティブな) 前景が表示されます。

- 必須フィールドには、**\<ウォーターマークとして必須>** を設定する必要があります。 まれな状況を除き、背景の色を変更しないでください。

- エラーの検証: [「Visual Studio の通知と進行状況」を](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)参照してください。

- 入力フィールドは、表示されるウィンドウの幅に合わせて、またはパスのように長いフィールドの長さに任意に一致するように、コンテンツに合わせてサイズを設定する必要があります。 長さは、フィールドで許容される文字数に関する制限をユーザーに示す場合があります。

     ![入力フィールドの長さが正しくない: 名前がこれほど長くなる可能性は低い。](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")<br />入力フィールドの長さが正しくない: 名前がこれほど長くなる可能性は低い。

     ![入力フィールドの長さを修正する: 入力フィールドは、予想される内容に適した幅です。](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")<br />入力フィールドの長さを修正する: 入力フィールドは、予想される内容に適した幅です。

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a>コンボ ボックスとドロップダウン リスト
一般的な操作動作については[、Windows デスクトップのドロップダウン リストとコンボ ボックスのガイドラインに従ってください](/windows/desktop/uxguide/ctrl-drop)。

#### <a name="visual-style"></a>視覚スタイル

- ユーティリティ ダイアログでは、コントロールの再テンプレートを行わないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ UI では、コンボ ボックスとドロップダウンはコントロールの標準テーマに従います。

#### <a name="layout"></a>レイアウト
コンボ ボックスとドロップダウン は、表示されるウィンドウの幅に合わせて、またはパスのように長いフィールドの長さに任意に一致しないように、コンテンツに合わせてサイズを調整する必要があります。

![正しくない: ドロップダウン幅が長すぎて表示されるコンテンツが長すぎます。](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")<br />正しくない: ドロップダウン幅が長すぎて表示されるコンテンツが長すぎます。

![正しい: ドロップダウンは翻訳の拡張を可能にするサイズですが、不必要に長くはありません。](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707-04_CorrectDropDownLayout")<br />正しい: ドロップダウンは翻訳の拡張を可能にするサイズですが、不必要に長くはありません。

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a>チェックボックス
一般的な対話動作については[、Windows デスクトップのチェック ボックスのガイドラインに従ってください](/windows/desktop/uxguide/ctrl-check-boxes)。

#### <a name="visual-style"></a>視覚スタイル

- ユーティリティ ダイアログでは、コントロールの再テンプレートを行わないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ UI では、チェック ボックスはコントロールの標準テーマに従います。

#### <a name="specialized-interactions"></a>特殊な相互作用

- チェック ボックスとの対話は、ダイアログをポップしたり、別の領域に移動したりしないでください。

- チェック ボックスをテキストの最初の行のベースラインに合わせます。

     ![正しくない: チェック ボックスがテキストの中央に配置されています。](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")<br />正しくない: チェック ボックスがテキストの中央に配置されています。

     ![正しい: チェック ボックスはテキストの最初の行に揃えられます。](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")<br />正しい: チェック ボックスはテキストの最初の行に揃えられます。

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a>ラジオボタン
一般的な対話動作については[、Windows デスクトップのラジオ ボタンのガイドラインに](/windows/desktop/uxguide/ctrl-radio-buttons)従ってください。

#### <a name="visual-style"></a>視覚スタイル
ユーティリティ ダイアログでは、ラジオ ボタンのスタイルを設定しないでください。 コントロールに固有の基本スタイルを使用します。

#### <a name="specialized-interactions"></a>特殊な相互作用
グループの区別を密に配置する必要がない限り、ラジオの選択肢を囲むためにグループ フレームを使用する必要はありません。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a>グループ フレーム
一般的な対話動作については、[グループ フレームの Windows デスクトップ ガイドラインに](/windows/desktop/uxguide/ctrl-group-boxes)従ってください。

#### <a name="visual-style"></a>視覚スタイル
ユーティリティ ダイアログでは、グループ フレームのスタイルを設定しないでください。 コントロールに固有の基本スタイルを使用します。

#### <a name="layout"></a>レイアウト

- グループの区別を密に配置する必要がない限り、ラジオの選択肢を囲むためにグループ フレームを使用する必要はありません。

- グループ フレームを 1 つのコントロールに使用しないでください。

- グループ フレーム コンテナーの代わりに水平規則を使用しても問題ありません。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a>テキスト コントロール

### <a name="static-text-fields"></a>静的テキスト フィールド

静的テキスト フィールドは読み取り専用の情報を表示し、ユーザーが選択することはできません。 ユーザーがクリップボードにコピーするテキストには使用しないでください。 ただし、静的テキストの読み取り専用は、状態の変化を反映するように変更できます。 次の例では、[情報] グループの下の [出力名] 静的テキストが変更され、その上の [ルート名前空間] テキスト ボックスに加えられた変更が反映されます。

静的テキスト情報を表示するには、2 つの方法があります。

グループ化の競合がない場合、静的テキストは、ダイアログ内で単独で使用できます。 ボックスの余分な行が本当に必要かどうかを決定します。 たとえば、次に示すように、グループ行で作成されたセクションの下にディレクトリ パスが表示されます。

![テキスト コントロールの静的テキスト情報](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "静的テキストを表示します。")<br />テキスト コントロールの静的テキスト情報

他のグループ化された領域が存在し、情報を格納するダイアログでは、読みやすさを向上させ、セクションを表示または表示できる場合 **([プロパティ] ウィンドウ**の説明ウィンドウのように) または類似の UI との整合性を保つ場合は、静的テキストをボックス内に配置します。 このグループ ボックスは、1 つのルールで、`ButtonShadow`で色付けされている必要があります。

![[プロパティ] ウィンドウの静的テキスト](../../extensibility/ux-guidelines/media/PropertiesWindow.png "プロパティウィンドウ.png")<br />[プロパティ] ウィンドウの静的テキスト

### <a name="read-only-text-box"></a>読み取り専用テキスト ボックス

これにより、ユーザーはフィールド内のテキストを選択できますが、編集はできません。 これらのテキスト ボックスは、`ButtonShadow`塗りつぶしを使用して通常の 3-D ノミに囲まれています。

ユーザーが関連付けられたコントロール (チェック ボックスのオン/オフ、ラジオ ボタンの選択/選択解除など) を変更すると、テキスト ボックスがアクティブ (編集可能) になることがあります。 たとえば、下に示す **[&gt;ツール オプション]** ページで、[既定の設定を**使用**] チェック ボックスがオフの場合、[**ホーム ページ**] テキスト ボックスがアクティブになります。

![非アクティブ状態とアクティブ状態を示す読み取り専用テキスト ボックス](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "読み取り専用テキスト ボックス.png")<br />非アクティブ状態とアクティブ状態を示す読み取り専用テキスト ボックス

### <a name="using-text-in-dialogs"></a>ダイアログでのテキストの使用

ダイアログ内のテキストに関する主なガイドライン:

- テーマに基づいて表示されていないダイアログボックスのテキストボックス、リストボックス、フレームのラベルは動詞で始まり、最初の単語にのみ初期の大文字が付き、コロンで終わります。

    > テーマを適用したダイアログのテキスト コントロールは[、Windows デスクトップの UX ガイドライン](/windows/desktop/uxguide/top-violations)に従い、ヘルプ リンクの疑問符を除いて、句読点を使用しません。

- チェック ボックスとオプション ボタンのラベルは動詞で始まり、先頭の単語の場合は先頭の大文字で始まり、句読点は含みなくなります。

- ボタン、メニュー、メニュー項目、およびタブのラベルには、各単語 (タイトルケース) の先頭の大文字が付いています。

- ラベルの用語は、他のダイアログの類似ラベルと一致している必要があります。

- 可能であれば、開発者にテキストを書き込むか承認してから実装を依頼してください。

- タブで十分な特別な状況を除き、すべてのコントロールにラベルを付ける必要があります。
必要に応じてヘルパー テキストを使用します。

### <a name="helper-text"></a>ヘルパー テキスト

ダイアログには、ユーザーがダイアログの目的を理解したり、実行するアクションを指定したりするための情報が含まれています。 ヘルパー テキストは、単純なダイアログを乱雑にしないようにするために必要な場合にのみ使用してください。 ヘルパー テキストの 2 つのバリエーションは、ダイアログとウォーターマークです。

ヘルパー テキストの一般的な場所に従い、新しい領域を導入する際に選択します。 ヘルパー テキストの一般的なシナリオは次のとおりです。

- ダイアログ内のヘルパー テキストで、複雑なダイアログと対話する方法に関する追加の指示を与えます。

- 空のツール ウィンドウまたはダイアログボックスのウォーターマークテキストで、コンテンツが表示されない理由を説明します。

- 説明ペイン **([プロパティ] ウィンドウ**の下部など)

- 空のエディタでウォーターマークテキストを使用して、ユーザーが開始するために実行する必要があるアクションを説明します。

### <a name="dialog-helper-text"></a>ダイアログ ヘルパー テキスト

ユーザー エクスペリエンス デザイナーは、ヘルパー テキストが適切かどうかを判断する際に役立ちます。 デザイナーは、ヘルパー テキストの表示場所と、その一般的なコンテンツを定義できます。 ユーザーアシスタンスは、実際のテキストを書き込み/編集できます。

### <a name="watermarks"></a>透かし

ダイアログには、わずかに異なるウォーターマークのガイドラインが用意されています。 ダイアログは、多くの UI 要素 (ラベル、ヒント テキスト、ボタン、テキストを含む他のコンテナー コントロール) でビジー状態に見えることがあるため、特に、黒`ButtonShadow`色で表示される場合、透かしは濃い灰色 (VSColor: ) で目立ちます。 通常、透かしは、白い背景を持つリスト ボックスのようなコントロール内に表示`Window`されます (VSColor: )。

- テキストは濃い灰色で表示されます (VSColor: `ButtonShadow`)。 ただし、透かしが中程度の灰色または他の色 (VSColor: `ButtonFace`) 背景に表示され、その読みやすさが懸念される場合は、黒`WindowText`のテキスト (VSColor: ) を使用します。

- 透かしは中央揃えまたは左揃えすることができます。 配置の決定を行う際に標準設計規則を適用する。 背景に透かしを選択することはできません。

![透かしテキストの例](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />透かしテキストの例

### <a name="context-specific-dynamic-text"></a>コンテキスト固有 (動的) テキスト

動的テキストは、ダイアログまたはモードレス UI で、動的ラベルとして、または動的コンテンツとして使用できます。

- ダイナミックラベル: ダイナミックテキストの一般的な使用は、右側のグリッドに表示される要素の要素とプロパティのリストを含むダイアログなど、選択した項目に関するより多くの情報を提供する説明パネルにあります。 プロパティ グリッドのラベルは動的に表示され、左側の項目を選択すると、右側のグリッドにその特定の項目の情報が表示されます。

- ダイナミック テキスト: この方法で一般的な情報ではなく特定の情報を表示する必要がある場合に役立ちますが、過度に使用しないように注意する必要があります。

ユーザーに情報をコピーする機能を持たされるようにするには、ダイナミック テキストを読み取り専用のテキスト フィールドに入力します。

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a>ボタンとハイパーリンク

### <a name="overview"></a>概要
ボタンとリンク コントロール (ハイパーリンク) は、使用法、文言、サイズ変更、および間隔[のハイパーリンクに関する Windows デスクトップの基本的なガイダンス](/windows/desktop/uxguide/ctrl-links)に従う必要があります。

### <a name="choosing-between-buttons-and-links"></a>ボタンとリンクの選択
従来、ボタンはアクションに使用され、ハイパーリンクはナビゲーション用に予約されていました。 ボタンは、すべての場合に使用できますが、Visual Studio では、ボタンとリンクの交換が可能な場合に、リンクの役割が拡張されています。

コマンド ボタンを使用する場合:

- プライマリ コマンド

- 入力の収集や選択に使用されるウィンドウの表示 (副次コマンドでも)

- 破壊的または不可逆的なアクション

- ウィザードおよびページ フロー内のコミットメント ボタン

ツール ウィンドウでコマンド ボタンを使用したり、ラベルに 3 つ以上の単語が必要な場合は、使用しないでください。 リンクのラベルは長くすることができます。

 リンクを使用する場合:

- 別のウィンドウ、ドキュメント、または Web ページへの移動

- アクションの意図を説明するために、より長いラベルまたは短い文を必要とする状況

- アクションが破壊的または不可逆的でない場合、ボタンが UI を圧倒する狭いスペース

- 多くのコマンドがある状況での 2 次コマンドの強調解除

#### <a name="examples"></a>使用例
![ステータス メッセージの後に表示される情報バーで使用されるコマンド リンク](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703-01_CommandLinkInfobar")<br />ステータス メッセージの後に表示される情報バーで使用されるコマンド リンク

![CodeLens ポップアップで使用されているリンク](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703-02_LinksInCodeLens")<br />CodeLens ポップアップで使用されているリンク

![ボタンがあまりに注目を集める二次コマンドに使用されるリンク](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")<br />ボタンがあまりに注目を集める二次コマンドに使用されるリンク

### <a name="common-buttons"></a>共通ボタン

#### <a name="text"></a>Text
[UI テキストと用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)の記述ガイドラインに従ってください。

#### <a name="visual-style"></a>視覚スタイル

##### <a name="standard-unthemed"></a>標準(テーマなし)
Visual Studio のほとんどのボタンはユーティリティ ダイアログに表示され、スタイルを設定しないでください。 オペレーティング システムによって指示されるボタンの標準的な外観を反映する必要があります。

##### <a name="themed"></a>テーマ
場合によっては、ボタンはスタイル付き UI 内で使用でき、これらのボタンは適切にスタイル設定する必要があります。 テーマ[コントロールの詳細については、「ダイアログ」](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)を参照してください。

### <a name="special-buttons"></a>特別なボタン

#### <a name="browse-buttons"></a>参照。。。ボタン
**[参照.]** ボタンは、グリッド、ダイアログ、ツール ウィンドウ、およびその他のモードレス UI 要素で使用されます。 ユーザーがコントロールに値を入力する際に使用するピッカーを表示します。 このボタンには、長いボタンと短い 2 つのバリエーションがあります。

![長い[参照..]ボタン](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703-04_BrowseLong")<br />長い[参照..]ボタン

![省略記号のみの短い [..] ボタン](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703-05_BrowseShort")<br />省略記号のみの短い [..] ボタン

省略記号のみの短いボタンを使用する場合:

- 複数のフィールドが閲覧を許可している場合のように、ダイアログに複数の長い **[Browse...]** ボタンがある場合。 この状況で作成される混乱を招くアクセス キーを避けるには、それぞれに対して短い **[..]** ボタンを使用します **(&参照**と**B&同**じダイアログの行)。

- タイトなダイアログで、または長いボタンを配置するための合理的な場所がない場合。

- ボタンがグリッド コントロールに表示される場合。

ボタンの使用に関するガイドライン:

- アクセスキーを使用しないでください。 キーボードを使用してアクセスするには、隣接するコントロールから Tab キーを押す必要があります。 タブ オーダーが、任意の参照ボタンがフィールドの直後に表示されるようにします。 最初のピリオドの下にアンダースコアを使用しないでください。

- Microsoft アクティブ アクセシビリティ (MSAA)**名**プロパティを**Browse...に**設定します。 マネージ コントロールの場合は **、"アクセス可能**" プロパティを設定します。

- 参照操作以外の場合は、省略記号 **[..]** ボタンを使用しないでください。 たとえば **、[New..]** ボタンが必要で、テキスト用の十分なスペースがない場合は、ダイアログを再設計する必要があります。

##### <a name="sizing-and-spacing"></a>サイズと間隔
![サイズ変更 [Browse..] ボタン: 標準バージョンは 75 x 23 ピクセル、ショート バージョンは 26x23 ピクセル](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703-06_BrowseSizing")<br />サイズ変更の [参照...] ボタン

![間隔 [Browse...] ボタン: 関連するコントロールと標準の参照ボタンの間隔 7 ピクセル、関連するコントロールと短い参照ボタンの間隔 5 ピクセル](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703-07_BrowseSpacing")<br />行間の [参照...] ボタン

#### <a name="graphical-buttons"></a>グラフィカルボタン
ボタンによっては、常にグラフィックイメージを使用し、スペースを節約し、ローカライズの問題を回避するためにテキストを含めない必要があります。 これらは、フィールド ピッカーやその他の並べ替え可能なリストでよく使用されます。

> [!NOTE]
> ユーザーはこれらのボタンにタブを移動する必要があるため(アクセスキーはありません)、賢明な順序でそれらを配置します。 スクリーン`name`リーダーがボタンアクションを正しく解釈できるように、ボタンのプロパティを、ボタンのアクションにマップします。

| 関数 | Button |
| --- | --- |
| 追加 | ![グラフィカルな [追加] ボタン](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703-08_ButtonAdd") |
| [削除] | ![グラフィカルな [削除] ボタン](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703-09_ButtonRemove") |
| [すべてを追加] | ![グラフィカルな [すべて追加] ボタン](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703-10_ButtonAddAll") |
| [すべて削除] | ![グラフィカルな [すべて削除] ボタン](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703-11_ButtonRemoveAll") |
| [上へ移動] | ![グラフィカルな [上へ移動] ボタン](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703-12_ButtonMoveUp") |
| [上へ移動] | ![グラフィカルな [下へ移動] ボタン](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703-13_ButtonMoveDown") |
| 削除 | ![グラフィカルな [消去] ボタン](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703-14_ButtonDelete") |

##### <a name="sizing-and-spacing"></a>サイズと間隔
グラフィカルボタンのサイズは **、[Browse..]** ボタンの短いバージョン(26x23ピクセル)の場合と同じです。

![ボタン上のグラフィックイメージの外観、透明な色の有無](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")<br />ボタン上のグラフィックイメージの外観、透明な色の有無

### <a name="hyperlinks"></a>ハイパーリンク
ハイパーリンクは、ヘルプ トピック、モーダル ダイアログ、ウィザードを開くなどのナビゲーションベースのアクションに適しています。 コマンドにハイパーリンクを使用する場合は、UI に対して常に目に見える変更が表示されます。 一般に、アクションにコミットするアクション (保存、キャンセル、削除など) は、ボタンを使用してより適切に伝達されます。

#### <a name="writing-style"></a>記述スタイル
ユーザー[インターフェイスのテキストに関する Windows デスクトップのガイダンスに](/windows/desktop/uxguide/text-ui)従ってください。 「詳細」「詳細を教えてください」「これについて助けを得る」という言い回しを使用しないでください。 代わりに、ヘルプ コンテンツが回答する主な質問に関して、ヘルプ リンク テキストを使用します。 たとえば、サーバー**エクスプローラにサーバーを追加する方法を説明します**。

#### <a name="visual-style"></a>視覚スタイル

- ハイパーリンクは常に[VSColor サービスを](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)使用する必要があります。 ハイパーリンクのスタイルが正しく設定されていない場合は、アクティブなときに赤く点滅するか、表示後に別の色で表示されます。

- リンクが透かしのように完全な文の中の文の断片でない限り、コントロールの静止状態に下線を含めないでください。

- 下線は、ホバーに表示されません。 代わりに、リンクがアクティブであるというユーザーへのフィードバックは、わずかな色の変更と適切なリンクカーソルです。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a>ツリービュー

ツリービューは、複雑なリストを親子グループに整理する方法を提供します。 ユーザーは、親グループを展開したり折りたたんだりして、基になる子項目を表示または非表示にできます。 ツリー ビュー内の各項目を選択して、さらにアクションを実行できます。

### <a name="tree-view-visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a>ツリー ビューのビジュアル スタイル

#### <a name="expanders"></a>エキスパンダー
ツリー ビュー コントロールは、Windows および Visual Studio で使用されるエキスパンダー デザインに準拠する必要があります。 各ノードは、展開コントロールを使用して、基になる項目を表示または非表示にします。 展開コントロールを使用すると、Windows と Visual Studio 内で異なるツリー ビューが発生する可能性があるユーザーに一貫性が提供されます。

![正しい: 展開コントロールを使用したツリー ビュー ノードの適切なスタイル](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正しい: 展開コントロールを使用したツリー ビュー ノードの適切なスタイル

![正しくない: ツリー ビュー ノードの不適切なスタイル](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705-2_TreeViewIncorrect1")<br />正しくない: ツリー ビュー ノードの不適切なスタイル

#### <a name="selection"></a>[選択]
ツリー ビュー内でノードを選択すると、ツリー ビュー コントロールの全幅にハイライトが展開されます。 これにより、ユーザーは選択したアイテムを明確に識別できます。 選択色は、現在の Visual Studio テーマを反映している必要があります。

![正しい: 選択したノードのハイライトは、ツリー ビュー コントロールの幅全体に適合します。](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正しい: 選択したノードのハイライトは、ツリー ビュー コントロールの幅全体に適合します。

![正しくない: 選択したノードの強調表示がツリー ビュー コントロールの幅全体に収まりません。](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705-3_TreeViewIncorrect2")<br />正しくない: 選択したノードの強調表示がツリー ビュー コントロールの幅全体に収まりません。

#### <a name="icons"></a>[小さいアイコン]
アイコンは、項目間の違いを視覚的に識別する場合にのみ、ツリー ビュー コントロールで使用してください。 一般に、アイコンは要素の種類を区別するために情報を伝達する異種リストでのみ使用する必要があります。 同種のリストでは、アイコンを使用するとノイズと見なされることが多く、避けるべきです。 その場合、グループアイコン(親)は、その中のアイテムの種類を伝えることができます。 このルールの例外は、アイコンが動的で、状態を示すために使用される場合です。

#### <a name="scroll-bars"></a>スクロール バー
コンテンツがツリー ビュー コントロール内に収まる場合は、スクロール バーは常に非表示にする必要があります。 スクロール バーを非表示にしたり、スクロール可能なウィンドウで半透明にしたりしてもかまいません。

![内容がツリー ビュー コントロールの制限を超えているため、垂直スクロール バーと水平スクロール バーの両方が表示されます。](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705-4_Scrollbars")<br />内容がツリー ビュー コントロールの制限を超えているため、垂直スクロール バーと水平スクロール バーの両方が表示されます。

### <a name="tree-view-interactions"></a><a name="BKMK_TreeViewInteractions"></a>ツリー ビューの相互作用

#### <a name="context-menus"></a>コンテキスト メニュー
ツリー ビュー ノードは、コンテキスト メニューのサブメニュー オプションを表示できます。 通常、この現象は、ユーザーが項目を右クリックした場合、または項目が選択されている状態で Windows キーボードの Menu キーを押した場合に発生します。 ノードがフォーカスを得て選択することが重要です。 これにより、サブメニューが属する項目をユーザーが識別できます。

![コンテキスト メニューを生成した項目は、選択された項目をユーザーに通知するフォーカスを得ます。](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705-5_ContextMenu")<br />コンテキスト メニューを生成した項目は、選択された項目をユーザーに通知するフォーカスを得ます。

#### <a name="keyboard"></a>キーボード
ツリー ビューでは、項目を選択したり、キーボードを使用してノードを展開/折りたたみしたりできます。 これにより、ナビゲーションがアクセシビリティ要件を満たしていることを確認できます。

##### <a name="tree-view-control"></a>ツリー ビュー コントロール
Visual Studio のツリー コントロールは、一般的なキーボード ナビゲーションに従う必要があります。

- **上矢印:** ツリーを上に移動して項目を選択する

- **下矢印:** ツリーを下に移動して項目を選択する

- **右矢印:** ツリー内のノードを展開する

- **左矢印:** ツリー内のノードを折りたたむ

- **キーを入力:** 選択した項目の開始、読み込み、実行

##### <a name="trid-tree-view-and-grid-view"></a>Trid (ツリー ビューとグリッド ビュー)
Trid コントロールは、グリッド内のツリー ビューを含む複雑なコントロールです。 ツリーの展開、折りたたみ、および移動は、ツリー ビューと同じキーボード コマンドを考慮し、次の追加機能を使用する必要があります。

- **右矢印:** ノードを展開します。 ノードが展開された後、右側の最も近い列に移動し続ける必要があります。 ナビゲーションは行の最後で停止します。

- **タブ:** 右側の最も近いセルに移動します。  行の最後に移動すると、次の行に移動します。

- **シフト + タブ:** 左側の最も近いセルに移動します。  行の先頭では、移動は前の行の右端のセルに移動し続けます。

![ビジュアル スタジオのコントロールをトリド](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705-6_Trid")<br />ビジュアル スタジオのコントロールをトリド
