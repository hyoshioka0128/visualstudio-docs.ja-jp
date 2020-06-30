---
title: コモン コントロール パターン
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dd2b2723a5ecfe66e9471cfea1e8eb55ed7ced59
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547447"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio の コモン コントロール パターン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="common-controls"></a><a name="BKMK_CommonControls"></a>コモンコントロール

### <a name="overview"></a>概要
 一般的なコントロールは、Visual Studio のユーザーインターフェイスの大部分を構成します。 Visual Studio インターフェイスで使用される最も一般的なコントロールは、 [Windows デスクトップの相互作用ガイドライン](https://msdn.microsoft.com/library/windows/desktop/dn742399.aspx)に従う必要があります。 このドキュメントは、Visual Studio に固有のものであり、これらの Windows のガイドラインを補強する特別な状況や詳細について説明しています。

#### <a name="common-controls-in-this-topic"></a>このトピックの一般的なコントロール

- [バー](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [入力フィールド](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [コンボボックスとドロップダウンリスト](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [チェック ボックス](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [ラジオ ボタン](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [フレームのグループ化](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [テキスト コントロール](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [ボタンとハイパーリンク](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [ツリー ビュー](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>視覚スタイル
 コントロールをスタイル設定するときに最初に考慮すべきことは、コントロールがテーマ付き UI で使用されるかどうかです。 標準 UI のコントロールは、テーマが適用されていない UI であり、[通常の Windows デスクトップスタイル](https://msdn.microsoft.com/library/windows/desktop/dn742399\(v=vs.85\).aspx)に従う必要があります。つまり、テンプレートは再テンプレート化されず、既定のコントロールの外観で表示されます。

- **標準 (ユーティリティ) のダイアログ:** テーマがありません。 再テンプレートしないでください。 基本的なコントロールスタイルの既定値を使用します。

- **ツールウィンドウ、ドキュメントエディター、デザインサーフェイス、およびテーマ付きダイアログ:** カラーサービスを使用して、特別にテーマを設定した外観を使用します。

### <a name="scrollbars"></a><a name="BKMK_Scrollbars"></a>バー
 コードエディターなどのコンテンツ情報を補完する場合を除き、スクロールバーは[Windows のスクロールバーの一般的な対話パターン](https://msdn.microsoft.com/library/windows/desktop/bb787527\(v=vs.85\).aspx)に従う必要があります。

### <a name="input-fields"></a><a name="BKMK_InputFields"></a>入力フィールド
 一般的な対話動作の場合は、 [Windows デスクトップのガイドラインに従ってテキストボックスを](https://msdn.microsoft.com/library/windows/desktop/dn742442\(v=vs.85\).aspx)表示します。

#### <a name="visual-style"></a>視覚スタイル

- 入力フィールドをユーティリティダイアログでスタイル設定しないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ付きの入力フィールドは、テーマ付きダイアログとツールウィンドウでのみ使用してください。

#### <a name="specialized-interactions"></a>特化された対話

- 読み取り専用フィールドには灰色 (無効) の背景がありますが、既定 (アクティブ) の前景が使用されます。

- 必須フィールドには **\<Required>** 、ウォーターマークとしてを含める必要があります。 まれな状況を除いて、背景色を変更しないでください。

- エラーの検証: 「 [Visual Studio の通知と進行状況」を](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)参照してください。

- 入力フィールドは、コンテンツに合わせてサイズを調整する必要があります。表示されるウィンドウの幅に合わせることはできません。また、パスなどの長いフィールドの長さと任意に一致させることもできません。 長さは、フィールドで使用できる文字数に制限があることをユーザーに示すことがあります。

     ![入力フィールドコントロールの幅が正しくあり](../../extensibility/ux-guidelines/media/0707-01-incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")ません **。入力フィールドの長さが正しくありません。名前が長すぎる可能性が**あります。

     ![正しい入力フィールドコントロールの幅](../../extensibility/ux-guidelines/media/0707-02-correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")**正しい入力フィールド長: 入力フィールドは、予期されるコンテンツの幅と**して適切です。

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a>コンボボックスとドロップダウンリスト
 一般的な対話動作の場合は、「 [Windows デスクトップのガイドライン」のドロップダウンリストとコンボボックスに](https://msdn.microsoft.com/library/windows/desktop/dn742404\(v=vs.85\).aspx)従います。

#### <a name="visual-style"></a>視覚スタイル

- ユーティリティダイアログでは、コントロールを再テンプレートしないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ付き UI では、コンボボックスとドロップダウンは、コントロールの標準のテーマに従います。

#### <a name="layout"></a>Layout
 コンボボックスとドロップダウンは、コンテンツに合わせてサイズを調整する必要があります。これは、表示されているウィンドウの幅に合わせることはできません。また、パスなどの長いフィールドの長さと自由に一致させることもできません。

 ![ドロップ&#45;ダウンレイアウトが正しくありません](../../extensibility/ux-guidelines/media/0707-03-incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")

 **ドロップダウンコントロールのフィールド長が正しくありません**

 ![ドロップ&#45;ダウンレイアウトを修正します](../../extensibility/ux-guidelines/media/0707-04-correctdropdownlayout.png "0707-04_CorrectDropDownLayout")

 **ドロップダウンコントロールの正しいフィールド長**

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a>チェックボックス
 一般的な対話動作の場合は、 [Windows デスクトップのガイドライン](https://msdn.microsoft.com/library/windows/desktop/dn742401\(v=vs.85\).aspx)に従ってチェックボックスをオンにします。

#### <a name="visual-style"></a>視覚スタイル

- ユーティリティダイアログでは、コントロールを再テンプレートしないでください。 コントロールに固有の基本スタイルを使用します。

- テーマ付き UI では、チェックボックスはコントロールの標準テーマに従います。

#### <a name="specialized-interactions"></a>特化された対話

- チェックボックスとの対話は、ダイアログをポップしたり、別の領域に移動したりすることはできません。

- チェックボックスをテキストの最初の行のベースラインに揃えます。

     ![無効なチェックボックスの配置](../../extensibility/ux-guidelines/media/0707-05-incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign"): チェックボックスの配置が正しくありません。チェックボックス**はテキストの中央にあります。**

     ![正しいチェックボックスの配置](../../extensibility/ux-guidelines/media/0707-06-correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")**正しいチェックボックスの配置: チェックボックスは、テキストの最初の行のベースラインに揃えられます。**

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a>オプションボタン
 一般的な対話動作の場合は、 [Windows デスクトップのガイドライン](https://msdn.microsoft.com/library/windows/desktop/dn742436\(v=vs.85\).aspx)に従ってラジオボタンを使用します。

#### <a name="visual-style"></a>視覚スタイル
 ユーティリティダイアログでは、オプションボタンをスタイルを適用しません。 コントロールに固有の基本スタイルを使用します。

#### <a name="specialized-interactions"></a>特化された対話
 オプションの選択を囲むためにグループフレームを使用する必要はありません。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a>フレームのグループ化
 一般的な相互作用の動作については、「[グループフレームの Windows デスクトップガイドライン](https://msdn.microsoft.com/library/windows/desktop/dn742405\(v=vs.85\).aspx)」に従ってください。

#### <a name="visual-style"></a>視覚スタイル
 ユーティリティダイアログでは、グループフレームのスタイルを適用しません。 コントロールに固有の基本スタイルを使用します。

#### <a name="layout"></a>Layout

- グループの区別を密なレイアウトで維持する必要がある場合を除き、オプションの選択を囲むためにグループフレームを使用する必要はありません。

- 1つのコントロールにはグループフレームを使用しないでください。

- グループフレームコンテナーではなく、水平方向の規則を使用することが許容される場合があります。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a>テキストコントロール

### <a name="labels"></a>ラベル

#### <a name="active-label-state"></a>アクティブなラベルの状態

##### <a name="utility-standard-dialogs"></a>ユーティリティ (標準) ダイアログ)

- 一般に、コントロールラベルについては、Windows デスクトップのガイダンスに従ってください。

- ユーティリティのダイアログでは、ラベルは標準環境のフォントとテキストの色で太字で表示されません。 「 [Visual Studio のフォントと書式設定」を](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)参照してください。

- 省略記号は常にラベルに従う必要があります。

##### <a name="signature-themed-dialogs"></a>署名 (テーマ) ダイアログ)
 ラベルコントロールは、太字または淡い灰色にすることができます。

#### <a name="disabled-label-state"></a>無効なラベルの状態
 ラベルには、関連付けられているコントロールの外観が反映されている必要があります。 たとえば、関連付けられたコントロールが無効になっている場合、ラベルは灰色で表示され、無効になります。 これは通常、OS によって処理され、特別な処理は必要ありません。

#### <a name="dynamic-labels"></a>動的なラベル
 動的ラベルは、現在の選択内容に基づいて変化します。 可能な場合は常に、マスター/詳細レイアウトで動的ラベルを使用して、表示される情報が特定の選択に関連し、一般的な情報ではないことをユーザーが理解できるようにします。

 ![動的コンテンツと共に使用される動的ラベル](../../extensibility/ux-guidelines/media/070702-01-dynamiclabel.png "070702-01_DynamicLabel")

 **動的なコンテンツと共に使用される動的ラベルの例**

#### <a name="instructional-text"></a>指示テキスト
 インターフェイス要素によっては、ユーザーが UI の目的を理解したり、実行するアクションを指定したりできるように、説明文の恩恵を受けることができます。

- 指示テキストは、ダイアログの上部で最も一般的に使用されますが、複雑なコントロールのグループ化に命令を与えるために、他の領域に表示することもできます。

- 指示テキストは非対話形式ですが、ヘルプトピックへのハイパーリンクが含まれている場合があります。

- 説明文は、必要なときにのみ使用してください。

##### <a name="formatting"></a>書式設定
 指示テキストは、環境フォント、標準の (テーマがない) コントロールテキストである必要があります。 「 [Visual Studio のフォントと書式設定」を](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)参照してください。

 指示テキストの記述の詳細については、「 [UI text and 用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)」を参照してください。

 ![説明テキストの書式設定](../../extensibility/ux-guidelines/media/070702-02-instructionaltextformatting.png "070702-02_InstructionalTextFormatting")

 **Visual Studio ダイアログの指示テキスト**

#### <a name="informational-text"></a>情報テキスト
 情報テキストは、ユーザーに追加情報を提供するテキストです。 静的であるか動的であるか、または通知として使用されている可能性があります。 これは常に読み取り専用ですが、ユーザーが情報をコピーできるようにするには、動的テキストを読み取り専用のテキストフィールドなどのコントロールコンテナーに配置する必要があります。

##### <a name="dynamic-context-specific-text"></a>動的 (コンテキスト固有) テキスト
 動的な情報テキストは、ユーザーがフォーカスを切り替えるときなど、コンテキストに応じて変化します。 多くの場合、動的なコンテンツは動的ラベルとペアになりますが、常にではありません。

 ![動的な情報テキスト](../../extensibility/ux-guidelines/media/070702-03-informationaldynamictext.png "070702-03_InformationalDynamicText")

 **コンテキストに応じて動的な情報テキストが変更されます。**

##### <a name="formatting"></a>書式設定
 読み取り専用のテキストフィールドを表示するには、UI 画面に直接表示する方法と、グループフレームやテキストボックスなどの別のコントロールに格納する方法の2つの方法があります。 どちらも状況に応じて正しいです。 読み取り専用情報を表示する方法は、機能デザイナーによって決まります。

 テキストは、読み取り専用のテキストボックス内に配置できます。 これは、通常、コンテンツを選択およびコピーできることを示していますが、編集することはできません。

 ![読み取り&#45;のみのフィールドの情報テキストの書式設定](../../extensibility/ux-guidelines/media/070702-04-informationalformatting.png "070702-04_InformationalFormatting")

 **読み取り専用フィールド用の情報テキストの書式設定**

#### <a name="watermarks"></a>透かし
 表現は同じですが、ウォーターマークと指示テキストの違いは、コントロール/ウィンドウが空でない場合は透かしがコンテンツに置き換えられ、指示テキストは常に表示されるという点です。

 ウィンドウまたはコントロールが空の場合は、透かしを使用する必要があります。 これらは、領域を設定するために実行する必要があることを示し、ドラッグソースなど、関連するウィンドウを開くためのアクションリンクを含めることができます。

##### <a name="visual-style"></a>視覚スタイル

- 透かしはウィンドウ内で水平方向に配置する必要があります。

- 透かしは、左揃えではなく中央揃えにする必要があります。

- 透かしは、垂直方向の中央揃えにするか、または領域の上部付近に配置することができます。 領域の上部付近にある場合は、ウォーターマークが目立つように、上に十分な領域が必要です。

- `Environment.GrayText`色トークンと標準環境フォントを使用します。 ハイパーリンクでは、標準のハイパーリンク共有トークン (、、、) を使用する必要があり `Environment.PanelHyperlink` `Environment.PanelHyperlinkHover` `Environment.PanelHyperlinkPressed` `Environment.PanelHyperlinkDisabled` ます。

- 背景で透かしを選択することはできません

- 可能であれば、ユーザーの作業を開始するために、ウォーターマークにリンクを含めます。

  ![デザイナー ウィンドウでのウォーターマーク テキスト](../../extensibility/ux-guidelines/media/070702-05-watermark1.png "070702-05_Watermark1")

  ![ツール ウィンドウでのウォーターマーク テキスト](../../extensibility/ux-guidelines/media/070702-06-watermark2.png "070702-06_Watermark2")

  **Visual Studio での透かしテキストの例**

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a>ボタンとハイパーリンク

### <a name="overview"></a>概要
 ボタンとリンクコントロール (ハイパーリンク) は、使用、表現、サイズ変更、およびスペースの[ハイパーリンクに関する基本的な Windows デスクトップガイダンス](https://msdn.microsoft.com/library/windows/desktop/dn742406\(v=vs.85\).aspx)に従う必要があります。

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
 ![ステータス メッセージに続く情報バー コマンドのリンク](../../extensibility/ux-guidelines/media/070703-01-commandlinkinfobar.png "070703-01_CommandLinkInfobar")

 **ステータスメッセージの後に情報バーで使用されるコマンドリンク**

 ![CodeLens ポップアップで使用されているリンク](../../extensibility/ux-guidelines/media/070703-02-linksincodelens.png "070703-02_LinksInCodeLens")

 **CodeLens ポップアップで使用されているリンク**

 ![セカンダリ コマンドとして使用されているリンク](../../extensibility/ux-guidelines/media/070703-03-linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")

 **ボタンがあまり注意を払わないセカンダリコマンドに使用されるリンク**

### <a name="common-buttons"></a>共通ボタン

#### <a name="text"></a>テキスト
 [UI のテキストと用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)の記述に関するガイドラインに従ってください。

#### <a name="visual-style"></a>視覚スタイル

##### <a name="standard-dialogs"></a>標準ダイアログ
 Visual Studio のほとんどのボタンは標準のダイアログに表示されるので、スタイルを設定しないでください。 これらは、オペレーティングシステムで指定されているように、標準のボタンの外観を反映している必要があります。

##### <a name="themed"></a>テーマ
 場合によっては、スタイル設定された UI 内でボタンが使用され、これらのボタンのスタイルを適切に設定する必要があります。 テーマ付きコントロールの詳細については、[ダイアログ](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs)を参照してください。

### <a name="special-buttons"></a>特別なボタン

#### <a name="browse-buttons"></a>参照... ボタン
 **[参照...]** ボタンは、グリッド、ダイアログ、ツールウィンドウ、およびその他のモードレス UI 要素で使用されます。 ユーザーがコントロールに値を入力するのを支援するピッカーが表示されます。 このボタンには、長い形式と短い形式の2種類があります。

 ![長い &#91;参照... &#93; ボタン](../../extensibility/ux-guidelines/media/070703-04-browselong.gif "070703-04_BrowseLong")

 **長い [Browse...] ボタン**

 ![省略記号&#45;&#91;参照... &#93; ボタン](../../extensibility/ux-guidelines/media/070703-05-browseshort.gif "070703-05_BrowseShort")

 **省略記号 ([...]) ボタン**

 省略記号の省略ボタンを使用する場合:

- 複数のフィールドで閲覧が許可されている場合など、ダイアログに長い **[Browse...]** ボタンがある場合。 この状況によって作成されたわかりにくいアクセスキーを回避するには、それぞれの **[...]** ボタンを使用します (**&参照**] をクリックし、同じダイアログで**B&r)** を選択します)。

- ダイアログボックスが短い場合、または長いボタンを配置するための適切な場所がない場合。

- ボタンがグリッドコントロールに表示される場合は。

  ボタンを使用するためのガイドライン:

- アクセスキーは使用しないでください。 キーボードを使用してアクセスするには、ユーザーが隣接するコントロールから tab キーを押す必要があります。 タブの順序が、すべての参照ボタンが、入力するフィールドの直後になるようにしてください。 最初の期間の下にアンダースコアを使用しないでください。

- "ドット-ドット" または "ピリオド-ピリオド" ではなく "参照" としてスクリーンリーダーが読み取るように、Microsoft Active Accessibility (MSAA)**名**プロパティを [**参照**] (省略記号を含む) に設定します。 マネージコントロールの場合、これは**AccessibleName**プロパティを設定することを意味します。

- 参照操作以外のすべてに対して、省略記号 **[...]** ボタンを使用しないでください。 たとえば、 **[新規...]** ボタンが必要で、テキスト用の十分な空き領域がない場合は、ダイアログを再設計する必要があります。

##### <a name="sizing-and-spacing"></a>サイズと間隔
 ![サイズ変更 &#91;参照... &#93; ボタン](../../extensibility/ux-guidelines/media/070703-06-browsesizing.png "070703-06_BrowseSizing")

 **サイズ変更 [参照...] ボタン**

 ![スペース &#91;参照... &#93; ボタン](../../extensibility/ux-guidelines/media/070703-07-browsespacing.png "070703-07_BrowseSpacing")

 **スペース [参照...] ボタン**

#### <a name="graphical-buttons"></a>グラフィカルボタン
 一部のボタンでは、常にグラフィックイメージを使用し、領域を節約し、ローカライズの問題を回避するためのテキストは含めないようにする必要があります。 これらは、フィールドピッカーやその他の並べ替え可能なリストでよく使用されます。

> [!NOTE]
> ユーザーはこれらのボタン (アクセスキーがない) にタブを設定する必要があるため、適切な順序で配置します。 ボタンの [name] プロパティを、スクリーンリーダーがボタンの操作を正しく解釈するために実行するアクションにマップします。

|名前|Image|
|-|-|
|追加|![グラフィカルな [追加] ボタン](../../extensibility/ux-guidelines/media/070703-08-buttonadd.png "070703-08_ButtonAdd")|
|削除|![グラフィカルな [削除] ボタン](../../extensibility/ux-guidelines/media/070703-09-buttonremove.png "070703-09_ButtonRemove")|
|[すべてを追加]|![グラフィカルな [すべて追加] ボタン](../../extensibility/ux-guidelines/media/070703-10-buttonaddall.png "070703-10_ButtonAddAll")|
|[すべて削除]|![グラフィカルな [すべて削除] ボタン](../../extensibility/ux-guidelines/media/070703-11-buttonremoveall.png "070703-11_ButtonRemoveAll")|
|[上へ移動]|![グラフィカルな [上へ移動] ボタン](../../extensibility/ux-guidelines/media/070703-12-buttonmoveup.png "070703-12_ButtonMoveUp")|
|[上へ移動]|![グラフィカルな [下へ移動] ボタン](../../extensibility/ux-guidelines/media/070703-13-buttonmovedown.png "070703-13_ButtonMoveDown")|
|削除|![グラフィカルな [消去] ボタン](../../extensibility/ux-guidelines/media/070703-14-buttondelete.png "070703-14_ButtonDelete")|

##### <a name="sizing-and-spacing"></a>サイズと間隔
 グラフィカルボタンのサイズ変更は、 **[参照**] ボタン (2 ~ 23 ピクセル) の短いバージョンの場合と同じです。

 ![透明色が表示されているボタンとそうでないボタン](../../extensibility/ux-guidelines/media/070703-15-graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")

 **透明色が表示され、透明色が表示されていない、ボタンのグラフィックイメージの外観**

### <a name="hyperlinks"></a>ハイパーリンク
 ハイパーリンクは、ヘルプトピックやモーダルダイアログ、ウィザードを開くなど、ナビゲーションベースの操作に適しています。 ハイパーリンクがコマンドに使用されている場合は、UI に対して常に表示され、顕著な変更が表示されます。 一般に、アクションにコミットされるアクション (保存、キャンセル、削除など) は、ボタンを使用してより適切に伝達されます。

#### <a name="writing-style"></a>記述スタイル
 [ユーザーインターフェイスのテキストについては、Windows デスクトップのガイダンス](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)に従ってください。 詳細については、「詳細情報」、「詳細を表示する」、または「この言い回しについてのヘルプ」を参照してください。 代わりに、ヘルプコンテンツによって回答される主な質問に関して、語句のヘルプをリンクします。 たとえば、"**操作方法サーバーエクスプローラーにサーバーを追加しますか?**" というようになります。

#### <a name="visual-style"></a>視覚スタイル

- ハイパーリンクでは、常に[VSColor サービス](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)を使用する必要があります。 ハイパーリンクのスタイルが正しく設定されていない場合、アクティブなときは赤が点滅し、表示された後に別の色が表示されます。

- ウォーターマークなど、完全な文内の文フラグメントである場合を除いて、コントロールの状態の下に下線を入れないでください。

- ホバー時に下線を表示することはできません。 代わりに、リンクがアクティブになっていることをユーザーにフィードバックすると、色が少し変更され、適切なリンクカーソルが設定されます。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a>ツリービュー

### <a name="overview"></a>概要
 ツリービューを使用すると、複雑なリストを親子グループにまとめることができます。 ユーザーは、親グループを展開または折りたたむことで、基になる子項目を表示または非表示にすることができます。 ツリービュー内の各項目は、さらにアクションを提供するように選択できます。

 このトピックでは、使用可能な、適切な設計、およびツリービューの機能について説明します。

#### <a name="in-this-topic"></a>このトピックの内容

- [視覚スタイル](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewVisualStyle)

- [インタラクション](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewInteractions)

### <a name="visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a>視覚スタイル

#### <a name="expanders"></a>展開コントロール
 ツリービューコントロールは、Windows および Visual Studio で使用されるエキスパンダーデザインに準拠している必要があります。 各ノードは、エキスパンダーコントロールを使用して、基になる項目を表示または非表示にします。 エキスパンダーコントロールを使用すると、Windows と Visual Studio 内で異なるツリービューが発生する可能性があるユーザーに一貫性が確保されます。

 ![正しいツリー ビュー コントロール](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705-1_TreeViewCorrect")

 **修正: エキスパンダーコントロールを使用する正しいスタイルのツリービューノード**

 ![正しくないツリー ビュー ノード](../../extensibility/ux-guidelines/media/070705-2-treeviewincorrect1.png "070705-2_TreeViewIncorrect1")

 **正しくない: ツリービューノードのスタイルが正しくありません**

#### <a name="selection"></a>選択ツール
 ツリービュー内でノードを選択すると、ツリービューコントロールの幅全体に強調表示されます。 これは、ユーザーが選択した項目を明確に識別するのに役立ちます。 選択した色は、現在の Visual Studio テーマを反映している必要があります。

 ![正しいツリー ビュー コントロール](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705-1_TreeViewCorrect")

 **[修正]: 選択したノードの強調表示は、ツリービューコントロールの幅全体に一致します。**

 ![正しくない ツリー ビュー の強調表示](../../extensibility/ux-guidelines/media/070705-3-treeviewincorrect2.png "070705-3_TreeViewIncorrect2")

 **正しくない: 選択したノードの強調表示が、ツリービューコントロールの幅全体に一致しません。**

#### <a name="icons"></a>アイコン
 項目間の相違点を視覚的に識別するのに役立つ場合は、ツリービューコントロールでのみアイコンを使用する必要があります。 一般に、アイコンは、要素の種類を区別するための情報が含まれている異種リストでのみ使用する必要があります。 同種のリストでは、アイコンを使用することがしばしばノイズと見なされ、回避する必要があります。 その場合、グループアイコン (親) は、その中の項目の種類を伝えることができます。 このルールの例外は、アイコンが動的で、状態を示すために使用される場合です。

#### <a name="scroll-bars"></a>スクロール バー
 ツリービューコントロール内にコンテンツが収まる場合は、スクロールバーを常に非表示にする必要があります。 スクロールバーを非表示にしたり、スクロール可能なウィンドウで半透明にしたり、ツリービューを含むウィンドウにフォーカスがあるとき、またはツリービュー自体の上にマウスポインターを置いたときに表示されるようにすることもできます。

 ![スクロール バーのあるツリー ビュー](../../extensibility/ux-guidelines/media/070705-4-scrollbars.png "070705-4_Scrollbars")

 **コンテンツがツリービューコントロールの制限を超えているため、垂直スクロールバーと水平スクロールバーの両方が表示されます。**

### <a name="interactions"></a><a name="BKMK_TreeViewInteractions"></a>作用

#### <a name="context-menus"></a>コンテキスト メニュー
 ツリービューノードは、ショートカットメニューのサブメニューオプションを表示できます。 通常、このエラーは、ユーザーが項目を右クリックしたとき、または項目が選択された状態で Windows キーボードのメニューキーを押したときに発生します。 ノードがフォーカスを取得し、選択されていることが重要です。 これにより、サブメニューが属する項目をユーザーが識別できるようになります。

 ![選択したツリー ノードとコンテキスト メニュー](../../extensibility/ux-guidelines/media/070705-5-contextmenu.png "070705-5_ContextMenu")

 **コンテキストメニューを生成した項目は、選択された項目をユーザーに通知するためにフォーカスを取得します。**

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

  ![Visual Studio での Trid コントロール](../../extensibility/ux-guidelines/media/070705-6-trid.png "070705-6_Trid")

  **Visual Studio の trid コントロール**
