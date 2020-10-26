---
title: Visual Studio のレイアウト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4eb8eb7468751d46b922c15530389c554a8d3e36
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698403"
---
# <a name="layout-for-visual-studio"></a>Visual Studio のレイアウト
Visual Studio ダイアログの大部分は [ユーティリティダイアログレイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout)です。これは、標準の [Windows デスクトップダイアログレイアウトの原則](/windows/desktop/uxguide/win-dialog-box)に従う、テーマが適用されていないダイアログです。 Visual Studio が UI を更新するために移動すると、より目立つようなダイアログの中には、製品定義のエクスペリエンスとして機能する新しいデザインが追加されています。 これらの [テーマ付きダイアログのレイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout) には、テーマが設定されています。

## <a name="utility-dialog-layout"></a><a name="BKMK_UtilityDialogLayout"></a> ユーティリティダイアログのレイアウト

- ユーティリティダイアログ内のすべてのコントロールは、左上から順に開始し、下にフローします。

- ダイアログの中央にコントロールを配置して、大きな領域を塗りつぶすことは避けてください。

- すべてのダイアログテキストに環境フォントを使用します。 ビジュアル仕様を記述するときは、特定のフォントとサイズを選択するのではなく、環境フォントを指定します。 [環境フォントを](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)参照してください。

- 一貫した制御スペースと配置を使用して、職人気質の品質の目標をサポートします。

- ダイアログは、より多くのコントロール、一意のコントロールの juxtaposition、またはその両方から、より複雑になる可能性があります。 このような複雑な状況については、制御グループ間に十分なスペースを与え、ユーザーに解析のための論理フローを与えることができます。

