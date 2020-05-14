---
title: ビジュアル スタジオの共有色 |マイクロソフトドキュメント
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 8d11b9a0-6175-4f2e-8e7f-79daee1bfd41
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3e31e5d9c3d1dc284694bd2db2a9f37d863462ad
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699927"
---
# <a name="shared-colors-for-visual-studio"></a>ビジュアル スタジオの共有色
共通の Visual Studio シェル要素を使用する UI を設計する場合、またはインターフェイス要素が類似の機能と一致するようにする場合は、パッケージ定義ファイル内の既存のトークン名を使用して色を選択および割り当てます。 これにより、UI が Visual Studio 環境全体で一貫性を保ち、テーマが追加された場合や更新された場合に自動的に更新されるようになります。

この記事では、類似の UI を構築する際に参照できる一般的な UI 要素と UI 要素で使用されるトークン名について説明します。 これらの色のトークンにアクセスする方法の詳細については、「 [The VSColor Service](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)」を参照してください。

トークン名は次のように正しく使用してください。

- **色自体ではなく、機能に基づいてトークン名を使用します。** 一般的な共有色は、特定のインターフェイス要素と関連付けられ、同一または類似した機能に対してのみ使用されることを想定しています。 たとえば、押されているコンボ ボックスの色を、単にその色が好きという理由で進行状況を示す回転アニメーションに再利用しないでください。 コンボ ボックスとアニメーションの機能が異なっており、コンボ ボックスに関連付けられた色が変更された場合、アニメーション要素に適した色ではない可能性があります。 色を一貫して使用すると、ユーザーの理解を助け、混乱を避けるために役立ちます。

- **背景色とテキストの色を適切な組み合わせで使用します。** テキストと共に使用することが想定された背景色には、テキストの色が関連付けられています。 その背景に指定されている色以外のテキストの色を使用しないでください。 関連付けられたテキストの色がない場合は、テキストを表示する必要があるすべてのサーフェスに対して、その背景色を使用しないでください。 テキストと背景色の他の組み合わせでは、読み取り不可能なインターフェイスが発生する可能性があります。

- **場所に適したコントロールの色を使用します。** 一部の状態では、一部の Visual Studio コントロールには、境界線と背景色が別々に表示されないものがあります。 代わりに、それらのコントロールにはその背後のサーフェイスから色が適用されます。 コントロールを配置する場所に適したトークン名を常に使用してください。

> [!IMPORTANT]
> 「スタートページ」または「サイダー」のカテゴリに見られるトークンを使用しないでください。

## <a name="common-shared-controls"></a>コモン共有コントロール

機能で標準の Visual Studio コマンド バーを使用すると、スタイル付きシェル コントロールにアクセスできます。 これらの共通コントロールを再テンプレートにしないでください。 ただし、カスタム コマンド バーを作成する必要がある場合は、カスタム コントロールも構築することが必要な場合があります。 その場合は、UI が Visual Studio の他の部分と一貫性を持つように、次の各コントロールに正しいトークン名を使用してください。

### <a name="button-controls"></a>ボタン コントロール

![ボタン コントロールの赤線](../../extensibility/ux-guidelines/media/0303-155_buttoncontrolredline.png "0303-155_ButtonControlRedline")

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...Visual Studio のテーマ (明色、濃い色、青、またはシステムのハイ コントラスト テーマ) と統合するドキュメントウェルのボタン。 | ...は、Visual Studio テーマの一部ではないカスタム背景に対して表示されるボタンです。 |

**ボタン: 標準状態**

![標準ボタン](../../extensibility/ux-guidelines/media/03.03.Button.Standard.png "03.03.ボタン.スタンダード")<br />標準ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| Button | `CommonControls.Button` |
| ボタンの境界線 | `CommonControls.ButtonBorder` |

**ボタン: デフォルトの状態**

![既定のボタン](../../extensibility/ux-guidelines/media/03.03.Button.Default.png "03.03.ボタン.デフォルト")<br />既定のボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| Button | `CommonControls.ButtonDefault` |
| ボタンの境界線 | `CommonControls.ButtonBorderDefault` |

**ボタン: 無効状態**

![無効ボタン](../../extensibility/ux-guidelines/media/03.03.Button.Disabled.png "03.03.ボタン.無効")<br />無効ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| Button | `CommonControls.ButtonDisabled` |
| ボタンの境界線 | `CommonControls.ButtonBorderDisabled` |

**ボタン: ホバー状態**

![ホバー時のボタン](../../extensibility/ux-guidelines/media/03.03.Button.hover.png "03.03.ボタン.ホバー")<br />ホバー時のボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| Button | `CommonControls.ButtonHover` |
| ボタンの境界線 | `CommonControls.ButtonBorderHover` |

**ボタン: 押された状態**

![押されたボタン](../../extensibility/ux-guidelines/media/03.03.Button.Pressed.png "03.03.ボタンを押した")<br />押されたボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| Button | `CommonControls.ButtonPressed` |
| ボタンの境界線 | `CommonControls.ButtonBorderPressed` |

**ボタン: フォーカス状態**

![フォーカスのあるボタン](../../extensibility/ux-guidelines/media/03.03.Button.Focused.png "03.03.ボタン.フォーカス")<br />フォーカスのあるボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| Button | `CommonControls.ButtonFocused` |
| ボタンの境界線 | `CommonControls.ButtonBorderFocused` |

### <a name="check-box-controls"></a>チェック ボックス コントロール
![チェックボックス(レッドライン)](../../extensibility/ux-guidelines/media/0303-161_checkboxredline.png "0303-161_CheckboxRedline")<br />チェックボックス(レッドライン)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ドキュメントウェル内に含まれるチェック ボックス コントロールの場合。 | ...チェック ボックス コントロールではない UI の場合。 |

**チェック ボックス: 既定の状態**

![チェック ボックス](../../extensibility/ux-guidelines/media/0303-162_checkbox.png "0303-162_Checkbox")<br />[既定] チェック ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackground` |
| Border | `CommonControls.CheckBoxBorder` |
| Text | `CommonControls.CheckBoxText` |
| グリフ | `CommonControls.CheckBoxGlyph` |

**チェック ボックス: 無効な状態**

![[無効] チェック ボックス](../../extensibility/ux-guidelines/media/0303-163_checkboxdisabled.png "0303-163_CheckboxDisabled")<br />[無効] チェック ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundDisabled` |
| Border | `CommonControls.CheckBoxBorderDisabled` |
| Text | `CommonControls.CheckBoxTextDisabled` |
| グリフ | `CommonControls.CheckBoxGlyphDisabled` |

**チェックボックス:ホバー状態**

 ![ホバー時のチェック ボックス](../../extensibility/ux-guidelines/media/0303-164_checkboxhover.png "0303-164_CheckboxHover")<br />ホバー時のチェック ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundHover` |
| Border | `CommonControls.CheckBoxBorderHover` |
| Text | `CommonControls.CheckBoxTextHover` |
| グリフ | `CommonControls.CheckBoxGlyphHover` |

**チェックボックス: 押された状態**

![[押された] チェック ボックス](../../extensibility/ux-guidelines/media/0303-165_checkboxpressed.png "0303-165_CheckboxPressed")<br />[押された] チェック ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundPressed` |
| Border | `CommonControls.CheckBoxBorderPressed` |
| Text | `CommonControls.CheckBoxTextPressed` |
| グリフ | `CommonControls.CheckBoxGlyphPressed` |

**チェックボックス: フォーカス状態**

![フォーカスチェック ボックス](../../extensibility/ux-guidelines/media/0303-166_checkboxfocused.png "0303-166_CheckboxFocused")<br />フォーカスチェック ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundFocused` |
| Border | `CommonControls.CheckBoxBorderFocused` |
| Text | `CommonControls.CheckBoxTextFocused` |
| グリフ | `CommonControls.CheckBoxGlyphFocused` |

### <a name="drop-downs-and-combo-boxes"></a>ドロップダウンとコンボ ボックス
![ドロップダウン/コンボ ボックス (朱書き)](../../extensibility/ux-guidelines/media/0303-167_dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")<br />ドロップダウン/コンボ ボックス (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ドキュメントのドロップダウンとコンボボックスの場合。 | ...ドロップダウンやコンボ ボックスではない UI の場合。 |
| | ...コマンド バー[のドロップダウン](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)または[コンボ ボックスの場合](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)。 |

**ドロップダウンとコンボ ボックス: 既定の状態**

![既定のドロップダウン/コンボ ボックス](../../extensibility/ux-guidelines/media/0303-168_dropdowncombobox.png "0303-168_DropDownComboBox")<br />既定のドロップダウン/コンボ ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackground` |
| Border | `CommonControls.ComboBoxBorder` |
| Text | `CommonControls.ComboBoxText` |
| 区切り記号 | `CommonControls.ComboBoxSeparator` |
| グリフ | `CommonControls.ComboBoxGlyph` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackground` |

**ドロップダウンとコンボ ボックス: 無効状態**

![無効なドロップダウン/コンボ ボックス](../../extensibility/ux-guidelines/media/0303-169_dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")<br />無効なドロップダウン/コンボ ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundDisabled` |
| Border | `CommonControls.ComboBoxBorderDisabled` |
| Text | `CommonControls.ComboBoxTextDisabled` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorDisabled` |
| グリフ | `CommonControls.ComboBoxGlyphDisabled` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundDisabled` |

**ドロップダウンとコンボ ボックス: ホバー状態**

