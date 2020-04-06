---
title: ビジュアルスタジオのレイアウト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4eb8eb7468751d46b922c15530389c554a8d3e36
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698403"
---
# <a name="layout-for-visual-studio"></a>Visual Studio のレイアウト
Visual Studio のダイアログの大部分は、標準の Windows デスクトップ[ダイアログ レイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout)[の原則](/windows/desktop/uxguide/win-dialog-box)に従うテーマのないダイアログ ボックスであるユーティリティ ダイアログ レイアウトです。 Visual Studio が UI の更新に移行するにつれて、より目立つダイアログボックスの一部には、製品定義エクスペリエンスとして確立する新しいデザインが用意されています。 これらの[テーマダイアログレイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout)は、テーマを持つ外観を持っています。

## <a name="utility-dialog-layout"></a><a name="BKMK_UtilityDialogLayout"></a>ユーティリティ ダイアログ のレイアウト

- ユーティリティ ダイアログ内のすべてのコントロールは、上/左から開始し、下に流れる必要があります。

- 大きな領域を塗りつぶすために、コントロールをダイアログの中央に配置しないでください。

- すべてのダイアログ テキストに環境フォントを使用します。 ビジュアルスペックを書くときは、特定のフォントとサイズを選択するのではなく、環境フォントを指定します。 [環境フォントを](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)参照してください。

- 一貫した制御間隔と配置を使用して、職人技の品質の目標をサポートします。

- ダイアログは、多数のコントロール、コントロールの一意な並置、またはその両方から、より複雑になる可能性があります。 このような複雑な状況では、制御グループ間に十分なスペースを確保して、ユーザーに解析する論理フローを与えます。