### <a name="utility-dialog-layout-examples"></a>ユーティリティのダイアログレイアウトの例
 すべてのディメンションは、ピクセルで表されます。

 ![コントロールの上のラベルのダイアログの間隔](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801-a_UtilitySpacingAbove")

 **図 08.01-a: コントロールの上にラベルが付いたユーティリティダイアログのスペーシングガイドライン**

 ![コントロールの左のラベルのダイアログの間隔](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801-b_UtilitySpacingLeft")

 **図 08.01-b: コントロールの左側にラベルを付けたユーティリティダイアログのスペーシングガイドライン**

### <a name="layout-details"></a>レイアウトの詳細

#### <a name="margins"></a>余白

- すべてのダイアログには、すべての端の周りに12ピクセルの境界線が付きます。

- グループフレーム内の余白は、フレームの端から9ピクセルである必要があります。

- タブコントロール内の余白は、タブコントロールの端から6ピクセルである必要があります。

#### <a name="command-buttons"></a>コマンドボタン

- コマンドボタンは、コンテンツではなく、ダイアログフレームに対して動作します。 これらは、右下に配置する必要があります。ボタンを明確に区別できるように、上に十分な可変領域が必要です。

- ダイアログ内で動作する水平方向のボタンがある場合、[代替コマンド] ボタンの構成は右上にある垂直方向のスタックです。 下の「 [内部コマンドボタン](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons) 」を参照してください。

- コマンドボタンの左側にあるスペース (ダイアログの左下/中央) は、ダイアログ操作コントロールの "バンド" の一部と見なされます。 この領域に割り込んする必要があるのは、タスクまたはダイアログ全体に関連するヘルプリンクだけです。

- コマンドボタンは 75 x 23 ピクセルである必要があります。

- コマンドボタンは、6ピクセル離れている必要があります。

  ![基本的なボタンの配置](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801-c_ButtonAlign")

  **図 08.01-c: 基本的なボタンの配置**

#### <a name="labels"></a>ラベル

- すべてのラベルを左揃えにします。

- コントロールの上にあるラベルの場合は、その下にあるコントロールと正確に左揃えにする必要があります。また、ラベルの下部は、他のコントロール (コンボボックスなど) の上部の5ピクセル上にする必要があります。

- コントロールの左側にあるラベルの場合、ラベルと入力コントロールの間の最小幅は10ピクセルです。 テキストボックス、コンボボックス、またはその他のコントロールを配置するために、暗黙的な2番目の列を設定する必要があります。

- ラベルは文形式であり、その後にコロンが続きます。 「 [テキストスタイル](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)」を参照してください。

#### <a name="distance-between-controls"></a>コントロール間の距離
 スタックコントロールは合理的です。 積み上げられたコントロール間の間隔に関する絶対ガイドラインはありません。 コントロール間の tightness は、ダイアログ間で若干異なる場合があります。 推奨される間隔は、垂直コントロール/ラベルのペアの場合は20ピクセル、水平コントロール/ラベルのペアの場合は9ピクセルです。 水平方向のペアの最小制御間隔は6ピクセルです。

 ![コントロール間の推奨される間隔](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801-d_ControlDistance")

 **図 08.01-d: コントロール間の距離に関する推奨事項**

#### <a name="control-indentation"></a>コントロールのインデント
 コントロールが入れ子になっている場合は、内側のコントロールを上のコントロールの左端 (通常はラベル) で水平方向に配置します。

 ![入れ子になったコントロールの配置](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801-e_ControlAlign")

 **図 08.01-e: 入れ子になったコントロールの配置**

#### <a name="control-width"></a>コントロールの幅
 テキストボックスまたはその他の同様のコントロールの幅は、フィールドの平均入力値以下である必要があります。 英単語の平均は5文字です。 たとえば、長いパス名を必要とするテキストボックスは、水平レイアウトで許可されている長さである必要があります。一方、プラットフォーム名のドロップダウンは、最大のエントリを許可する長さである必要があります。

#### <a name="helper-text"></a>ヘルパーテキスト

- ダイアログには、ダイアログの目的に関する詳細情報を提供するヘルパーテキストを表示できます。 これは通常、上部にあり、1-2 文にすることができます。

- 行の長さは、ユーザーが解析および読み取りを行うときに使いやすい幅にする必要があります。 中規模のダイアログは550ピクセル以下でなければなりません。

#### <a name="interior-command-buttons"></a><a name="BKMK_InteriorCommandButtons"></a> 内部コマンドボタン
 より複雑なダイアログでは、内部コントロールが独自の関連ボタンを持つ場合があります。これは、ダイアログのコミットボタンが配置されている場所に影響を与える可能性があります。

- **[OK**] [ / **キャンセル**] が右下隅で水平方向に配置されている場合は、内部ボタンの垂直方向の配置 (列) を使用します。

- **[OK**] / **キャンセル**が右上隅で垂直方向に配置されている場合は、内部ボタンの水平方向の配置 (行) を使用します。 この状況はあまり一般的ではありません。

- 内部ボタンのサイズは、可能な場合は **[OK**] / **[キャンセル**] ボタンのサイズと一致する標準のボタンサイズ75x23 ピクセルをターゲットにする必要があります。 ボタンのラベルによってボタンのサイズが標準のボタンのサイズを超えた場合、そのセット内の他のボタンはそのサイズよりも大きくなります。

  ![横方向の [OK] と [キャンセル] ボタン](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801-f_HorizOKCan")

  **図 08.01-f: 横方向の OK/キャンセルを含む縦の内部ボタン**

  ![縦方向の [OK] と [キャンセル] ボタン](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801-g_VertOKCan")

  **図 08.01-g: 垂直方向の OK/キャンセルを含む横方向の内部ボタン**

#### <a name="browse-button"></a>[参照...];
 **[参照...]** テキストボックスの後に表示されるボタンでは、"参照..." と表示されます。完全 (省略記号を含む)。 領域が狭い場合、または画面に複数の **[Browse...]** ボタンがある場合、ボタンは省略記号だけに縮小できます。

## <a name="themed-dialog-layout"></a><a name="BKMK_ThemedDialogLayout"></a> テーマ付きダイアログのレイアウト
 Visual Studio のテーマ付きダイアログの外観は薄くなり、より多くの空白が提供されます。 タイポグラフィでは、より多くの行間隔とフォントサイズと太さのバリエーションが提供されるため、より強調および関心があります。 可能な場合は、chrome とタイトルバーが縮小または削除されています。 これらのダイアログのレイアウトは、次の基本的なパターンに従う必要があります。

1. ダイアログの背景は白です。

2. 中間値の灰色には、1ピクセルのルールの境界線があります。

3. ダイアログタイトルはタイトルバーには存在しませんが、大きなポイントサイズでは視覚的な関心と強調表示が提供されます。 (「 [テキストスタイル](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)」の「フォントサイズ」セクションを参照してください)。

4. 説明などの追加テキストと結合されたラベルは、 **環境フォント + 太字**にする必要があります。

5. 内部列は、薄い灰色の1ピクセルのルールで区切られます。

6. 既定のリンクにはアンダースコアがありません。 ホバー状態と押された状態には、色の変更とアンダースコアがあります。

7. コミットボタン ( **OK** / **キャンセル**など) は右下隅に配置されます。

### <a name="themed-dialog-layout-examples"></a>テーマ付きダイアログのレイアウトの例
 ![テーマが適用されたダイアログのレイアウト](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801-h_ThemedDialog")

 **図 08.01-h: テーマ付きダイアログ**

 ![テーマが適用されたダイアログのディメンション](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801-i_ThemedDialogDimensions")

 **図 08.01-i: テーマ付きダイアログ-ディメンション**

 ![テーマが適用されたダイアログのフォント](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801-j_ThemedDialogFonts")

 **図 08.01-j: テーマ付きダイアログ-フォント**

 ![テーマが適用されたダイアログの色](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801-k_ThemedDialogColors")

 **図 08.01-k: テーマ付きダイアログ-色**

## <a name="see-also"></a>関連項目
- [Visual Studio のアプリケーション パターン](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)
- [コントロール (Windows)](/windows/desktop/uxguide/controls)
- [ダイアログボックス (Windows)](/windows/desktop/uxguide/win-dialog-box)