![ホバー時のドロップダウン/コンボ ボックス](../../extensibility/ux-guidelines/media/0303-170_dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")<br />ホバー時のドロップダウン/コンボ ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundHover` |
| Border | `CommonControls.ComboBoxBorderHover` |
| Text | `CommonControls.ComboBoxTextHover` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorHover` |
| グリフ | `CommonControls.ComboBoxGlyphHover` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundHover` |

**ドロップダウンとコンボボックス:押された状態**

![押されたドロップダウン/コンボ ボックス](../../extensibility/ux-guidelines/media/0303-171_dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")<br />押されたドロップダウン/コンボ ボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundPressed` |
| Border | `CommonControls.ComboBoxBorderPressed` |
| Text | `CommonControls.ComboBoxTextPressed` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorPressed` |
| グリフ | `CommonControls.ComboBoxGlyphPressed` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundPressed` |

**ドロップダウンリストとコンボボックスリスト項目ビュー: 押された状態**

 ![ドロップダウン/コンボ ボックスが押されたリスト項目ビュー](../../extensibility/ux-guidelines/media/0303-174_dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")<br />ドロップダウン/コンボ ボックスが押されたリスト項目ビュー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxListBackground`<br />`CommonControls.ComboBoxListBackgroundHover`<br />`CommonControls.ComboBoxListItemBackgroundPressed`<br />`CommonControls.ComboBoxListItemBackgroundFocused` |
| Border | `CommonControls.ComboBoxListBorder`<br />`CommonControls.ComboBoxListBorderHover`<br />`CommonControls.ComboBoxListBorderPressed`<br />`CommonControls.ComboBoxListBorderFocused` |
| 項目のテキスト | `CommonControls.ComboBoxListItemText`<br /> `CommonControls.ComboBoxListItemTextHover`<br />`CommonControls.ComboBoxListItemTextPressed`<br />`CommonControls.ComboBoxListItemTextFocused` |
| 背景の影 | `CommonControls.ComboBoxListBackgroundShadow` |

**ドロップダウンとコンボボックス:フォーカス状態**

![フォーカスのあるドロップダウン/コンボボックス](../../extensibility/ux-guidelines/media/0303-172_dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")<br />フォーカスのあるドロップダウン/コンボボックス

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.ComboBoxBackgroundFocused` |
| Border | `CommonControls.ComboBoxBorderFocused` |
| Text | `CommonControls.ComboBoxTextFocused` |
| 区切り記号 | `CommonControls.ComboBoxSeparatorFocused` |
| グリフ | `CommonControls.ComboBoxGlyphFocused` |
| グリフの背景 | `CommonControls.ComboBoxGlyphBackgroundFocused` |

**ドロップダウンとコンボ ボックス: テキスト入力の選択**

![ドロップダウン/コンボ ボックステキスト入力の選択](../../extensibility/ux-guidelines/media/0303-173_dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")<br />ドロップダウン/コンボ ボックステキスト入力の選択

| 要素 | トークン名: Category.color |
| --- | --- |
| ハイライト | `CommonControls.ComboBoxTextInputSelection` |

### <a name="tabular-data-grid-controls"></a>表形式のデータ (グリッド) コントロール
表形式のデータ コントロール (グリッド コントロールとも呼ばれる) は、複数列の大量のデータを表示するために使用する Visual Studio のコモン コントロールです。 標準の表形式のデータ コントロールは、[エラー一覧] ツール ウィンドウ、IntelliTrace レポート、メモリ ヒープ ビューなど、Visual Studio 内の複数の場所にあります。 提供される標準の表形式のデータ コントロールを常に使用します。 まれに、標準の表形式のデータ コントロールにアクセスできないことがあります。 このような場合は、次のトークン名を使用して、UI が Visual Studio の他の表形式のデータ コントロールと一貫性を保つようにします。

![表形式のデータ/グリッド コントロール (朱折)](../../extensibility/ux-guidelines/media/0303-197_tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")<br />表形式のデータ/グリッド コントロール (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...表形式コントロールまたはグリッド コントロールの場合。 | ...表形式またはグリッド コントロールではない UI の場合。 |

#### <a name="column-headers"></a>列見出し
列ヘッダーは、背景、境界線、タイトル テキスト、およびグリッドがその列で並べ替えられたときに通常使用されるオプションのグリフで構成されます。

**列ヘッダー: デフォルトの状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Header.Default` |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Header.Glyph` |
| Border | `Header.SeparatorLine` |

**列ヘッダー: ホバー状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Header.MouseOver` |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 前景 (グリフ) | `Header.MouseOverGlyph` |
| Border | `Header.SeparatorLine` |

**列ヘッダー: 押された状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `CommonControls.CheckBoxBackgroundPressed` |
| 前景 (テキスト) | `CommonControls.CheckBoxBorderPressed` |
| 前景 (グリフ) | `CommonControls.CheckBoxTextPressed` |
| Border | `CommonControls.CheckBoxGlyphPressed` |

#### <a name="list-view-items"></a>リスト ビュー項目
 リスト ビュー項目は、背景とコンテンツで構成されます。 コンテンツは、テキスト、アイコン、またはその両方の場合があります。

**リスト ビュー アイテム: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 透明 |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| Border | None |

**リスト ビューアイテム: アクティブな状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive` |
| 前景 (テキスト) | `TreeView.SelectedItemActiveText` |
| Border | None |

**リスト ビューアイテム: 非アクティブ状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive` |
| 前景 (テキスト) | `TreeView.SelectedItemInactiveText` |
| Border | None |

### <a name="ui-text"></a>UI テキスト

#### <a name="instructional-text"></a>説明テキスト
説明文は、ダイアログまたはドキュメントページで何をすべきかについて、主要な説明を提供します。

![既定の説明テキスト](../../extensibility/ux-guidelines/media/0303_InstructionalText.png "0303_InstructionalText.png")<br />既定の説明テキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlText` |

#### <a name="secondary-instructional-text"></a>二次説明テキスト
多数のテキストとコントロールを含むドキュメント ページでは、一部の説明文で使用される色の値が異なります。 これにより、どの情報が最も重要かを伝え、UI 要素の全体的な密度を減らすことができます。 (ヒントテキストの下のセクションも参照してください。

![二次説明テキスト](../../extensibility/ux-guidelines/media/0303_SecondaryInstructionalText.png "0303_SecondaryInstructionalText.png")<br />二次説明テキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlEditHintText` |

#### <a name="hint-text"></a>ヒントテキスト
ヒント テキストは、空のコントロール、コントロールの下、または空のドキュメントサーフェイスに表示され、ユーザーが次に実行する操作を示します。 ヒント テキストは、ウィンドウまたはコントロールの背景と共に使用できます。

**デフォルトのヒントテキスト**

![デフォルトのヒントテキスト](../../extensibility/ux-guidelines/media/0303_HintText.png "0303_HintText.png")<br />デフォルトのヒントテキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlEditHintText` |

**必須のヒント テキスト**

![必須のヒント テキスト](../../extensibility/ux-guidelines/media/0303_RequiredHintText.png "0303_RequiredHintText.png")<br />必須のヒント テキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.ControlRequiredHintText` |
| バックグラウンド | `Environment.ControlRequiredBackground` |

**検索ボックス コントロールテキスト**

> 検索コントロールに関連するその他のカラー トークンについては、「検索[ボックス](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_SearchBoxes)」を参照してください。

![検索ボックス コントロールテキスト](../../extensibility/ux-guidelines/media/0303_SearchBoxControl.png "0303_SearchBoxControl.png")<br />検索ボックス コントロールテキスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `SearchControl.UnfocusedWatermarkText` |

### <a name="hyperlink"></a>ハイパーリンク
ハイパーリンクは、前景と背景のペアを持たない 1 つのコントロールです。 いずれの場合も、背景が暗い、灰色、白の背景に正しく表示される前景のハイパーリンク色を使用します。 ハイパーリンク コントロールに色のトークンを使用しない場合は、"押された" の既定のシステム カラーが表示され、赤が点滅します。 これは、コントロールが正しい環境の色のトークンを使用していないことを示すシグナルです。

![ハイパーリンク (朱線)](../../extensibility/ux-guidelines/media/0303-133_hyperlinkredline.png "0303-133_HyperlinkRedline")<br />ハイパーリンク (朱線)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム ハイパーリンクを作成する必要がある場合。 | ...ハイパーリンクではないものに対して。 |

**ハイパーリンク: 既定の状態**

![既定のハイパーリンク](../../extensibility/ux-guidelines/media/0303-134_hyperlink.png "0303-134_Hyperlink")<br />既定のハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlink` |

**ハイパーリンク: ホバー状態**

![ホバー時のハイパーリンク](../../extensibility/ux-guidelines/media/0303-135_hyperlinkhover.png "0303-135_HyperlinkHover")<br />ホバー時のハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlinkHover` |

**ハイパーリンク: 押された状態**

![押されたハイパーリンク](../../extensibility/ux-guidelines/media/0303-136_hyperlinkpressed.png "0303-136_HyperlinkPressed")<br />押されたハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlinkPressed` |

**ハイパーリンク: 無効な状態**

![無効なハイパーリンク](../../extensibility/ux-guidelines/media/0303-137_hyperlinkdisabled.png "0303-137_HyperlinkDisabled")<br />無効なハイパーリンク

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.PanelHyperlinkDisabled` |

### <a name="infobars"></a>インフォバー
情報バーは該当するコンテキストの詳細を提供するために使用され、常にドキュメント ウィンドウまたはツール ウィンドウの上部に表示されます。

![情報バー (レッドライン)](../../extensibility/ux-guidelines/media/0303-138_infobarredline.png "0303-138_InfobarRedline")<br />情報バー (レッドライン)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム情報バーを作成する場合。 | ...情報バーと似ていない UI 要素の場合。 |

**情報バー: 既定の状態**

![既定の情報バー](../../extensibility/ux-guidelines/media/0303-139_infobar.png "0303-139_Infobar")<br />既定の情報バー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.InfoBarBackground` |
| 前景 (テキスト) | `InfoBar.InfoBar` |
| Border | `InfoBar.InfoBarBorder` |

**情報バーの閉&times;じる ( ) ボタン: 既定の状態**

![既定の情報バー&times;[閉じる] ( ) ボタン](../../extensibility/ux-guidelines/media/0303_InfobarCloseDefault.png "0303_InfobarCloseDefault.png")<br />既定の情報バー&times;[閉じる] ( ) ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.CloseButton` |
| Border | `InfoBar.CloseButtonBorder` |
| グリフ | `InfoBar.CloseButtonGlyph` |

**インフォバーの閉&times;じる ( ) ボタン: ホバー状態**

![ホバー時の&times;情報バーの閉じる ( ) ボタン](../../extensibility/ux-guidelines/media/0303_InfobarCloseHover.png "0303_InfobarCloseHover.png")<br />ホバー時の&times;情報バーの閉じる ( ) ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.CloseButtonHover` |
| Border | `InfoBar.CloseButtonHoverBorder` |
| グリフ | `InfoBar.CloseButtonHoverGlyph` |

**インフォバーの閉&times;じる ( ) ボタン: 押された状態**

![[押されたインフォバー&times;を閉じる] ( ) ボタン](../../extensibility/ux-guidelines/media/0303_InfobarClosePressed.png "0303_InfobarClosePressed.png")<br />[押されたインフォバー&times;を閉じる] ( ) ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.CloseButtonDown` |
| Border | `InfoBar.CloseButtonDownBorder` |
| グリフ | `InfoBar.CloseButtonDownGlyph` |

**情報バーのハイパーリンク ボタン: 既定の状態**

![既定の情報バーのハイパーリンク ボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />既定の情報バーのハイパーリンク ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `InfoBar.Hyperlink` |

**インフォバーのハイパーリンク ボタン: ホバー状態**

![ホバー時の情報バーのハイパーリンク ボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonHover.png "0303_InfobarHyperlinkButtonHover.png")<br />ホバー時の情報バーのハイパーリンク ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseOver`<br />(下線付き) |

**インフォバーのハイパーリンク ボタン: 押された状態**

![[押されたインフォバーハイパーリンク] ボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonPressed.png "0303_InfobarHyperlinkButtonPressed.png")<br />[押されたインフォバーハイパーリンク] ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseDown`<br />(下線付き) |

**インフォバーのインラインハイパーリンク (文内): 既定の状態**

![既定のインライン情報バーのハイパーリンク ボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkButtonDefault.png "0303_InfobarHyperlinkButtonDefault.png")<br />既定のインライン情報バーのハイパーリンク ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `InfoBar.Hyperlink` |

**インフォバーのインラインハイパーリンク(文内): ホバー状態**

![ホバー時のインフォバーのインラインハイパーリンクボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlineHover.png "0303_InfobarHyperlinkInlineHover.png")<br />ホバー時のインフォバーのインラインハイパーリンクボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseOver`<br />(下線付き) |

**インフォバーのインラインハイパーリンク(文内): 押された状態**

![[インフォバーのインライン ハイパーリンク] ボタン](../../extensibility/ux-guidelines/media/0303_InfobarHyperlinkInlinePressed.png "0303_InfobarHyperlinkInlinePressed.png")<br />[インフォバーのインライン ハイパーリンク] ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Infobar.HyperlinkMouseDown`<br />(下線付き) |

**[情報バー] ボタン: 既定の状態**

![既定の情報バー ボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonDefault.png "0303_InfobarButtonDefault.png")<br />既定の情報バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.Button` |
| 前景 (テキスト) | `InfoBar.Button` |
| Border | `InfoBar.ButtonBorder` |

**[情報バー] ボタン: ホバー状態**

![ホバー時の情報バーボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonHover.png "0303_InfobarButtonHover.png")<br />ホバー時の情報バーボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonMouseOver` |
| 前景 (テキスト) | `InfoBar.ButtonMouseOver` |
| Border | `InfoBar.ButtonMouseOverBorder` |

**情報バーボタン: 押された状態**

![[押された情報バー] ボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonPressed.png "0303_InfobarButtonPressed.png")<br />[押された情報バー] ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonMouseDown` |
| 前景 (テキスト) | `InfoBar.ButtonMouseDown` |
| Border | `InfoBar.ButtonMouseDownBorder` |

**[情報バー] ボタン: 無効な状態**

![無効な情報バー ボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonDisabled.png "0303_InfobarButtonDisabled.png")<br />無効な情報バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonDisabled` |
| 前景 (テキスト) | `InfoBar.ButtonDisabled` |
| Border | `InfoBar.ButtonDisabledBorder` |

**情報バーボタン: フォーカス状態**

![フォーカス情報バー ボタン](../../extensibility/ux-guidelines/media/0303_InfobarButtonFocus.png "0303_InfobarButtonFocus.png")<br />フォーカス情報バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `InfoBar.ButtonFocus` |
| 前景 (テキスト) | `InfoBar.ButtonFocus` |
| Border | `InfoBar.ButtonFocusBorder` |

### <a name="scroll-bars"></a>スクロール バー
スクロール バーは Visual Studio 環境によってスタイル設定されるため、テーマを設定する必要はありません。 ただし、UI が常に Visual Studio 環境のこの部分と一貫性を持って表示されるように、スクロール バーで使用される色を活用する必要がある場合があります。

![スクロールバー(朱折)](../../extensibility/ux-guidelines/media/0303-140_scrollbarredline.png "0303-140_ScrollbarRedline")<br />スクロールバー(朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...Visual Studio のスクロール バーに一致させる UI を作成する場合。 | ...スクロール バーの UI と常に一致させたくない場合。 |

**スクロールバー: デフォルトの状態**

![既定のスクロール バー](../../extensibility/ux-guidelines/media/0303-141_scrollbar.png "0303-141_Scrollbar")<br />既定のスクロール バー

| 要素 | トークン名: Category.color |
| --- | --- |
| スクロール バー | `Environment.ScrollBarBackground` |
| 前景 (つまみ) | `Environment.ScrollBarThumbBackground` |

**スクロールバー:ホバー状態**

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

**スクロールバーの矢印: デフォルトの状態**

![既定のスクロール バーの矢印](../../extensibility/ux-guidelines/media/0303-142_scrollbararrow.png "0303-142_ScrollbarArrow")<br />既定のスクロール バーの矢印

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ScrollBarArrowBackground`<br />(スクロール バーと同じ色に設定します)。 |
| 前景 (グリフ) | `Environment.ScrollBarArrowGlyph` |

**スクロールバーの矢印: ホバー状態**

![ホバー時のスクロール バーの矢印](../../extensibility/ux-guidelines/media/0303-144_scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br />ホバー時のスクロール バーの矢印

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ScrollBarArrowMouseOverBackground`<br />(スクロール バーと同じ色に設定します)。 |
| 前景 (グリフ) | `Environment.ScrollBarArrowGlyphMouseOver` |

**スクロールバーの矢印:押された状態**

![押されたスクロール バーの矢印](../../extensibility/ux-guidelines/media/0303-146_scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br />押されたスクロール バーの矢印

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ScrollBarArrowPressedBackground`<br />(スクロール バーと同じ色に設定します)。 |
| 前景 (グリフ) | `Environment.ScrollBarArrowGlyphPressed` |

### <a name="search-boxes"></a><a name="BKMK_SearchBoxes"></a>検索ボックス
可能な場合は常に、Visual Studio 環境で提供されるコモン検索コントロールを使用します。 検索ボックスの色は、入力フィールド、動作設定ボタン、ドロップダウン ボタン、ドロップダウン メニューのトークン名が格納されている **ShellColors.pkgdef** ファイルの "SearchControl" カテゴリにあります。

検索ボックスは次の複数の状態のいずれかの場合があり、一部の状態は相互に排他的です。

- "フォーカスされている" または "フォーカスされていない" は、カーソルがテキスト ボックス内にあるかどうかを示します。

- "アクティブ" または "非アクティブ" は、ユーザーがテキスト ボックスに検索クエリを入力したかどうかを示します。

- "ホバー" は、ユーザーがマウスを使用して検索ボックスの上にマウス ポインターを置いたことを意味します (この状態は他のすべての状態よりもオーバーライドされます)。

- "無効" は、現在のコンテキストに対して検索機能がオフになっていることを意味します。

![検索ボックス (レッドライン)](../../extensibility/ux-guidelines/media/0303-110_searchboxredline.png "0303-110_SearchBoxRedline")<br />検索ボックス (レッドライン)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム検索ボックスをデザインする場合。 | ...検索ボックスではないものに対して。 |
| | ...検索ボックスの UI に常に一致させたくない場合は、何でも使用できます。 |

**フォーカス検索入力フィールド**

![フォーカス検索入力フィールド](../../extensibility/ux-guidelines/media/0303-111_searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br />フォーカス検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.FocusedBackground` |
| 前景 (テキスト) | `SearchControl.FocusedBackground` |
| Border | `SearchControl.FocusedBorder` |
| 区切り記号 | `SearchControl.FocusedDropDownSeparator` |

**フォーカスのないアクティブな検索入力フィールド**

![フォーカスされていない検索入力フィールド](../../extensibility/ux-guidelines/media/0303-114_searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br />フォーカスのないアクティブな検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.SearchActiveBackground` |
| 前景 (テキスト) | `SearchControl.SearchActiveBackground` |
| Border | `SearchControl.UnfocusedBorder` |
| 区切り記号 | `SearchControl.DropDownSeparator` |

**フォーカスのない非アクティブな検索入力フィールド**

![フォーカスのない非アクティブな検索入力フィールド](../../extensibility/ux-guidelines/media/0303-114-1_searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br />フォーカスのない非アクティブな検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.Unfocused` |
| 前景 (テキスト) | `SearchControl.Unfocused` |
| Border | `SearchControl.UnfocusedBorder` |
| 区切り記号 | `SearchControl.DropDownSeparator` |

**強調表示された検索入力フィールド (テキストのみ)**

![強調表示された検索入力フィールド](../../extensibility/ux-guidelines/media/0303-120_searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br />強調表示された検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.Selection` |
| 前景 (テキスト) | `SearchControl.FocusedBackground` |
| Border | None |
| 区切り記号 | `SearchControl.FocusedDropDownSeparator` |

**無効な検索入力フィールド**

![無効な検索入力フィールド](../../extensibility/ux-guidelines/media/0303-121_searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br />無効な検索入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.Disabled` |
| 前景 (テキスト) | `SearchControl.Disabled` |
| Border | `SearchControl.DisabledBorder` |
| 区切り記号 | `SearchControl.DropDownSeparator` |

**フォーカス検索アクションボタン**

![フォーカスされた検索操作ボタン](../../extensibility/ux-guidelines/media/0303-112_searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br />フォーカス検索アクションボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (検索グリフ) | `SearchControl.SearchGlyph` |
| 前景 (停止グリフ) | `SearchControl.StopGlyph` |
| 前景 (クリア グリフ) | `SearchControl.ClearGlyph` |
| Border | 該当なし |

**フォーカスのない検索アクションボタン**

![フォーカスのない検索アクションボタン](../../extensibility/ux-guidelines/media/0303-115_searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br />フォーカスのない検索アクションボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (検索グリフ) | `SearchControl.SearchGlyph` |
| 前景 (停止グリフ) | `SearchControl.StopGlyph` |
| 前景 (クリア グリフ) | `SearchControl.ClearGlyph` |
| Border | 該当なし |

**押された検索アクションボタン**

![押された検索アクションボタン](../../extensibility/ux-guidelines/media/0303-116-1_searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br />押された検索アクションボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.ActionButtonMouseDown` |
| 前景 (グリフ) | `SearchControl.ActionButtonMouseDownGlyph` |
| Border | `SearchControl.ActionButtonMouseDownBorder` |

**無効な検索アクション ボタン**

![無効にされた検索操作ボタン](../../extensibility/ux-guidelines/media/0303-122_searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br />無効な検索アクション ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (グリフ) | `SearchControl.ActionButtonDisabledGlyph` |
| Border | None |

**フォーカス検索ドロップダウンボタン**

![フォーカス検索ドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-113_searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br />フォーカス検索ドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.FocusedDropDownButton` |
| 前景 (グリフ) | `SearchControl.FocusedDropDownButtonGlyph` |
| Border | `SearchControl.FocusedDropDownButtonBorder` |

**フォーカスのない検索ドロップダウン ボタン**

![フォーカスのない検索ドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-116_searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br />フォーカスのない検索ドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.UnfocusedDropDownButton` |
| 前景 (グリフ) | `SearchControl.UnfocusedDropDownButtonGlyph` |
| Border | `SearchControl.UnfocusedDropDownButtonBorder` |

**押された検索ドロップダウンボタン**

![押された検索ドロップダウンボタン](../../extensibility/ux-guidelines/media/0303-116-2_searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br />押された検索ドロップダウンボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.MouseDownDropDownButton` |
| 前景 (グリフ) | `SearchControl.MouseDownDropDownButtonGlyph` |
| Border | `SearchControl.MouseDownDropDownButtonBorder` |

**無効な検索ドロップダウン ボタン**

![無効な検索ドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-123_searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br />無効な検索ドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (グリフ) | `SearchControl.DisabledDownButtonGlyph` |
| Border | None |

#### <a name="search-drop-down-lists"></a>検索ドロップダウン リスト
検索ボックスのドロップダウン メニューは、Visual Studio の他のドロップダウン メニューよりもやや複雑になる可能性があります。 「推奨検索」と「検索オプション」セクションは、メニューに単独で表示することも、メニュー内で一緒に表示することもできます。 これらの 2 つのセクションが一緒に表示される場合は線で区切られ、ドロップダウン メニュー全体が境界線で囲まれます。

![検索ドロップダウン リスト (朱折)](../../extensibility/ux-guidelines/media/0303-124_searchdropdownredline.png "0303-124_SearchDropdownRedline")<br />検索ドロップダウン リスト (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム検索ドロップダウン リストを作成する場合。 | ...他のコンテキストに表示されるドロップダウン リストの場合。 |
| ...正しいリストコンポーネントの正しいトークン名。 | ...指定以外の任意の背景/前景の組み合わせで。 |

**検索ドロップダウン リスト要素**

| 要素 | トークン名: Category.color |
| --- | --- |
| Border | `SearchControl.PopupBorder` |
| 区切り記号 | `SearchControl.PopupSectionHeaderSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**推奨される検索: 既定の状態**

![デフォルトの推奨検索](../../extensibility/ux-guidelines/media/0303-125_searchsuggested.png "0303-125_SearchSuggested")<br />デフォルトの推奨検索

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupItemsListBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `SearchControl.PopupItemText` |

**推奨検索: ホバー状態**

![ホバー時の推奨検索](../../extensibility/ux-guidelines/media/0303-128_searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br />ホバー時の推奨検索

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `SearchControl.PopupMouseOverItemText` |
| Border | `SearchControl.PopupControlMouseOverBorder` |

**検索オプション: デフォルトの状態**

![検索チェック ボックス](../../extensibility/ux-guidelines/media/0303-126_searchcheckbox.png "0303-126_SearchCheckbox")<br />既定の検索オプション (チェック ボックス)

![検索オプション](../../extensibility/ux-guidelines/media/0303-127_searchoptions.png "0303-127_SearchOptions")<br />デフォルトの検索オプション (リンク)

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupSectionBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (チェック ボックス テキスト) | `SearchControl.PopupCheckboxText` |
| 前景 (リンク テキスト) | `SearchControl.PopupButtonText` |
| ヘッダーの背景 | `SearchControl.PopupSectionHeaderGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (ヘッダー テキスト) | `SearchControl.PopupSectionHeaderText` |

**検索オプション: ホバー状態**

![ホバー時の検索オプション (チェックボックス)](../../extensibility/ux-guidelines/media/0303-129_searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br />ホバー時の検索オプション (チェックボックス)

![ホバー時の検索オプション(リンク)](../../extensibility/ux-guidelines/media/0303-130_searchoptionshover.png "0303-130_SearchOptionsHover")<br />ホバー時の検索オプション(リンク)

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (チェック ボックス テキスト) | `SearchControl.PopupCheckboxMouseDownText` |
| 前景 (リンク テキスト) | `SearchControl.PopupButtonMouseDownText` |
| Border | `SearchControl.PopupControlMouseOverBorder` |

**検索オプション: 押された状態**

![押された検索オプション (チェックボックス)](../../extensibility/ux-guidelines/media/0303-131_searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br />押された検索オプション (チェックボックス)

![押された検索オプション (リンク)](../../extensibility/ux-guidelines/media/0303-132_searchoptionspressed.png "0303-132_SearchOptionsPressed")<br />押された検索オプション (リンク)

| 要素 | トークン名: Category.color |
| --- | --- |
| チェック ボックスの背景 | `SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br />`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (チェック ボックス テキスト) | `SearchControl.PopupCheckboxMouseDownText` |
| リンクの背景 | `SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (リンク テキスト) | `SearchControl.PopupButtonMouseDownText` |

### <a name="tree-views"></a><a name="BKMK_TreeView"></a>ツリービュー
ソリューション エクスプローラ、サーバー エクスプローラ、クラス ビューなど、いくつかのツール ウィンドウには、カテゴリの色名によって色が制御される階層構造`TreeView`が実装されています。 ツリー ビューのすべての項目に背景色とテキスト色があります。 入れ子にされた子要素がある項目には、項目が展開されているか折りたたまれているかを示すグリフもあります。

![ツリービュー(朱折)](../../extensibility/ux-guidelines/media/0303-147_treeviewredline.png "0303-147_TreeViewRedline")<br />ツリービュー(朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...階層的な組織ビューを実装する必要がある場所。 | ...ツリー ビューと似ていないものに対して。 |
| | ...指定以外の任意の背景/前景の組み合わせで。 |

**ツリー ビュー アイテム: 既定の状態**

![既定のツリー ビュー アイテム](../../extensibility/ux-guidelines/media/0303-148_treeview.png "0303-148_TreeView")<br />既定のツリー ビュー アイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.Background` |
| 前景 (テキスト) | `TreeView.Background` |
| 前景 (グリフ) | `TreeView.Glyph` |
| Border | None |

**ツリービューアイテム: ホバー状態**

![ホバー時のツリー ビュー アイテム](../../extensibility/ux-guidelines/media/0303-149_treeviewhover.png "0303-149_TreeViewHover")<br />ホバー時のツリー ビュー アイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.Background` |
| 前景 (テキスト) | `TreeView.Background` |
| 前景 (グリフ) | `TreeView.GlyphMouseOver` |
| Border | None |

**ツリービューアイテム: ドラッグオーバー状態**

![ドラッグオーバー時のツリービューアイテム](../../extensibility/ux-guidelines/media/0303-150_treeviewdragover.png "0303-150_TreeViewDragOver")<br />ドラッグオーバー時のツリービューアイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.DragOverItem` |
| 前景 (テキスト) | `TreeView.DragOverItem` |
| 前景 (グリフ) | `TreeView.DragOverItemGlyph` |
| Border | None |

**ツリービューアイテム:選択済み、フォーカス状態**

![選択され、フォーカスされたツリー ビュー アイテム](../../extensibility/ux-guidelines/media/0303-151_treeviewfocused.png "0303-151_TreeViewFocused")<br />選択され、フォーカスされたツリー ビュー アイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive` |
| 前景 (テキスト) | `TreeView.SelectedItemActive` |
| 前景 (グリフ) | `TreeView.SelectedItemActiveGlyph` |
| Border | `TreeView.FocusVisualBorder` |

**ツリービューアイテム:選択済み、フォーカスなしの状態**

![選択された、フォーカスのないツリー ビュー アイテム](../../extensibility/ux-guidelines/media/0303-152_treeviewunfocused.png "0303-152_TreeViewUnfocused")<br />選択された、フォーカスのないツリー ビュー アイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive` |
| 前景 (テキスト) | `TreeView.SelectedItemInactive` |
| 前景 (グリフ) | `TreeView.SelectedItemInactiveGlyph` |
| Border | None |

**ツリー ビュー アイテム: ホバー、選択済み、フォーカス状態**

![ホバー時に選択され、フォーカスされたツリー ビュー アイテム](../../extensibility/ux-guidelines/media/0303-153_treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br />ホバー時に選択され、フォーカスされたツリー ビュー アイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive` |
| 前景 (テキスト) | `TreeView.SelectedItemActive` |
| 前景 (グリフ) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Border | `TreeView.FocusVisualBorder` |

**ツリー ビュー アイテム: ホバー、選択、およびフォーカスなしの状態**

![ホバー時に選択された、フォーカスのないツリー ビュー アイテム](../../extensibility/ux-guidelines/media/0303-154_treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br />ホバー時に選択された、フォーカスのないツリー ビュー アイテム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive` |
| 前景 (テキスト) | `TreeView.SelectedItemInactive` |
| 前景 (グリフ) | `TreeView.SelectedItemActiveGlyphMouseOver` |
| Border | None |

## <a name="shell-appearance"></a>シェルの外観

### <a name="background"></a>バックグラウンド
環境の背景色は、2 つのレイヤーで構成されます。 下部レイヤーは、IDE 全体にわたる単色です。 上部レイヤーは、コマンド シェルフの下、および IDE の左端と右端のツール ウィンドウ自動非表示チャネルの間に収まります。 上下の背景レイヤーは、明るいテーマと濃いテーマで同じ色に設定されます。

![ビジュアル スタジオ シェルの背景 (レッドライン)](../../extensibility/ux-guidelines/media/0303-187_shellbackgroundredline.png "0303-187_ShellBackgroundRedline")<br />ビジュアル スタジオ シェルの背景 (レッドライン)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...を使用して、Visual Studio 環境の背景を一致させる場所を指定します。 | ...背景サーフェスではない場所の塗りつぶしとして使用します。 |
| | ...前景要素を配置するための背景として使用します。 |

**ボトムレイヤシェルの外観**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.EnvironmentBackground` |

**トップ レイヤーシェルの外観**

> グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.EnvironmentBackgroundGradientBegin`<br />`Environment.EnvironmentBackgroundGradientEnd`<br />`Environment.EnvironmentBackgroundGradientMiddle1`<br />`Environment.EnvironmentBackgroundGradientMiddle2` |

### <a name="command-shelf"></a>コマンド シェルフ
コマンド シェルフの背景には 2 セットのトークン名が使用されます。1 セットはメニュー バーが位置する場所、もう 1 セットはコマンド バーが位置する場所に使用されます。 個々のコマンド バー グループには、独自の背景色値があります。これについては「コマンド バー」セクションで詳しく説明しています。 メニュー バーとコマンド バーのテキストについては、それぞれメニューとコマンド バーのセクションで説明しています。

![ビジュアル スタジオ コマンド シェルフ (朱折り)](../../extensibility/ux-guidelines/media/0303-188_commandshelfredline.png "0303-188_CommandShelfRedline")<br />ビジュアル スタジオ コマンド シェルフ (朱折り)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...メニューまたはツールバーを配置する領域。 | ...コマンド シェルフと似ていない領域の場合。 |
|...正しいバックグラウンド/フォアグラウンドトークン名の組み合わせを使用します。 | |

**コマンド シェルフ メニュー バー**

> グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandShelfHighlightGradientBegin`<br /><br />`Environment.CommandShelfHighlightGradientMiddle`<br />`Environment.CommandShelfHighlightGradientEnd` |

**コマンド シェルフ コマンド バー**

> グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandShelfBackgroundGradientBegin`<br />`Environment.CommandShelfBackgroundGradientMiddle`<br />`Environment.CommandShelfBackgroundGradientEnd` |

## <a name="manifest-designer"></a>マニフェスト デザイナー
マニフェスト デザイナーは、Windows 8 および Windows Phone 8 プロジェクトのマニフェスト ファイルを編集しやすくするための手段として設計されています。 使用可能な共有フレームワークはありませんが、向き/ナビゲーション タブと全体的な構造のデザイン レイアウトおよび色を一致させることが適切な場合があります。 レイアウトの詳細については、「 [Layout for Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md)」を参照してください。

![マニフェスト デザイナー (朱折)](../../extensibility/ux-guidelines/media/0303-175_manifestdesignerredline.png "0303-175_ManifestDesignerRedline")<br />マニフェスト デザイナー (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...マニフェスト デザイナーに似たデザイナーの場合。 | ...6 つ以上のタブがある場合。 |
| ...ドキュメント内のエディターの上部にある共通のタブ コントロールを使用する代わりに、 | ...マニフェスト デザイナーのように構成されていない UI に対して使用します。 |

**マニフェスト デザイナーが選択したタブ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.TabActive` |
| Border | None |

**マニフェスト デザイナーで選択された説明ウィンドウ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.DescriptionPane` |

**マニフェスト デザイナー選択コンテンツ ページ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.Background` |
| ダイアログ ヘルパー テキスト | `ManifestDesigner.WatermarkText`<br />(このトークン名は、その機能と一致しません。 |

**[マニフェスト デザイナー] タブ: 選択されていない状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.Tab.Inactive` |

**[マニフェスト デザイナー] タブ: ホバー状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `ManifestDesigner.Tab.Mouseover` |

## <a name="command-structures"></a>コマンドの構造

### <a name="menus"></a><a name="BKMK_CommandMenus"></a>メニュー
メニューは、Visual Studio 内のいくつかの場所で行うことができます: メイン メニュー バー、ドキュメントウィンドウまたはツール ウィンドウに埋め込まれている、または IDE 全体のさまざまな場所で右クリックします。 他の UI 要素に関連付けられたメニューの実装については、それぞれの要素のセクションで説明します。 Visual Studio 環境で提供される標準のメニュー実装を常に使用してください。 ただし、まれに、標準の Visual Studio メニューにアクセスできないことがあります。 このような場合は、次のトークン名を使用して、UI が Visual Studio の他のメニューと一貫性を保つようにします。

![ビジュアルスタジオメニュー (朱折)](../../extensibility/ux-guidelines/media/0303-000_menuredline.png "0303-000_MenuRedline")<br />ビジュアルスタジオメニュー (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム メニューを作成する必要がある場合。| ...背景色のみ。 常に指定された背景と前景の組み合わせを使用します。 |
| ...新しい UI コンポーネントが Visual Studio メニューと一致する場合。| |

#### <a name="menu-titles"></a>メニュータイトル
メニュー タイトルは、背景、境界線、タイトル テキスト、および通常、メニューがコマンド バーにあるときは、オプションのグリフで構成されます。

![メニュータイトル(朱書き)](../../extensibility/ux-guidelines/media/0303-001_menutitleredline.png "0303-001_MenuTitleRedline")<br />メニュータイトル(朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム メニュー タイトルを作成する場合は常に、そのたびに表示されます。 | ...メニュータイトルと常に一致したくないものに対して。 |
| | ...指定以外の任意の背景/前景の組み合わせで。 |

**メニュータイトル: デフォルトの状態**

![既定のメニュー タイトル](../../extensibility/ux-guidelines/media/0303-002_menutitledefault.png "0303-002_MenuTitleDefault")<br />既定のメニュー タイトル

![グリフを含む既定のメニュー タイトル](../../extensibility/ux-guidelines/media/0303-003_menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br />グリフを含む既定のメニュー タイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Environment.CommandBarMenuGlyph` |
| Border | None |

**メニュータイトル: ホバー状態**

![ホバー時のメニュー タイトル](../../extensibility/ux-guidelines/media/0303-004_menutitlehover.png "0303-004_MenuTitleHover")<br />ホバー時のメニュー タイトル

![ホバー時のグリフのメニュー タイトル](../../extensibility/ux-guidelines/media/0303-005_menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br />ホバー時のグリフのメニュー タイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 前景 (グリフ) | `Environment.CommandBarMenuMouseOverGlyph` |
| Border | `Environment.CommandBarBorder` |

**メニュータイトル:押された状態**

![押されたメニュータイトル](../../extensibility/ux-guidelines/media/0303-006_menutitlepressed.png "0303-006_MenuTitlePressed")<br />押されたメニュータイトル

![グリフ付きの押されたメニュータイトル](../../extensibility/ux-guidelines/media/0303-007_menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br />グリフ付きの押されたメニュータイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMenuBackgroundGradientBegin`<br/>(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Environment.CommandBarMenuMouseDownGlyph` |
| Border | `Environment.CommandBarMenuBorder`<br />(左、上、右の側のみ)。 |

**メニュータイトル: 無効状態**

![グリフで無効なメニュータイトル](../../extensibility/ux-guidelines/media/0303-008_menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br />グリフで無効なメニュータイトル

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (テキスト) | `Environment.CommandBarTextInactive` |
| 前景 (グリフ) | `Environment.CommandBarTextInactive` |
| Border | None |

#### <a name="menu-items"></a>メニュー項目
個々のメニュー項目は、メニュー テキストとオプションのアイコン、チェック ボックス、またはサブメニュー グリフで構成されます。 その背景色とテキストの色はホバー時に変化します。 この色トークンは、背景と前景のペアです。

![メニュー項目の赤線](../../extensibility/ux-guidelines/media/0303-009_menuitemredline.png "0303-009_MenuItemRedline")

| 使用。。。 | 使用しないでください. |
|---|---|
| ...メニュー バーまたはコマンド バーから起動されるドロップダウン リスト。 | ...を別のコンテキストの任意のドロップダウン リストに対して使用します。 |
| | ...指定以外の任意の背景/前景の組み合わせで。 |

**メニュー項目: デフォルト状態**

![既定のメニュー項目](../../extensibility/ux-guidelines/media/0303-010_menudefault.png "0303-010_MenuDefault")<br />既定のメニュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMenuBackgroundGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (サブメニュー グリフ) | `Environment.CommandBarMenuSubmenuGlyph` |
| Border | `Environment.CommandBarMenuBorder` |
| アイコン チャネルの背景 | `Environment.CommandBarMenuIconBackground` |
| 区切り記号 | `Environment.CommandBarMenuSeparator` |
| Shadow | `Environment.DropShadowBackground` |

**メニュー項目: オン状態と選択状態**

![チェックされたメニュー](../../extensibility/ux-guidelines/media/0303-011_menuchecked.png "0303-011_MenuChecked")<br />チェックされたメニュー項目

![選択されたメニュー](../../extensibility/ux-guidelines/media/0303-012_menuselected.png "0303-012_MenuSelected")<br />選択されたメニュー項目

| 要素 | トークン名: Category.color |
| --- | --- |
| チェック マーク | `Environment.CommandBarCheckBox` |
| チェック マークの背景 | `Environment.CommandBarSelectedIcon` |
| アイコンの背景 | `Environment.CommandBarSelected` |
| アイコンの境界線 | `Environment.CommandBarSelectedBorder` |

**メニュー項目: ホバー状態**

![メニュー ホバー](../../extensibility/ux-guidelines/media/0303-013_menuhover.png "0303-013_MenuHover")<br />ホバー時のメニュー項目

![チェックされたメニュー ホバー](../../extensibility/ux-guidelines/media/0303-014_menuhoverchecked.png "0303-014_MenuHoverChecked")<br />ホバー時にオンになっているメニュー項目

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

![チェックされたメニューの無効化](../../extensibility/ux-guidelines/media/0303-017_menudisabledchecked.png "0303-017_MenuDisabledChecked")<br />無効なメニュー項目 (チェック マーク付き)

| 要素 | トークン名: Category.color |
| --- | --- |
| 前景 (テキスト) | `Environment.CommandBarTextInactive` |
| 前景 (サブメニュー グリフ) | `Environment.CommandBarMenuSubmenuGlyph` |
| チェック マーク | `Environment.CommandBarCheckBoxDisabled` |
| チェック マークの背景 | `Environment.CommandBarSelectedIconDisabled` |

### <a name="command-bars"></a>コマンド バー
コマンド バーは、Visual Studio IDE 内の複数の場所に表示できます。

通常は、Visual Studio 環境で提供される標準のコマンド バー実装を常に使用してください。 標準メカニズムを使用すると、すべての表示の詳細が正しく表示され、対話型要素が他の Visual Studio のコマンド バーのコントロールと一貫して動作するようになります。 ただし、独自のコマンド バーを作成する必要がある場合は、次のトークン名を使用してスタイルを正しく設定してください。

![コマンド バーの赤線](../../extensibility/ux-guidelines/media/0303-018_commandbarredline.png "0303-018_CommandBarRedline")<br />コマンド バー (レッドライン)

![オーバーフロー ボタンの赤線](../../extensibility/ux-guidelines/media/0303-019_overflowbuttonredline.png "0303-019_OverflowButtonRedline")<br />オーバーフロー ボタン (赤線)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...埋め込みコマンド バーが必要ですが、Visual Studio の標準のコマンド バー実装を使用できない場所で使用できます。 | ...コマンド バーと似ていない UI 要素の場合。 |
| | ...トークン名が指定されているコンポーネント以外のコマンド バー コンポーネント。 |

#### <a name="command-bar-groups"></a>コマンド バー グループ
コマンド バー グループは、関連する一連のコマンド バー コントロールで構成され、任意の数のボタン、分割ボタン、ドロップダウン メニュー、コンボ ボックス、またはメニューを含めることができます。 これらのコントロールの色は別々のトークン名によって制御され、このガイドの他の場所で個別に説明されています。 区切り線を使用して、コマンド バー グループを関連するサブグループに分割します。

![コマンド バー グループの赤線](../../extensibility/ux-guidelines/media/0303-020_commandbargroupredline.png "0303-020_CommandBarGroupRedline")<br />コマンド バー グループ (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...埋め込みコマンド バーが必要ですが、Visual Studio の標準のコマンド バー実装を使用できない場所で使用できます。 | ...コマンド バーと似ていない UI 要素の場合。 |
| | ...トークン名が指定されているコンポーネント以外のコマンド バー コンポーネント。 |

**コマンド バー グループ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| Border | `Environment.CommandBarToolBarBorder` |
| ドラッグ ハンドル | `Environment.CommandBarDragHandle` |
| 区切り記号 | `Environment.CommandBarToolBarSeparator`<br />`Environment.CommandBarToolBarSeparatorHighlight` |

#### <a name="command-icons"></a>コマンド アイコン
![コマンド アイコンの赤線](../../extensibility/ux-guidelines/media/0303-021_commandiconredline1.png "0303-021_CommandIconRedline1")<br />コマンド アイコン (朱折)

![テキストの朱書きが付いたコマンド アイコン](../../extensibility/ux-guidelines/media/0303-022_commandiconredline2.png "0303-022_CommandIconRedline2")<br />テキスト付きコマンド アイコン (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...コマンド バーに配置されるボタン。 | ...独自のトークン名を持つコントロールの場合。 |
| | ...指定以外の任意の背景/前景の組み合わせで。 |

**コマンド アイコン: 既定の状態**

![コマンド アイコンの既定値](../../extensibility/ux-guidelines/media/0303-023_commandicondefault.png "0303-023_CommandIconDefault")<br />既定のコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし (コマンド バーの背景から継承) |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| Border | 該当なし |

**コマンド アイコン: 既定の状態、選択済み**

![既定の選択されたコマンド アイコン](../../extensibility/ux-guidelines/media/0303-024_commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br />既定の選択されたコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarSelected` |
| 前景 (テキスト) | `Environment.CommandBarTextSelected` |
| Border | `Environment.CommandBarSelectedBorder` |

**コマンドアイコン:ホバー状態またはフォーカス状態**

![ホバーまたはフォーカスのコマンド アイコン](../../extensibility/ux-guidelines/media/0303-025_commandiconhover.png "0303-025_CommandIconHover")<br />ホバーまたはフォーカスのコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| Border | `Environment.CommandBarBorder` |

**コマンド アイコン: ホバー状態またはフォーカス状態、選択**

![ホバーまたはフォーカスの選択したコマンド アイコン](../../extensibility/ux-guidelines/media/0303-026_commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br />ホバーまたはフォーカスの選択したコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarHoverOverSelected` |
| 前景 (テキスト) | `Environment.CommandBarTextHoverOverSelected` |
| Border | `Environment.CommandBarHoverOverSelectedIconBorder` |

 **コマンド アイコン: 押された状態**

![押されているコマンド アイコン](../../extensibility/ux-guidelines/media/0303-027_commandiconpressed.png "0303-027_CommandIconPressed")<br />押されているコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseDownBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextMouseDown` |
| Border | `Environment.CommandBarBorder` |

**コマンド アイコン: 無効状態**

![無効化されたコマンド アイコン](../../extensibility/ux-guidelines/media/0303-028_commandicondisabled.png "0303-028_CommandIconDisabled")<br />無効化されたコマンド アイコン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし (コマンド バーの背景から継承) |
| 前景 (テキスト) | `Environment.CommandBarTextInactive` |
| Border | 該当なし |

#### <a name="command-bar-combo-boxes"></a><a name="BKMK_CommandComboBox"></a>コマンド バーのコンボ ボックス

> [!IMPORTANT]
> コンボ ボックスはドロップダウンに似ていますが、編集可能なテキスト領域が含まれます。 ドロップダウンに編集可能なテキスト領域が含まれていない場合は、[コマンド バー ドロップダウン](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandDropDown)の色のトークンを使用します。

![コマンド バーコンボ ボックスの赤線](../../extensibility/ux-guidelines/media/0303-029_comboboxredline.png "0303-029_ComboBoxRedline")<br />コマンド バーのコンボ ボックス (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム コンボ ボックスを作成する場合。 | ...コマンド バーの UI と常に一致させる必要はありません。 |
| ...コンボ ボックスに似たコマンド バー コントロールを作成するとき。 | ...スタイル付きコンボ ボックスにアクセスできる場合。 |

**コマンド バーコンボ ボックス入力フィールド: 既定の状態**

![コマンド バーコンボ ボックス入力フィールド](../../extensibility/ux-guidelines/media/0303-030_comboboxinputfield.png "0303-030_ComboBoxInputField")<br />コマンド バーコンボ ボックス入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxBackground` |
| 前景 (テキスト) | `Environment.ComboBoxText` |
| Border | `Environment.ComboBoxBorder` |
| 区切り記号 | 区切り記号なし |

**コマンド バーのドロップダウン ボタン: 既定の状態**

![コンボ ボックスのドロップダウン&#45;ダウン ボタン](../../extensibility/ux-guidelines/media/0303-031_comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br />コマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし (コマンド バーの背景から継承) |
| 前景 (グリフ) | `Environment.ComboBoxGlyph` |

**コマンド バードロップダウン リスト: 既定の状態**

![コマンド バードロップダウン リスト](../../extensibility/ux-guidelines/media/0303-032_comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br />コマンド バードロップダウン リスト

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxPopupBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.ComboBoxItemText` |
| Border | `Environment.ComboBoxPopupBorder` |

**コマンド バーコンボ ボックス入力フィールド: ホバー状態**

![ホバー時のコマンド バー コンボ ボックス入力フィールド](../../extensibility/ux-guidelines/media/0303-033_comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br />ホバー時のコマンド バー コンボ ボックス入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.ComboBoxMouseOverText` |
| Border | `Environment.ComboBoxMouseOverBorder` |
| 区切り記号 | `Environment.ComboBoxMouseOverSeparator` |

 **コマンド バーのドロップダウン ボタン: ホバー状態**

![ホバー時のコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-034_comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br />ホバー時のコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxButtonMouseOverBackground` |
| 前景 (グリフ) | `Environment.ComboBoxMouseOverGlyph` |

**コマンド バー ドロップダウン リスト: ホバー状態**

 ![ホバー時のコマンド バー ドロップダウン リスト](../../extensibility/ux-guidelines/media/0303-035_comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br />ホバー時のコマンド バー ドロップダウン リスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (メニュー項目) | `Environment.ComboBoxItemMouseOverBackground` |
| 前景 (テキスト) | `Environment.ComboBoxItemMouseOverText` |
| 境界線 (メニュー項目) | `Environment.ComboBoxItemMouseOverBorder` |

 **コマンド バーコンボ ボックス入力フィールド: フォーカス状態**

![フォーカスのあるコマンド バーコンボ ボックス入力フィールド](../../extensibility/ux-guidelines/media/0303-036_comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br />フォーカスのあるコマンド バーコンボ ボックス入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxFocusedBackground` |
| 前景 (テキスト) | `Environment.ComboBoxFocusedText` |
| Border | `Environment.ComboBoxFocusedBorder` |
| 区切り記号 | `Environment.ComboBoxFocusedButtonSeparator` |

**コマンド バーのドロップダウン ボタン: フォーカス状態**

![フォーカスのあるコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-037_comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br />フォーカスのあるコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxFocusedButtonBackground` |
| 前景 (グリフ) | `Environment.ComboBoxFocusedGlyph` |

 **コマンド バーコンボ ボックス入力フィールド: 押された状態**

![押されたコマンド バー コンボ ボックス入力フィールド](../../extensibility/ux-guidelines/media/0303-038_comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br />押されたコマンド バー コンボ ボックス入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxMouseDownBackground` |
| 前景 (テキスト) | `Environment.ComboBoxMouseDownText` |
| Border | `Environment.ComboBoxMouseDownBorder` |
| 区切り記号 | `Environment.ComboBoxMouseDownSeparator` |

**コマンド バーのドロップダウン ボタン: 押された状態**

![押されたコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-039_comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br />押されたコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxButtonMouseDownBackground` |
| 前景 (グリフ) | `Environment.ComboBoxMouseDownGlyph` |

**コマンド バーコンボ ボックス入力フィールド: 無効状態**

![無効なコマンド バー コンボ ボックス入力フィールド](../../extensibility/ux-guidelines/media/0303-041_comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br />無効なコマンド バー コンボ ボックス入力フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ComboBoxDisabledBackground` |
| 前景 (テキスト) | `Environment.ComboBoxDisabledText` |
| Border | `Environment.ComboBoxDisabledBorder` |
| 区切り記号 | 区切り記号なし |

**コマンド バーのドロップダウン ボタン: 無効な状態**

![無効なコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-040_comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br />無効なコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (グリフ) | `Environment.ComboBoxDisabledGlyph` |

#### <a name="command-bar-drop-downs"></a><a name="BKMK_CommandDropDown"></a>コマンド バーのドロップダウン

> [!IMPORTANT]
> ドロップダウンはコンボ ボックスに似ていますが、編集可能なテキスト領域がありません。 ドロップダウンに編集可能なテキスト領域が含まれている場合は、[コマンド バーのコンボ ボックス](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandComboBox)の色のトークンを使用します。

![コマンド バー ドロップダウン (朱折り)](../../extensibility/ux-guidelines/media/0303-042_dropdownredline.png "0303-042_DropdownRedline")<br />コマンド バー ドロップダウン (朱折り)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタムドロップダウン リスト コントロールを作成する場合。 | ...ドロップダウン リストに類似していないものに対して。 |
| | ...コンボ ボックスまたは分割ボタンの場合。 |

**コマンド バーのドロップダウン選択フィールド: 既定の状態**

![既定のコマンド バードロップダウン選択フィールド](../../extensibility/ux-guidelines/media/0303-043_dropdownselectionfield.png "0303-043_DropdownSelectionField")<br />既定のコマンド バードロップダウン選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownBackground` |
| 前景 (テキスト) | `DropDownText` |
| Border | `DropDownBorder` |
| 区切り記号 | 区切り記号なし |

**コマンド バーのドロップダウン ボタン: 既定の状態**

![既定のコマンド バー ドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-044_dropdownbutton.png "0303-044_DropdownButton")<br />既定のコマンド バー ドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (グリフ) | `Environment.DropDownGlyph` |

**コマンド バードロップダウン リスト: 既定の状態**

![既定のコマンド バー ドロップダウン リスト](../../extensibility/ux-guidelines/media/0303-045_dropdownlist.png "0303-045_DropdownList")<br />既定のコマンド バー ドロップダウン リスト

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownPopupBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.ComboBoxItemText` |
| Border | `Environment.DropDownPopupBorder` |
| Shadow | `Environment.DropShadowBackground` |

**コマンド バーのドロップダウン選択フィールド: ホバー状態**

![ホバー時のコマンド バードロップダウン選択フィールド](../../extensibility/ux-guidelines/media/0303-046_dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br />ホバー時のコマンド バードロップダウン選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.DropDownMouseOverText` |
| Border | `Environment.DropDownMouseOverBorder` |
| 区切り記号 | `Environment.DropDownButtonMouseOverSeparator` |

**コマンド バーのドロップダウン ボタン: ホバー状態**

![ホバー時のコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-047_dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br />ホバー時のコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownButtonMouseOverBackground` |
| 前景 (グリフ) | `Environment.DropDownMouseOverGlyph` |

**コマンド バー ドロップダウン リスト: ホバー状態**

![ホバー時のコマンド バー ドロップダウン リスト](../../extensibility/ux-guidelines/media/0303-048_dropdownlisthover.png "0303-048_DropdownListHover")<br />ホバー時のコマンド バー ドロップダウン リスト

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (メニュー項目) | `Environment.ComboBoxItemMouseOverBackground` |
| 前景 (テキスト) | `Environment.ComboBoxItemMouseOverText` |
| 境界線 (メニュー項目) | `Environment.ComboBoxItemMouseOverBorder` |

 **コマンド バードロップダウン選択フィールド: 押された状態**

![ドロップダウン&#45;選択フィールドが押された](../../extensibility/ux-guidelines/media/0303-049_dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br />押されたコマンド バードロップダウン選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownMouseDownBackground` |
| 前景 (テキスト) | `Environment.DropDownMouseDownText` |
| Border | `Environment.DropDownMouseDownBorder` |
| 区切り記号 | `Environment.DropDownButtonMouseDownSeparator` |

**コマンド バーのドロップダウン ボタン: 押された状態**

![押されたコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-050_dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br />押されたコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownButtonMouseDownBackground` |
| 前景 (グリフ) | `Environment.DropDownMouseDownGlyph` |

**コマンド バーのドロップダウン選択フィールド: 無効な状態**

![無効なコマンド バードロップダウン 選択フィールド](../../extensibility/ux-guidelines/media/0303-051_dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")<br />無効なコマンド バードロップダウン 選択フィールド

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DropDownDisabledBackground` |
| 前景 (テキスト) | `Environment.DropDownDisabledText` |
| Border | `Environment.DropDownDisabledBorder` |
| 区切り記号 | 区切り記号なし |

**コマンド バーのドロップダウン ボタン: 無効な状態**

![無効なコマンド バーのドロップダウン ボタン](../../extensibility/ux-guidelines/media/0303-052_dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")<br />無効なコマンド バーのドロップダウン ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Environment.DropDownDisabledGlyph` |

#### <a name="command-bar-split-buttons"></a>コマンド バーの分割ボタン
分割ボタンは、ボタン、メニュー、コマンド バー テキストなど、他のコマンド バー コントロールと多くのトークン名を共有します。 ここでは利便性のために、すべての必要なアクション ボタンとドロップダウン ボタンのトークン名を繰り返しています。 [分割] ボタンのドロップダウン リストは[、コマンド バー メニュー](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)の実装です。

![分割ボタンの赤線](../../extensibility/ux-guidelines/media/0303-053_splitbuttonredline.png "0303-053_SplitButtonRedline")<br />コマンド バーの分割ボタン (朱折り)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム分割ボタンを作成する場合。 | ...他の種類のボタンの場合。 |
| | ...指定以外の任意の背景/前景の組み合わせで。 |

**コマンド バー分割ボタン: 既定の状態**

![既定のコマンド バー分割ボタン](../../extensibility/ux-guidelines/media/0303-054_splitbutton.png "0303-054_SplitButton")<br />既定のコマンド バー分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | None |
| 前景 (テキスト) | `Environment.CommandBarTextActive` |
| 前景 (グリフ) | `Environment.CommandBarSplitButtonGlyph` |
| Border | 該当なし |
| 区切り記号 | 該当なし |

**コマンド バー分割ボタン: ホバー状態**

![ホバー時のコマンド バー分割ボタン](../../extensibility/ux-guidelines/media/0303-055_splitbuttonhover.png "0303-055_SplitButtonHover")<br />ホバー時のコマンド バー分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextHover` |
| 前景 (グリフ) | `Environment.CommandBarSplitButtonMouseOverGlyph` |
| Border | `Environment.CommandBarBorder` |
| 区切り記号 | `Environment.CommandBarSplitButtonSeparator` |

**コマンド バー分割ボタン: 押された状態**

![押されたコマンド バー分割ボタン](../../extensibility/ux-guidelines/media/0303-056_splitbuttonpressed.png "0303-056_SplitButtonPressed")<br />押されたコマンド バー分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarMouseDownBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.CommandBarTextMouseDown` |
| 前景 (グリフ) | `Environment.CommandBarSplitButtonMouseDownGlyph` |
| Border | `Environment.CommandBarBorder` |
| 区切り記号 | 該当なし |

**コマンド バー分割ボタン: 無効状態**

![無効なコマンド バー分割ボタン](../../extensibility/ux-guidelines/media/0303-057_splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br />無効なコマンド バー分割ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (テキスト) | `Environment.ComboBoxItemTextInactive` |
| 前景 (グリフ) | `Environment.CommandBarTextInactive` |
| Border | 該当なし |
| 区切り記号 | 該当なし |

#### <a name="command-bar-more-options-and-overflow-buttons"></a>コマンド バー 'その他のオプション' と 'オーバーフロー' ボタン
[その他のオプション] ボタンは、関連するコマンド バー ボタンを追加または削除して、コマンド バー グループをカスタマイズできる場合に使用します。 [オーバーフロー] ボタンは、横のスペースが不足しているためにコマンド バーが切り詰められた場合に表示され、クリックすると、表示できないコマンド バー ボタンを含むメニューが表示されます。 これら 2 つのボタンの色は、同じトークン名のセットによって制御されます。

![コマンド バーの [その他のオプション] ボタン (レッドライン)](../../extensibility/ux-guidelines/media/0303-058_moreoptionsredline.png "0303-058_MoreOptionsRedline")<br />コマンド バーの [その他のオプション] ボタン (レッドライン)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタムの 「その他のオプション」または「オーバーフロー」ボタンの場合。 | ...[その他のオプション] ボタンや [オーバーフロー] ボタンと同様の機能を持たないボタンの場合 |

**コマンド バーの [その他のオプション] ボタンと [オーバーフロー] ボタン: 既定の状態**

![既定のコマンド バー 'その他のオプション' ボタン](../../extensibility/ux-guidelines/media/0303-059_moreoptions.png "0303-059_MoreOptions")<br />既定のコマンド バー 'その他のオプション' ボタン

![デフォルトのコマンドバー'オーバーフロー'ボタン](../../extensibility/ux-guidelines/media/0303-060_overflow.png "0303-060_Overflow")<br />デフォルトのコマンドバー'オーバーフロー'ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarOptionsBackground` |
| 前景 (グリフ) | `Environment.CommandBarOptionsGlyph` |

**コマンド バーの [その他のオプション] ボタンと [オーバーフロー] ボタン: ホバー状態**

![ホバー時のコマンドバー'その他のオプション'ボタン](../../extensibility/ux-guidelines/media/0303-061_moreoptionshover.png "0303-061_MoreOptionsHover")<br />ホバー時のコマンドバー'その他のオプション'ボタン

![ホバー時のコマンドバー'オーバーフロー'ボタン](../../extensibility/ux-guidelines/media/0303-062_overflowoptions.png "0303-062_OverflowOptions")<br />ホバー時のコマンドバー'オーバーフロー'ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarOptionsMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (グリフ) | `Environment.CommandBarOptionsMouseDownGlyph` |

**コマンド バーの [その他のオプション] ボタンと [オーバーフロー] ボタン: 押された状態**

![押されたコマンド バー 'その他のオプション' ボタン](../../extensibility/ux-guidelines/media/0303-063_moreoptionspressed.png "0303-063_MoreOptionsPressed")<br />押されたコマンド バー 'その他のオプション' ボタン

![押されたオーバーフロー](../../extensibility/ux-guidelines/media/0303-064_overflowpressed.png "0303-064_OverflowPressed")<br />押されたコマンド バー 'オーバーフロー' ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.CommandBarOptionsMouseDownBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (グリフ) | `Environment.CommandBarOptionsMouseDownGlyph` |

## <a name="document-windows"></a>ドキュメント ウィンドウ
ドキュメント ウィンドウは Visual Studio 環境によって提供されるため、レプリケートする必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一貫性のある状態で表示されるように、ドキュメント ウィンドウで使用する色を活用することができます。

ドキュメント ウィンドウのカラー トークンを使用する場合は、同じような要素にのみ使用し、常にペアで使用するように注意してください。 これを行わない場合は、UI で予期しない結果が発生する可能性があります。

### <a name="document-window-frames"></a>ドキュメント ウィンドウのフレーム
ドキュメント ウィンドウは IDE にドッキングしたり、別のウィンドウとしてフローティングさせたりすることができます。 ドキュメントウィンドウが IDE の外側に浮かんでいる場合でも、ドキュメントウェルに位置し、IDE の一部のときと同じ背景、枠線、テキスト、タブの色が表示されます。 ただし、ドキュメントは、独自の背景、境界線、テキストの色を持つフレーム内に配置されます。 ツール ウィンドウをドキュメント ウェルにドッキングした場合、ツール ウィンドウはタブの動作と色をドキュメント ウィンドウのトークン名から継承します。

![ドッキングされたドキュメント ウィンドウ (朱書き)](../../extensibility/ux-guidelines/media/0303-065_dockeddocumentwindowredline.png "0303-065_DockedDocumentWindowRedline")<br />ドッキングされたドキュメント ウィンドウ (朱書き)

![フローティング ドキュメント ウィンドウ (朱書き)](../../extensibility/ux-guidelines/media/0303-066_floatingdocumentwindowredline.png "0303-066_FloatingDocumentWindowRedline")<br />フローティング ドキュメント ウィンドウ (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ドキュメント ウィンドウに合わせて UI を作成する場合は、どこにでもいます。 | ... シェルにテーマの更新がある場合に自動的に変更しない UI。 |

**ドッキングまたはフローティング ドキュメント ウィンドウ: 既定の状態**

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | ドキュメントの種類によって異なります |
| 前景 (テキスト) | ドキュメントの種類によって異なります |
| Border | `Environment.ToolWindowBorder` |

**フォーカスが置かれたフローティング ドキュメント ウィンドウ フレーム: 既定の状態**

![既定のフォーカスのあるフローティング ドキュメント ウィンドウ フレーム](../../extensibility/ux-guidelines/media/0303-067_framefocused.png "0303-067_FrameFocused")<br />既定のフォーカスのあるフローティング ドキュメント ウィンドウ フレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowFloatingFrame` |
| 前景 (テキスト) | `Environment.ToolWindowFloatingFrame` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonActiveGlyph` |
| Border | `Environment.MainWindowActiveDefaultBorder` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonActiveBorder`<br />(透明に設定) |

**フォーカスされていないフローティング ドキュメント ウィンドウ フレーム: 既定の状態**

![既定のフォーカスなし、フローティング ドキュメント ウィンドウ フレーム](../../extensibility/ux-guidelines/media/0303-068_frameunfocused.png "0303-068_FrameUnfocused")<br />既定のフォーカスなし、フローティング ドキュメント ウィンドウ フレーム

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowFloatingFrameInactive` |
| 前景 (テキスト) | `Environment.ToolWindowFloatingFrameInactive` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonInactiveGlyph` |
| Border | `Environment.MainWindowInactiveBorder` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonInactiveBorder`<br />(透明に設定) |

**フォーカスが置かれたフローティング ドキュメント ウィンドウ フレーム: ホバー状態**

![フォーカスが置かれたフローティング ドキュメント ウィンドウ フレーム (ホバー時)](../../extensibility/ux-guidelines/media/0303-069_framefocusedhover.png "0303-069_FrameFocusedHover")<br />フォーカスが置かれたフローティング ドキュメント ウィンドウ フレーム (ホバー時)

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (グリフ) | `Environment.RaftedWindowButtonHoverActive` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonHoverActiveGlyph` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonHoverActiveBorder` |

**フォーカスされていないフローティング ドキュメント ウィンドウ フレーム: ホバー状態**

![フォーカスが設定されていない、フローティング ドキュメント ウィンドウ フレームがホバーされた場合](../../extensibility/ux-guidelines/media/0303-070_frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br />フォーカスが設定されていない、フローティング ドキュメント ウィンドウ フレームがホバーされた場合

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (グリフ) | `EnvironmentRaftedWindowButtonHoverInactive` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonHoverInactiveGlyph` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonHoverInactiveBorder` |

**フォーカスが置かれたフローティング ドキュメント ウィンドウ フレーム: 押された状態**

![フォーカスを持つフローティング ドキュメント ウィンドウ フレームを押す](../../extensibility/ux-guidelines/media/0303-071_framefocusedpressed.png "0303-071_FrameFocusedPressed")<br />フォーカスを持つフローティング ドキュメント ウィンドウ フレームを押す

| 要素 | トークン名: Category.color |
| --- | --- |
| 背景 (グリフ) | `Environment.RaftedWindowButtonDown` |
| 前景 (グリフ) | `Environment.RaftedWindowButtonDownGlyph` |
| 境界線 (グリフ) | `Environment.RaftedWindowButtonDownBorder` |

### <a name="document-tabs"></a>ドキュメント タブ
ドキュメント タブはタブ チャネル内に存在し、現在どのドキュメントが開いているか、およびどのドキュメントが現在選択されているか、またはアクティブなドキュメントであるかを示します。 ツール ウィンドウも、ユーザーが配置した場合、ドキュメント タブ チャネルにドッキングできます。 この場合、ツール ウィンドウではドキュメント ウィンドウと同じタブの色が使用されます。 ドキュメント ウィンドウの色と常に一致する UI を作成する場合は (テーマの更新や、新しいテーマがインストールされた場合を含む)、これらの色のトークンを参照します。

![ドキュメントタブ (朱書き)](../../extensibility/ux-guidelines/media/0303-072_documenttabredline.png "0303-072_DocumentTabRedline")<br />ドキュメントタブ (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ドキュメント タブを一致させ、テーマの更新や新しいテーマの色を自動的に取得する UI を作成する場所。 | ...シェルにテーマの更新が含まれている場合に自動的に変更したくない UI。 |

#### <a name="open-document-tabs"></a>開いているドキュメントのタブ
開いている各ドキュメントには、ドキュメント タブ チャネルに名前を表示するタブがあります。 ドキュメントはバックグラウンドで選択したり開いたりすることができ、タブはこれらの状態を反映します。

- 選択されているタブは、現在ドキュメント ウェルに表示されているドキュメントを表します。 選択されているタブには、ドキュメント ウェルの上端にまたがって拡張するドキュメントの境界線があります。

- 背景タブは、現在選択されているタブではないドキュメントタブです。クリックすると、選択されたタブになり、それらのトークン名からすべての背景、境界線、およびテキストの色を取得します。

![[ドキュメントを開く] タブ (朱書き)](../../extensibility/ux-guidelines/media/0303-073_opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")<br />[ドキュメントを開く] タブ (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタムドキュメントタブを作成する場合。 | ...暫定 (プレビュー) タブ用。 |
| | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

**選択されたフォーカスのあるドキュメント タブ**

![選択されたフォーカスのあるドキュメント タブ](../../extensibility/ux-guidelines/media/0303-074_selectedtabfocused.png "0303-074_SelectedTabFocused")<br />選択されたフォーカスのあるドキュメント タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabSelectedGradientTop`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.FileTabSelectedText` |
| Border | `Environment.FileTabSelectedBorder`<br />(背景と同じ色に設定します。 |
| ドキュメントの境界線 | `Environment.FileTabDocumentBorderBackground` |

**選択された、フォーカスのないドキュメント タブ**

![選択された、フォーカスのないドキュメント タブ](../../extensibility/ux-guidelines/media/0303-075_selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br />選択された、フォーカスのないドキュメント タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabInactiveGradientTop`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.FileTabInactiveText` |
| Border | `Environment.FileTabInactiveBorder`<br />(背景と同じ色に設定します。 |
| ドキュメントの境界線 | `Environment.FileTabInactiveDocumentBorderBackground` |

**[バックグラウンド ドキュメント] タブ: 既定の状態**

![既定の背景ドキュメント タブ](../../extensibility/ux-guidelines/media/0303-076_backgroundtab.png "0303-076_BackgroundTab")<br />既定の背景ドキュメント タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabBackground` |
| 前景 (テキスト) | `Environment.FileTabText` |
| Border | `Environment.FileTabBorder`<br />(背景と同じ色に設定します。 |

**[バックグラウンド ドキュメント] タブ: ホバー状態**

![ホバー時の [バックグラウンド ドキュメント] タブ](../../extensibility/ux-guidelines/media/0303-077_backgroundtabhover.png "0303-077_BackgroundTabHover")<br />ホバー時の [バックグラウンド ドキュメント] タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabHotGradientTop`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.FileTabHotText` |
| Border | `Environment.FileTabHotBorder`<br />(背景と同じ色に設定します。 |

#### <a name="preview-tab"></a>プレビュー タブ
「暫定」タブとも呼ばれます。プレビュー タブは、ユーザーがソリューション エクスプローラー のツール ウィンドウで項目をクリックすると、ドキュメント タブ チャネルの右側に表示されます。 プレビュー タブはドキュメントのプレビューとして機能し、ユーザーはドキュメント タブ チャネルの左側でドキュメントを開いたままにできます。 プレビュー タブは一度に 1 つのみ開くことができます。 プレビュー タブには、開いているタブと同様に、背景と選択された状態の両方があり、アクティブな状態でフォーカスされている場合とフォーカスされていない場合があります。

![[プレビュー] タブ (朱折)](../../extensibility/ux-guidelines/media/0303-078_previewtabredline.png "0303-078_PreviewTabRedline")<br />[プレビュー] タブ (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...暫定プレビューを作成している任意の場所で、一部の要素が現在のプレビュータブの色と一致するようにします。 | ...暫定的でないドキュメントまたはタブの種類 (プレビュー) に対して。 |
| | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

**フォーカスのある選択したプレビュー タブ**

![フォーカスのある選択したプレビュー タブ](../../extensibility/ux-guidelines/media/0303-079_previewtabfocused.png "0303-079_PreviewTabFocused")<br />フォーカスのある選択したプレビュー タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalSelectedActive` |
| 前景 (テキスト) | `Environment.FileTabProvisionalSelectedActiveForeground` |
| Border | `Environment.FileTabProvisionalSelectedActiveBorder`<br />(背景と同じ色に設定します。 |
| ドキュメントの境界線 | `Environment.FileTabProvisionalSelectedActiveBorder` |

**フォーカスが設定されていない、選択したプレビュー タブ**

![フォーカスが設定されていない、選択したプレビュー タブ](../../extensibility/ux-guidelines/media/0303-080_previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br />フォーカスが設定されていない、選択したプレビュー タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalSelectedInactive` |
| 前景 (テキスト) | `Environment.FileTabProvisionalSelectedInactiveForeground` |
| Border | `Environment.FileTabProvisionalSelectedInactiveBorder` |
| ドキュメントの境界線 | `Environment.FileTabProvisionalSelectedInactiveBorder` |

**[バックグラウンド プレビュー] タブ: 既定の状態**

![既定の背景プレビュー タブ](../../extensibility/ux-guidelines/media/0303-081_previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br />既定の背景プレビュー タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalInactive` |
| 前景 (テキスト) | `Environment.FileTabProvisionalInactiveForeground` |
| Border | `Environment.FileTabProvisionalInactiveBorder`<br />(背景と同じ色に設定します。 |

**[バックグラウンドプレビュー] タブ: ホバー状態**

![ホバー時の [バックグラウンド プレビュー] タブ](../../extensibility/ux-guidelines/media/0303-082_previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br />ホバー時の [バックグラウンド プレビュー] タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.FileTabProvisionalHover` |
| 前景 (テキスト) | `Environment.FileTabProvisionalHoverForeground` |
| Border | `Environment.FileTabProvisionalHoverBorder`<br />(背景と同じ色に設定します。 |

#### <a name="document-overflow-button"></a>ドキュメント オーバーフロー ボタン
ドキュメント オーバーフロー ボタンは、すべてのドキュメント タブに適した垂直スペースが現在の構成にあるかどうかに関係なく、1 つ以上のドキュメントが開いている場合に表示されます。 [コマンド バーのメニュー](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_CommandMenus)の色で制御されるドキュメント オーバーフロー ドロップダウン メニューには、開いているすべてのドキュメントの一覧が表示され、開いているドキュメントがすべてタブ チャネルに表示されているかどうかに応じてオーバーフロー グリフが変化します。

![ドキュメントオーバーフローボタン (朱書き)](../../extensibility/ux-guidelines/media/0303-083_overflowredline.png "0303-083_OverflowRedline")<br />ドキュメントオーバーフローボタン (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...カスタム ドキュメント オーバーフロー ボタンを作成する場合。 | ...オーバーフロー ボタンと似ていない UI の場合。 |
| | ...コマンド バーのオーバーフロー ボタンの場合。 |

**ドキュメント オーバーフロー ボタン: 既定の状態**

![既定のドキュメント オーバーフロー ボタン](../../extensibility/ux-guidelines/media/0303-084_overflow.png "0303-084_Overflow")<br />既定のドキュメント オーバーフロー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DocWellOverflowButtonBackground` |
| 前景 (グリフ) | `Environment.DocWellOverflowButtonGlyph` |
| Border | 該当なし |

**ドキュメントオーバーフローボタン: ホバー状態**

![ホバー時のドキュメント オーバーフロー ボタン](../../extensibility/ux-guidelines/media/0303-085_overflowhover.png "0303-085_OverflowHover")<br />ホバー時のドキュメント オーバーフロー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DocWellOverflowButtonMouseOverBackground` |
| 前景 (グリフ) | `Environment.DocWellOverflowButtonMouseOverGlyph` |
| Border | `Environment.DocWellOverflowButtonMouseOverBorder` |

**ドキュメント オーバーフロー ボタン: 押された状態**

![押す時のドキュメント オーバーフロー ボタン](../../extensibility/ux-guidelines/media/0303-086_overflowpressed.png "0303-086_OverflowPressed")<br />押す時のドキュメント オーバーフロー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.DocWellOverflowButtonMouseDownBackground` |
| 前景 (グリフ) | `Environment.DocWellOverflowButtonMouseDownGlyph` |
| Border | `Environment.DocWellOverflowButtonMouseDownBorder` |

### <a name="tagging"></a>タグ付け
Visual Studio は、タグ付けをサポートしています。タグ付けにより、ユーザーは追跡のために検索可能なキーワードを宣言できます。 たとえば、プロジェクト マネージャーと開発者は、Team Foundation Server (TFS) を使用して作業項目にタグを付けることができます。 次の表に、タグ自体と、ホバー時および選択済み状態で表示される "アイコンを閉じる" グリフの両方の色の名前を示します。

![ビジュアル スタジオでのタグ付け (朱折り)](../../extensibility/ux-guidelines/media/0303-176_taggingredline.png "0303-176_TaggingRedline")<br />ビジュアル スタジオでのタグ付け (朱折り)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...タグ付けをサポートする UI 用。 | ...その他の種類の UI の場合。 |

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

**タグ: 選択した状態**

![選択したタグ](../../extensibility/ux-guidelines/media/0303-180_tagselected.png "0303-180_TagSelected")<br />選択したタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.SelectedBackground` |
| 前景 (テキスト) | `Tag.SelectedBackgroundText` |

#### <a name="close-times-tag-glyph"></a>クローズ&times;( ) タググリフ

**クローズ&times;( ) タググリフ: デフォルト状態**

![既定のクローズ&times;( ) タグ グリフ](../../extensibility/ux-guidelines/media/0303-181_tagglyph.png "0303-181_TagGlyph")<br />既定のクローズ&times;( ) タグ グリフ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Tag.TagHoverGlyph` |

**閉じる&times;( ) タググリフ: ホバー状態**

![閉じる&times;( ) タググリフをホバー時に](../../extensibility/ux-guidelines/media/0303-182_tagglyphhover.png "0303-182_TagGlyphHover")<br />閉じる&times;( ) タググリフをホバー時に

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagHoverGlyphHoverBackground` |
| 前景 (グリフ) | `Tag.TagHoverGlyphHover` |
| Border | `Tag.TagHoverGlyphHoverBorder` |

**閉じる&times;( ) タググリフ: 押された状態**

![押されたクローズ&times;( ) タググリフ](../../extensibility/ux-guidelines/media/0303-183_tagglyphpressed.png "0303-183_TagGlyphPressed")<br />押されたクローズ&times;( ) タググリフ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagHoverGlyphPressedBackground` |
| 前景 (グリフ) | `Tag.TagHoverGlyphPressed` |
| Border | `Tag.TagHoverGlyphPressedBorder` |

**クローズ ( )&times;グリフを含む選択されたタグ: デフォルト状態**

![クローズ ( )&times;グリフを持つ既定の選択されたタグ](../../extensibility/ux-guidelines/media/0303-184_tagselected.png "0303-184_TagSelected")<br />クローズ ( )&times;グリフを持つ既定の選択されたタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Tag.TagSelectedGlyph` |

**閉じる (&times;) グリフを含む選択されたタグ: ホバー状態**

![閉じる (&times;) グリフがホバーされた状態で選択されたタグ](../../extensibility/ux-guidelines/media/0303-185_tagselectedhover.png "0303-185_TagSelectedHover")<br />閉じる (&times;) グリフがホバーされた状態で選択されたタグ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagSelectedGlyphHoverBackground` |
| 前景 (グリフ) | `Tag.TagSelectedGlyphHover` |
| Border | `Tag.TagSelectedGlyphHoverBorder` |

**閉じる ()&times;グリフを含む選択されたタグ: 押された状態**

![選択済み、押されたタグ&times;と閉じる ( ) グリフ](../../extensibility/ux-guidelines/media/0303-186_tagselectedpressed.png "0303-186_TagSelectedPressed")<br />選択済み、押されたタグ&times;と閉じる ( ) グリフ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Tag.TagSelectedGlyphPressedBackground` |
| 前景 (グリフ) | `Tag.TagSelectedGlyphPressed` |
| Border | `Tag.TagSelectedGlyphPressedBorder` |

## <a name="tool-windows"></a>ツール ウィンドウ
ツール ウィンドウは Visual Studio 環境によって提供されるため、ツール ウィンドウをレプリケートする必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一貫性のある状態で表示されるように、ツール ウィンドウで使用する色を活用することができます。

![ツール ウィンドウ (レッドライン)](../../extensibility/ux-guidelines/media/0303-087_toolwindowredline.png "0303-087_ToolWindowRedline")<br />ツール ウィンドウ (レッドライン)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ツール ウィンドウに合わせて UI を作成する場合はどこでも使用できます。 | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

### <a name="tool-window-frame"></a>ツール ウィンドウ フレーム
Visual Studio のツール ウィンドウはさまざまなタスクに使用され、いくつかの異なる状態の 1 つで配置できます。 ツール ウィンドウが開いている場合、ドキュメント領域の 4 辺のいずれかに割り当てることができます。 ツール ウィンドウは IDE の外部でフローティングさせることもでき、ユーザーの画面内の任意の場所に再配置できます。 フローティング ウィンドウは、常に IDE の一番上に配置されます。 最後に、ツール ウィンドウはドキュメント ウィンドウとしてドッキングし、ドキュメント ウェルのタブとして表示できます。 ドキュメント ウィンドウとしてドッキングされたツール ウィンドウは、ドキュメント ウィンドウのトークン名を使用して一部の色が付けられます。

![ツール ウィンドウフレーム (朱折)](../../extensibility/ux-guidelines/media/0303-088_toolwindowframeredline.png "0303-088_ToolWindowFrameRedline")<br />ツール ウィンドウフレーム (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ... ツール ウィンドウに合わせて UI を作成する場合はどこでも使用できます。 | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

**ドッキングツールウィンドウ**

![ドッキングツールウィンドウ](../../extensibility/ux-guidelines/media/0303-089_toolwindowdocked.png "0303-089_ToolWindowDocked")<br />ドッキングツールウィンドウ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowBackground` |
| Border | `Environment.ToolWindowBorder` |

**浮動、フォーカスのあるツール ウィンドウ**

![浮動、フォーカスのあるツール ウィンドウ](../../extensibility/ux-guidelines/media/0303-090_toolwindowfocused.png "0303-090_ToolWindowFocused")<br />浮動、フォーカスのあるツール ウィンドウ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowBackground` |
| Border | `Environment.MainWindowActiveDefaultBorder` |

**浮動、フォーカスのないツール ウィンドウ**

![浮動、フォーカスのないツール ウィンドウ](../../extensibility/ux-guidelines/media/0303-091_toolwindowunfocused.png "0303-091_ToolWindowUnfocused")<br />浮動、フォーカスのないツール ウィンドウ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowBackground` |
| Border | `Environment.MainWindowInactiveBorder` |

### <a name="toolbox-like-windows"></a>ツールボックスのようなウィンドウ
ツールボックスは、Visual Studio で最もよく使用される一般的なツール ウィンドウの 1 つです。 これは本質的に特別なテーマとスタイルが適用されたツリーコントロールです。

![ツールボックスのようなウィンドウ (赤線)](../../extensibility/ux-guidelines/media/0303-189_toolboxredline.png "0303-189_ToolboxRedline")<br />ツールボックスのようなウィンドウ (赤線)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ツール ウィンドウをデザインするときに、常にシェル ツールボックスと一貫性を保つ必要があります。 | ...ツールボックス UI と似ていないもの、またはシェル ツールボックスの色が変わった場合に UI に問題が発生するかどうかが不明な場合。 |

**ツールボックス ノード: 既定の状態**

![既定のツールボックスの親ノード](../../extensibility/ux-guidelines/media/0303-190_toolboxparentnode.png "0303-190_ToolboxParentNode")<br />既定のツールボックスの親ノード

![既定のツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-191_toolboxchildnode.png "0303-191_ToolboxChildNode")<br />既定のツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolboxContent`<br />(見出し) |
| バックグラウンド | `Environment.ToolWindowBackground`<br />(個々の項目、または使用可能なコントロールがない場合はウィンドウ全体) |
| Border | None |
| 前景 (グリフ) | `Environment.ToolboxContent` |
| 前景 (テキスト) | `Environment.ToolboxContent` |

**ツールボックスの子ノード: ホバー状態**

![ホバー時のツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-192_toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br />ホバー時のツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolboxContentMouseOver`<br />(個別アイテムのみ) |
| Border | None |
| 前景 (テキスト) | `Environment.ToolboxContentMouseOver`<br />(個別アイテムのみ) |

**選択されたツールボックス ノード: フォーカス状態**

![フォーカスが置かれた、選択したツールボックスの親ノード](../../extensibility/ux-guidelines/media/0303-193_toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br />フォーカスが置かれた、選択したツールボックスの親ノード

![フォーカスが置かれた、選択されたツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-194_toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br />フォーカスが置かれた、選択されたツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemActive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| Border | `TreeView.FocusVisualBorder`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 前景 (グリフ) | `TreeView.SelectedItemActive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 前景 (テキスト) | `TreeView.SelectedItemActive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |

**選択したツールボックス ノード: フォーカスなしの状態**

![選択された、フォーカスされていないツールボックスの親ノード](../../extensibility/ux-guidelines/media/0303-195_toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br />選択された、フォーカスされていないツールボックスの親ノード

![選択された、フォーカスされていないツールボックスの子ノード](../../extensibility/ux-guidelines/media/0303-196_toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br />選択された、フォーカスされていないツールボックスの子ノード

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `TreeView.SelectedItemInactive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| Border | None |
| 前景 (グリフ) | `TreeView.SelectedItemInactive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |
| 前景 (テキスト) | `TreeView.SelectedItemInactive`<br />[Tree view](../../extensibility/ux-guidelines/shared-colors-for-visual-studio.md#BKMK_TreeView) カテゴリから |

### <a name="tool-window-title-bar"></a>ツール ウィンドウのタイトル バー
タイトル バーの境界線は、実際の境界線ではなく、タイトル バーの上部に太い線が表示されます。 フォーカスのない状態のトークン名はありません。

![ツール ウィンドウのタイトル バー (赤線)](../../extensibility/ux-guidelines/media/0303-092_toolwindowtitlebarredline.png "0303-092_ToolWindowTitleBarRedline")<br />ツール ウィンドウのタイトル バー (赤線)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ツール ウィンドウに合わせて UI を作成する場合はどこでも使用できます。 | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

**フォーカスされたタイトル バー**

![フォーカスされたタイトル バー](../../extensibility/ux-guidelines/media/0303-093_titlebarfocused.png "0303-093_TitleBarFocused")<br />フォーカスされたタイトル バー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.TitleBarActiveGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.TitleBarActiveText` |
| Border | `Environment.TitleBarActiveBorder`<br />(背景と同じ色に設定します。 |
| ドラッグ ハンドル | `Environment.TitleBarDragHandleActive` |

**フォーカスされていないタイトル バー**

![フォーカスされていないタイトル バー](../../extensibility/ux-guidelines/media/0303-094_titlebarunfocused.png "0303-094_TitleBarUnfocused")<br />フォーカスされていないタイトル バー

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.TitleBarInactiveGradientBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.TitleBarInactiveText` |
| Border | 該当なし |
| ドラッグ ハンドル | `Environment.TitleBarDragHandle` |

#### <a name="tool-window-title-bar-buttons"></a>ツール ウィンドウのタイトル バー ボタン
![タイトル バー ボタン (朱書き)](../../extensibility/ux-guidelines/media/0303-095_titlebarbuttonredline.png "0303-095_TitleBarButtonRedline")<br />タイトル バー ボタン (朱書き)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ツール ウィンドウのタイトル バーの色のトークンを使用する UI に表示されるボタン。 | ...他の場所に表示されるボタンの場合 |
| | ...指定以外の任意の背景/前景の組み合わせで。 |

**フォーカスのあるタイトル バー ボタン: 既定の状態**

![既定のフォーカスのあるタイトル バー ボタン](../../extensibility/ux-guidelines/media/0303-096_titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br />既定のフォーカスのあるタイトル バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Environment.ToolWindowButtonActiveGlyph` |
| Border | 該当なし |

**フォーカスのないタイトル バー ボタン: 既定の状態**

![既定のフォーカスのないタイトル バー ボタン](../../extensibility/ux-guidelines/media/0303-097_titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br />既定のフォーカスのないタイトル バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | 該当なし |
| 前景 (グリフ) | `Environment.ToolWindowButtonInactiveGlyph` |
| Border | 該当なし |

**フォーカスのあるタイトル バー ボタン: ホバー状態**

![ホバー時のフォーカスのあるタイトル バー ボタン](../../extensibility/ux-guidelines/media/0303-098_titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br />ホバー時のフォーカスのあるタイトル バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonHoverActive` |
| 前景 (グリフ) | `Environment.ToolWindowButtonHoverActiveGlyph` |
| Border | `Environment.ToolWindowButtonHoverActiveBorder` |

**フォーカスのないタイトル バー ボタン: ホバー状態**

![ホバー時のフォーカスのないタイトル バー ボタン](../../extensibility/ux-guidelines/media/0303-099_titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br />ホバー時のフォーカスのないタイトル バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonHoverInactive` |
| 前景 (グリフ) | `Environment.ToolWindowButtonHoverInactiveGlyph` |
| Border | `Environment.ToolWindowButtonHoverInactiveBorder` |

**フォーカスのあるタイトルバーボタン:押された状態**

![押しの上にフォーカスを置いたタイトル バー ボタン](../../extensibility/ux-guidelines/media/0303-100_titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br />押しの上にフォーカスを置いたタイトル バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonDown` |
| 前景 (グリフ) | `Environment.ToolWindowButtonDownActiveGlyph` |
| Border | `Environment.ToolWindowButtonDownBorder` |

**フォーカスのないタイトル バー ボタン: 押された状態**

![押しの上にフォーカスのないタイトル バー ボタン](../../extensibility/ux-guidelines/media/0303-101_titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br />押しの上にフォーカスのないタイトル バー ボタン

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowButtonDown` |
| 前景 (グリフ) | `Environment.ToolWindowButtonDownInactiveGlyph` |
| Border | `Environment.ToolWindowButtonDownBorder` |

### <a name="tool-window-tabs"></a>ツール ウィンドウ タブ
![ツール ウィンドウ タブ (朱折)](../../extensibility/ux-guidelines/media/0303-102_toolwindowtabredline.png "0303-102_ToolWindowTabRedline")<br />ツール ウィンドウ タブ (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...ツール ウィンドウに合わせて UI を作成する場合はどこでも使用できます。 | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

**選択され、フォーカスされたツール ウィンドウ タブ**

![選択され、フォーカスされたツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-103_toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br />選択され、フォーカスされたツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabSelectedTab` |
| 前景 (テキスト) | `Environment.ToolWindowTabSelectedActiveText` |
| Border | `Environment.ToolWindowTabSelectedBorder`<br />(背景と同じ色に設定します。 |

**選択され、フォーカスされていないツール ウィンドウ タブ**

![選択され、フォーカスされていないツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-104_toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br />選択され、フォーカスされていないツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabSelectedTab` |
| 前景 (テキスト) | `Environment.ToolWindowTabSelectedText` |
| Border | `Environment.ToolWindowTabSelectedBorder`<br />(背景と同じ色に設定します。 |

**[バックグラウンド ツール] ウィンドウ タブ: 既定の状態**

![既定の背景ツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-105_toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br />既定の背景ツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabGradientBegin`<br />`Environment.ToolWindowTabGradientEnd`<br />(グラデーションの分岐点は、Visual Studio 2013 で同じ色の値に設定されます。 |
| 前景 (テキスト) | `Environment.ToolWindowTabText` |
| Border | `Environment.ToolWindowTabBorder` |

**[バックグラウンド ツール] ウィンドウ タブ: ホバー状態**

![ホバー時の背景ツール ウィンドウ タブ](../../extensibility/ux-guidelines/media/0303-106_toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br />ホバー時の背景ツール ウィンドウ タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.ToolWindowTabMouseOverBackgroundBegin`<br />`Environment.ToolWindowTabMouseOverBackgroundEnd`<br />(グラデーションの分岐点は、Visual Studio 2013 で同じ色の値に設定されます。 |
| 前景 (テキスト) | `Environment.ToolWindowTabMouseOverText` |
| Border | `Environment.ToolWindowTabMouseOverBorder`<br />(背景と同じ色に設定します。 |

### <a name="auto-hide-tabs"></a>自動非表示タブ

![タブを自動的に非表示にする (朱折)](../../extensibility/ux-guidelines/media/0303-107_autohideredline.png "0303-107_AutoHideRedline")タブを自動的に非表示にする (朱折)

| 使用。。。 | 使用しないでください. |
| --- | --- |
| ...自動非表示ツール ウィンドウ タブと一致させる UI を作成している場所。 | ...シェルにテーマの更新がある場合に自動的に変更したくない UI。 |

**タブを自動的に非表示にする: 既定の状態**

![既定の自動非表示タブ](../../extensibility/ux-guidelines/media/0303-108_autohidetab.png "0303-108_AutoHideTab")<br />既定の自動非表示タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.AutoHideTabBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.AutoHideTabText` |
| Border | `Environment.AutoHideTabBorder` |

**タブを自動的に非表示にする: ホバー状態**

![ホバー時の [自動非表示] タブ](../../extensibility/ux-guidelines/media/0303-109_autohidetabhover.png "0303-109_AutoHideTabHover")<br />ホバー時の [自動非表示] タブ

| 要素 | トークン名: Category.color |
| --- | --- |
| バックグラウンド | `Environment.AutoHideTabMouseOverBackgroundBegin`<br />(このトークンのグラデーションの分岐点は、テーマ UI では使用されません。 |
| 前景 (テキスト) | `Environment.AutoHideTabMouseOverText` |
| Border | `Environment.AutoHideTabMouseOverBorder` |