### <a name="utility-dialog-layout-examples"></a>ユーティリティ ダイアログ のレイアウト例
 すべての寸法はピクセルで表されます。

 ![コントロールの上のラベルのダイアログの間隔](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801-a_UtilitySpacingAbove")

 **図 08.01-a: 上のコントロールのラベルを持つユーティリティ ダイアログの間隔のガイドライン**

 ![コントロールの左のラベルのダイアログの間隔](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801-b_UtilitySpacingLeft")

 **図 08.01-b: コントロールの左側にラベルがあるユーティリティ ダイアログの間隔のガイドライン**

### <a name="layout-details"></a>レイアウトの詳細

#### <a name="margins"></a>余白

- すべてのダイアログボックスで、すべてのエッジの周りに 12 ピクセルの境界線を設定する必要があります。

- グループ フレーム内の余白は、フレームの端から 9 ピクセルにする必要があります。

- タブ コントロール内の余白は、タブ コントロールの端から 6 ピクセルにする必要があります。

#### <a name="command-buttons"></a>コマンド ボタン

- コマンド ボタンは、コンテンツではなくダイアログ フレームで動作します。 これらは右下に配置する必要があり、ボタンを明確に分離するために十分な可変スペースが必要です。

- ダイアログ内で動作する水平ボタンがある場合、代替コマンド ボタンの設定は右上の垂直スタックになります。 [以下の「内部コマンド ボタン](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons)」を参照してください。

- コマンド ボタンの左側のスペース (ダイアログの左下/中央) は、ダイアログ操作コントロールの "バンド" の一部と見なされます。 そのスペースに侵入する必要があるのは、タスクまたはダイアログ全体に関連するヘルプリンクだけです。

- コマンド ボタンは 75 x 23 ピクセルにする必要があります。

- コマンド ボタンは 6 ピクセル離れている必要があります。

  ![基本的なボタンの配置](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801-c_ButtonAlign")

  **図 08.01-c: 基本的なボタンの配置**

#### <a name="labels"></a>ラベル

- すべてのラベルを左揃えします。

- コントロールの上に位置するラベルの場合は、その下のコントロールと正確に左揃えにし、ラベルの下部は、他のコントロール (コンボ ボックスなど) の上に 5 ピクセル上にする必要があります。

- コントロールの左側に表示されるラベルの場合、ラベルと入力コントロールの間の最小幅は 10 ピクセルです。 テキスト ボックス、コンボ ボックス、またはその他のコントロールを配置するために、暗黙の 2 列目を作成する必要があります。

- ラベルは文の大文字と小文字で、その後にコロンが続きます。 [テキストスタイル](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)を参照してください。

#### <a name="distance-between-controls"></a>コントロール間の距離
 スタックコントロールは合理的です。 積み上げコントロール間の間隔に関する絶対的なガイドラインはありません。 コントロール間の堅さは、ダイアログの間で若干異なる場合があります。 垂直方向のコントロールとラベルのペアの場合は 20 ピクセル、水平コントロールとラベルのペアの場合は 9 ピクセルの間隔を推奨します。 水平方向のペアの最小コントロール間隔は 6 ピクセルです。

 ![コントロール間の推奨される間隔](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801-d_ControlDistance")

 **図 08.01-d: コントロール間の距離に関する推奨事項**

#### <a name="control-indentation"></a>コントロールのインデント
 コントロールが入れ子になっている場合は、内側のコントロールを上のコントロールの左端 (通常はラベル) に水平方向に配置します。

 ![入れ子になったコントロールの配置](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801-e_ControlAlign")

 **図 08.01-e: 入れ子になったコントロールの配置**

#### <a name="control-width"></a>コントロール幅
 テキスト ボックスやその他の類似のコントロールの幅は、フィールドの平均入力値より長くする必要があります。 英語の平均単語は 5 文字です。 たとえば、長いパス名を必要とするテキスト ボックスは、横方向のレイアウトで許可されている限り、プラットフォーム名のドロップダウンは最長のエントリを許可する長さだけである必要があります。

#### <a name="helper-text"></a>ヘルパー テキスト

- ダイアログボックスには、ダイアログの目的に関する詳細情報を提供するヘルパーテキストを表示できます。 これは通常、一番上にあり、1-2文にすることができます。

- 行の長さは、ユーザーが解析して読み取るための快適な幅にする必要があります。 中程度のダイアログは、幅が 550 ピクセル以下にする必要があります。

#### <a name="interior-command-buttons"></a><a name="BKMK_InteriorCommandButtons"></a>内部コマンド ボタン
 より複雑なダイアログでは、内部コントロールに固有の関連ボタンが存在する場合があり、ダイアログのコミット ボタンの場所に影響を与える可能性があります。

- **[OK**/**キャンセル]** が右下隅に水平方向に配置されている場合は、内側のボタンの縦方向の配置(列)を使用します。

- **[OK**/**キャンセル]** が右上隅に垂直方向に設定されている場合は、内側のボタンの水平方向の配置(行)を使用します。 この状況はあまり一般的ではありません。

- 内部ボタンのサイズは、75 x 23 ピクセルの標準ボタン サイズを対象とし、可能な場合は**OK**/**キャンセル**ボタンのサイズに一致する必要があります。 ボタンラベルによってボタンが標準ボタンサイズを超える場合、そのセット内の他のボタンは、その幅の大きさに合わせる必要があります。

  ![横方向の [OK] と [キャンセル] ボタン](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801-f_HorizOKCan")

  **図 08.01-f: 水平 OK/キャンセルを使用した垂直の内側ボタン**

  ![縦方向の [OK] と [キャンセル] ボタン](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801-g_VertOKCan")

  **図 08.01-g: 垂直 OK/キャンセルを使用した水平方向の内部ボタン**

#### <a name="browse-button"></a>[参照.]ボタン
 **[参照.]** テキスト ボックスの後に続くボタンは"Browse."と綴ります。省略記号を含めて完全に。 スペースが狭い場合、または画面上に複数の **[Browse..]** ボタンがある場合は、ボタンを省略記号だけに縮小できます。

## <a name="themed-dialog-layout"></a><a name="BKMK_ThemedDialogLayout"></a>テーマを含むダイアログ のレイアウト
 Visual Studio のテーマダイアログは、見た目が軽く、空白が多くなります。 タイポグラフィは、より多くのオープン行間隔とフォントサイズと太さのバリエーションを提供し、より強調し、関心を提供します。 可能な場合は、クロムバーとタイトル バーが縮小または削除されています。 これらのダイアログのレイアウトは、次の基本パターンに従う必要があります。

1. ダイアログの背景は白です。

2. 中間値グレーの 1 ピクセルのルール罫線があります。

3. ダイアログ タイトルはタイトル バーに配置されなくなりましたが、ポイント サイズを大きくすると視覚的な関心と強調が提供されます。 ([テキストスタイル](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)のフォントサイズセクションを参照してください。

4. 説明などの追加テキストとラベルを組み合わせるには、**環境フォント + 太字**を指定する必要があります。

5. 内部列は、明るいグレーの 1 ピクセルのルールで区切られています。

6. デフォルトリンクにはアンダースコアがありません。 ホバー状態と押された状態には、色の変化とアンダースコアが付いています。

7. コミットボタン **(OK**/**キャンセル**など) は右下隅に配置されます。

### <a name="themed-dialog-layout-examples"></a>テーマ型ダイアログレイアウトの例
 ![テーマが適用されたダイアログのレイアウト](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801-h_ThemedDialog")

 **図 08.01-h: テーマダイアログ**

 ![テーマが適用されたダイアログのディメンション](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801-i_ThemedDialogDimensions")

 **図 08.01-i: テーマダイアログ - 寸法**

 ![テーマが適用されたダイアログのフォント](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801-j_ThemedDialogFonts")

 **図 08.01-j: テーマダイアログ - フォント**

 ![テーマが適用されたダイアログの色](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801-k_ThemedDialogColors")

 **図 08.01-k: テーマダイアログ - 色**

## <a name="see-also"></a>関連項目
- [Visual Studio のアプリケーション パターン](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)
- [コントロール (ウィンドウ)](/windows/desktop/uxguide/controls)
- [ダイアログ ボックス (ウィンドウ)](/windows/desktop/uxguide/win-dialog-box)
