---
title: Visual Studio の共有色 |Microsoft Docs
description: 一般的な Visual Studio シェルの要素とテーマを使用して、Visual Studio 環境と一貫性のある独自のカスタム UI をデザインする方法について説明します。
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 939a327100b1fcf0908c56a4fc67540e646eac7e
ms.sourcegitcommit: 8a0d0f4c4910e2feb3bc7bd19e8f49629df78df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2020
ms.locfileid: "97668912"
---
# <a name="shared-colors-for-visual-studio"></a>Visual Studio の共有色
共通の Visual Studio シェル要素を使用する UI を設計する場合、またはインターフェイス要素と同様の機能を使用する場合は、パッケージ定義ファイル内の既存のトークン名を使用して、色を選択して割り当てます。 これにより、UI が Visual Studio 環境全体で一貫性を保ち、テーマが追加された場合や更新された場合に自動的に更新されるようになります。

この記事では、類似の UI を構築する際に参照できる一般的な UI 要素と UI 要素で使用されるトークン名について説明します。 これらの色のトークンにアクセスする方法の詳細については、「 [The VSColor Service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)」を参照してください。

トークン名は次のように正しく使用してください。

- **色自体ではなく、機能に基づいてトークン名を使用します。** 一般的な共有色は、特定のインターフェイス要素と関連付けられ、同一または類似した機能に対してのみ使用されることを想定しています。 たとえば、押されているコンボ ボックスの色を、単にその色が好きという理由で進行状況を示す回転アニメーションに再利用しないでください。 コンボボックスとアニメーションの機能は異なり、コンボボックスに関連付けられている色が変更された場合、アニメーション要素に適した色ではなくなる可能性があります。 色を一貫して使用すると、ユーザーの理解を助け、混乱を避けるために役立ちます。

- **背景色とテキストの色を適切な組み合わせで使用します。** テキストと共に使用することが想定された背景色には、テキストの色が関連付けられています。 その背景に指定されている色以外のテキストの色を使用しないでください。 テキストの色が関連付けられていない場合は、テキストを表示するサーフェイスにその背景色を使用しないでください。 テキストと背景色の他の組み合わせによって、インターフェイスの読み取りが不可能になる場合があります。

- **場所に適したコントロールの色を使用します。** 特定の状態では、一部の Visual Studio コントロールに個別の境界線と背景色がありません。 代わりに、それらのコントロールにはその背後のサーフェイスから色が適用されます。 コントロールを配置する場所に適したトークン名を常に使用してください。

> [!IMPORTANT]
> カテゴリ "スタートページ" または "Cider" で見つかったトークンは使用しないでください。

## <a name="common-shared-controls"></a>コモン共有コントロール

機能で標準の Visual Studio コマンドバーを使用すると、スタイル設定されたシェルコントロールにアクセスできるようになります。 これらのコモンコントロールを再テンプレートすることはできません。 ただし、カスタム コマンド バーを作成する必要がある場合は、カスタム コントロールも構築することが必要な場合があります。 その場合は、UI が Visual Studio の他の部分と一貫性を持つように、次の各コントロールに正しいトークン名を使用してください。

### <a name="button-controls"></a>ボタン コントロール

