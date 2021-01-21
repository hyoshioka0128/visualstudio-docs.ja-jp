---
title: Visual Studio のコモンコントロールパターン |Microsoft Docs
description: Visual Studio の一般的なコントロールが Windows デスクトップの対話ガイドラインに従う方法と、それらのガイドラインを拡張する特殊な状況について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3c1caccebf1dc14146bef214a4d33e1216243780
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715887"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio の コモン コントロール パターン
## <a name="common-controls"></a><a name="BKMK_CommonControls"></a> コモンコントロール

### <a name="overview"></a>概要
一般的なコントロールは、Visual Studio のユーザーインターフェイスの大部分を構成します。 Visual Studio インターフェイスで使用される最も一般的なコントロールは、 [Windows デスクトップの相互作用ガイドライン](/windows/desktop/uxguide/controls)に従う必要があります。 このトピックは、Visual Studio に固有のものであり、これらの Windows のガイドラインを補強する特別な状況や詳細について説明しています。

#### <a name="common-controls-in-this-topic"></a>このトピックの一般的なコントロール

- [スクロールバー](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [入力フィールド](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [コンボボックスとドロップダウンリスト](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [チェック ボックス](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [ラジオ ボタン](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [フレームのグループ化](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [テキスト コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [ボタンとハイパーリンク](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [ツリー ビュー](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>視覚スタイル
コントロールをスタイル設定するときに最初に考慮すべきことは、コントロールがテーマ付き UI で使用されるかどうかです。 標準 UI のコントロールは、テーマが適用されていない UI であり、 [通常の Windows デスクトップスタイル](/windows/desktop/uxguide/controls)に従う必要があります。つまり、テンプレートは再テンプレート化されず、既定のコントロールの外観で表示されます。

- **標準 (ユーティリティ) のダイアログ:** テーマがありません。 再テンプレートしないでください。 基本的なコントロールスタイルの既定値を使用します。

- **ツールウィンドウ、ドキュメントエディター、デザインサーフェイス、およびテーマ付きダイアログ:** カラーサービスを使用して、特別にテーマを設定した外観を使用します。

### <a name="scroll-bars"></a><a name="BKMK_Scrollbars"></a> スクロールバー
 スクロールバーは、コードエディターなどのコンテンツ情報で拡張されている場合を除き、 [Windows のスクロールバーの一般的な対話パターン](/windows/desktop/Controls/about-scroll-bars) に従う必要があります。

### <a name="input-fields"></a><a name="BKMK_InputFields"></a> 入力フィールド
 一般的な対話動作の場合は、 [Windows デスクトップのガイドラインに従ってテキストボックスを](/windows/desktop/uxguide/ctrl-text-boxes)表示します。

#### <a name="visual-style"></a>視覚スタイル

- 入力フィールドのスタイルをユーティリティダイアログで設定することはできません。 コントロールに固有の基本スタイルを使用します。

- テーマ付きの入力フィールドは、テーマ付きダイアログとツールウィンドウでのみ使用してください。

#### <a name="specialized-interactions"></a>特化された対話

- 読み取り専用フィールドには灰色 (無効) の背景がありますが、既定 (アクティブ) の前景が使用されます。

- 必須フィールドには **\<Required>** 、ウォーターマークとしてを含める必要があります。 まれな状況を除いて、背景色を変更しないでください。

- エラーの検証: 「 [Visual Studio の通知と進行状況」を](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)参照してください。

- 入力フィールドは、コンテンツに合わせてサイズを調整する必要があります。表示されるウィンドウの幅に合わせることはできません。また、パスのように、長いフィールドの長さと任意に一致させることもできません。 長さは、フィールドで使用できる文字数に制限があることをユーザーに示すことがあります。

     ![入力フィールドの長さが正しくありません: 名前が長すぎる可能性があります。](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")<br />入力フィールドの長さが正しくありません: 名前が長すぎる可能性があります。

     ![入力フィールドの長さの修正: 入力フィールドは、予期されるコンテンツの幅として適切です。](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")<br />入力フィールドの長さの修正: 入力フィールドは、予期されるコンテンツの幅として適切です。

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a> コンボボックスとドロップダウンリスト
一般的な対話動作の場合は、「 [Windows デスクトップのガイドライン」のドロップダウンリストとコンボボックスに](/windows/desktop/uxguide/ctrl-drop)従います。

#### <a name="visual-style"></a>視覚スタイル

- ユーティリティダイアログでは、コントロールを再テンプレートしないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ付き UI では、コンボボックスとドロップダウンは、コントロールの標準のテーマに従います。

#### <a name="layout"></a>Layout
コンボボックスとドロップダウンは、コンテンツに合わせてサイズを調整する必要があります。これは、表示されているウィンドウの幅に合わせることはできません。また、パスのように、長いフィールドの長さと任意に一致させることもできません。

![正しくない: ドロップダウンの幅が、表示されるコンテンツに対して長すぎます。](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")<br />正しくない: ドロップダウンの幅が、表示されるコンテンツに対して長すぎます。

![[修正]: ドロップダウンは、翻訳の増加に対応するようにサイズ変更されますが、不必要に長くなることはありません。](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707-04_CorrectDropDownLayout")<br />[修正]: ドロップダウンは、翻訳の増加に対応するようにサイズ変更されますが、不必要に長くなることはありません。

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a> チェックボックス
一般的な対話動作の場合は、 [Windows デスクトップのガイドライン](/windows/desktop/uxguide/ctrl-check-boxes)に従ってチェックボックスをオンにします。

#### <a name="visual-style"></a>視覚スタイル

- ユーティリティダイアログでは、コントロールを再テンプレートしないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ付き UI では、チェックボックスはコントロールの標準テーマに従います。

#### <a name="specialized-interactions"></a>特化された対話

- チェックボックスとの対話は、ダイアログをポップしたり、別の領域に移動したりすることはできません。

- チェックボックスをテキストの最初の行のベースラインに揃えます。

     ![[正しくない]: チェックボックスは、テキストの中央に表示されます。](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")<br />[正しくない]: チェックボックスは、テキストの中央に表示されます。

     ![[修正]: チェックボックスは、テキストの最初の行に合わせて調整されます。](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")<br />[修正]: チェックボックスは、テキストの最初の行に合わせて調整されます。

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a> オプションボタン
一般的な対話動作の場合は、 [Windows デスクトップのガイドライン](/windows/desktop/uxguide/ctrl-radio-buttons)に従ってラジオボタンを使用します。

#### <a name="visual-style"></a>視覚スタイル
ユーティリティダイアログでは、オプションボタンをスタイルを適用しません。 コントロールに固有の基本スタイルを使用します。

#### <a name="specialized-interactions"></a>特化された対話
グループの区別を密なレイアウトで維持する必要がある場合を除き、オプションの選択を囲むためにグループフレームを使用する必要はありません。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a> フレームのグループ化
一般的な相互作用の動作については、「 [グループフレームの Windows デスクトップガイドライン](/windows/desktop/uxguide/ctrl-group-boxes)」に従ってください。

#### <a name="visual-style"></a>視覚スタイル
ユーティリティダイアログでは、グループフレームをスタイル化しないでください。 コントロールに固有の基本スタイルを使用します。

#### <a name="layout"></a>Layout

- グループの区別を密なレイアウトで維持する必要がある場合を除き、オプションの選択を囲むためにグループフレームを使用する必要はありません。

- 1つのコントロールにはグループフレームを使用しないでください。

- グループフレームコンテナーではなく、水平方向の規則を使用することが許容される場合があります。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a> テキストコントロール

### <a name="static-text-fields"></a>静的テキストフィールド

静的テキストフィールドには読み取り専用の情報が表示され、ユーザーが選択することはできません。 ユーザーがクリップボードにコピーする可能性のあるテキストには使用しないでください。 ただし、読み取り専用の静的テキストは、状態の変化を反映するように変更される可能性があります。 次の例では、情報グループの下にある [出力名] の静的テキストが、その上にある [ルート名前空間] テキストボックスに加えられた変更を反映するように変更されています。

静的テキスト情報を表示するには、2つの方法があります。

静的テキストは、グループ化の競合がない場合でも、ダイアログ内で単独で使用できます。 ボックスの余分な行が本当に必要かどうかを判断します。 例として、次に示すように、グループ行によって作成されたセクションの下にディレクトリパスを表示します。

![テキストコントロールの静的なテキスト情報](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "DisplayingStaticText.png")<br />テキストコントロールの静的なテキスト情報

他のグループ化された領域が存在し、情報の含有が読みやすくなるダイアログで、セクションを表示または非表示にする ( **プロパティウィンドウ** 説明ウィンドウなど) 場合、または同様の UI との一貫性を維持する場合は、静的テキストをボックス内に配置します。 このグループボックスは1つのルールで、次のように色分けされてい `ButtonShadow` ます。

![プロパティウィンドウ内の静的なテキスト](../../extensibility/ux-guidelines/media/PropertiesWindow.png "PropertiesWindow.png")<br />プロパティウィンドウ内の静的なテキスト

### <a name="read-only-text-box"></a>読み取り専用テキストボックス

これにより、ユーザーはフィールド内のテキストを選択できますが、編集することはできません。 これらのテキストボックスには、通常の 3-d chisel と塗りつぶしの境界線が表示され `ButtonShadow` ます。

ユーザーが関連付けられたコントロールを変更すると、テキストボックスがアクティブ (編集可能) になることがあります。たとえば、チェックボックスのオン/オフを選択したり、オプションボタンを選択/選択解除したりすることができます。 たとえば、次に示す [**ツール &gt; オプション**] ページで、[**既定値を使用**] チェックボックスをオフにした場合、[**ホームページ**] テキストボックスはアクティブになります。

![非アクティブ状態とアクティブな状態を示す読み取り専用のテキストボックス](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "ReadOnlyTextBox.png")<br />非アクティブ状態とアクティブな状態を示す読み取り専用のテキストボックス

### <a name="using-text-in-dialogs"></a>使用 (テキストをダイアログで)

ダイアログボックスのテキストの主要なガイドライン:

- テーマが設定されていないダイアログ内のテキストボックス、リストボックス、およびフレームのラベルは、動詞で始まり、最初の単語の最初の大文字のみで、コロンで終わります。

    > テーマ付きダイアログのテキストコントロールは、 [Windows デスクトップ UX のガイドライン](/windows/desktop/uxguide/top-violations) に従います。また、ヘルプリンク内の疑問符を除き、末尾の区切りは行われません。

- チェックボックスおよびオプションボタンのラベルは、動詞、最初の単語の最初の大文字、および末尾の区切り記号を使用しません。

- ボタン、メニュー、メニュー項目、およびタブのラベルには、各単語の最初の大文字 (タイトルケース) があります。

- ラベルの用語は、他のダイアログの類似するラベルと一致している必要があります。

- 可能であれば、開発者が実装する前に、ライターまたはエディターにテキストを書き込みまたは承認してください。

- Tab キーを使用するだけで十分な場合を除き、すべてのコントロールにラベルを付ける必要があります。
必要に応じてヘルパーテキストを使用します。

### <a name="helper-text"></a>ヘルパーテキスト

ダイアログに含まれており、ユーザーがダイアログの目的を理解したり、実行するアクションを指定したりできるようにします。 ヘルパーテキストは、煩雑なダイアログを避けるために必要な場合にのみ使用してください。 ヘルパーテキストには、ダイアログとウォーターマークの2種類があります。

ヘルパーテキストの一般的な場所に従い、新しい領域の導入を選択できます。 ヘルパーテキストの一般的なシナリオは次のとおりです。

- ダイアログ内のヘルパーテキスト。複雑なダイアログとの対話方法について、追加の方向を指定します。

- 空のツールウィンドウまたはダイアログのウォーターマークテキスト。コンテンツが表示されない理由を説明します。

- **プロパティウィンドウ** の下部にあるような説明ペイン。

- 空のエディターで透かしテキストを使用して、ユーザーが作業を開始するためにどのようなアクションを実行する必要があるかを説明します。

### <a name="dialog-helper-text"></a>ダイアログ ヘルパー テキスト

ユーザーエクスペリエンスデザイナーは、ヘルパーテキストが適切であるかどうかを判断するのに役立ちます。 デザイナーでは、ヘルパーテキストの表示場所、およびその一般的なコンテンツを定義できます。 ユーザーアシスタンスは、実際のテキストを作成/編集できます。

### <a name="watermarks"></a>透かし

ダイアログでは、ウォーターマークのガイドラインが若干異なります。 ダイアログは多くの UI 要素 (ラベル、ヒントテキスト、ボタン、およびテキストを使用するコンテナーコントロール) でビジー状態で表示されることがあるため、特に黒で表示されている場合は、ウォーターマークが濃い灰色 (VSColor:) の方が優れて `ButtonShadow` います。 通常、ウォーターマークは、白い背景 (VSColor:) のリストボックスなどのコントロール内に表示され `Window` ます。

- テキストが濃い灰色 (VSColor:) で表示され `ButtonShadow` ます。 ただし、ウォーターマークがグレーまたは他の色 (VSColor:) の背景に表示され、 `ButtonFace` 読みやすさに懸念がある場合は、黒のテキスト (vscolor:) を使用してください `WindowText` 。

- 透かしは、中央揃えにすることも、左にフラッシュすることもできます。 配置に関する決定を行うときに、標準のデザイン規則を適用します。 背景で透かしを選択することはできません。

![透かしテキストの例](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />透かしテキストの例

### <a name="context-specific-dynamic-text"></a>コンテキスト固有の (動的な) テキスト

動的テキストは、ダイアログまたはモードレス UI の2つの方法のいずれかで使用できます。動的なラベルとして、または動的なコンテンツとして使用できます。

- 動的ラベル: 動的テキストの一般的な使用方法は、選択した項目の詳細を示す説明的なパネルです。たとえば、ダイアログボックスには、右側のグリッドに表示される要素の要素とプロパティの一覧が含まれています。 プロパティグリッドのラベルは動的な場合があるため、左側の項目を選択すると、右側のグリッドにその特定の項目の情報が表示されます。

- 動的テキスト: この方法では、特定の情報を表示する必要があるが、一般的な情報は表示しない場合に便利ですが、使用しないように注意する必要があります。

ユーザーが情報をコピーできるようにするには、動的テキストが読み取り専用のテキストフィールドに含まれている必要があります。

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a> ボタンとハイパーリンク

### <a name="overview"></a>概要
ボタンとリンクコントロール (ハイパーリンク) は、使用、表現、サイズ変更、およびスペースの [ハイパーリンクに関する基本的な Windows デスクトップガイダンス](/windows/desktop/uxguide/ctrl-links) に従う必要があります。

### <a name="choosing-between-buttons-and-links"></a>ボタンとリンクの選択
従来、操作にはボタンが使用されており、ハイパーリンクはナビゲーション用に予約されていました。 ボタンはどのような場合でも使用できますが、一部の条件では、ボタンとリンクが置き換えられるように、Visual Studio でリンクの役割が拡張されています。

コマンドボタンを使用する場合:

- 主なコマンド

- 入力の収集または選択を行うために使用されるウィンドウの表示 (セカンダリコマンドの場合でも)

- 破棄または元に戻す操作

- ウィザードとページフロー内のコミットメントボタン

ツールウィンドウではコマンドボタンを使用しないようにし、ラベルには3つ以上の単語が必要な場合は使用しないようにします。 リンクのラベルが長くなる可能性があります。

 リンクを使用する場合:

- 別のウィンドウ、ドキュメント、または web ページへの移動

- アクションの目的を説明するために長いラベルまたは短い文が必要な状況

- アクションが破壊的または元に戻せない場合に、ボタンが UI の過負荷になるスペース

- 多数のコマンドが存在する状況でのセカンダリコマンドの強調を解除する

#### <a name="examples"></a>例
![ステータスメッセージの後に情報バーで使用されるコマンドリンク](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703-01_CommandLinkInfobar")<br />ステータスメッセージの後に情報バーで使用されるコマンドリンク

![CodeLens ポップアップで使用されているリンク](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703-02_LinksInCodeLens")<br />CodeLens ポップアップで使用されているリンク

![ボタンがあまり注意を払わないセカンダリコマンドに使用されるリンク](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")<br />ボタンがあまり注意を払わないセカンダリコマンドに使用されるリンク

### <a name="common-buttons"></a>共通ボタン

#### <a name="text"></a>Text
[UI のテキストと用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)の記述に関するガイドラインに従ってください。

#### <a name="visual-style"></a>視覚スタイル

##### <a name="standard-unthemed"></a>標準 (テーマなし)
Visual Studio のほとんどのボタンはユーティリティダイアログに表示され、スタイルを設定することはできません。 これらは、オペレーティングシステムで指定されているように、標準のボタンの外観を反映している必要があります。

##### <a name="themed"></a>テーマ
場合によっては、スタイル設定された UI 内でボタンが使用され、これらのボタンのスタイルを適切に設定する必要があります。 テーマ付きコントロールの詳細については、 [ダイアログ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) を参照してください。

### <a name="special-buttons"></a>特別なボタン

#### <a name="browse-buttons"></a>参照...83'7b
**[参照...]** ボタンは、グリッド、ダイアログ、ツールウィンドウ、およびその他のモードレス UI 要素で使用されます。 ユーザーがコントロールに値を入力するのを支援するピッカーが表示されます。 このボタンには、長い形式と短い形式の2種類があります。

![長い [Browse...] ボタン](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703-04_BrowseLong")<br />長い [Browse...] ボタン

![省略記号 ([...]) ボタン](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703-05_BrowseShort")<br />省略記号 ([...]) ボタン

省略記号の省略ボタンを使用する場合:

- 複数のフィールドで閲覧が許可されている場合など、ダイアログに長い **[参照** ] ボタンが複数ある場合。 この状況によって作成されたわかりにくいアクセスキーを回避するには、それぞれの **[...]** ボタンを使用します (**&参照** ] をクリックし、同じダイアログで **B&r)** を選択します)。

- ダイアログボックスが短い場合、または長いボタンを配置するための適切な場所がない場合。

- ボタンがグリッドコントロールに表示される場合は。

ボタンを使用するためのガイドライン:

- アクセスキーは使用しないでください。 キーボードを使用してアクセスするには、ユーザーが隣接するコントロールから tab キーを押す必要があります。 タブの順序が、すべての参照ボタンが、入力するフィールドの直後になるようにしてください。 最初の期間の下にアンダースコアを使用しないでください。

- "ドット-ドット" または "ピリオド-ピリオド" ではなく "参照" としてスクリーンリーダーが読み取るように、Microsoft Active Accessibility (MSAA) **名** プロパティを [ **参照** ] (省略記号を含む) に設定します。 マネージコントロールの場合、これは **AccessibleName** プロパティを設定することを意味します。

- 参照操作以外のすべてに対して、省略記号 **[...]** ボタンを使用しないでください。 たとえば、 **[新規...]** ボタンが必要で、テキスト用の十分な空き領域がない場合は、ダイアログを再設計する必要があります。

##### <a name="sizing-and-spacing"></a>サイズと間隔
![サイズ変更 [参照...] ボタン: 標準バージョンは 75 x 23 ピクセル、短いバージョンは26x23 ピクセル](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703-06_BrowseSizing")<br />サイズ変更の [参照...] ボタン

![スペーシング [参照...] ボタン: 関連するコントロールと標準の参照ボタンの間の間隔7ピクセル、関連するコントロールと短い参照ボタンの間の間隔5ピクセル](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703-07_BrowseSpacing")<br />行間の [参照...] ボタン

#### <a name="graphical-buttons"></a>グラフィカルボタン
一部のボタンでは、常にグラフィックイメージを使用し、領域を節約し、ローカライズの問題を回避するためのテキストは含めないようにする必要があります。 これらは、フィールドピッカーやその他の並べ替え可能なリストでよく使用されます。

> [!NOTE]
> ユーザーはこれらのボタン (アクセスキーがない) にタブを設定する必要があるため、適切な順序で配置します。 `name`ボタンのプロパティを、スクリーンリーダーがボタンの操作を正しく解釈するために実行するアクションにマップします。

| 機能 | Button |
| --- | --- |
| 追加 | ![グラフィカルな [追加] ボタン](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703-08_ButtonAdd") |
| 削除 | ![グラフィカルな [削除] ボタン](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703-09_ButtonRemove") |
| [すべてを追加] | ![グラフィカルな [すべて追加] ボタン](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703-10_ButtonAddAll") |
| [すべて削除] | ![グラフィカルな [すべて削除] ボタン](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703-11_ButtonRemoveAll") |
| [上へ移動] | ![グラフィカルな [上へ移動] ボタン](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703-12_ButtonMoveUp") |
| [上へ移動] | ![グラフィカルな [下へ移動] ボタン](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703-13_ButtonMoveDown") |
| 削除 | ![グラフィカルな [消去] ボタン](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703-14_ButtonDelete") |

##### <a name="sizing-and-spacing"></a>サイズと間隔
グラフィカルボタンのサイズ変更は、 **[参照** ] ボタン (2 ~ 23 ピクセル) の短いバージョンの場合と同じです。

![透明色が表示され、透明色が表示されていない、ボタンのグラフィックイメージの外観](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")<br />透明色が表示され、透明色が表示されていない、ボタンのグラフィックイメージの外観

### <a name="hyperlinks"></a>ハイパーリンク
ハイパーリンクは、ヘルプトピック、モーダルダイアログ、ウィザードを開くなど、ナビゲーションベースのアクションに適しています。 ハイパーリンクがコマンドに使用されている場合は、UI に対して常に表示され、顕著な変更が表示されます。 一般に、アクションにコミットされるアクション (保存、キャンセル、削除など) は、ボタンを使用してより適切に伝達されます。

#### <a name="writing-style"></a>記述スタイル
[ユーザーインターフェイスのテキストについては、Windows デスクトップのガイダンス](/windows/desktop/uxguide/text-ui)に従ってください。 詳細については、「詳細情報」、「詳細を表示する」、または「この言い回しについてのヘルプ」を参照してください。 代わりに、ヘルプコンテンツによって回答される主な質問に関して、語句のヘルプをリンクします。 たとえば、"**操作方法サーバーエクスプローラーにサーバーを追加しますか?**" というようになります。

#### <a name="visual-style"></a>視覚スタイル

- ハイパーリンクでは、常に [VSColor サービス](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)を使用する必要があります。 ハイパーリンクのスタイルが正しく設定されていない場合、アクティブなときは赤が点滅し、表示された後に別の色が表示されます。

- ウォーターマークのような完全な文内の文フラグメントである場合を除いて、コントロールの状態の下に下線を入れないでください。

- ホバー時に下線を表示することはできません。 代わりに、リンクがアクティブになっていることをユーザーにフィードバックすると、色が少し変更され、適切なリンクカーソルが設定されます。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a> ツリービュー

ツリービューを使用すると、複雑なリストを親子グループにまとめることができます。 ユーザーは、親グループを展開または折りたたむことで、基になる子項目を表示または非表示にすることができます。 ツリービュー内の各項目は、さらにアクションを提供するように選択できます。

### <a name="tree-view-visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a> ツリービューの視覚スタイル

#### <a name="expanders"></a>展開コントロール
ツリービューコントロールは、Windows および Visual Studio で使用されるエキスパンダーデザインに準拠している必要があります。 各ノードは、エキスパンダーコントロールを使用して、基になる項目を表示または非表示にします。 エキスパンダーコントロールを使用すると、Windows と Visual Studio 内で異なるツリービューが発生する可能性があるユーザーに一貫性が確保されます。

![修正: エキスパンダーコントロールを使用する正しいスタイルのツリービューノード](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />修正: エキスパンダーコントロールを使用する正しいスタイルのツリービューノード

![正しくない: ツリービューノードのスタイルが正しくありません](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705-2_TreeViewIncorrect1")<br />正しくない: ツリービューノードのスタイルが正しくありません

#### <a name="selection"></a>選択
ツリービュー内でノードを選択すると、ツリービューコントロールの幅全体に強調表示されます。 これは、ユーザーが選択した項目を明確に識別するのに役立ちます。 選択した色は、現在の Visual Studio テーマを反映している必要があります。

![[修正]: 選択したノードの強調表示は、ツリービューコントロールの幅全体に一致します。](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />[修正]: 選択したノードの強調表示は、ツリービューコントロールの幅全体に一致します。

![正しくない: 選択したノードの強調表示が、ツリービューコントロールの幅全体に一致しません。](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705-3_TreeViewIncorrect2")<br />正しくない: 選択したノードの強調表示が、ツリービューコントロールの幅全体に一致しません。

#### <a name="icons"></a>アイコン
項目間の相違点を視覚的に識別するのに役立つ場合は、ツリービューコントロールでのみアイコンを使用する必要があります。 一般に、アイコンは、要素の種類を区別するための情報が含まれている異種リストでのみ使用する必要があります。 同種のリストでは、アイコンを使用することがしばしばノイズと見なされ、回避する必要があります。 その場合、グループアイコン (親) は、その中の項目の種類を伝えることができます。 このルールの例外は、アイコンが動的で、状態を示すために使用される場合です。

#### <a name="scroll-bars"></a>スクロール バー
ツリービューコントロール内にコンテンツが収まる場合は、スクロールバーを常に非表示にする必要があります。 スクロールバーを非表示にしたり、スクロール可能なウィンドウで半透明にしたり、ツリービューを含むウィンドウにフォーカスがあるとき、またはツリービュー自体の上にマウスポインターを置いたときに表示されるようにすることもできます。

![コンテンツがツリービューコントロールの制限を超えているため、垂直スクロールバーと水平スクロールバーの両方が表示されます。](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705-4_Scrollbars")<br />コンテンツがツリービューコントロールの制限を超えているため、垂直スクロールバーと水平スクロールバーの両方が表示されます。

### <a name="tree-view-interactions"></a><a name="BKMK_TreeViewInteractions"></a> ツリービューの相互作用

#### <a name="context-menus"></a>コンテキスト メニュー
ツリービューノードは、ショートカットメニューのサブメニューオプションを表示できます。 通常、このエラーは、ユーザーが項目を右クリックしたとき、または項目が選択された状態で Windows キーボードのメニューキーを押したときに発生します。 ノードがフォーカスを取得し、選択されていることが重要です。 これにより、サブメニューが属する項目をユーザーが識別できるようになります。

![コンテキストメニューを生成した項目は、選択された項目をユーザーに通知するためにフォーカスを取得します。](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705-5_ContextMenu")<br />コンテキストメニューを生成した項目は、選択された項目をユーザーに通知するためにフォーカスを取得します。

#### <a name="keyboard"></a>キーボード
ツリービューでは、キーボードを使用して項目を選択し、ノードを展開または折りたたむことができます。 これにより、ナビゲーションはユーザー補助の要件を満たします。

##### <a name="tree-view-control"></a>ツリービューコントロール
Visual Studio のツリーコントロールは、一般的なキーボードナビゲーションに従う必要があります。

- **↑:** ツリーを上に移動して項目を選択する

- **下方向キー:** ツリーの下へ移動して項目を選択する

- **右矢印:** ツリー内のノードを展開します。

- **←:** ツリー内のノードを折りたたむ

- **キーの入力:** 選択した項目の開始、読み込み、実行

##### <a name="trid-tree-view-and-grid-view"></a>Trid (ツリービューおよびグリッドビュー)
Trid コントロールは、グリッド内のツリービューを含む複雑なコントロールです。 ツリーの展開、折りたたみ、および移動を行うには、ツリービューと同じキーボードコマンドを使用する必要があります。次の追加機能があります。

- **右矢印:** ノードを展開します。 ノードが展開されると、右側の最も近い列に移動し続けます。 移動は、行の最後に停止します。

- **Tab:** 右側の最も近いセルに移動します。  行の末尾で、ナビゲーションは次の行に進みます。

- **Shift + Tab:** 左側の最も近いセルに移動します。  行の先頭では、前の行の一番右のセルに移動します。

![Visual Studio の trid コントロール](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705-6_Trid")<br />Visual Studio の trid コントロール