![ボタン コントロールの赤線](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303-155_ButtonControlRedline")

| 使用する... | 使用しない... |
| --- | --- |
| ...Visual Studio のテーマ (淡色、濃色、青、またはシステムハイコントラストテーマ) と統合するドキュメントウェルのボタン。 | ...Visual Studio のテーマの一部ではないカスタム背景に対して表示されるボタン。 |

**ボタン: 標準の状態**

![[標準] ボタン](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03")<br />[標準] ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| ボタン | `CommonControls.Button` |
| ボタンの境界線 | `CommonControls.ButtonBorder` |

**Button: 既定の状態**

![既定のボタン](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03")<br />既定のボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| ボタン | `CommonControls.ButtonDefault` |
| ボタンの境界線 | `CommonControls.ButtonBorderDefault` |

**ボタン: 無効な状態**

![[無効] ボタン](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03")<br />[無効] ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| ボタン | `CommonControls.ButtonDisabled` |
| ボタンの境界線 | `CommonControls.ButtonBorderDisabled` |

**ボタン: ホバー状態**

![ホバー時のボタン](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03")<br />ホバー時のボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| ボタン | `CommonControls.ButtonHover` |
| ボタンの境界線 | `CommonControls.ButtonBorderHover` |

**Button: 押された状態**

![押されたボタン](../../extensibility/ux-guidelines/media/03.03.Button.Pressed.png "03.03")<br />押されたボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| ボタン | `CommonControls.ButtonPressed` |
| ボタンの境界線 | `CommonControls.ButtonBorderPressed` |

**ボタン: フォーカスのある状態**

![フォーカスボタン](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03")<br />フォーカスボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| ボタン | `CommonControls.ButtonFocused` |
| ボタンの境界線 | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>チェック ボックス コントロール
![チェックボックス (赤線)](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303-161_CheckboxRedline")<br />チェックボックス (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ドキュメントウェル内に含まれるチェックボックスコントロール。 | ...チェックボックスコントロールではない UI。 |

**チェックボックス: 既定の状態**

![チェック ボックス](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303-162_Checkbox")<br />既定のチェックボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackground` |
| 境界線 | `CommonControls.CheckBoxBorder` |
| Text | `CommonControls.CheckBoxText` |
| グリフ | `CommonControls.CheckBoxGlyph` |

**チェックボックス: 無効な状態**

![無効になっているチェックボックス](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303-163_CheckboxDisabled")<br />無効になっているチェックボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundDisabled` |
| 境界線 | `CommonControls.CheckBoxBorderDisabled` |
| Text | `CommonControls.CheckBoxTextDisabled` |
| グリフ | `CommonControls.CheckBoxGlyphDisabled` |

**チェックボックス: ホバー状態**

 ![ホバー時のチェック ボックス](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303-164_CheckboxHover")<br />ホバー時のチェック ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundHover` |
| 境界線 | `CommonControls.CheckBoxBorderHover` |
| Text | `CommonControls.CheckBoxTextHover` |
| グリフ | `CommonControls.CheckBoxGlyphHover` |

**チェックボックス: 押された状態**

![押されたチェックボックス](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303-165_CheckboxPressed")<br />押されたチェックボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundPressed` |
| 境界線 | `CommonControls.CheckBoxBorderPressed` |
| Text | `CommonControls.CheckBoxTextPressed` |
| グリフ | `CommonControls.CheckBoxGlyphPressed` |

**チェックボックス: フォーカス状態**

![フォーカスチェックボックス](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303-166_CheckboxFocused")<br />フォーカスチェックボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundFocused` |
| 境界線 | `CommonControls.CheckBoxBorderFocused` |
| Text | `CommonControls.CheckBoxTextFocused` |
| グリフ | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>ドロップダウンとコンボボックス
![ドロップダウン/コンボボックス (赤線)](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")<br />ドロップダウン/コンボボックス (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ドキュメントウェルのドロップダウンとコンボボックス。 | ...ドロップダウンまたはコンボボックスではない UI。 |
| | ...コマンドバーの [ドロップダウン](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown) または [コンボボックス](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)の場合。 |

**ドロップダウンとコンボボックス: 既定の状態**

![既定のドロップダウン/コンボボックス](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303-168_DropDownComboBox")<br />既定のドロップダウン/コンボボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackground` |
| 境界線 | `CommonControls.ComboBoxBorder` |
| Text | `CommonControls.ComboBoxText` |
| 区切り記号 | `CommonControls.ComboBoxSeparator` |
| グリフ | `CommonControls.ComboBoxGlyph` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackground` |

**ドロップダウンとコンボボックス: 無効の状態**

![無効になっているドロップダウン/コンボボックス](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")<br />無効になっているドロップダウン/コンボボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundDisabled` |
| 境界線 | `CommonControls.ComboBoxBorderDisabled` |
| Text | `CommonControls.ComboBoxTextDisabled` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorDisabled` |
| グリフ | `CommonControls.ComboBoxGlyphDisabled` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**ドロップダウンとコンボボックス: ホバー状態**

![ホバー時のドロップダウン/コンボ ボックス](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")<br />ホバー時のドロップダウン/コンボ ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundHover` |
| 境界線 | `CommonControls.ComboBoxBorderHover` |
| Text | `CommonControls.ComboBoxTextHover` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorHover` |
| グリフ | `CommonControls.ComboBoxGlyphHover` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundHover` |

**ドロップダウンとコンボボックス: 押された状態**

![押されたドロップダウン/コンボボックス](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")<br />押されたドロップダウン/コンボボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundPressed` |
| 境界線 | `CommonControls.ComboBoxBorderPressed` |
| Text | `CommonControls.ComboBoxTextPressed` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorPressed` |
| グリフ | `CommonControls.ComboBoxGlyphPressed` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**ドロップダウンとコンボボックスリスト項目ビュー: 押された状態**

 ![ドロップダウン/コンボボックス押されたリスト項目ビュー](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")<br />ドロップダウン/コンボボックス押されたリスト項目ビュー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| 境界線 | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| 項目のテキスト | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| 背景の影 | `CommonControls.ComboBoxListBackgroundShadow` |

**ドロップダウンとコンボボックス: フォーカスされた状態**

![フォーカスのあるドロップダウン/コンボボックス](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")<br />フォーカスのあるドロップダウン/コンボボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundFocused` |
| 境界線 | `CommonControls.ComboBoxBorderFocused` |
| Text | `CommonControls.ComboBoxTextFocused` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorFocused` |
| グリフ | `CommonControls.ComboBoxGlyphFocused` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**ドロップダウンとコンボボックス: テキスト入力の選択**

![ドロップダウン/コンボボックスのテキスト入力の選択](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")<br />ドロップダウン/コンボボックスのテキスト入力の選択

| 要素 | トークン名: Category.color |
| --- | --- |
| 強調表示 | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>表形式のデータ (グリッド) コントロール
表形式のデータ コントロール (グリッド コントロールとも呼ばれる) は、複数列の大量のデータを表示するために使用する Visual Studio のコモン コントロールです。 標準の表形式のデータ コントロールは、[エラー一覧] ツール ウィンドウ、IntelliTrace レポート、メモリ ヒープ ビューなど、Visual Studio 内の複数の場所にあります。 提供される標準の表形式のデータ コントロールを常に使用します。 まれに、標準の表形式のデータ コントロールにアクセスできないことがあります。 このような場合は、次のトークン名を使用して、UI が Visual Studio の他の表形式のデータ コントロールと一貫性を保つようにします。

![表形式データ/グリッドコントロール (赤線)](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")<br />表形式データ/グリッドコントロール (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...表形式コントロールまたはグリッドコントロールの場合。 | ...表形式またはグリッドコントロール以外の UI。 |

#### <a name="column-headers"></a>列見出し
列ヘッダーは、背景、境界線、タイトル テキスト、およびグリッドがその列で並べ替えられたときに通常使用されるオプションのグリフで構成されます。

**列ヘッダー: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Header.Default` |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Header.Glyph` |
| 境界線 | `Header.SeparatorLine` |

**列ヘッダー: ホバー状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Header.MouseOver` |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 前景 (グリフ) | `Header.MouseOverGlyph` |
| 境界線 | `Header.SeparatorLine` |

**列ヘッダー: 押された状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundPressed` |
| 前景 (テキスト) | `CommonControls.CheckBoxBorderPressed` |
| 前景 (グリフ) | `CommonControls.CheckBoxTextPressed` |
| 境界線 | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>リスト ビュー項目
 リスト ビュー項目は、背景とコンテンツで構成されます。 コンテンツは、テキスト、アイコン、またはその両方の場合があります。

**リストビュー項目: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 透明 |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 境界線 | なし |

**リストビュー項目: アクティブ状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive` |
| 前景 (テキスト) | `TreeView.SelectedItemActiveText` |
| 境界線 | なし |

**リストビュー項目: 非アクティブ状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive` |
| 前景 (テキスト) | `TreeView.SelectedItemInactiveText` |
| 境界線 | なし |

### <a name="ui-text"></a>UI テキスト

#### <a name="instructional-text"></a>指示テキスト
説明文は、ダイアログまたはドキュメントページで何を行うかについて、目立つように説明します。

![既定の指示テキスト](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />既定の指示テキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>2番目の指示テキスト
多くのテキストとコントロールを含むドキュメントページでは、一部の説明テキストで異なる色値が使用されています。 これにより、最も重要な情報を伝え、UI 要素全体の密度を下げることができます。 (ヒントテキストについては、以下のセクションも参照してください。)

![2番目の指示テキスト](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />2番目の指示テキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>ヒントテキスト
ヒントテキストは、空のコントロール、コントロールの下、または空のドキュメントサーフェイスに表示され、次に実行する操作をユーザーに表示します。 ヒントテキストは、ウィンドウまたはコントロールの背景と共に使用できます。

**既定のヒントテキスト**

![既定のヒントテキスト](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />既定のヒントテキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlEditHintText` |

**必須のヒントテキスト**

![必須のヒントテキスト](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />必須のヒントテキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlRequiredHintText` |
| バックグラウンド | `Environment.ControlRequiredBackground` |

**検索ボックスのコントロールテキスト**

> 検索コントロールに関連するその他の色のトークンについては、「 [検索ボックス](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes) 」を参照してください。

![検索ボックスのコントロールテキスト](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />検索ボックスのコントロールテキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>ハイパーリンク
ハイパーリンクは、前景と背景のペアを持たないコントロールの1つです。 どのような場合でも、前景ハイパーリンクの色を使用します。これは、濃色、灰色、白の背景で正しく表示されます。 Hyperlink コントロールに色のトークンを使用しない場合は、"押された" の既定のシステムカラーが表示されます。これは、赤で点滅します。 これは、コントロールが正しい環境の色トークンを使用していないことを通知するものです。

![Hyperlink (赤線)](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303-133_HyperlinkRedline")<br />Hyperlink (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムハイパーリンクを作成する必要がある場合。 | ...ハイパーリンク以外のすべてのもの。 |

**Hyperlink: 既定の状態**

![既定のハイパーリンク](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303-134_Hyperlink")<br />既定のハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlink` |

**ハイパーリンク: ホバー状態**

![ホバー時のハイパーリンク](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303-135_HyperlinkHover")<br />ホバー時のハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlinkHover` |

**Hyperlink: 押された状態**

![押されたハイパーリンク](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303-136_HyperlinkPressed")<br />押されたハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlinkPressed` |

**Hyperlink: disabled 状態**

![無効なハイパーリンク](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303-137_HyperlinkDisabled")<br />無効なハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>情報バー
情報バーは該当するコンテキストの詳細を提供するために使用され、常にドキュメント ウィンドウまたはツール ウィンドウの上部に表示されます。

![情報バー (赤線)](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303-138_InfobarRedline")<br />情報バー (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタム infを作成する場合。 | ...情報バーに類似していない UI 要素。 |

**情報バー: 既定の状態**

![既定の情報バー](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303-139_Infobar")<br />既定の情報バー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.InfoBarBackground` |
| 前景 (テキスト) | `InfoBar.InfoBar` |
| 境界線 | `InfoBar.InfoBarBorder` |

**情報バーのクローズ ( &times; ) ボタン: 既定の状態**

![既定の情報バーの閉じる &times; ボタン ()](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />既定の情報バーの閉じる &times; ボタン ()

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.CloseButton` |
| 境界線 | `InfoBar.CloseButtonBorder` |
| グリフ | `InfoBar.CloseButtonGlyph` |

**情報バーのクローズ ( &times; ) ボタン: ホバー状態**

![&times;ホバー時の情報バーの閉じるボタン ()](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />&times;ホバー時の情報バーの閉じるボタン ()

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.CloseButtonHover` |
| 境界線 | `InfoBar.CloseButtonHoverBorder` |
| グリフ | `InfoBar.CloseButtonHoverGlyph` |

**情報バーのクローズ ( &times; ) ボタン: 押された状態**

![情報バーを閉じる &times; ボタン ()](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />情報バーを閉じる &times; ボタン ()

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.CloseButtonDown` |
| 境界線 | `InfoBar.CloseButtonDownBorder` |
| グリフ | `InfoBar.CloseButtonDownGlyph` |

**情報バーハイパーリンクボタン: 既定の状態**

![既定の情報バーハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />既定の情報バーハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `InfoBar.Hyperlink` |

**情報バーハイパーリンクボタン: ホバー状態**

![ホバー時の情報バーハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />ホバー時の情報バーハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseOver`<br />(下線付き) |

**情報バーハイパーリンクボタン: 押された状態**

![押された情報バーのハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />押された情報バーのハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseDown`<br />(下線付き) |

**情報バーのインラインハイパーリンク (文内): 既定の状態**

![既定のインライン情報バーハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />既定のインライン情報バーハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `InfoBar.Hyperlink` |

**情報バーのインラインハイパーリンク (文内): ホバー状態**

![ホバー時の情報バーのインラインハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />ホバー時の情報バーのインラインハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseOver`<br />(下線付き) |

**情報バーのインラインハイパーリンク (文内): 押された状態**

![押された情報バーインラインハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />押された情報バーインラインハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseDown`<br />(下線付き) |

**情報バーボタン: 既定の状態**

![既定の情報バーボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />既定の情報バーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.Button` |
| 前景 (テキスト) | `InfoBar.Button` |
| 境界線 | `InfoBar.ButtonBorder` |

**情報バーボタン: ホバー状態**

![ホバー時の情報バーボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />ホバー時の情報バーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonMouseOver` |
| 前景 (テキスト) | `InfoBar.ButtonMouseOver` |
| 境界線 | `InfoBar.ButtonMouseOverBorder` |

**情報バーボタン: 押された状態**

![押された情報バーボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />押された情報バーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonMouseDown` |
| 前景 (テキスト) | `InfoBar.ButtonMouseDown` |
| 境界線 | `InfoBar.ButtonMouseDownBorder` |

**情報バーボタン: 無効状態**

![無効な情報バーボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />無効な情報バーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonDisabled` |
| 前景 (テキスト) | `InfoBar.ButtonDisabled` |
| 境界線 | `InfoBar.ButtonDisabledBorder` |

**情報バーボタン: フォーカス状態**

![フォーカス情報バーボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />フォーカス情報バーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonFocus` |
| 前景 (テキスト) | `InfoBar.ButtonFocus` |
| 境界線 | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>スクロール バー
スクロールバーは、Visual Studio 環境によってスタイルが設定されており、テーマを設定する必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一致するように、スクロールバーで使用する色を利用することもできます。

![スクロールバー (赤線)](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303-140_ScrollbarRedline")<br />スクロールバー (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...Visual Studio のスクロールバーと一致させる UI を作成しているとき。 | ...スクロールバーの UI と常に一致させたくないものがある場合。 |

**スクロールバー: 既定の状態**

![既定のスクロールバー](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303-141_Scrollbar")<br />既定のスクロールバー

| 要素 | トークン名: Category.color |
| --- | --- |
| スクロール バー | `Environment.ScrollBarBackground` |
| 前景 (つまみ) | `Environment.ScrollBarThumbBackground` |

**スクロールバー: ホバー状態**

![ホバー時のスクロール バー](../../extensibility/ux-guidelines/media/0303-143_scrollbarhover.png "0303-143_ScrollbarHover")<br />ホバー時のスクロール バー

| 要素 | トークン名: Category.color |
| --- | --- |
| スクロール バー | `Environment.ScrollBarBackground` |
| 前景 (つまみ) | `Environment.ScrollBarThumbMouseOverBackground` |

*スクロールバー: 押された状態**

![押されたスクロールバー](../../extensibility/ux-guidelines/media/0303-145_scrollbarpressed.png "0303-145_ScrollbarPressed")<br />押されたスクロールバー

| 要素 | トークン名: Category.color |
| --- | --- |
| スクロール バー | `Environment.ScrollBarBackground` |
| 前景 (つまみ) | `Environment.ScrollBarThumbPressedBackground` |

**スクロールバーの矢印: 既定の状態**

![既定のスクロールバーの矢印](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303-142_ScrollbarArrow")<br />既定のスクロールバーの矢印

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ScrollBarArrowBackground`<br />(スクロールバーと同じ色に設定されます)。 |
| 前景 (グリフ) | `Environment.ScrollBarArrowGlyph` |

**スクロールバーの矢印: ホバー状態**

![ホバー時のスクロール バーの矢印](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br />ホバー時のスクロール バーの矢印

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ScrollBarArrowMouseOverBackground`<br />(スクロールバーと同じ色に設定されます)。 |
| 前景 (グリフ) | `Environment.ScrollBarArrowGlyphMouseOver` |

**スクロールバーの矢印: 押された状態**

![押されたスクロールバーの矢印](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br />押されたスクロールバーの矢印

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ScrollBarArrowPressedBackground`<br />(スクロールバーと同じ色に設定されます)。 |
| 前景 (グリフ) | `Environment.ScrollBarArrowGlyphPressed` |

### <a name="search-boxes"></a><a name="BKMK_SearchBoxes"></a>検索ボックス
可能な場合は常に、Visual Studio 環境で提供されるコモン検索コントロールを使用します。 検索ボックスの色は、入力フィールド、動作設定ボタン、ドロップダウン ボタン、ドロップダウン メニューのトークン名が格納されている **ShellColors.pkgdef** ファイルの "SearchControl" カテゴリにあります。

検索ボックスは次の複数の状態のいずれかの場合があり、一部の状態は相互に排他的です。

- "フォーカスされている" または "フォーカスされていない" は、カーソルがテキスト ボックス内にあるかどうかを示します。

- "アクティブ" または "非アクティブ" は、ユーザーがテキスト ボックスに検索クエリを入力したかどうかを示します。

- "ホバー" は、ユーザーがマウスを使用して検索ボックスの上にマウス ポインターを置いたことを意味します (この状態は他のすべての状態よりもオーバーライドされます)。

- "無効" は、現在のコンテキストに対して検索機能がオフになっていることを意味します。

![検索ボックス (赤線)](../../extensibility/ux-guidelines/media/0303-110_searchboxredline.png "0303-110_SearchBoxRedline")<br />検索ボックス (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタム検索ボックスを設計する場合。 | ...検索ボックスではないものがあります。 |
| | ...検索ボックスの UI と常に一致させたくないものがある場合。 |

**フォーカス検索入力フィールド**

![フォーカス検索入力フィールド](../../extensibility/ux-guidelines/media/0303-111_searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br />フォーカス検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.FocusedBackground` |
| 前景 (テキスト) | `SearchControl.FocusedBackground` |
| 境界線 | `SearchControl.FocusedBorder` |
| 区切り記号 | `SearchControl.FocusedDropDownSeparator` |

**見る、アクティブな検索の入力フィールド**

![フォーカスされていない検索入力フィールド](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br />見る、アクティブな検索の入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.SearchActiveBackground` |
| 前景 (テキスト) | `SearchControl.SearchActiveBackground` |
| 境界線 | `SearchControl.UnfocusedBorder` |
| 区切り記号 | `SearchControl.DropDownSeparator` |

**見る、非アクティブな検索入力フィールド**

![見る、非アクティブな検索入力フィールド](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br />見る、非アクティブな検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.Unfocused` |
| 前景 (テキスト) | `SearchControl.Unfocused` |
| 境界線 | `SearchControl.UnfocusedBorder` |
| 区切り記号 | `SearchControl.DropDownSeparator` |

**強調表示された検索入力フィールド (テキストのみ)**

![強調表示された検索入力フィールド](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br />強調表示された検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.Selection` |
| 前景 (テキスト) | `SearchControl.FocusedBackground` |
| 境界線 | なし |
| 区切り記号 | `SearchControl.FocusedDropDownSeparator` |

**無効な検索入力フィールド**

![無効な検索入力フィールド](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br />無効な検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.Disabled` |
| 前景 (テキスト) | `SearchControl.Disabled` |
| 境界線 | `SearchControl.DisabledBorder` |
| 区切り記号 | `SearchControl.DropDownSeparator` |

**フォーカス検索操作ボタン**

![フォーカスされた検索操作ボタン](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br />フォーカス検索操作ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (検索グリフ) | `SearchControl.SearchGlyph` |
| 前景 (停止グリフ) | `SearchControl.StopGlyph` |
| 前景 (クリア グリフ) | `SearchControl.ClearGlyph` |
| 境界線 | 該当なし |

**見る検索アクションボタン**

![見る検索アクションボタン](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br />見る検索アクションボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (検索グリフ) | `SearchControl.SearchGlyph` |
| 前景 (停止グリフ) | `SearchControl.StopGlyph` |
| 前景 (クリア グリフ) | `SearchControl.ClearGlyph` |
| 境界線 | 該当なし |

**押された検索操作ボタン**

![押された検索操作ボタン](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br />押された検索操作ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.ActionButtonMouseDown` |
| 前景 (グリフ) | `SearchControl.ActionButtonMouseDownGlyph` |
| 境界線 | `SearchControl.ActionButtonMouseDownBorder` |

**無効な検索操作ボタン**

![無効にされた検索操作ボタン](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br />無効な検索操作ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (グリフ) | `SearchControl.ActionButtonDisabledGlyph` |
| 境界線 | なし |

**フォーカス検索ドロップダウンボタン**

![フォーカス検索ドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br />フォーカス検索ドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.FocusedDropDownButton` |
| 前景 (グリフ) | `SearchControl.FocusedDropDownButtonGlyph` |
| 境界線 | `SearchControl.FocusedDropDownButtonBorder` |

**見る検索ドロップダウンボタン**

![見る検索ドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br />見る検索ドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.UnfocusedDropDownButton` |
| 前景 (グリフ) | `SearchControl.UnfocusedDropDownButtonGlyph` |
| 境界線 | `SearchControl.UnfocusedDropDownButtonBorder` |

**押された検索ドロップダウンボタン**

![押された検索ドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br />押された検索ドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.MouseDownDropDownButton` |
| 前景 (グリフ) | `SearchControl.MouseDownDropDownButtonGlyph` |
| 境界線 | `SearchControl.MouseDownDropDownButtonBorder` |

**無効な検索のドロップダウンボタン**

![無効な検索のドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br />無効な検索のドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (グリフ) | `SearchControl.DisabledDownButtonGlyph` |
| 境界線 | なし |

#### <a name="search-drop-down-lists"></a>検索ドロップダウン リスト
検索ボックスのドロップダウンメニューは、Visual Studio の他のドロップダウンメニューよりも少し複雑になる可能性があります。 [提案された検索] セクションと [検索オプション] セクションは、単独で、または1つのメニューにまとめて表示され、それぞれに個別に色分けされています。 これらの 2 つのセクションが一緒に表示される場合は線で区切られ、ドロップダウン メニュー全体が境界線で囲まれます。

![検索ドロップダウンリスト (赤線)](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303-124_SearchDropdownRedline")<br />検索ドロップダウンリスト (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタム検索ドロップダウンリストを作成している場合。 | ...他のコンテキストで表示されるドロップダウンリスト。 |
| ...正しいリストコンポーネントの正しいトークン名。 | ...指定された以外の背景と前景の組み合わせ。 |

**検索ドロップダウンリストの要素**

| 要素 | トークン名: Category.color |
| --- | --- |
| 境界線 | `SearchControl.PopupBorder` |
| 区切り記号 | `SearchControl.PopupSectionHeaderSeparator` |
| シャドウ | `Environment.DropShadowBackground` |

**推奨される検索: 既定の状態**

![既定の推奨される検索](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303-125_SearchSuggested")<br />既定の推奨される検索

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `SearchControl.PopupItemText` |

**提案された検索: ホバー状態**

![ホバー時の候補検索](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br />ホバー時の候補検索

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `SearchControl.PopupMouseOverItemText` |
| 境界線 | `SearchControl.PopupControlMouseOverBorder` |

**検索オプション: 既定の状態**

![検索チェック ボックス](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303-126_SearchCheckbox")<br />既定の検索オプション (チェックボックス)

![［検索のオプション］](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303-127_SearchOptions")<br />既定の検索オプション (リンク)

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupSectionBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (チェック ボックス テキスト) | `SearchControl.PopupCheckboxText` |
| 前景 (リンク テキスト) | `SearchControl.PopupButtonText` |
| ヘッダーの背景 | `SearchControl.PopupSectionHeaderGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (ヘッダー テキスト) | `SearchControl.PopupSectionHeaderText` |

**検索オプション: ホバー状態**

![ホバー時の検索オプション (チェックボックス)](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br />ホバー時の検索オプション (チェックボックス)

![ホバー時の検索オプション (リンク)](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303-130_SearchOptionsHover")<br />ホバー時の検索オプション (リンク)

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (チェック ボックス テキスト) | `SearchControl.PopupCheckboxMouseDownText` |
| 前景 (リンク テキスト) | `SearchControl.PopupButtonMouseDownText` |
| 境界線 | `SearchControl.PopupControlMouseOverBorder` |

**検索オプション: 押された状態**

![押された検索オプション (チェックボックス)](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br />押された検索オプション (チェックボックス)

![押された検索オプション (リンク)](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303-132_SearchOptionsPressed")<br />押された検索オプション (リンク)

| 要素 | トークン名: Category.color |
| --- | --- |
| チェック ボックスの背景 | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (チェック ボックス テキスト) | `SearchControl.PopupCheckboxMouseDownText` |
| リンクの背景 | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (リンク テキスト) | `SearchControl.PopupButtonMouseDownText` |

### <a name="tree-views"></a><a name="BKMK_TreeView"></a> ツリービュー
ソリューションエクスプローラー、サーバーエクスプローラー、クラスビューなど、いくつかのツールウィンドウには、色がカテゴリ内の色の名前によって制御される階層構造の組織スキームが実装されて `TreeView` います。 ツリー ビューのすべての項目に背景色とテキスト色があります。 入れ子にされた子要素がある項目には、項目が展開されているか折りたたまれているかを示すグリフもあります。

![ツリービュー (赤線)](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303-147_TreeViewRedline")<br />ツリービュー (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...階層構造の組織ビューを実装する必要がある場所。 | ...ツリービューに似ていないものがある場合。 |
| | ...指定された以外の背景と前景の組み合わせ。 |

**ツリービュー項目: 既定の状態**

![既定のツリービューアイテム](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303-148_TreeView")<br />既定のツリービューアイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.Background` |
| 前景 (テキスト) | `TreeView.Background` |
| 前景 (グリフ) | `TreeView.Glyph` |
| 境界線 | なし |

**ツリービュー項目: ホバー状態**

![ホバー時のツリービュー項目](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303-149_TreeViewHover")<br />ホバー時のツリービュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.Background` |
| 前景 (テキスト) | `TreeView.Background` |
| 前景 (グリフ) | `TreeView.GlyphMouseOver` |
| 境界線 | なし |

**ツリービュー項目: 状態をドラッグしてドラッグ**

![ドラッグ時のツリービュー項目](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303-150_TreeViewDragOver")<br />ドラッグ時のツリービュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.DragOverItem` |
| 前景 (テキスト) | `TreeView.DragOverItem` |
| 前景 (グリフ) | `TreeView.DragOverItemGlyph` |
| 境界線 | なし |

**ツリービュー項目: 選択済み、フォーカスされた状態**

![選択およびフォーカスされたツリービュー項目](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303-151_TreeViewFocused")<br />選択およびフォーカスされたツリービュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive` |
| 前景 (テキスト) | `TreeView.SelectedItemActive` |
| 前景 (グリフ) | `TreeView.SelectedItemActiveGlyph` |
| 境界線 | `TreeView.FocusVisualBorder` |

**ツリービュー項目: selected、見る state**

![選択および見るツリービュー項目](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303-152_TreeViewUnfocused")<br />選択および見るツリービュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive` |
| 前景 (テキスト) | `TreeView.SelectedItemInactive` |
| 前景 (グリフ) | `TreeView.SelectedItemInactiveGlyph` |
| 境界線 | なし |

**ツリービュー項目: ホバー、選択済み、フォーカスされた状態**

![ホバー時の選択されたフォーカスされたツリービュー項目](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br />ホバー時の選択されたフォーカスされたツリービュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive` |
| 前景 (テキスト) | `TreeView.SelectedItemActive` |
| 前景 (グリフ) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| 境界線 | `TreeView.FocusVisualBorder` |

**ツリービュー項目: ホバー、選択済み、見る状態**

![ホバー時の選択された見るツリービュー項目](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br />ホバー時の選択された見るツリービュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive` |
| 前景 (テキスト) | `TreeView.SelectedItemInactive` |
| 前景 (グリフ) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| 境界線 | なし |

## <a name="shell-appearance"></a>シェルの外観

### <a name="background"></a>バックグラウンド
環境の背景色は、2 つのレイヤーで構成されます。 下部レイヤーは、IDE 全体にわたる単色です。 上部レイヤーは、コマンド シェルフの下、および IDE の左端と右端のツール ウィンドウ自動非表示チャネルの間に収まります。 上部と下部の背景レイヤーは、ライトテーマとダークテーマで同じ色に設定されます。

![Visual Studio シェルの背景 (赤線)](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303-187_ShellBackgroundRedline")<br />Visual Studio シェルの背景 (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...Visual Studio 環境の背景を一致させる場所。 | ...背景の表面ではない場所の塗りつぶし。 |
| | ...前景要素を配置するための背景として。 |

**下部レイヤーシェルの外観**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.EnvironmentBackground` |

**上位のレイヤーシェルの外観**

> グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |

### <a name="command-shelf"></a>コマンド シェルフ
コマンド シェルフの背景には 2 セットのトークン名が使用されます。1 セットはメニュー バーが位置する場所、もう 1 セットはコマンド バーが位置する場所に使用されます。 個々のコマンド バー グループには、独自の背景色値があります。これについては「コマンド バー」セクションで詳しく説明しています。 メニュー バーとコマンド バーのテキストについては、それぞれメニューとコマンド バーのセクションで説明しています。

![Visual Studio コマンドシェルフ (赤線)](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303-188_CommandShelfRedline")<br />Visual Studio コマンドシェルフ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...メニューまたはツールバーを配置する領域。 | ...コマンドシェルフに類似していない領域。 |
|...正しい背景/フォアグラウンドトークン名の組み合わせで指定します。 | |

**コマンドシェルフのメニューバー**

> グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

**コマンドシェルフのコマンドバー**

> グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>マニフェスト デザイナー
マニフェスト デザイナーは、Windows 8 および Windows Phone 8 プロジェクトのマニフェスト ファイルを編集しやすくするための手段として設計されています。 使用可能な共有フレームワークはありませんが、向き/ナビゲーション タブと全体的な構造のデザイン レイアウトおよび色を一致させることが適切な場合があります。 レイアウトの詳細については、「 [Layout for Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md)」を参照してください。

![マニフェストデザイナー (赤線)](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303-175_ManifestDesignerRedline")<br />マニフェストデザイナー (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...マニフェストデザイナーに似たデザイナーの。 | ...6つ以上のタブがある場合。 |
| ...ドキュメントウェル内のエディターの上部でコモンタブコントロールを使用する代わりに使用します。 | ...マニフェストデザイナーのように構成されていない UI。 |

**マニフェストデザイナーの選択されたタブ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.TabActive` |
| 境界線 | なし |

**マニフェストデザイナーの選択された説明ペイン: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.DescriptionPane` |

**マニフェストデザイナーの選択されたコンテンツページ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.Background` |
| ダイアログ ヘルパー テキスト | `ManifestDesigner.WatermarkText`<br />(このトークン名はその関数と一致しません)。 |

**マニフェストデザイナータブ: 未選択状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.Tab.Inactive` |

**[マニフェストデザイナー] タブ: ホバー状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>コマンドの構造

### <a name="menus"></a><a name="BKMK_CommandMenus"></a> ポップアップ
メニューは、メインメニューバー、ドキュメントまたはツールウィンドウに埋め込まれている、または IDE 全体のさまざまな場所で右クリックしたときに、Visual Studio 内の複数の場所で実行できます。 他の UI 要素に関連付けられたメニューの実装については、それぞれの要素のセクションで説明します。 Visual Studio 環境で提供される標準のメニュー実装を常に使用してください。 ただし、まれに、標準の Visual Studio メニューにアクセスできないことがあります。 このような場合は、次のトークン名を使用して、UI が Visual Studio の他のメニューと一貫性を保つようにします。

![Visual Studio のメニュー (赤線)](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303-000_MenuRedline")<br />Visual Studio のメニュー (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムメニューを作成する必要がある場合。| ...背景色のみ。 常に指定された背景と前景の組み合わせを使用します。 |
| ...Visual Studio のメニューと一致させる新しい UI コンポーネントがある場合。| |

#### <a name="menu-titles"></a>メニュータイトル
メニュー タイトルは、背景、境界線、タイトル テキスト、および通常、メニューがコマンド バーにあるときは、オプションのグリフで構成されます。

![メニュータイトル (赤線)](../../extensibility/ux-guidelines/media/0303-001_menutitleredline.png "0303-001_MenuTitleRedline")<br />メニュータイトル (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムメニュータイトルを作成する場合。 | ...メニュータイトルと常に一致させたくないものがある場合。 |
| | ...指定された以外の背景と前景の組み合わせ。 |

**メニュータイトル: 既定の状態**

![既定のメニュータイトル](../../extensibility/ux-guidelines/media/0303-002_menutitledefault.png "0303-002_MenuTitleDefault")<br />既定のメニュータイトル

![グリフ付きの既定のメニュータイトル](../../extensibility/ux-guidelines/media/0303-003_menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br />グリフ付きの既定のメニュータイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Environment.CommandBarMenuGlyph` |
| 境界線 | なし |

**メニュータイトル: ホバー状態**

![ホバー時のメニュー タイトル](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303-004_MenuTitleHover")<br />ホバー時のメニュー タイトル

![ホバー時のグリフのメニュー タイトル](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br />ホバー時のグリフのメニュー タイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 前景 (グリフ) | `Environment.CommandBarMenuMouseOverGlyph` |
| 境界線 | `Environment.CommandBarBorder` |

**メニュータイトル: 押された状態**

![押されたメニュータイトル](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303-006_MenuTitlePressed")<br />押されたメニュータイトル

![メニュータイトルをグリフ付きで押す](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br />メニュータイトルをグリフ付きで押す

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Environment.CommandBarMenuMouseDownGlyph` |
| 境界線 | `Environment.CommandBarMenuBorder`<br />(Left、top、right のみ)。 |

**メニュータイトル: 無効な状態**

![グリフ付きの無効なメニュータイトル](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br />グリフ付きの無効なメニュータイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (テキスト) | `Environment.CommandBarTextInactive` |
| 前景 (グリフ) | `Environment.CommandBarTextInactive` |
| 境界線 | なし |

#### <a name="menu-items"></a>メニュー項目
個々のメニュー項目は、メニュー テキストとオプションのアイコン、チェック ボックス、またはサブメニュー グリフで構成されます。 その背景色とテキストの色はホバー時に変化します。 この色トークンは、背景と前景のペアです。

![メニュー項目の赤線](../../extensibility/ux-guidelines/media/0303-009_menuitemredline.png "0303-009_MenuItemRedline")

| 使用する... | 使用しない... |
|---|---|
| ...メニューバーまたはコマンドバーから起動されるドロップダウンリスト。 | ...別のコンテキストのドロップダウンリスト。 |
| | ...指定された以外の背景と前景の組み合わせ。 |

**メニュー項目: 既定の状態**

![既定のメニュー項目](../../extensibility/ux-guidelines/media/0303-010_menudefault.png "0303-010_MenuDefault")<br />既定のメニュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMenuBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (サブメニュー グリフ) | `Environment.CommandBarMenuSubmenuGlyph` |
| 境界線 | `Environment.CommandBarMenuBorder` |
| アイコン チャネルの背景 | `Environment.CommandBarMenuIconBackground` |
| 区切り記号 | `Environment.CommandBarMenuSeparator` |
| シャドウ | `Environment.DropShadowBackground` |

**メニュー項目: 状態の確認と選択**

![チェックされたメニュー](../../extensibility/ux-guidelines/media/0303-011_menuchecked.png "0303-011_MenuChecked")<br />選択されたメニュー項目

![選択されたメニュー](../../extensibility/ux-guidelines/media/0303-012_menuselected.png "0303-012_MenuSelected")<br />選択されたメニュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| チェック マーク | `Environment.CommandBarCheckBox` |
| チェック マークの背景 | `Environment.CommandBarSelectedIcon` |
| アイコンの背景 | `Environment.CommandBarSelected` |
| アイコンの境界線 | `Environment.CommandBarSelectedBorder` |

**メニュー項目: ホバー状態**

![メニュー ホバー](../../extensibility/ux-guidelines/media/0303-013_menuhover.png "0303-013_MenuHover")<br />ホバー時のメニュー項目

![チェックされたメニュー ホバー](../../extensibility/ux-guidelines/media/0303-014_menuhoverchecked.png "0303-014_MenuHoverChecked")<br />ホバー時にメニュー項目をチェックしました

![選択されたメニュー ホバー](../../extensibility/ux-guidelines/media/0303-015_menuhoverselected.png "0303-015_MenuHoverSelected")<br />ホバー時に選択されたメニュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMenuItemMouseOver` |
| 前景 (テキスト) | `Environment.CommandBarMenuItemMouseOverText` |
| 前景 (サブメニュー グリフ) | `Environment.CommandBarMenuMouseOverSubmenuGlyph` |
| チェック マーク | `Environment.CommandBarCheckBoxMouseOver` |
| チェック マークの背景 | `Environment.CommandBarHoverOverSelectedIcon` |
| アイコンの背景 | `Environment.CommandBarHoverOverSelected` |
| アイコンの境界線 | `Environment.CommandBarHoverOverSelectedIconBorder` |

**メニュー項目: 無効状態**

![メニューの無効化](../../extensibility/ux-guidelines/media/0303-016_menudisabled.png "0303-016_MenuDisabled")<br />無効なメニュー項目

![チェックされたメニューの無効化](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303-017_MenuDisabledChecked")<br />チェックマークが付いた無効なメニュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.CommandBarTextInactive` |
| 前景 (サブメニュー グリフ) | `Environment.CommandBarMenuSubmenuGlyph` |
| チェック マーク | `Environment.CommandBarCheckBoxDisabled` |
| チェック マークの背景 | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>コマンド バー
コマンドバーは、Visual Studio IDE 内の複数の場所、特にコマンドシェルフ、およびツールまたはドキュメントウィンドウに埋め込まれています。

通常は、Visual Studio 環境で提供される標準のコマンド バー実装を常に使用してください。 標準メカニズムを使用すると、すべての表示の詳細が正しく表示され、対話型要素が他の Visual Studio のコマンド バーのコントロールと一貫して動作するようになります。 ただし、独自のコマンド バーを作成する必要がある場合は、次のトークン名を使用してスタイルを正しく設定してください。

![コマンド バーの赤線](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303-018_CommandBarRedline")<br />コマンドバー (赤線)

![オーバーフロー ボタンの赤線](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303-019_OverflowButtonRedline")<br />オーバーフローボタン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...埋め込みコマンドバーが必要であるが、Visual Studio の標準のコマンドバー実装を使用できない場所。 | ...コマンドバーに類似していない UI 要素。 |
| | ...トークン名が指定されているもの以外のコマンドバーコンポーネント。 |

#### <a name="command-bar-groups"></a>コマンドバーグループ
コマンド バー グループは、関連する一連のコマンド バー コントロールで構成され、任意の数のボタン、分割ボタン、ドロップダウン メニュー、コンボ ボックス、またはメニューを含めることができます。 これらのコントロールの色は別々のトークン名によって制御され、このガイドの他の場所で個別に説明されています。 区切り線を使用して、コマンド バー グループを関連するサブグループに分割します。

![コマンド バー グループの赤線](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303-020_CommandBarGroupRedline")<br />コマンドバーグループ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...埋め込みコマンドバーが必要であるが、Visual Studio の標準のコマンドバー実装を使用できない場所。 | ...コマンドバーに類似していない UI 要素。 |
| | ...トークン名が指定されているもの以外のコマンドバーコンポーネント。 |

**コマンドバーグループ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 境界線 | `Environment.CommandBarToolBarBorder` |
| ドラッグ ハンドル | `Environment.CommandBarDragHandle` |
| 区切り記号 | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>コマンド アイコン
![コマンド アイコンの赤線](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303-021_CommandIconRedline1")<br />コマンドアイコン (赤線)

![赤線テキストを含むコマンドアイコン](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303-022_CommandIconRedline2")<br />テキスト付きコマンドアイコン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...コマンドバーに配置されるボタン。 | ...独自のトークン名を持つコントロールの場合。 |
| | ...指定された以外の背景と前景の組み合わせ。 |

**コマンドアイコン: 既定の状態**

![コマンド アイコンの既定値](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303-023_CommandIconDefault")<br />既定のコマンドアイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし (コマンド バーの背景から継承) |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 境界線 | 該当なし |

**コマンドアイコン: 既定の状態、選択済み**

![既定の [選択されたコマンド] アイコン](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br />既定の [選択されたコマンド] アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarSelected` |
| 前景 (テキスト) | `Environment.CommandBarTextSelected` |
| 境界線 | `Environment.CommandBarSelectedBorder` |

**コマンドアイコン: ホバー状態またはフォーカス状態**

![ホバー時またはフォーカス時のコマンドアイコン](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303-025_CommandIconHover")<br />ホバー時またはフォーカス時のコマンドアイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 境界線 | `Environment.CommandBarBorder` |

**コマンドアイコン: ホバーまたはフォーカスの状態、選択済み**

![ホバー時またはフォーカス時に選択されたコマンドアイコン](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br />ホバー時またはフォーカス時に選択されたコマンドアイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarHoverOverSelected` |
| 前景 (テキスト) | `Environment.CommandBarTextHoverOverSelected` |
| 境界線 | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **コマンドアイコン: 押された状態**

![押されているコマンド アイコン](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303-027_CommandIconPressed")<br />押されているコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseDownBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextMouseDown` |
| 境界線 | `Environment.CommandBarBorder` |

**コマンドアイコン: 無効な状態**

![無効化されたコマンド アイコン](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303-028_CommandIconDisabled")<br />無効化されたコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし (コマンド バーの背景から継承) |
| 前景 (テキスト) | `Environment.CommandBarTextInactive` |
| 境界線 | 該当なし |

#### <a name="command-bar-combo-boxes"></a><a name="BKMK_CommandComboBox"></a> コマンドバーのコンボボックス

> [!IMPORTANT]
> コンボ ボックスはドロップダウンに似ていますが、編集可能なテキスト領域が含まれます。 ドロップダウンに編集可能なテキスト領域が含まれていない場合は、 [コマンドバーのドロップ](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)ダウンの色トークンを使用します。

![コマンドバーコンボボックス赤線](../../extensibility/ux-guidelines/media/0303-029_comboboxredline.png "0303-029_ComboBoxRedline")<br />コマンドバーコンボボックス (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムコンボボックスを作成する場合。 | ...コマンドバーの UI と常に一致させる必要がないすべてのもの。 |
| ...コンボボックスに類似したコマンドバーコントロールを作成する場合。 | ...スタイル設定されたコンボボックスにアクセスできる場合。 |

**コマンドバーコンボボックスの入力フィールド: 既定の状態**

![コマンドバーコンボボックスの入力フィールド](../../extensibility/ux-guidelines/media/0303-030_comboboxinputfield.png "0303-030_ComboBoxInputField")<br />コマンドバーコンボボックスの入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxBackground` |
| 前景 (テキスト) | `Environment.ComboBoxText` |
| 境界線 | `Environment.ComboBoxBorder` |
| 区切り記号 | 区切り記号なし |

**コマンドバーのドロップダウンボタン: 既定の状態**

![コンボボックスのドロップダウン&#45;ボタン](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br />コマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし (コマンド バーの背景から継承) |
| 前景 (グリフ) | `Environment.ComboBoxGlyph` |

**コマンドバーのドロップダウンリスト: 既定の状態**

![コマンドバーのドロップダウンリスト](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br />コマンドバーのドロップダウンリスト

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxPopupBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.ComboBoxItemText` |
| 境界線 | `Environment.ComboBoxPopupBorder` |

**コマンドバーのコンボボックスの入力フィールド: ホバー状態**

![ホバー時のコマンドバーのコンボボックスの入力フィールド](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br />ホバー時のコマンドバーのコンボボックスの入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.ComboBoxMouseOverText` |
| 境界線 | `Environment.ComboBoxMouseOverBorder` |
| 区切り記号 | `Environment.ComboBoxMouseOverSeparator` |

 **コマンドバーのドロップダウンボタン: ホバー状態**

![ホバー時のコマンドバーコンボボックスのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br />ホバー時のコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxButtonMouseOverBackground` |
| 前景 (グリフ) | `Environment.ComboBoxMouseOverGlyph` |

**コマンドバーのドロップダウンリスト: ホバー状態**

 ![ホバー時のコマンドバーのコンボボックスのドロップダウンリスト](../../extensibility/ux-guidelines/media/0303-035_comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br />ホバー時のコマンドバーのドロップダウンリスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (メニュー項目) | `Environment.ComboBoxItemMouseOverBackground` |
| 前景 (テキスト) | `Environment.ComboBoxItemMouseOverText` |
| 境界線 (メニュー項目) | `Environment.ComboBoxItemMouseOverBorder` |

 **コマンドバーコンボボックスの入力フィールド: フォーカス状態**

![フォーカスしたコマンドバーコンボボックスの入力フィールド](../../extensibility/ux-guidelines/media/0303-036_comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br />フォーカスしたコマンドバーコンボボックスの入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxFocusedBackground` |
| 前景 (テキスト) | `Environment.ComboBoxFocusedText` |
| 境界線 | `Environment.ComboBoxFocusedBorder` |
| 区切り記号 | `Environment.ComboBoxFocusedButtonSeparator` |

**コマンドバーのドロップダウンボタン: フォーカス状態**

![フォーカスを持つコマンドバーのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br />フォーカスを持つコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxFocusedButtonBackground` |
| 前景 (グリフ) | `Environment.ComboBoxFocusedGlyph` |

 **コマンドバーコンボボックスの入力フィールド: 押された状態**

![押されたコマンドバーコンボボックスの入力フィールド](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br />押されたコマンドバーコンボボックスの入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxMouseDownBackground` |
| 前景 (テキスト) | `Environment.ComboBoxMouseDownText` |
| 境界線 | `Environment.ComboBoxMouseDownBorder` |
| 区切り記号 | `Environment.ComboBoxMouseDownSeparator` |

**コマンドバーのドロップダウンボタン: 押された状態**

![押されたコマンドバーコンボボックスのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br />押されたコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxButtonMouseDownBackground` |
| 前景 (グリフ) | `Environment.ComboBoxMouseDownGlyph` |

**コマンドバーコンボボックスの入力フィールド: 無効な状態**

![無効なコマンドバーコンボボックスの入力フィールド](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br />無効なコマンドバーコンボボックスの入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxDisabledBackground` |
| 前景 (テキスト) | `Environment.ComboBoxDisabledText` |
| 境界線 | `Environment.ComboBoxDisabledBorder` |
| 区切り記号 | 区切り記号なし |

**コマンドバーのドロップダウンボタン: 無効な状態**

![無効なコマンドバーコンボボックスのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br />無効なコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (グリフ) | `Environment.ComboBoxDisabledGlyph` |

#### <a name="command-bar-drop-downs"></a><a name="BKMK_CommandDropDown"></a> コマンドバーのドロップダウン

> [!IMPORTANT]
> ドロップダウンはコンボ ボックスに似ていますが、編集可能なテキスト領域がありません。 ドロップダウンに編集可能なテキスト領域が含まれている場合は、[コマンドバーの色のトークン [] コンボボックス](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)を使用します。

![コマンドバーのドロップダウン (赤線)](../../extensibility/ux-guidelines/media/0303-042_dropdownredline.png "0303-042_DropdownRedline")<br />コマンドバーのドロップダウン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムドロップダウンリストコントロールを作成している場合。 | ...ドロップダウンリストに類似していないものがある場合。 |
| | ...コンボボックスまたは分割ボタン。 |

**コマンドバーのドロップダウンの選択フィールド: 既定の状態**

![既定のコマンドバーのドロップダウンの選択フィールド](../../extensibility/ux-guidelines/media/0303-043_dropdownselectionfield.png "0303-043_DropdownSelectionField")<br />既定のコマンドバーのドロップダウンの選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownBackground` |
| 前景 (テキスト) | `DropDownText` |
| 境界線 | `DropDownBorder` |
| 区切り記号 | 区切り記号なし |

**コマンドバーのドロップダウンボタン: 既定の状態**

![既定のコマンドバーのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303-044_DropdownButton")<br />既定のコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (グリフ) | `Environment.DropDownGlyph` |

**コマンドバーのドロップダウンリスト: 既定の状態**

![既定のコマンドバーのドロップダウンリスト](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303-045_DropdownList")<br />既定のコマンドバーのドロップダウンリスト

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownPopupBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.ComboBoxItemText` |
| 境界線 | `Environment.DropDownPopupBorder` |
| シャドウ | `Environment.DropShadowBackground` |

**コマンドバーのドロップダウンの選択フィールド: ホバー状態**

![ホバー時のコマンドバーのドロップダウンの選択フィールド](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br />ホバー時のコマンドバーのドロップダウンの選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.DropDownMouseOverText` |
| 境界線 | `Environment.DropDownMouseOverBorder` |
| 区切り記号 | `Environment.DropDownButtonMouseOverSeparator` |

**コマンドバーのドロップダウンボタン: ホバー状態**

![ホバー時のコマンドバーのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br />ホバー時のコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownButtonMouseOverBackground` |
| 前景 (グリフ) | `Environment.DropDownMouseOverGlyph` |

**コマンドバーのドロップダウンリスト: ホバー状態**

![ホバー時のコマンドバーのドロップダウンリスト](../../extensibility/ux-guidelines/media/0303-048_dropdownlisthover.png "0303-048_DropdownListHover")<br />ホバー時のコマンドバーのドロップダウンリスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (メニュー項目) | `Environment.ComboBoxItemMouseOverBackground` |
| 前景 (テキスト) | `Environment.ComboBoxItemMouseOverText` |
| 境界線 (メニュー項目) | `Environment.ComboBoxItemMouseOverBorder` |

 **コマンドバーのドロップダウンの選択フィールド: 押された状態**

![押された&#45;下選択フィールドをドロップします](../../extensibility/ux-guidelines/media/0303-049_dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br />押されたコマンドバーのドロップダウンの選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownMouseDownBackground` |
| 前景 (テキスト) | `Environment.DropDownMouseDownText` |
| 境界線 | `Environment.DropDownMouseDownBorder` |
| 区切り記号 | `Environment.DropDownButtonMouseDownSeparator` |

**コマンドバーのドロップダウンボタン: 押された状態**

![押されたコマンドバーのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br />押されたコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownButtonMouseDownBackground` |
| 前景 (グリフ) | `Environment.DropDownMouseDownGlyph` |

**コマンドバーのドロップダウンの選択フィールド: 無効な状態**

![無効なコマンドバーのドロップダウンの選択フィールド](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")<br />無効なコマンドバーのドロップダウンの選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownDisabledBackground` |
| 前景 (テキスト) | `Environment.DropDownDisabledText` |
| 境界線 | `Environment.DropDownDisabledBorder` |
| 区切り記号 | 区切り記号なし |

**コマンドバーのドロップダウンボタン: 無効な状態**

![無効なコマンドバーのドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")<br />無効なコマンドバーのドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Environment.DropDownDisabledGlyph` |

#### <a name="command-bar-split-buttons"></a>コマンドバーの分割ボタン
分割ボタンは、ボタン、メニュー、コマンド バー テキストなど、他のコマンド バー コントロールと多くのトークン名を共有します。 ここでは利便性のために、すべての必要なアクション ボタンとドロップダウン ボタンのトークン名を繰り返しています。 分割ボタンのドロップダウンリストは、 [コマンドバーのメニュー](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)の実装です。

![分割ボタンの赤線](../../extensibility/ux-guidelines/media/0303-053_splitbuttonredline.png "0303-053_SplitButtonRedline")<br />コマンドバーの分割ボタン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタム分割ボタンを作成する場合。 | ...他の種類のボタン。 |
| | ...指定された以外の背景と前景の組み合わせ。 |

**コマンドバーの分割ボタン: 既定の状態**

![既定のコマンドバーの分割ボタン](../../extensibility/ux-guidelines/media/0303-054_splitbutton.png "0303-054_SplitButton")<br />既定のコマンドバーの分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | なし |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Environment.CommandBarSplitButtonGlyph` |
| 境界線 | 該当なし |
| 区切り記号 | 該当なし |

**コマンドバー分割ボタン: ホバー状態**

![ホバー時のコマンドバーの分割ボタン](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303-055_SplitButtonHover")<br />ホバー時のコマンドバーの分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 前景 (グリフ) | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| 境界線 | `Environment.CommandBarBorder` |
| 区切り記号 | `Environment.CommandBarSplitButtonSeparator` |

**コマンドバー分割ボタン: 押された状態**

![押されたコマンドバーの分割ボタン](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303-056_SplitButtonPressed")<br />押されたコマンドバーの分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseDownBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.CommandBarTextMouseDown` |
| 前景 (グリフ) | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| 境界線 | `Environment.CommandBarBorder` |
| 区切り記号 | 該当なし |

**コマンドバー分割ボタン: 無効状態**

![無効なコマンドバーの分割ボタン](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br />無効なコマンドバーの分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (テキスト) | `Environment.ComboBoxItemTextInactive` |
| 前景 (グリフ) | `Environment.CommandBarTextInactive` |
| 境界線 | 該当なし |
| 区切り記号 | 該当なし |

#### <a name="command-bar-more-options-and-overflow-buttons"></a>コマンドバーの [その他のオプション] ボタンと [オーバーフロー] ボタン
[その他のオプション] ボタンは、関連するコマンド バー ボタンを追加または削除して、コマンド バー グループをカスタマイズできる場合に使用します。 [オーバーフロー] ボタンは、横のスペースが不足しているためにコマンド バーが切り詰められた場合に表示され、クリックすると、表示できないコマンド バー ボタンを含むメニューが表示されます。 これら 2 つのボタンの色は、同じトークン名のセットによって制御されます。

![コマンドバーの [その他のオプション] ボタン (赤線)](../../extensibility/ux-guidelines/media/0303-058_moreoptionsredline.png "0303-058_MoreOptionsRedline")<br />コマンドバーの [その他のオプション] ボタン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムの [その他のオプション] ボタンまたは [オーバーフロー] ボタン。 | ...[その他のオプション] ボタンまたは [オーバーフロー] ボタンと同様の機能を持たないボタン。 |

**コマンドバーの [その他のオプション] ボタンと [オーバーフロー] ボタン: 既定の状態**

![既定のコマンドバーの [その他のオプション] ボタン](../../extensibility/ux-guidelines/media/0303-059_moreoptions.png "0303-059_MoreOptions")<br />既定のコマンドバーの [その他のオプション] ボタン

![既定のコマンドバーの [オーバーフロー] ボタン](../../extensibility/ux-guidelines/media/0303-060_overflow.png "0303-060_Overflow")<br />既定のコマンドバーの [オーバーフロー] ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarOptionsBackground` |
| 前景 (グリフ) | `Environment.CommandBarOptionsGlyph` |

**コマンドバーの [その他のオプション] ボタンと [オーバーフロー] ボタン: ホバー状態**

![ホバー時のコマンドバーの [その他のオプション] ボタン](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303-061_MoreOptionsHover")<br />ホバー時のコマンドバーの [その他のオプション] ボタン

![ホバー時のコマンドバーの ' Overflow ' ボタン](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303-062_OverflowOptions")<br />ホバー時のコマンドバーの ' Overflow ' ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (グリフ) | `Environment.CommandBarOptionsMouseDownGlyph` |

**コマンドバーの [その他のオプション] ボタンと [オーバーフロー] ボタン: 押された状態**

![コマンドバーの [その他のオプション] ボタンを押しました](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303-063_MoreOptionsPressed")<br />コマンドバーの [その他のオプション] ボタンを押しました

![押されたオーバーフロー](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303-064_OverflowPressed")<br />押されたコマンドバーの ' Overflow ' ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (グリフ) | `Environment.CommandBarOptionsMouseDownGlyph` |

## <a name="document-windows"></a>ドキュメント ウィンドウ
ドキュメントウィンドウは、Visual Studio 環境によって提供されているため、レプリケートする必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一貫性のある状態で表示されるように、ドキュメント ウィンドウで使用する色を活用することができます。

ドキュメントウィンドウの色のトークンを使用する場合は、類似の要素と常にペアで使用するように注意してください。 そうしないと、UI に予期しない結果が表示されることがあります。

### <a name="document-window-frames"></a>ドキュメントウィンドウフレーム
ドキュメント ウィンドウは IDE にドッキングしたり、別のウィンドウとしてフローティングさせたりすることができます。 ドキュメントウィンドウは、IDE の外部でフローティングされている場合でも、ドキュメントウェルのままで、IDE の一部であるときと同じように、背景、境界線、テキスト、およびタブの色を持ちます。 ただし、ドキュメントは、独自の背景、境界線、テキストの色を持つフレーム内に配置されます。 ツール ウィンドウをドキュメント ウェルにドッキングした場合、ツール ウィンドウはタブの動作と色をドキュメント ウィンドウのトークン名から継承します。

![ドッキングされたドキュメントウィンドウ (赤線)](../../extensibility/ux-guidelines/media/0303-065_dockeddocumentwindowredline.png "0303-065_DockedDocumentWindowRedline")<br />ドッキングされたドキュメントウィンドウ (赤線)

![フローティングドキュメントウィンドウ (赤線)](../../extensibility/ux-guidelines/media/0303-066_floatingdocumentwindowredline.png "0303-066_FloatingDocumentWindowRedline")<br />フローティングドキュメントウィンドウ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ドキュメントウィンドウと一致させる UI を作成するすべての場所。 | ... シェルにテーマの更新がある場合に自動的に変更されないようにする UI。 |

**ドッキングまたはフローティングドキュメントウィンドウ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | ドキュメントの種類によって異なります |
| 前景 (テキスト) | ドキュメントの種類によって異なります |
| 境界線 | `Environment.ToolWindowBorder` |

**フォーカス、フローティングドキュメントウィンドウフレーム: 既定の状態**

![既定のフォーカス、フローティングドキュメントウィンドウフレーム](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303-067_FrameFocused")<br />既定のフォーカス、フローティングドキュメントウィンドウフレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowFloatingFrame` |
| 前景 (テキスト) | `Environment.ToolWindowFloatingFrame` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonActiveGlyph` |
| 境界線 | `Environment.MainWindowActiveDefaultBorder` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonActiveBorder`<br />(透明に設定) |

**見る、フローティングドキュメントウィンドウフレーム: 既定の状態**

![既定の見る、フローティングドキュメントウィンドウフレーム](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303-068_FrameUnfocused")<br />既定の見る、フローティングドキュメントウィンドウフレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowFloatingFrameInactive` |
| 前景 (テキスト) | `Environment.ToolWindowFloatingFrameInactive` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonInactiveGlyph` |
| 境界線 | `Environment.MainWindowInactiveBorder` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonInactiveBorder`<br />(透明に設定) |

**フォーカス、フローティングドキュメントウィンドウフレーム: ホバー状態**

![フォーカスされる、ホバー時のフローティングドキュメントウィンドウフレーム](../../extensibility/ux-guidelines/media/0303-069_framefocusedhover.png "0303-069_FrameFocusedHover")<br />フォーカスされる、ホバー時のフローティングドキュメントウィンドウフレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (グリフ) | `Environment.RaftedWindowButtonHoverActive` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonHoverActiveGlyph` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonHoverActiveBorder` |

**見る、フローティングドキュメントウィンドウフレーム: ホバー状態**

![見る、ホバー時のフローティングドキュメントウィンドウフレーム](../../extensibility/ux-guidelines/media/0303-070_frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br />見る、ホバー時のフローティングドキュメントウィンドウフレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (グリフ) | `EnvironmentRaftedWindowButtonHoverInactive` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonHoverInactiveGlyph` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonHoverInactiveBorder` |

**フォーカス、フローティングドキュメントウィンドウフレーム: 押された状態**

![フォーカスされる、押されるとフローティング状態のドキュメントウィンドウフレーム](../../extensibility/ux-guidelines/media/0303-071_framefocusedpressed.png "0303-071_FrameFocusedPressed")<br />フォーカスされる、押されるとフローティング状態のドキュメントウィンドウフレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (グリフ) | `Environment.RaftedWindowButtonDown` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonDownGlyph` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonDownBorder` |

### <a name="document-tabs"></a>ドキュメント タブ
ドキュメント タブはタブ チャネル内に存在し、現在どのドキュメントが開いているか、およびどのドキュメントが現在選択されているか、またはアクティブなドキュメントであるかを示します。 ツール ウィンドウも、ユーザーが配置した場合、ドキュメント タブ チャネルにドッキングできます。 この場合、ツール ウィンドウではドキュメント ウィンドウと同じタブの色が使用されます。 ドキュメント ウィンドウの色と常に一致する UI を作成する場合は (テーマの更新や、新しいテーマがインストールされた場合を含む)、これらの色のトークンを参照します。

![ドキュメントタブ (赤線)](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303-072_DocumentTabRedline")<br />ドキュメントタブ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ドキュメントタブと一致し、テーマの更新や新しいテーマの色を自動的に取得する UI を作成するすべての場所。 | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

#### <a name="open-document-tabs"></a>開いているドキュメントのタブ
開いている各ドキュメントには、ドキュメント タブ チャネルに名前を表示するタブがあります。 ドキュメントはバックグラウンドで選択したり開いたりすることができ、タブはこれらの状態を反映します。

- 選択されているタブは、現在ドキュメント ウェルに表示されているドキュメントを表します。 選択されているタブには、ドキュメント ウェルの上端にまたがって拡張するドキュメントの境界線があります。

- 背景タブは、現在選択されているタブではないドキュメントタブです。クリックすると、選択したタブになり、それらのトークン名からすべての背景、境界線、テキストの色が取得されます。

![ドキュメントタブを開く (赤線)](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")<br />ドキュメントタブを開く (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムドキュメントタブを作成する場合。 | ...一時的な (プレビュー) タブ。 |
| | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**選択された、フォーカスされたドキュメントタブ**

![選択された、フォーカスされたドキュメントタブ](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303-074_SelectedTabFocused")<br />選択された、フォーカスされたドキュメントタブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabSelectedGradientTop`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.FileTabSelectedText` |
| 境界線 | `Environment.FileTabSelectedBorder`<br />(背景と同じ色に設定されます)。 |
| ドキュメントの境界線 | `Environment.FileTabDocumentBorderBackground` |

**選択済み、見るドキュメントタブ**

![選択済み、見るドキュメントタブ](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br />選択済み、見るドキュメントタブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabInactiveGradientTop`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.FileTabInactiveText` |
| 境界線 | `Environment.FileTabInactiveBorder`<br />(背景と同じ色に設定されます)。 |
| ドキュメントの境界線 | `Environment.FileTabInactiveDocumentBorderBackground` |

**バックグラウンドドキュメントタブ: 既定の状態**

![既定のバックグラウンドドキュメントタブ](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303-076_BackgroundTab")<br />既定のバックグラウンドドキュメントタブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabBackground` |
| 前景 (テキスト) | `Environment.FileTabText` |
| 境界線 | `Environment.FileTabBorder`<br />(背景と同じ色に設定されます)。 |

**バックグラウンドドキュメントタブ: ホバー状態**

![ホバー時の背景ドキュメントタブ](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303-077_BackgroundTabHover")<br />ホバー時の背景ドキュメントタブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabHotGradientTop`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.FileTabHotText` |
| 境界線 | `Environment.FileTabHotBorder`<br />(背景と同じ色に設定されます)。 |

#### <a name="preview-tab"></a>プレビュー タブ
"仮の" タブとも呼ばれます。[プレビュー] タブは、ユーザーがソリューションエクスプローラーツールウィンドウで項目をクリックしたときに、ドキュメントタブチャネルの右側に表示されます。 プレビュー タブはドキュメントのプレビューとして機能し、ユーザーはドキュメント タブ チャネルの左側でドキュメントを開いたままにできます。 プレビュー タブは一度に 1 つのみ開くことができます。 プレビュー タブには、開いているタブと同様に、背景と選択された状態の両方があり、アクティブな状態でフォーカスされている場合とフォーカスされていない場合があります。

![[プレビュー] タブ (赤線)](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303-078_PreviewTabRedline")<br />[プレビュー] タブ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...一時的なプレビューを作成するすべての場所で、いくつかの要素が現在のプレビュータブの色と一致するようにします。 | ...仮 (プレビュー) ではない任意の種類のドキュメントまたはタブ。 |
| | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**フォーカスされ、選択されたプレビュータブ**

![フォーカスされ、選択されたプレビュータブ](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303-079_PreviewTabFocused")<br />フォーカスされ、選択されたプレビュータブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalSelectedActive` |
| 前景 (テキスト) | `Environment.FileTabProvisionalSelectedActiveForeground` |
| 境界線 | `Environment.FileTabProvisionalSelectedActiveBorder`<br />(背景と同じ色に設定されます)。 |
| ドキュメントの境界線 | `Environment.FileTabProvisionalSelectedActiveBorder` |

**見る、選択されたプレビュータブ**

![見る、選択されたプレビュータブ](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br />見る、選択されたプレビュータブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalSelectedInactive` |
| 前景 (テキスト) | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| 境界線 | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| ドキュメントの境界線 | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**背景プレビュータブ: 既定の状態**

![既定のバックグラウンドプレビュータブ](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br />既定のバックグラウンドプレビュータブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalInactive` |
| 前景 (テキスト) | `Environment.FileTabProvisionalInactiveForeground` |
| 境界線 | `Environment.FileTabProvisionalInactiveBorder`<br />(背景と同じ色に設定されます)。 |

**バックグラウンドプレビュータブ: ホバー状態**

![ホバー時の背景プレビュータブ](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br />ホバー時の背景プレビュータブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalHover` |
| 前景 (テキスト) | `Environment.FileTabProvisionalHoverForeground` |
| 境界線 | `Environment.FileTabProvisionalHoverBorder`<br />(背景と同じ色に設定されます)。 |

#### <a name="document-overflow-button"></a>ドキュメント オーバーフロー ボタン
ドキュメント オーバーフロー ボタンは、すべてのドキュメント タブに適した垂直スペースが現在の構成にあるかどうかに関係なく、1 つ以上のドキュメントが開いている場合に表示されます。 [コマンドバーのメニュー](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)色によって制御されるドキュメントオーバーフロードロップダウンメニューには、開いているすべてのドキュメントの一覧が表示され、非表示になっています。また、すべての開いているドキュメントがタブチャネルに表示されるかどうかに応じてオーバーフローグリフが変化します。

![ドキュメントオーバーフローボタン (赤線)](../../extensibility/ux-guidelines/media/0303-083_overflowredline.png "0303-083_OverflowRedline")<br />ドキュメントオーバーフローボタン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...カスタムドキュメントオーバーフローボタンを作成する場合。 | ...オーバーフローボタンと類似していない UI。 |
| | ...コマンドバーのオーバーフローボタンの場合。 |

**ドキュメントオーバーフローボタン: 既定の状態**

![既定のドキュメントオーバーフローボタン](../../extensibility/ux-guidelines/media/0303-084_overflow.png "0303-084_Overflow")<br />既定のドキュメントオーバーフローボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DocWellOverflowButtonBackground` |
| 前景 (グリフ) | `Environment.DocWellOverflowButtonGlyph` |
| 境界線 | 該当なし |

**ドキュメントオーバーフローボタン: ホバー状態**

![ホバー時のドキュメント オーバーフロー ボタン](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303-085_OverflowHover")<br />ホバー時のドキュメント オーバーフロー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DocWellOverflowButtonMouseOverBackground` |
| 前景 (グリフ) | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| 境界線 | `Environment.DocWellOverflowButtonMouseOverBorder` |

**ドキュメントオーバーフローボタン: 押された状態**

![押したときのドキュメントオーバーフローボタン](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303-086_OverflowPressed")<br />押したときのドキュメントオーバーフローボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DocWellOverflowButtonMouseDownBackground` |
| 前景 (グリフ) | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| 境界線 | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>タグ付け
Visual Studio は、タグ付けをサポートしています。タグ付けにより、ユーザーは追跡のために検索可能なキーワードを宣言できます。 たとえば、プロジェクト マネージャーと開発者は、Team Foundation Server (TFS) を使用して作業項目にタグを付けることができます。 次の表に、タグ自体と、ホバー時および選択済み状態で表示される "アイコンを閉じる" グリフの両方の色の名前を示します。

![Visual Studio でのタグ付け (赤線)](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303-176_TaggingRedline")<br />Visual Studio でのタグ付け (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...タグ付けをサポートする UI。 | ...その他の種類の UI。 |

#### <a name="tags"></a>Tags

**タグ: 既定の状態**

![既定のタグ](../../extensibility/ux-guidelines/media/0303-177_tag.png "0303-177_Tag")<br />既定のタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.Background` |
| 前景 (テキスト) | `Tag.Background` |

**タグ: ホバー状態**

![ホバー時のタグ](../../extensibility/ux-guidelines/media/0303-178_taghover.png "0303-178_TagHover")<br />ホバー時のタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.HoverBackground` |
| 前景 (テキスト) | `Tag.HoverBackgroundText` |

**タグ: 押された状態**

![押されたタグ](../../extensibility/ux-guidelines/media/0303-179_tagpressed.png "0303-179_TagPressed")<br />押されたタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.PressedBackground` |
| 前景 (テキスト) | `Tag.PressedBackgroundText` |

**タグ: 選択された状態**

![選択されたタグ](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303-180_TagSelected")<br />選択されたタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.SelectedBackground` |
| 前景 (テキスト) | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>タググリフを閉じる ( &times; )

**Close ( &times; ) タググリフ: 既定の状態**

![既定の Close ( &times; ) タググリフ](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303-181_TagGlyph")<br />既定の Close ( &times; ) タググリフ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Tag.TagHoverGlyph` |

**閉じる ( &times; ) タググリフ: ホバー状態**

![&times;ホバー時にタググリフを閉じる ()](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303-182_TagGlyphHover")<br />&times;ホバー時にタググリフを閉じる ()

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagHoverGlyphHoverBackground` |
| 前景 (グリフ) | `Tag.TagHoverGlyphHover` |
| 境界線 | `Tag.TagHoverGlyphHoverBorder` |

**閉じる ( &times; ) タググリフ: 押された状態**

![閉じる ( &times; ) タググリフを押しました](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303-183_TagGlyphPressed")<br />閉じる ( &times; ) タググリフを押しました

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagHoverGlyphPressedBackground` |
| 前景 (グリフ) | `Tag.TagHoverGlyphPressed` |
| 境界線 | `Tag.TagHoverGlyphPressedBorder` |

**Close () グリフを含む選択されたタグ &times; : 既定の状態**

![既定の選択されたタグと閉じる ( &times; ) グリフ](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303-184_TagSelected")<br />既定の選択されたタグと閉じる ( &times; ) グリフ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Tag.TagSelectedGlyph` |

**選択したタグと閉じる ( &times; ) グリフ: ホバー状態**

![&times;ホバー時に閉じる () グリフを含む選択されたタグ](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303-185_TagSelectedHover")<br />&times;ホバー時に閉じる () グリフを含む選択されたタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagSelectedGlyphHoverBackground` |
| 前景 (グリフ) | `Tag.TagSelectedGlyphHover` |
| 境界線 | `Tag.TagSelectedGlyphHoverBorder` |

**閉じた ( &times; ) グリフ: 押された状態の選択したタグ**

![選択された、押したタグと閉じる ( &times; ) グリフ](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303-186_TagSelectedPressed")<br />選択された、押したタグと閉じる ( &times; ) グリフ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagSelectedGlyphPressedBackground` |
| 前景 (グリフ) | `Tag.TagSelectedGlyphPressed` |
| 境界線 | `Tag.TagSelectedGlyphPressedBorder` |

## <a name="tool-windows"></a>ツール ウィンドウ
ツールウィンドウは、Visual Studio 環境によって提供されているため、レプリケートする必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一貫性のある状態で表示されるように、ツール ウィンドウで使用する色を活用することができます。

![ツールウィンドウ (赤線)](../../extensibility/ux-guidelines/media/0303-087_toolwindowredline.png "0303-087_ToolWindowRedline")<br />ツールウィンドウ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ツールウィンドウと一致させる UI を作成するすべての場所。 | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

### <a name="tool-window-frame"></a>ツール ウィンドウ フレーム
Visual Studio のツール ウィンドウはさまざまなタスクに使用され、いくつかの異なる状態の 1 つで配置できます。 ツール ウィンドウが開いている場合、ドキュメント領域の 4 辺のいずれかに割り当てることができます。 ツール ウィンドウは IDE の外部でフローティングさせることもでき、ユーザーの画面内の任意の場所に再配置できます。 フローティング ウィンドウは、常に IDE の一番上に配置されます。 最後に、ツール ウィンドウはドキュメント ウィンドウとしてドッキングし、ドキュメント ウェルのタブとして表示できます。 ドキュメント ウィンドウとしてドッキングされたツール ウィンドウは、ドキュメント ウィンドウのトークン名を使用して一部の色が付けられます。

![ツールウィンドウフレーム (赤線)](../../extensibility/ux-guidelines/media/0303-088_toolwindowframeredline.png "0303-088_ToolWindowFrameRedline")<br />ツールウィンドウフレーム (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ... ツールウィンドウと一致させる UI を作成するすべての場所。 | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**ドッキングツールウィンドウ**

![ドッキングツールウィンドウ](../../extensibility/ux-guidelines/media/0303-089_toolwindowdocked.png "0303-089_ToolWindowDocked")<br />ドッキングツールウィンドウ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowBackground` |
| 境界線 | `Environment.ToolWindowBorder` |

**フォーカスがあるフローティングツールウィンドウ**

![フォーカスがあるフローティングツールウィンドウ](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303-090_ToolWindowFocused")<br />フォーカスがあるフローティングツールウィンドウ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowBackground` |
| 境界線 | `Environment.MainWindowActiveDefaultBorder` |

**フローティング、見るツールウィンドウ**

![フローティング、見るツールウィンドウ](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303-091_ToolWindowUnfocused")<br />フローティング、見るツールウィンドウ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowBackground` |
| 境界線 | `Environment.MainWindowInactiveBorder` |

### <a name="toolbox-like-windows"></a>ツールボックスのようなウィンドウ
ツールボックスは、Visual Studio で最もよく使用される一般的なツールウィンドウの1つです。 これは基本的に、特別なテーマとスタイルが適用されたツリーコントロールです。

![ツールボックスのようなウィンドウ (赤線)](../../extensibility/ux-guidelines/media/0303-189_toolboxredline.png "0303-189_ToolboxRedline")<br />ツールボックスのようなウィンドウ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...常にシェルツールボックスとの一貫性を維持するツールウィンドウをデザインする場合。 | ...ツールボックス UI に似ていないものがある場合、またはシェルツールボックスの色が変更された場合に UI に問題があるかどうかわからない場合。 |

**ツールボックスノード: 既定の状態**

![既定のツールボックスの親ノード](../../extensibility/ux-guidelines/media/0303-190_toolboxparentnode.png "0303-190_ToolboxParentNode")<br />既定のツールボックスの親ノード

![既定のツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-191_toolboxchildnode.png "0303-191_ToolboxChildNode")<br />既定のツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolboxContent`<br />見出し |
| バックグラウンド | `Environment.ToolWindowBackground`<br />(個々の項目、または使用可能なコントロールがない場合はウィンドウ全体) |
| 境界線 | なし |
| 前景 (グリフ) | `Environment.ToolboxContent` |
| 前景 (テキスト) | `Environment.ToolboxContent` |

**ツールボックスの子ノード: ホバー状態**

![ホバー時のツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br />ホバー時のツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolboxContentMouseOver`<br />(個々の項目のみ) |
| 境界線 | なし |
| 前景 (テキスト) | `Environment.ToolboxContentMouseOver`<br />(個々の項目のみ) |

**選択したツールボックスノード: フォーカスされた状態**

![フォーカス済み、選択されたツールボックスの親ノード](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br />フォーカス済み、選択されたツールボックスの親ノード

![フォーカスされている、選択したツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br />フォーカスされている、選択したツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 境界線 | `TreeView.FocusVisualBorder`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 前景 (グリフ) | `TreeView.SelectedItemActive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 前景 (テキスト) | `TreeView.SelectedItemActive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |

**選択されたツールボックスノード: 見る状態**

![選択済み、見るツールボックスの親ノード](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br />選択済み、見るツールボックスの親ノード

![選択済み、見るツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br />選択済み、見るツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 境界線 | なし |
| 前景 (グリフ) | `TreeView.SelectedItemInactive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 前景 (テキスト) | `TreeView.SelectedItemInactive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |

### <a name="tool-window-title-bar"></a>ツール ウィンドウのタイトル バー
タイトルバーの境界線は、実際の境界線ではありません。タイトルバーの上部にある太い線です。 見る状態のトークン名はありません。

![ツールウィンドウのタイトルバー (赤線)](../../extensibility/ux-guidelines/media/0303-092_toolwindowtitlebarredline.png "0303-092_ToolWindowTitleBarRedline")<br />ツールウィンドウのタイトルバー (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ツールウィンドウと一致させる UI を作成するすべての場所。 | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**フォーカスされたタイトル バー**

![フォーカスされたタイトル バー](../../extensibility/ux-guidelines/media/0303-093_titlebarfocused.png "0303-093_TitleBarFocused")<br />フォーカスされたタイトル バー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.TitleBarActiveGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.TitleBarActiveText` |
| 境界線 | `Environment.TitleBarActiveBorder`<br />(背景と同じ色に設定されます)。 |
| ドラッグ ハンドル | `Environment.TitleBarDragHandleActive` |

**フォーカスされていないタイトル バー**

![フォーカスされていないタイトル バー](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303-094_TitleBarUnfocused")<br />フォーカスされていないタイトル バー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.TitleBarInactiveGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.TitleBarInactiveText` |
| 境界線 | 該当なし |
| ドラッグ ハンドル | `Environment.TitleBarDragHandle` |

#### <a name="tool-window-title-bar-buttons"></a>ツールウィンドウのタイトルバーボタン
![タイトルバーボタン (赤線)](../../extensibility/ux-guidelines/media/0303-095_titlebarbuttonredline.png "0303-095_TitleBarButtonRedline")<br />タイトルバーボタン (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ツールウィンドウのタイトルバーの色のトークンを使用する UI に表示されるボタン。 | ...他の場所に表示されるボタン。 |
| | ...指定された以外の背景と前景の組み合わせ。 |

**フォーカスがあるタイトルバーボタン: 既定の状態**

![既定のフォーカスがあるタイトルバーボタン](../../extensibility/ux-guidelines/media/0303-096_titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br />既定のフォーカスがあるタイトルバーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Environment.ToolWindowButtonActiveGlyph` |
| 境界線 | 該当なし |

**見るのタイトルバーボタン: 既定の状態**

![既定の見るタイトルバーボタン](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br />既定の見るタイトルバーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Environment.ToolWindowButtonInactiveGlyph` |
| 境界線 | 該当なし |

**フォーカスがあるタイトルバーボタン: ホバー状態**

![ホバー時にフォーカスされるタイトルバーボタン](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br />ホバー時にフォーカスされるタイトルバーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonHoverActive` |
| 前景 (グリフ) | `Environment.ToolWindowButtonHoverActiveGlyph` |
| 境界線 | `Environment.ToolWindowButtonHoverActiveBorder` |

**見るのタイトルバーボタン: ホバー状態**

![ホバー時のタイトルバーボタンの見る](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br />ホバー時のタイトルバーボタンの見る

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonHoverInactive` |
| 前景 (グリフ) | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| 境界線 | `Environment.ToolWindowButtonHoverInactiveBorder` |

**フォーカスがあるタイトルバーボタン: 押された状態**

![プレス時にフォーカスされるタイトルバーボタン](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br />プレス時にフォーカスされるタイトルバーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonDown` |
| 前景 (グリフ) | `Environment.ToolWindowButtonDownActiveGlyph` |
| 境界線 | `Environment.ToolWindowButtonDownBorder` |

**見るのタイトルバーボタン: 押された状態**

![見るにタイトルバーボタンを表示する](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br />見るにタイトルバーボタンを表示する

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonDown` |
| 前景 (グリフ) | `Environment.ToolWindowButtonDownInactiveGlyph` |
| 境界線 | `Environment.ToolWindowButtonDownBorder` |

### <a name="tool-window-tabs"></a>ツール ウィンドウ タブ
![[ツールウィンドウ] タブ (赤線)](../../extensibility/ux-guidelines/media/0303-102_toolwindowtabredline.png "0303-102_ToolWindowTabRedline")<br />[ツールウィンドウ] タブ (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...ツールウィンドウと一致させる UI を作成するすべての場所。 | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**選択され、フォーカスされたツール ウィンドウ タブ**

![選択され、フォーカスされたツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-103_toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br />選択され、フォーカスされたツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabSelectedTab` |
| 前景 (テキスト) | `Environment.ToolWindowTabSelectedActiveText` |
| 境界線 | `Environment.ToolWindowTabSelectedBorder`<br />(背景と同じ色に設定されます)。 |

**選択され、フォーカスされていないツール ウィンドウ タブ**

![選択され、フォーカスされていないツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br />選択され、フォーカスされていないツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabSelectedTab` |
| 前景 (テキスト) | `Environment.ToolWindowTabSelectedText` |
| 境界線 | `Environment.ToolWindowTabSelectedBorder`<br />(背景と同じ色に設定されます)。 |

**バックグラウンドツールウィンドウタブ: 既定の状態**

![既定の背景ツールウィンドウタブ](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br />既定の背景ツールウィンドウタブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br />(グラデーションは、Visual Studio 2013 で同じ色の値に設定されます)。 |
| 前景 (テキスト) | `Environment.ToolWindowTabText` |
| 境界線 | `Environment.ToolWindowTabBorder` |

**バックグラウンドツールウィンドウタブ: ホバー状態**

![ホバー時の背景ツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br />ホバー時の背景ツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br />(グラデーションは、Visual Studio 2013 で同じ色の値に設定されます)。 |
| 前景 (テキスト) | `Environment.ToolWindowTabMouseOverText` |
| 境界線 | `Environment.ToolWindowTabMouseOverBorder`<br />(背景と同じ色に設定されます)。 |

### <a name="auto-hide-tabs"></a>自動非表示タブ

![タブの自動非表示 (赤線)](../../extensibility/ux-guidelines/media/0303-107_autohideredline.png "0303-107_AutoHideRedline")タブの自動非表示 (赤線)

| 使用する... | 使用しない... |
| --- | --- |
| ...自動非表示のツールウィンドウタブと一致させる UI を作成するすべての場所。 | ...シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**タブの自動非表示: 既定の状態**

![既定の自動非表示タブ](../../extensibility/ux-guidelines/media/0303-108_autohidetab.png "0303-108_AutoHideTab")<br />既定の自動非表示タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.AutoHideTabBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.AutoHideTabText` |
| 境界線 | `Environment.AutoHideTabBorder` |

**タブの自動非表示: ホバー状態**

![ホバー時の [自動非表示] タブ](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303-109_AutoHideTabHover")<br />ホバー時の [自動非表示] タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ付き UI では使用されません)。 |
| 前景 (テキスト) | `Environment.AutoHideTabMouseOverText` |
| 境界線 | `Environment.AutoHideTabMouseOverBorder` |
