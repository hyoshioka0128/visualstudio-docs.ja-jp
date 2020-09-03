---
title: 共有色 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 9d3186f3-07d2-441f-b33e-435e95d8a0b8
caps.latest.revision: 11
ms.author: brgeorge
ms.openlocfilehash: 76c04680b63eb362e02fdf26d817660d671b3b52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548357"
---
# <a name="shared-colors"></a>共有の色
概要をここに挿入。  
  
## <a name="shared-colors"></a>共有の色  
 共通の Visual Studio シェル要素を使用する UI を設計する場合、または類似の機能との一貫性をインターフェイス要素に持たせる場合、パッケージ定義ファイルにある既存のトークン名を使用して色を選択し、割り当てます。 これにより、UI が Visual Studio 環境全体で一貫性を保ち、テーマが追加された場合や更新された場合に自動的に更新されるようになります。  
  
 この記事では、類似の UI を構築する際に参照できる一般的な UI 要素と UI 要素で使用されるトークン名について説明します。 これらの色のトークンにアクセスする方法の詳細については、「 [The VSColor Service](../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)」を参照してください。  
  
 トークン名は次のように正しく使用してください。  
  
- **色自体ではなく、機能に基づいてトークン名を使用します。** 一般的な共有色は、特定のインターフェイス要素と関連付けられ、同一または類似した機能に対してのみ使用されることを想定しています。 たとえば、押されているコンボ ボックスの色を、単にその色が好きという理由で進行状況を示す回転アニメーションに再利用しないでください。 コンボ ボックスとアニメーションの機能は異なり、コンボ ボックスに関連付けられている色が変更された場合、アニメーション要素にとっては適切な色でなくなる可能性があります。 色を一貫して使用すると、ユーザーの理解を助け、混乱を避けるために役立ちます。  
  
- **背景色とテキストの色を適切な組み合わせで使用します。** テキストと共に使用することが想定された背景色には、テキストの色が関連付けられています。 その背景に指定されている色以外のテキストの色を使用しないでください。 テキストの色が関連付けられていない背景色は、テキストを表示する予定のサーフェイスで使用しないでください。 テキストの色と背景色の他の組み合わせによって、読み取り不可能なインターフェイスが生成される場合があります。  
  
- **場所に適したコントロールの色を使用します。** 特定の状態では、一部の Visual Studio コントロールに個別の境界線の色と背景色がありません。 代わりに、それらのコントロールにはその背後のサーフェイスから色が適用されます。 コントロールを配置する場所に適したトークン名を常に使用してください。  
  
> [!IMPORTANT]
> "スタート ページ" や "Cider" のカテゴリにあるトークンは使用しないでください。  
  
### <a name="command-structures"></a>コマンドの構造  
  
#### <a name="menus"></a><a name="BKMK_CommandMenus"></a> ポップアップ  
 メニューは、メイン メニュー バー、ドキュメントまたはツール ウィンドウへの埋め込み、IDE 全体のさまざまな場所での右クリックなど、Visual Studio 2013 内の複数の場所で表示することができます。 他の UI 要素に関連付けられたメニューの実装については、それぞれの要素のセクションで説明します。 Visual Studio 環境で提供される標準のメニュー実装を常に使用してください。 ただし、まれに、標準の Visual Studio メニューにアクセスできないことがあります。 このような場合は、次のトークン名を使用して、UI が Visual Studio の他のメニューと一貫性を保つようにします。  
  
 ![メニューの赤線](../extensibility/ux-guidelines/media/0303-000-menuredline.png "0303-000_MenuRedline")  
  
使用するケース  
- カスタム メニューを作成する必要がある場合。  
  
- Visual Studio メニューと一致させる新しい UI コンポーネントがある場合。  
  
使用しないケース  
背景色単独の場合。 常に指定された背景と前景の組み合わせを使用します。  
  
##### <a name="menu-title"></a>メニュー タイトル  
 メニュー タイトルは、背景、境界線、タイトル テキスト、および通常、メニューがコマンド バーにあるときは、オプションのグリフで構成されます。  
  
 ![メニュー タイトルの赤線](../extensibility/ux-guidelines/media/0303-001-menutitleredline.png "0303-001_MenuTitleRedline")  
  
使用するケース  
カスタム メニュー タイトルを作成する場合。  
  
使用しないケース  
- メニュー タイトルと常に一致させるわけではないすべてのもの。  
  
- 指定以外の背景と前景の組み合わせ。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![メニュー タイトルの既定値](../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303-002_MenuTitleDefault")<br /><br /> **メニュー タイトル**|背景|なし|  
|![メニュー タイトルの既定値](../extensibility/ux-guidelines/media/0303-002-menutitledefault.png "0303-002_MenuTitleDefault")<br /><br /> **メニュー タイトル**|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|![既定グリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br /><br /> **グリフがあるメニュー タイトル**|前景 (グリフ)|`Environment.CommandBarMenuGlyph`|  
|![既定グリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-003-menutitlewithglyphdefault.png "0303-003_MenuTitleWithGlyphDefault")<br /><br /> **グリフがあるメニュー タイトル**|境界線|なし|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のメニュー タイトル](../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303-004_MenuTitleHover")<br /><br /> **メニュー タイトル**|背景|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時のメニュー タイトル](../extensibility/ux-guidelines/media/0303-004-menutitlehover.png "0303-004_MenuTitleHover")<br /><br /> **メニュー タイトル**|前景 (テキスト)|`Environment.CommandBarTextHover`|  
|![ホバー時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br /><br /> **グリフがあるメニュー タイトル**|前景 (グリフ)|`Environment.CommandBarMenuMouseOverGlyph`|  
|![ホバー時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-005-menutitlewithglyphhover.png "0303-005_MenuTitleWithGlyphHover")<br /><br /> **グリフがあるメニュー タイトル**|境界線|`Environment.CommandBarBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたメニュー タイトル](../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303-006_MenuTitlePressed")<br /><br /> **メニュー タイトル**|背景|`Environment.CommandBarMenuBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押されたメニュー タイトル](../extensibility/ux-guidelines/media/0303-006-menutitlepressed.png "0303-006_MenuTitlePressed")<br /><br /> **メニュー タイトル**|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|![押された時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br /><br /> **グリフがあるメニュー タイトル**|前景 (グリフ)|`Environment.CommandBarMenuMouseDownGlyph`|  
|![押された時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-007-menutitlewithglyphpressed.png "0303-007_MenuTitleWithGlyphPressed")<br /><br /> **グリフがあるメニュー タイトル**|境界線|`Environment.CommandBarMenuBorder`<br /><br /> 左側、上部、右側のみ。|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **グリフがあるメニュー タイトル**|背景|なし|  
|![無効時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **グリフがあるメニュー タイトル**|前景 (テキスト)|`Environment.CommandBarTextInactive`|  
|![無効時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **グリフがあるメニュー タイトル**|前景 (グリフ)|`Environment.CommandBarTextInactive`|  
|![無効時のグリフのメニュー タイトル](../extensibility/ux-guidelines/media/0303-008-menutitlewithglyphdisabled.png "0303-008_MenuTitleWithGlyphDisabled")<br /><br /> **グリフがあるメニュー タイトル**|境界線|なし|  
  
##### <a name="menu"></a>メニュー  
 個々のメニュー項目は、メニュー テキストとオプションのアイコン、チェック ボックス、またはサブメニュー グリフで構成されます。 その背景色とテキストの色はホバー時に変化します。 この色トークンは、背景と前景のペアです。  
  
 ![メニュー項目の赤線](../extensibility/ux-guidelines/media/0303-009-menuitemredline.png "0303-009_MenuItemRedline")  
  
 使用するケース  
 メニュー バーまたはコマンド バーから起動されるドロップダウン リスト。  
  
使用しないケース  
- 別のコンテキストで発生するドロップダウン リスト。  

- 指定以外の背景と前景の組み合わせ。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|背景|`Environment.CommandBarMenuBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|前景 (サブメニュー グリフ)|`Environment.CommandBarMenuSubmenuGlyph`|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|境界線|`Environment.CommandBarMenuBorder`|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|アイコン チャネルの背景|`Environment.CommandBarMenuIconBackground`|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|区切り記号|`Environment.CommandBarMenuSeparator`|  
|![メニューの既定値](../extensibility/ux-guidelines/media/0303-010-menudefault.png "0303-010_MenuDefault")<br /><br /> **Menu**|シャドウ|`Environment.DropShadowBackground`|  
|![チェックされたメニュー](../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303-011_MenuChecked")<br /><br /> **オン**|チェック マーク|`Environment.CommandBarCheckBox`|  
|![チェックされたメニュー](../extensibility/ux-guidelines/media/0303-011-menuchecked.png "0303-011_MenuChecked")<br /><br /> **オン**|チェック マークの背景|`Environment.CommandBarSelectedIcon`|  
|![選択されたメニュー](../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303-012_MenuSelected")<br /><br /> **Selected**|アイコンの背景|`Environment.CommandBarSelected`|  
|![選択されたメニュー](../extensibility/ux-guidelines/media/0303-012-menuselected.png "0303-012_MenuSelected")<br /><br /> **Selected**|アイコンの境界線|`Environment.CommandBarSelectedBorder`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![メニュー ホバー](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **メニュー項目**|背景|`Environment.CommandBarMenuItemMouseOver`|  
|![メニュー ホバー](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **メニュー項目**|前景 (テキスト)|`Environment.CommandBarMenuItemMouseOver`|  
|![メニュー ホバー](../extensibility/ux-guidelines/media/0303-013-menuhover.png "0303-013_MenuHover")<br /><br /> **メニュー項目**|前景 (サブメニュー グリフ)|`Environment.CommandBarMenuMouseOverSubmenuGlyph`|  
|![チェックされたメニュー ホバー](../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303-014_MenuHoverChecked")<br /><br /> **オン**|チェック マーク|`Environment.CommandBarCheckBoxMouseOver`|  
|![チェックされたメニュー ホバー](../extensibility/ux-guidelines/media/0303-014-menuhoverchecked.png "0303-014_MenuHoverChecked")<br /><br /> **オン**|チェック マークの背景|`Environment.CommandBarHoverOverSelectedIcon`|  
|![選択されたメニュー ホバー](../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303-015_MenuHoverSelected")<br /><br /> **Selected**|アイコンの背景|`Environment.CommandBarHoverOverSelected`|  
|![選択されたメニュー ホバー](../extensibility/ux-guidelines/media/0303-015-menuhoverselected.png "0303-015_MenuHoverSelected")<br /><br /> **Selected**|アイコンの境界線|`Environment.CommandBarHoverOverSelectedIconBorder`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![メニューの無効化](../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303-016_MenuDisabled")<br /><br /> メニュー項目|前景 (テキスト)|`Environment.CommandBarTextInactive`|  
|![メニューの無効化](../extensibility/ux-guidelines/media/0303-016-menudisabled.png "0303-016_MenuDisabled")<br /><br /> メニュー項目|前景 (サブメニュー グリフ)|`Environment.CommandBarMenuSubmenuGlyph`|  
|![チェックされたメニューの無効化](../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303-017_MenuDisabledChecked")<br /><br /> オン|チェック マーク|`Environment.CommandBarCheckBoxDisabled`|  
|![チェックされたメニューの無効化](../extensibility/ux-guidelines/media/0303-017-menudisabledchecked.png "0303-017_MenuDisabledChecked")<br /><br /> オン|チェック マークの背景|`Environment.CommandBarSelectedIconDisabled`|  
  
#### <a name="command-bar"></a>コマンド バー  
 コマンド バーは、Visual Studio IDE 内の複数の場所、特にコマンド シェルフ、およびツールまたはドキュメント ウィンドウへの埋め込みで表示できます。  
  
 通常は、Visual Studio 環境で提供される標準のコマンド バー実装を常に使用してください。 標準メカニズムを使用すると、すべての表示の詳細が正しく表示され、対話型要素が他の Visual Studio のコマンド バーのコントロールと一貫して動作するようになります。 ただし、独自のコマンド バーを作成する必要がある場合は、次のトークン名を使用してスタイルを正しく設定してください。  
  
 ![コマンド バーの赤線](../extensibility/ux-guidelines/media/0303-018-commandbarredline.png "0303-018_CommandBarRedline")  
  
 ![オーバーフロー ボタンの赤線](../extensibility/ux-guidelines/media/0303-019-overflowbuttonredline.png "0303-019_OverflowButtonRedline")  
  
 使用するケース  
 埋め込みコマンド バーが必要だが、標準の Visual Studio のコマンド バー実装を使用できない場所。  
  
使用しないケース  
- コマンド バーに類似していない UI 要素。  

- トークン名が指定されているもの以外のコマンド バー コンポーネント。  
  
##### <a name="command-bar-group"></a>コマンド バー グループ  
 コマンド バー グループは、関連する一連のコマンド バー コントロールで構成され、任意の数のボタン、分割ボタン、ドロップダウン メニュー、コンボ ボックス、またはメニューを含めることができます。 これらのコントロールの色は別々のトークン名によって制御され、このガイドの他の場所で個別に説明されています。 区切り線を使用して、コマンド バー グループを関連するサブグループに分割します。  
  
 ![コマンド バー グループの赤線](../extensibility/ux-guidelines/media/0303-020-commandbargroupredline.png "0303-020_CommandBarGroupRedline")  
  
 使用するケース  
 埋め込みコマンド バーが必要だが、標準の Visual Studio のコマンド バー実装を使用できない場所。  
  
使用しないケース  
- コマンド バーに類似していない UI 要素。  

- トークン名が指定されているもの以外のコマンド バー コンポーネント。  
  
  **既定** (他の状態はありません)  
  
|要素|トークン名: Category.color|  
|-------------|--------------------------------|  
|背景|`Environment.CommandBarGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|境界線|`Environment.CommandBarToolBarBorder`|  
|ドラッグ ハンドル|`Environment.CommandBarDragHandle`|  
|区切り記号|`Environment.CommandBarToolBarSeparator`<br /><br /> `Environment.CommandBarToolBarSeparatorHighlight`|  
  
##### <a name="command-icons"></a>コマンド アイコン  
 ![コマンド アイコンの赤線](../extensibility/ux-guidelines/media/0303-021-commandiconredline1.png "0303-021_CommandIconRedline1")  
  
 ![コマンド アイコンの赤線](../extensibility/ux-guidelines/media/0303-022-commandiconredline2.png "0303-022_CommandIconRedline2")  
  
 使用するケース  
 コマンド バーに配置されるボタン。  
  
使用しないケース  
- 独自のトークン名があるコントロール。  

- 指定以外の背景と前景の組み合わせ。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![コマンド アイコンの既定値](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303-023_CommandIconDefault")<br /><br /> **既定**|背景|該当なし (コマンド バーの背景から継承)|  
|![コマンド アイコンの既定値](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303-023_CommandIconDefault")<br /><br /> **既定**|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|![コマンド アイコンの既定値](../extensibility/ux-guidelines/media/0303-023-commandicondefault.png "0303-023_CommandIconDefault")<br /><br /> **既定**|境界線|該当なし|  
|![選択されたコマンドのアイコンの既定値](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br /><br /> **Selected**|背景|`Environment.CommandBarSelected`|  
|![選択されたコマンドのアイコンの既定値](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br /><br /> **Selected**|前景 (テキスト)|`Environment.CommandBarTextSelected`|  
|![選択されたコマンドのアイコンの既定値](../extensibility/ux-guidelines/media/0303-024-commandicondefaultselected.png "0303-024_CommandIconDefaultSelected")<br /><br /> **Selected**|境界線|`Environment.CommandBarSelectedBorder`|  
  
 **ホバー時とキーボード フォーカス**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![コマンド アイコン ホバー](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303-025_CommandIconHover")<br /><br /> **ホバー時の標準**|背景|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![コマンド アイコン ホバー](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303-025_CommandIconHover")<br /><br /> **ホバー時の標準**|前景 (テキスト)|`Environment.CommandBarTextHover`|  
|![コマンド アイコン ホバー](../extensibility/ux-guidelines/media/0303-025-commandiconhover.png "0303-025_CommandIconHover")<br /><br /> **ホバー時の標準**|境界線|`Environment.CommandBarBorder`|  
|![選択されたコマンド アイコン ホバー](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br /><br /> **ホバー時に選択済み**|背景|`Environment.CommandBarHoverOverSelected`|  
|![選択されたコマンド アイコン ホバー](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br /><br /> **ホバー時に選択済み**|前景 (テキスト)|`Environment.CommandBarTextHoverOverSelected`|  
|![選択されたコマンド アイコン ホバー](../extensibility/ux-guidelines/media/0303-026-commandiconhoverselected.png "0303-026_CommandIconHoverSelected")<br /><br /> **ホバー時に選択済み**|境界線|`Environment.CommandBarHoverOverSelectedIconBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたコマンド アイコン](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303-027_CommandIconPressed")<br /><br /> **押されているコマンド アイコン**|背景|`Environment.CommandBarMouseDownBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押されたコマンド アイコン](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303-027_CommandIconPressed")<br /><br /> **押されているコマンド アイコン**|前景 (テキスト)|`Environment.CommandBarTextMouseDown`|  
|![押されたコマンド アイコン](../extensibility/ux-guidelines/media/0303-027-commandiconpressed.png "0303-027_CommandIconPressed")<br /><br /> **押されているコマンド アイコン**|境界線|`Environment.CommandBarBorder`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効にされたコマンド アイコン](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303-028_CommandIconDisabled")<br /><br /> **無効化されたコマンド アイコン**|背景|該当なし (コマンド バーの背景から継承)|  
|![無効にされたコマンド アイコン](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303-028_CommandIconDisabled")<br /><br /> **無効化されたコマンド アイコン**|前景 (テキスト)|`Environment.CommandBarTextInactive`|  
|![無効にされたコマンド アイコン](../extensibility/ux-guidelines/media/0303-028-commandicondisabled.png "0303-028_CommandIconDisabled")<br /><br /> **無効化されたコマンド アイコン**|境界線|該当なし|  
  
##### <a name="combo-box"></a><a name="BKMK_CommandComboBox"></a> コンボボックス  
  
> [!IMPORTANT]
> コンボ ボックスはドロップダウンに似ていますが、編集可能なテキスト領域が含まれます。 ドロップダウンに編集可能なテキスト領域が含まれていない場合は、 [Drop-down](../misc/shared-colors.md#BKMK_CommandDropDown)に記載した色トークンを使用します。  
  
 ![コンボ ボックスの赤線](../extensibility/ux-guidelines/media/0303-029-comboboxredline.png "0303-029_ComboBoxRedline")  
  
使用するケース  
- カスタム コンボ ボックスを作成する場合。  

- コンボ ボックスに類似したコマンド バー コントロールを作成する場合。  

使用しないケース  
- コマンド バー UI と常に一致させるわけではないすべてのもの。  

- スタイル設定されたコンボ ボックスにアクセスできる場合。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![コンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **入力フィールド**|背景|`Environment.ComboBoxBackground`|  
|![コンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **入力フィールド**|前景 (テキスト)|`Environment.ComboBoxText`|  
|![コンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **入力フィールド**|境界線|`Environment.ComboBoxBorder`|  
|![コンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-030-comboboxinputfield.png "0303-030_ComboBoxInputField")<br /><br /> **入力フィールド**|区切り記号|区切り記号なし|  
|![コンボボックスのドロップダウン&#45;ボタン](../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br /><br /> **ドロップダウン ボックス**|背景|該当なし (継承)|  
|![コンボボックスのドロップダウン&#45;ボタン](../extensibility/ux-guidelines/media/0303-031-comboboxdropdownbutton.png "0303-031_ComboBoxDropdownButton")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.ComboBoxGlyph`|  
|![コンボボックス&#47;ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br /><br /> **ドロップダウンリスト**|背景|`Environment.ComboBoxPopupBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![コンボボックス&#47;ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br /><br /> **ドロップダウンリスト**|前景 (テキスト)|`Environment.ComboBoxItemText`|  
|![コンボボックス&#47;ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-032-comboboxdropdownlist.png "0303-032_ComboBoxDropdownList")<br /><br /> **ドロップダウンリスト**|境界線|`Environment.ComboBoxPopupBorder`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **入力フィールド**|背景|`Environment.ComboBoxMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時のコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **入力フィールド**|前景 (テキスト)|`Environment.ComboBoxMouseOverText`|  
|![ホバー時のコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **入力フィールド**|境界線|`Environment.ComboBoxMouseOverBorder`|  
|![ホバー時のコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-033-comboboxinputfieldhover.png "0303-033_ComboBoxInputFieldHover")<br /><br /> **入力フィールド**|区切り記号|`Environment.ComboBoxMouseOverSeparator`|  
|![ホバー時にドロップダウンボタン&#47;ドロップ&#45;コンボボックス](../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br /><br /> **ドロップダウン ボックス**|背景|`Environment.ComboBoxButtonMouseOverBackground`|  
|![ホバー時にドロップダウンボタン&#47;ドロップ&#45;コンボボックス](../extensibility/ux-guidelines/media/0303-034-comboboxdropdownbuttonhover.png "0303-034_ComboBoxDropdownButtonHover")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.ComboBoxMouseOverGlyph`|  
|![ホバー時にドロップ&#45;ドロップダウンリスト&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br /><br /> **ドロップダウンリスト**|背景 (メニュー項目)|`Environment.ComboBoxItemMouseOverBackground`|  
|![ホバー時にドロップ&#45;ドロップダウンリスト&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br /><br /> **ドロップダウンリスト**|前景 (テキスト)|`Environment.ComboBoxItemMouseOverText`|  
|![ホバー時にドロップ&#45;ドロップダウンリスト&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-035-comboboxdropdownlisthover.png "0303-035_ComboBoxDropdownListHover")<br /><br /> **ドロップダウンリスト**|境界線 (メニュー項目)|`Environment.ComboBoxItemMouseOverBorder`|  
  
 **Focused**  
  
|コンポーネント|要素|トークン名: Color.category|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **入力フィールド**|背景|`Environment.ComboBoxFocusedBackground`|  
|![フォーカスされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **入力フィールド**|前景 (テキスト)|`Environment.ComboBoxFocusedText`|  
|![フォーカスされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **入力フィールド**|境界線|`Environment.ComboBoxFocusedBorder`|  
|![フォーカスされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-036-comboboxinputfieldfocused.png "0303-036_ComboBoxInputFieldFocused")<br /><br /> **入力フィールド**|区切り記号|`Environment.ComboBoxFocusedButtonSeparator`|  
|![コンボボックス&#47;ドロップ&#45;下にフォーカスするボタン](../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br /><br /> **ドロップダウン ボックス**|背景|`Environment.ComboBoxFocusedButtonBackground`|  
|![コンボボックス&#47;ドロップ&#45;下にフォーカスするボタン](../extensibility/ux-guidelines/media/0303-037-comboboxdropdownbuttonfocused.png "0303-037_ComboBoxDropdownButtonFocused")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.ComboBoxFocusedGlyph`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Color.category|  
|---------------|-------------|--------------------------------|  
|![押されたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **入力フィールド**|背景|`Environment.ComboBoxMouseDownBackground`|  
|![押されたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **入力フィールド**|前景 (テキスト)|`Environment.ComboBoxMouseDownText`|  
|![押されたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **入力フィールド**|境界線|`Environment.ComboBoxMouseDownBorder`|  
|![押されたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-038-comboboxinputfieldpressed.png "0303-038_ComboBoxInputFieldPressed")<br /><br /> **入力フィールド**|区切り記号|`Environment.ComboBoxMouseDownSeparator`|  
|![コンボボックス&#47;ドロップダウン&#45;押されたボタン](../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|背景|`Environment.ComboBoxButtonMouseDownBackground`|  
|![コンボボックス&#47;ドロップダウン&#45;押されたボタン](../extensibility/ux-guidelines/media/0303-039-comboboxdropdownbuttonpressed.png "0303-039_ComboBoxDropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.ComboBoxMouseDownGlyph`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Color.category|  
|---------------|-------------|--------------------------------|  
|![無効にされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **入力フィールド**|背景|`Environment.ComboBoxDisabledBackground`|  
|![無効にされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **入力フィールド**|前景 (テキスト)|`Environment.ComboBoxDisabledText`|  
|![無効にされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **入力フィールド**|境界線|`Environment.ComboBoxDisabledBorder`|  
|![無効にされたコンボ ボックスの入力フィールド](../extensibility/ux-guidelines/media/0303-041-comboboxinputfielddisabled.png "0303-041_ComboBoxInputFieldDisabled")<br /><br /> **入力フィールド**|区切り記号|区切り記号なし|  
|![コンボボックス&#47;ドロップ&#45;[下へ] ボタンが無効になっています](../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br /><br /> **ドロップダウン ボックス**|背景|なし|  
|![コンボボックス&#47;ドロップ&#45;[下へ] ボタンが無効になっています](../extensibility/ux-guidelines/media/0303-040-comboboxdropdownbuttondisabled.png "0303-040_ComboBoxDropdownButtonDisabled")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.ComboBoxDisabledGlyph`|  
  
##### <a name="drop-down"></a><a name="BKMK_CommandDropDown"></a> ドロップダウン  
  
> [!IMPORTANT]
> ドロップダウンはコンボ ボックスに似ていますが、編集可能なテキスト領域がありません。 ドロップダウンに編集可能なテキスト領域が含まれる場合は、 [Combo box](../misc/shared-colors.md#BKMK_CommandComboBox)に見つかる色トークンを使用します。  
  
 ![ドロップダウン&#45;赤線](../extensibility/ux-guidelines/media/0303-042-dropdownredline.png "0303-042_DropdownRedline")  
  
 使用するケース  
 カスタム ドロップダウン リスト コントロールを作成する場合。  
  
使用しないケース  
- ドロップダウン リストに類似していないすべてのもの。  

- コンボ ボックスまたは分割ボタン。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドロップダウン&#45;選択フィールド](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **選択フィールド**|背景|`Environment.DropDownBackground`|  
|![ドロップダウン&#45;選択フィールド](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **選択フィールド**|前景 (テキスト)|`DropDownText`|  
|![ドロップダウン&#45;選択フィールド](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **選択フィールド**|境界線|`DropDownBorder`|  
|![ドロップダウン&#45;選択フィールド](../extensibility/ux-guidelines/media/0303-043-dropdownselectionfield.png "0303-043_DropdownSelectionField")<br /><br /> **選択フィールド**|区切り記号|区切り記号なし|  
|![ドロップダウン&#45;ボタン](../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303-044_DropdownButton")<br /><br /> **ドロップダウン ボックス**|背景|なし|  
|![ドロップダウン&#45;ボタン](../extensibility/ux-guidelines/media/0303-044-dropdownbutton.png "0303-044_DropdownButton")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.DropDownGlyph`|  
|![ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **ドロップダウンリスト**|背景|`Environment.DropDownPopupBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **ドロップダウンリスト**|前景 (テキスト)|`Environment.ComboBoxItemText`|  
|![ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **ドロップダウンリスト**|境界線|`Environment.DropDownPopupBorder`|  
|![ドロップダウンリスト&#45;ドロップダウンリスト](../extensibility/ux-guidelines/media/0303-045-dropdownlist.png "0303-045_DropdownList")<br /><br /> **ドロップダウンリスト**|シャドウ|`Environment.DropShadowBackground`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時に選択フィールドをドロップ&#45;](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **選択フィールド**|背景|`Environment.DropDownMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時に選択フィールドをドロップ&#45;](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **選択フィールド**|前景 (テキスト)|`Environment.DropDownMouseOverText`|  
|![ホバー時に選択フィールドをドロップ&#45;](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **選択フィールド**|境界線|`Environment.DropDownMouseOverBorder`|  
|![ホバー時に選択フィールドをドロップ&#45;](../extensibility/ux-guidelines/media/0303-046-dropdownselectionfieldhover.png "0303-046_DropdownSelectionFieldHover")<br /><br /> **選択フィールド**|区切り記号|`Environment.DropDownButtonMouseOverSeparator`|  
|![ホバー時に&#45;下へ移動ボタン](../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br /><br /> **ドロップダウン ボックス**|背景|`Environment.DropDownButtonMouseOverBackground`|  
|![ホバー時に&#45;下へ移動ボタン](../extensibility/ux-guidelines/media/0303-047-dropdownbuttonhover.png "0303-047_DropdownButtonHover")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.DropDownMouseOverGlyph`|  
|![ホバー時に&#45;ダウンリストをドロップする](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303-048_DropdownListHover")<br /><br /> **ドロップダウンリスト**|背景 (メニュー項目)|`Environment.ComboBoxItemMouseOverBackground`|  
|![ホバー時に&#45;ダウンリストをドロップする](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303-048_DropdownListHover")<br /><br /> **ドロップダウンリスト**|前景 (テキスト)|`Environment.ComboBoxItemMouseOverText`|  
|![ホバー時に&#45;ダウンリストをドロップする](../extensibility/ux-guidelines/media/0303-048-dropdownlisthover.png "0303-048_DropdownListHover")<br /><br /> **ドロップダウンリスト**|境界線 (メニュー項目)|`Environment.ComboBoxItemMouseOverBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押された&#45;下選択フィールドをドロップします](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **選択フィールド**|背景|`Environment.DropDownMouseDownBackground`|  
|![押された&#45;下選択フィールドをドロップします](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **選択フィールド**|前景 (テキスト)|`Environment.DropDownMouseDownText`|  
|![押された&#45;下選択フィールドをドロップします](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **選択フィールド**|境界線|`Environment.DropDownMouseDownBorder`|  
|![押された&#45;下選択フィールドをドロップします](../extensibility/ux-guidelines/media/0303-049-dropdownselectionfieldpressed.png "0303-049_DropdownSelectionFieldPressed")<br /><br /> **選択フィールド**|区切り記号|`Environment.DropDownButtonMouseDownSeparator`|  
|![押された&#45;下矢印ボタン](../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|背景|`Environment.DropDownButtonMouseDownBackground`|  
|![押された&#45;下矢印ボタン](../extensibility/ux-guidelines/media/0303-050-dropdownbuttonpressed.png "0303-050_DropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`Environment.DropDownMouseDownGlyph`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドロップ&#45;下選択フィールドが無効です](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|背景|`Environment.DropDownDisabledBackground`|  
|![ドロップ&#45;下選択フィールドが無効です](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|前景 (テキスト)|`Environment.DropDownDisabledText`|  
|![ドロップ&#45;下選択フィールドが無効です](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|境界線|`Environment.DropDownDisabledBorder`|  
|![ドロップ&#45;下選択フィールドが無効です](../extensibility/ux-guidelines/media/0303-051-dropdownselectionfielddisabled.png "0303-051_DropdownSelectionFieldDisabled")|区切り記号|区切り記号なし|  
|![ドロップ&#45;下矢印ボタンが無効です](../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")|背景|該当なし|  
|![ドロップ&#45;下矢印ボタンが無効です](../extensibility/ux-guidelines/media/0303-052-dropdownbuttondisabled.png "0303-052_DropdownButtonDisabled")|前景 (グリフ)|`Environment.DropDownDisabledGlyph`|  
  
##### <a name="split-button"></a>分割ボタン  
 分割ボタンは、ボタン、メニュー、コマンド バー テキストなど、他のコマンド バー コントロールと多くのトークン名を共有します。 ここでは利便性のために、すべての必要なアクション ボタンとドロップダウン ボタンのトークン名を繰り返しています。 分割ボタンのドロップダウン リストは、コマンド バー [Menus](../misc/shared-colors.md#BKMK_CommandMenus)の実装です。  
  
 ![分割ボタンの赤線](../extensibility/ux-guidelines/media/0303-053-splitbuttonredline.png "0303-053_SplitButtonRedline")  
  
 使用するケース  
 カスタム分割ボタンを構築する場合。  
  
使用しないケース  
- 他の種類のボタン。  

- 指定以外の背景と前景の組み合わせ。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![分割ボタン](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **分割ボタン (既定)**|背景|なし|  
|![分割ボタン](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **分割ボタン (既定)**|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|![分割ボタン](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **分割ボタン (既定)**|前景 (グリフ)|`Environment.CommandBarSplitButtonGlyph`|  
|![分割ボタン](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **分割ボタン (既定)**|境界線|該当なし|  
|![分割ボタン](../extensibility/ux-guidelines/media/0303-054-splitbutton.png "0303-054_SplitButton")<br /><br /> **分割ボタン (既定)**|区切り記号|該当なし|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時の分割ボタン](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **分割ボタン (ホバー時)**|背景|`Environment.CommandBarMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時の分割ボタン](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **分割ボタン (ホバー時)**|前景 (テキスト)|`Environment.CommandBarTextHover`|  
|![ホバー時の分割ボタン](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **分割ボタン (ホバー時)**|前景 (グリフ)|`Environment.CommandBarSplitButtonMouseOverGlyph`|  
|![ホバー時の分割ボタン](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **分割ボタン (ホバー時)**|境界線|`Environment.CommandBarBorder`|  
|![ホバー時の分割ボタン](../extensibility/ux-guidelines/media/0303-055-splitbuttonhover.png "0303-055_SplitButtonHover")<br /><br /> **分割ボタン (ホバー時)**|区切り記号|`Environment.CommandBarSplitButtonSeparator`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押された分割ボタン](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **(押されている) 分割ボタン**|背景|`Environment.CommandBarMouseDownBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された分割ボタン](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **(押されている) 分割ボタン**|前景 (テキスト)|`Environment.CommandBarTextMouseDown`|  
|![押された分割ボタン](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **(押されている) 分割ボタン**|前景 (グリフ)|`Environment.CommandBarSplitButtonMouseDownGlyph`|  
|![押された分割ボタン](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **(押されている) 分割ボタン**|境界線|`Environment.CommandBarBorder`|  
|![押された分割ボタン](../extensibility/ux-guidelines/media/0303-056-splitbuttonpressed.png "0303-056_SplitButtonPressed")<br /><br /> **(押されている) 分割ボタン**|区切り記号|該当なし|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効になった分割ボタン](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **分割ボタン (無効)**|背景|該当なし|  
|![無効になった分割ボタン](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **分割ボタン (無効)**|前景 (テキスト)|`Environment.ComboBoxItemTextInactive`|  
|![無効になった分割ボタン](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **分割ボタン (無効)**|前景 (グリフ)|`Environment.CommandBarTextInactive`|  
|![無効になった分割ボタン](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **分割ボタン (無効)**|境界線|該当なし|  
|![無効になった分割ボタン](../extensibility/ux-guidelines/media/0303-057-splitbuttondisabled.png "0303-057_SplitButtonDisabled")<br /><br /> **分割ボタン (無効)**|区切り記号|該当なし|  
  
##### <a name="more-options-and-overflow-buttons"></a>"その他のオプション" ボタンと "オーバーフロー" ボタン  
 [その他のオプション] ボタンは、関連するコマンド バー ボタンを追加または削除して、コマンド バー グループをカスタマイズできる場合に使用します。 [オーバーフロー] ボタンは、横のスペースが不足しているためにコマンド バーが切り詰められた場合に表示され、クリックすると、表示できないコマンド バー ボタンを含むメニューが表示されます。 これら 2 つのボタンの色は、同じトークン名のセットによって制御されます。  
  
 ![その他のオプションの赤線](../extensibility/ux-guidelines/media/0303-058-moreoptionsredline.png "0303-058_MoreOptionsRedline")  
  
 使用するケース  
 カスタムの [その他のオプション] または [オーバーフロー] ボタン。  
  
 使用しないケース  
 [その他のオプション] または [オーバーフロー] ボタンと同様の機能を持たないボタン。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![その他のオプション](../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303-059_MoreOptions")<br /><br /> **その他のオプション**|背景|`Environment.CommandBarOptionsBackground`|  
|![その他のオプション](../extensibility/ux-guidelines/media/0303-059-moreoptions.png "0303-059_MoreOptions")<br /><br /> **その他のオプション**|前景 (グリフ)|`Environment.CommandBarOptionsGlyph`|  
|![オーバーフロー ボタン](../extensibility/ux-guidelines/media/0303-060-overflow.png "0303-060_Overflow")<br /><br /> **オーバーフロー**|背景|`Environment.CommandBarOptionsBackground`|  
|![オーバーフロー ボタン](../extensibility/ux-guidelines/media/0303-060-overflow.png "0303-060_Overflow")<br /><br /> **オーバーフロー**|前景 (グリフ)|`Environment.CommandBarOptionsGlyph`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のその他のオプション](../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303-061_MoreOptionsHover")<br /><br /> **その他のオプション**|背景|`Environment.CommandBarOptionsMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時のその他のオプション](../extensibility/ux-guidelines/media/0303-061-moreoptionshover.png "0303-061_MoreOptionsHover")<br /><br /> **その他のオプション**|前景 (グリフ)|`Environment.CommandBarOptionsMouseDownGlyph`|  
|![ホバー時のオーバーフロー](../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303-062_OverflowOptions")<br /><br /> **オーバーフロー**|背景|`Environment.CommandBarOptionsMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時のオーバーフロー](../extensibility/ux-guidelines/media/0303-062-overflowoptions.png "0303-062_OverflowOptions")<br /><br /> **オーバーフロー**|前景 (グリフ)|`Environment.CommandBarOptionsMouseDownGlyph`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたその他のオプション](../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303-063_MoreOptionsPressed")<br /><br /> **その他のオプション**|背景|`Environment.CommandBarOptionsMouseDownBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押されたその他のオプション](../extensibility/ux-guidelines/media/0303-063-moreoptionspressed.png "0303-063_MoreOptionsPressed")<br /><br /> **その他のオプション**|前景 (グリフ)|`Environment.CommandBarOptionsMouseDownGlyph`|  
|![押されたオーバーフロー](../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303-064_OverflowPressed")<br /><br /> **オーバーフロー**|背景|`Environment.CommandBarOptionsMouseDownBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押されたオーバーフロー](../extensibility/ux-guidelines/media/0303-064-overflowpressed.png "0303-064_OverflowPressed")<br /><br /> **オーバーフロー**|前景 (グリフ)|`Environment.CommandBarOptionsMouseDownGlyph`|  
  
### <a name="document-windows"></a>ドキュメント ウィンドウ  
 Visual Studio 環境で提供されるため、ドキュメント ウィンドウをレプリケートする必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一貫性のある状態で表示されるように、ドキュメント ウィンドウで使用する色を活用することができます。  
  
 ドキュメント ウィンドウの色のトークンを使用する場合は、類似の要素に対してのみ、常にペアで使用するように注意する必要があります。 そうしない場合、UI に予期しない結果が発生します。  
  
#### <a name="document-window-frame"></a>ドキュメント ウィンドウ フレーム  
 ドキュメント ウィンドウは IDE にドッキングしたり、別のウィンドウとしてフローティングさせたりすることができます。 ドキュメント ウィンドウは、IDE の外部にフローティングしているときも、ドキュメント ウェル内に存在し、IDE の一部であるときと同じ背景、境界線、テキスト、タブの色を持ちます。 ただし、ドキュメントは、独自の背景、境界線、テキストの色を持つフレーム内に配置されます。 ツール ウィンドウをドキュメント ウェルにドッキングした場合、ツール ウィンドウはタブの動作と色をドキュメント ウィンドウのトークン名から継承します。  
  
 ![ドッキングされたドキュメント ウィンドウの赤線](../extensibility/ux-guidelines/media/0303-065-dockeddocumentwindowredline.png "0303-065_DockedDocumentWindowRedline")  
  
 **ドッキングされたドキュメント ウィンドウ**  
  
 ![フローティング ドキュメント ウィンドウの赤線](../extensibility/ux-guidelines/media/0303-066-floatingdocumentwindowredline.png "0303-066_FloatingDocumentWindowRedline")  
  
 **フローティング ドキュメント ウィンドウ**  
  
 使用するケース  
 ドキュメント ウィンドウと一致させる UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|ドキュメント: ドッキングまたはフローティング|背景|ドキュメントの種類によって異なります|  
|ドキュメント: ドッキングまたはフローティング|前景 (テキスト)|ドキュメントの種類によって異なります|  
|ドキュメント: ドッキングまたはフローティング|境界線|`Environment.ToolWindowBorder`|  
|![フォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **フレーム: フローティング、フォーカスされている**|背景|`Environment.ToolWindowFloatingFrame`|  
|![フォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **フレーム: フローティング、フォーカスされている**|前景 (テキスト)|`Environment.ToolWindowFloatingFrame`|  
|![フォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **フレーム: フローティング、フォーカスされている**|前景 (グリフ)|`Environment.RaftedWindowButtonActiveGlyph`|  
|![フォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **フレーム: フローティング、フォーカスされている**|境界線|`Environment.MainWindowActiveDefaultBorder`|  
|![フォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-067-framefocused.png "0303-067_FrameFocused")<br /><br /> **フレーム: フローティング、フォーカスされている**|境界線 (グリフ)|`Environment.RaftedWindowButtonActiveBorder`<br /><br /> 透明に設定されます|  
|![フォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **フレーム: フローティング、フォーカスされていない**|背景|`Environment.ToolWindowFloatingFrameInactive`|  
|![フォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **フレーム: フローティング、フォーカスされていない**|前景 (テキスト)|`Environment.ToolWindowFloatingFrameInactive`|  
|![フォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **フレーム: フローティング、フォーカスされていない**|前景 (グリフ)|`Environment.RaftedWindowButtonInactiveGlyph`|  
|![フォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **フレーム: フローティング、フォーカスされていない**|境界線|`Environment.MainWindowInactiveBorder`|  
|![フォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-068-frameunfocused.png "0303-068_FrameUnfocused")<br /><br /> **フレーム: フローティング、フォーカスされていない**|境界線 (グリフ)|`Environment.RaftedWindowButtonInactiveBorder`<br /><br /> 透明に設定されます|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のフォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303-069_FrameFocusedHover")<br /><br /> **フレーム: フローティング、フォーカスされている**|背景 (グリフ)|`Environment.RaftedWindowButtonHoverActive`|  
|![ホバー時のフォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303-069_FrameFocusedHover")<br /><br /> **フレーム: フローティング、フォーカスされている**|前景 (グリフ)|`Environment.RaftedWindowButtonHoverActiveGlyph`|  
|![ホバー時のフォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-069-framefocusedhover.png "0303-069_FrameFocusedHover")<br /><br /> **フレーム: フローティング、フォーカスされている**|境界線 (グリフ)|`Environment.RaftedWindowButtonHoverActiveBorder`|  
|![ホバー時のフォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br /><br /> **フレーム: フローティング、フォーカスされていない**|背景 (グリフ)|`EnvironmentRaftedWindowButtonHoverInactive`|  
|![ホバー時のフォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br /><br /> **フレーム: フローティング、フォーカスされていない**|前景 (グリフ)|`Environment.RaftedWindowButtonHoverInactiveGlyph`|  
|![ホバー時のフォーカスされていないフレーム](../extensibility/ux-guidelines/media/0303-070-frameunfocusedhover.png "0303-070_FrameUnfocusedHover")<br /><br /> **フレーム: フローティング、フォーカスされていない**|境界線 (グリフ)|`Environment.RaftedWindowButtonHoverInactiveBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたフォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303-071_FrameFocusedPressed")<br /><br /> **フレーム: フローティング、フォーカスされている**|背景 (グリフ)|`Environment.RaftedWindowButtonDown`|  
|![押されたフォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303-071_FrameFocusedPressed")<br /><br /> **フレーム: フローティング、フォーカスされている**|前景 (グリフ)|`Environment.RaftedWindowButtonDownGlyph`|  
|![押されたフォーカスされたフレーム](../extensibility/ux-guidelines/media/0303-071-framefocusedpressed.png "0303-071_FrameFocusedPressed")<br /><br /> **フレーム: フローティング、フォーカスされている**|境界線 (グリフ)|`Environment.RaftedWindowButtonDownBorder`|  
  
#### <a name="document-tabs"></a>ドキュメント タブ  
 ドキュメント タブはタブ チャネル内に存在し、現在どのドキュメントが開いているか、およびどのドキュメントが現在選択されているか、またはアクティブなドキュメントであるかを示します。 ツール ウィンドウも、ユーザーが配置した場合、ドキュメント タブ チャネルにドッキングできます。 この場合、ツール ウィンドウではドキュメント ウィンドウと同じタブの色が使用されます。 ドキュメント ウィンドウの色と常に一致する UI を作成する場合は (テーマの更新や、新しいテーマがインストールされた場合を含む)、これらの色のトークンを参照します。  
  
 ![[ドキュメント] タブの赤線](../extensibility/ux-guidelines/media/0303-072-documenttabredline.png "0303-072_DocumentTabRedline")  
  
 使用するケース  
 ドキュメント タブと一致し、テーマの更新や新しいテーマの色を自動的に取得する UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
##### <a name="open-document-tabs"></a>開いているドキュメントのタブ  
 開いている各ドキュメントには、ドキュメント タブ チャネルに名前を表示するタブがあります。 ドキュメントはバックグラウンドで選択したり開いたりすることができ、タブはこれらの状態を反映します。  
  
- 選択されているタブは、現在ドキュメント ウェルに表示されているドキュメントを表します。 選択されているタブには、ドキュメント ウェルの上端にまたがって拡張するドキュメントの境界線があります。  
  
- 背景タブは、現在選択されているタブではないドキュメントタブです。クリックすると、選択したタブになり、それらのトークン名からすべての背景、境界線、テキストの色が取得されます。  
  
  ![[ドキュメントを開く] タブの赤線](../extensibility/ux-guidelines/media/0303-073-opendocumenttabredline.png "0303-073_OpenDocumentTabRedline")  
  
  使用するケース  
  カスタム ドキュメント タブを作成する場合。  
  
  使用しないケース  
  - 一時的な (プレビュー) タブ。  
  
- シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
##### <a name="selected-tab"></a>選択されているタブ  
 **Focused**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされた [選択済み] タブ](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされている**|背景|`Environment.FileTabSelectedGradientTop`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![フォーカスされた [選択済み] タブ](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされている**|前景 (テキスト)|`Environment.FileTabSelectedText`|  
|![フォーカスされた [選択済み] タブ](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされている**|境界線|`Environment.FileTabSelectedBorder`<br /><br /> 背景と同じ色に設定されます。|  
|![フォーカスされた [選択済み] タブ](../extensibility/ux-guidelines/media/0303-074-selectedtabfocused.png "0303-074_SelectedTabFocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされている**|ドキュメントの境界線|`Environment.FileTabDocumentBorderBackground`|  
  
 **フォーカスされていない**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされていない [選択済み] タブ](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされていない**|背景|`Environment.FileTabInactiveGradientTop`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![フォーカスされていない [選択済み] タブ](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされていない**|前景 (テキスト)|`Environment.FileTabInactiveText`|  
|![フォーカスされていない [選択済み] タブ](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされていない**|境界線|`Environment.FileTabInactiveBorder`<br /><br /> 背景と同じ色に設定されます。|  
|![フォーカスされていない [選択済み] タブ](../extensibility/ux-guidelines/media/0303-075-selectedtabunfocused.png "0303-075_SelectedTabUnfocused")<br /><br /> **選択されているドキュメント タブ、フォーカスされていない**|ドキュメントの境界線|`Environment.FileTabInactiveDocumentBorderBackground`|  
  
##### <a name="background-tab"></a>背景タブ  
 **既定**  
  
|コンポーネント|要素|トークン名: Color.category|  
|---------------|-------------|--------------------------------|  
|![背景タブ](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303-076_BackgroundTab")<br /><br /> **背景タブ既定**|背景|`Environment.FileTabBackground`|  
|![背景タブ](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303-076_BackgroundTab")<br /><br /> **背景タブ既定**|前景 (テキスト)|`Environment.FileTabText`|  
|![背景タブ](../extensibility/ux-guidelines/media/0303-076-backgroundtab.png "0303-076_BackgroundTab")<br /><br /> **背景タブ既定**|境界線|`Environment.FileTabBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Color.category|  
|---------------|-------------|--------------------------------|  
|![ホバー時の背景タブ](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303-077_BackgroundTabHover")<br /><br /> **ホバー時の背景タブ**|背景|`Environment.FileTabHotGradientTop`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時の背景タブ](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303-077_BackgroundTabHover")<br /><br /> **ホバー時の背景タブ**|前景 (テキスト)|`Environment.FileTabHotText`|  
|![ホバー時の背景タブ](../extensibility/ux-guidelines/media/0303-077-backgroundtabhover.png "0303-077_BackgroundTabHover")<br /><br /> **ホバー時の背景タブ**|境界線|`Environment.FileTabHotBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
##### <a name="preview-tab"></a>プレビュー タブ  
 プレビュー タブは、ユーザーがソリューション エクスプローラーのツール ウィンドウで項目をクリックすると、ドキュメント タブ チャネルの右側に表示されます。 プレビュー タブはドキュメントのプレビューとして機能し、ユーザーはドキュメント タブ チャネルの左側でドキュメントを開いたままにできます。 プレビュー タブは一度に 1 つのみ開くことができます。 プレビュー タブには、開いているタブと同様に、背景と選択された状態の両方があり、アクティブな状態でフォーカスされている場合とフォーカスされていない場合があります。  
  
 ![[プレビュー] タブの赤線](../extensibility/ux-guidelines/media/0303-078-previewtabredline.png "0303-078_PreviewTabRedline")  
  
 使用するケース  
 一時的なプレビューを作成し、一部の要素を現在のプレビュー タブの色と一致させるすべての場所。  
  
使用しないケース  
- 一時的 (プレビュー) でないすべての種類のドキュメントまたはタブ。  

- シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
  **選択されたプレビュー タブ: フォーカスされている**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされた [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **フォーカスされたプレビュー タブ**|背景|`Environment.FileTabProvisionalSelectedActive`|  
|![フォーカスされた [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **フォーカスされたプレビュー タブ**|前景 (テキスト)|`Environment.FileTabProvisionalSelectedActiveForeground`|  
|![フォーカスされた [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **フォーカスされたプレビュー タブ**|境界線|`Environment.FileTabProvisionalSelectedActiveBorder`<br /><br /> 背景と同じ色に設定されます。|  
|![フォーカスされた [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-079-previewtabfocused.png "0303-079_PreviewTabFocused")<br /><br /> **フォーカスされたプレビュー タブ**|ドキュメントの境界線|`Environment.FileTabProvisionalSelectedActiveBorder`|  
  
 **選択されたプレビュー タブ: フォーカスされていない**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされていない [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **フォーカスされていないプレビュー タブ**|背景|`Environment.FileTabProvisionalSelectedInactive`|  
|![フォーカスされていない [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **フォーカスされていないプレビュー タブ**|前景 (テキスト)|`Environment.FileTabProvisionalSelectedInactiveForeground`|  
|![フォーカスされていない [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **フォーカスされていないプレビュー タブ**|境界線|`Environment.FileTabProvisionalSelectedInactiveBorder`|  
|![フォーカスされていない [プレビュー] タブ](../extensibility/ux-guidelines/media/0303-080-previewtabunfocused.png "0303-080_PreviewTabUnfocused")<br /><br /> **フォーカスされていないプレビュー タブ**|ドキュメントの境界線|`Environment.FileTabProvisionalSelectedInactiveBorder`|  
  
 **背景プレビュー タブ: 既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![[プレビューの背景] タブ](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br /><br /> **プレビュー タブ背景タブ**|背景|`Environment.FileTabProvisionalInactive`|  
|![[プレビューの背景] タブ](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br /><br /> **プレビュー タブ背景タブ**|前景 (テキスト)|`Environment.FileTabProvisionalInactiveForeground`|  
|![[プレビューの背景] タブ](../extensibility/ux-guidelines/media/0303-081-previewbackgroundtab.png "0303-081_PreviewBackgroundTab")<br /><br /> **プレビュー タブ背景タブ**|境界線|`Environment.FileTabProvisionalInactiveBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
 **背景プレビュー タブ: ホバー時**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時の [プレビューの背景] タブ](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br /><br /> **ホバー時のプレビュー タブ背景タブ**|背景|`Environment.FileTabProvisionalHover`|  
|![ホバー時の [プレビューの背景] タブ](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br /><br /> **ホバー時のプレビュー タブ背景タブ**|前景 (テキスト)|`Environment.FileTabProvisionalHoverForeground`|  
|![ホバー時の [プレビューの背景] タブ](../extensibility/ux-guidelines/media/0303-082-previewbackgroundtabhover.png "0303-082_PreviewBackgroundTabHover")<br /><br /> **ホバー時のプレビュー タブ背景タブ**|境界線|`Environment.FileTabProvisionalHoverBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
##### <a name="document-overflow-button"></a>ドキュメント オーバーフロー ボタン  
 ドキュメント オーバーフロー ボタンは、すべてのドキュメント タブに適した垂直スペースが現在の構成にあるかどうかに関係なく、1 つ以上のドキュメントが開いている場合に表示されます。 **CommandBarMenu** 色 (「 [Menus](../misc/shared-colors.md#BKMK_CommandMenus)」を参照) で制御されるドキュメント オーバーフロー ドロップダウン メニューには、表示と非表示の両方の開いているすべてのドキュメントのリストが表示され、オーバーフロー グリフは開いているすべてのドキュメントがタブ チャネルに表示されるかどうかに応じて変化します。  
  
 ![オーバーフローの赤線](../extensibility/ux-guidelines/media/0303-083-overflowredline.png "0303-083_OverflowRedline")  
  
使用するケース  
カスタム ドキュメント オーバーフロー ボタンを作成する場合。  

使用しないケース  
- オーバーフロー ボタンと類似していない UI。  

- コマンド バー オーバーフロー ボタン。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![オーバーフロー](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **ドキュメント オーバーフロー ボタン**|背景|`Environment.DocWellOverflowButtonBackground`|  
|![オーバーフロー](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **ドキュメント オーバーフロー ボタン**|前景 (グリフ)|`Environment.DocWellOverflowButtonGlyph`|  
|![オーバーフロー](../extensibility/ux-guidelines/media/0303-084-overflow.png "0303-084_Overflow")<br /><br /> **ドキュメント オーバーフロー ボタン**|境界線|該当なし|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のオーバーフロー](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303-085_OverflowHover")<br /><br /> **ホバー時のドキュメント オーバーフロー ボタン**|背景|`Environment.DocWellOverflowButtonMouseOverBackground`|  
|![ホバー時のオーバーフロー](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303-085_OverflowHover")<br /><br /> **ホバー時のドキュメント オーバーフロー ボタン**|前景 (グリフ)|`Environment.DocWellOverflowButtonMouseOverGlyph`|  
|![ホバー時のオーバーフロー](../extensibility/ux-guidelines/media/0303-085-overflowhover.png "0303-085_OverflowHover")<br /><br /> **ホバー時のドキュメント オーバーフロー ボタン**|境界線|`Environment.DocWellOverflowButtonMouseOverBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたオーバーフロー](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303-086_OverflowPressed")<br /><br /> **押されているドキュメント オーバーフロー ボタン**|背景|`Environment.DocWellOverflowButtonMouseDownBackground`|  
|![押されたオーバーフロー](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303-086_OverflowPressed")<br /><br /> **押されているドキュメント オーバーフロー ボタン**|前景 (グリフ)|`Environment.DocWellOverflowButtonMouseDownGlyph`|  
|![押されたオーバーフロー](../extensibility/ux-guidelines/media/0303-086-overflowpressed.png "0303-086_OverflowPressed")<br /><br /> **押されているドキュメント オーバーフロー ボタン**|境界線|`Environment.DocWellOverflowButtonMouseDownBorder`|  
  
### <a name="tool-windows"></a>ツール ウィンドウ  
 Visual Studio 環境で提供されるため、ツール ウィンドウをレプリケートする必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一貫性のある状態で表示されるように、ツール ウィンドウで使用する色を活用することができます。  
  
 ![[ツール] ウィンドウの赤線](../extensibility/ux-guidelines/media/0303-087-toolwindowredline.png "0303-087_ToolWindowRedline")  
  
 使用するケース  
 ツール ウィンドウと一致させる UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
#### <a name="tool-window-frame"></a>ツール ウィンドウ フレーム  
 Visual Studio のツール ウィンドウはさまざまなタスクに使用され、いくつかの異なる状態の 1 つで配置できます。 ツール ウィンドウが開いている場合、ドキュメント領域の 4 辺のいずれかに割り当てることができます。 ツール ウィンドウは IDE の外部でフローティングさせることもでき、ユーザーの画面内の任意の場所に再配置できます。 フローティング ウィンドウは、常に IDE の一番上に配置されます。 最後に、ツール ウィンドウはドキュメント ウィンドウとしてドッキングし、ドキュメント ウェルのタブとして表示できます。 ドキュメント ウィンドウとしてドッキングされたツール ウィンドウは、ドキュメント ウィンドウのトークン名を使用して一部の色が付けられます。  
  
 ![[ツール] ウィンドウ フレームの赤線](../extensibility/ux-guidelines/media/0303-088-toolwindowframeredline.png "0303-088_ToolWindowFrameRedline")  
  
 使用するケース  
 ツール ウィンドウと一致させる UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
 **さ**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドッキングされた [ツール] ウィンドウ](../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303-089_ToolWindowDocked")|背景|`Environment.ToolWindowBackground`|  
|![ドッキングされた [ツール] ウィンドウ](../extensibility/ux-guidelines/media/0303-089-toolwindowdocked.png "0303-089_ToolWindowDocked")|境界線|`Environment.ToolWindowBorder`|  
  
 **フローティング: フォーカスされている**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされた [ツール] ウィンドウ](../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303-090_ToolWindowFocused")|背景|`Environment.ToolWindowBackground`|  
|![フォーカスされた [ツール] ウィンドウ](../extensibility/ux-guidelines/media/0303-090-toolwindowfocused.png "0303-090_ToolWindowFocused")|境界線|`Environment.MainWindowActiveDefaultBorder`|  
  
 **フローティング: フォーカスされていない**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされていない [ツール] ウィンドウ](../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303-091_ToolWindowUnfocused")|背景|`Environment.ToolWindowBackground`|  
|![フォーカスされていない [ツール] ウィンドウ](../extensibility/ux-guidelines/media/0303-091-toolwindowunfocused.png "0303-091_ToolWindowUnfocused")|境界線|`Environment.MainWindowInactiveBorder`|  
  
#### <a name="tool-window-title-bar"></a>ツール ウィンドウのタイトル バー  
 タイトル バーの境界線は実際の境界線ではありませんが、タイトル バーの上部にわたる太い線です。 フォーカスされていない状態のトークン名はありません。  
  
 ![[ツール] ウィンドウのタイトル バーの赤線](../extensibility/ux-guidelines/media/0303-092-toolwindowtitlebarredline.png "0303-092_ToolWindowTitleBarRedline")  
  
 使用するケース  
 ツール ウィンドウと一致させる UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
 **Focused**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたタイトル バー](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **フォーカスされたタイトル バー**|背景|`Environment.TitleBarActiveGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![フォーカスされたタイトル バー](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **フォーカスされたタイトル バー**|前景 (テキスト)|`Environment.TitleBarActiveText`|  
|![フォーカスされたタイトル バー](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **フォーカスされたタイトル バー**|境界線|`Environment.TitleBarActiveBorder`<br /><br /> 背景と同じ色に設定されます。|  
|![フォーカスされたタイトル バー](../extensibility/ux-guidelines/media/0303-093-titlebarfocused.png "0303-093_TitleBarFocused")<br /><br /> **フォーカスされたタイトル バー**|ドラッグ ハンドル|`Environment.TitleBarDragHandleActive`|  
  
 **フォーカスされていない**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされていないタイトル バー](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **フォーカスされていないタイトル バー**|背景|`Environment.TitleBarInactiveGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![フォーカスされていないタイトル バー](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **フォーカスされていないタイトル バー**|前景 (テキスト)|`Environment.TitleBarInactiveText`|  
|![フォーカスされていないタイトル バー](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **フォーカスされていないタイトル バー**|境界線|該当なし|  
|![フォーカスされていないタイトル バー](../extensibility/ux-guidelines/media/0303-094-titlebarunfocused.png "0303-094_TitleBarUnfocused")<br /><br /> **フォーカスされていないタイトル バー**|ドラッグ ハンドル|`Environment.TitleBarDragHandle`|  
  
##### <a name="title-bar-buttons"></a>タイトル バー ボタン  
 ![タイトル バー ボタンの赤線](../extensibility/ux-guidelines/media/0303-095-titlebarbuttonredline.png "0303-095_TitleBarButtonRedline")  
  
 使用するケース  
 ツール ウィンドウのタイトル バーの色のトークンを使用する UI に表示されるボタン。  
  
使用しないケース  
- その他の場所に表示されるボタン。  

- 指定以外の背景と前景の組み合わせ。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br /><br /> **Focused**|背景|該当なし|  
|![フォーカスされたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br /><br /> **Focused**|前景 (グリフ)|`Environment.ToolWindowButtonActiveGlyph`|  
|![フォーカスされたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-096-titlebarbuttonfocused.png "0303-096_TitleBarButtonFocused")<br /><br /> **Focused**|境界線|該当なし|  
|![タイトルバーボタン見る](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br /><br /> **フォーカスされていない**|背景|該当なし|  
|![タイトルバーボタン見る](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br /><br /> **フォーカスされていない**|前景 (グリフ)|`Environment.ToolWindowButtonInactiveGlyph`|  
|![タイトルバーボタン見る](../extensibility/ux-guidelines/media/0303-097-titlebarbuttonunfocused.png "0303-097_TitleBarButtonUnfocused")<br /><br /> **フォーカスされていない**|境界線|該当なし|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のフォーカスされたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br /><br /> **Focused**|背景|`Environment.ToolWindowButtonHoverActive`|  
|![ホバー時のフォーカスされたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br /><br /> **Focused**|前景 (グリフ)|`Environment.ToolWindowButtonHoverActiveGlyph`|  
|![ホバー時のフォーカスされたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-098-titlebarbuttonfocusedhover.png "0303-098_TitleBarButtonFocusedHover")<br /><br /> **Focused**|境界線|`Environment.ToolWindowButtonHoverActiveBorder`|  
|![ホバー時のフォーカスされていないタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br /><br /> **フォーカスされていない**|背景|`Environment.ToolWindowButtonHoverInactive`|  
|![ホバー時のフォーカスされていないタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br /><br /> **フォーカスされていない**|前景 (グリフ)|`Environment.ToolWindowButtonHoverInactiveGlyph`|  
|![ホバー時のフォーカスされていないタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-099-titlebarbuttonunfocusedhover.png "0303-099_TitleBarButtonUnfocusedHover")<br /><br /> **フォーカスされていない**|境界線|`Environment.ToolWindowButtonHoverInactiveBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスおよび押されたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br /><br /> **Focused**|背景|`Environment.ToolWindowButtonDown`|  
|![フォーカスおよび押されたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br /><br /> **Focused**|前景 (グリフ)|`Environment.ToolWindowButtonDownActiveGlyph`|  
|![フォーカスおよび押されたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-100-titlebarbuttonfocusedpressed.png "0303-100_TitleBarButtonFocusedPressed")<br /><br /> **Focused**|境界線|`Environment.ToolWindowButtonDownBorder`|  
|![フォーカスされず押されたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br /><br /> **フォーカスされていない**|背景|`Environment.ToolWindowButtonDown`|  
|![フォーカスされず押されたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br /><br /> **フォーカスされていない**|前景 (グリフ)|`Environment.ToolWindowButtonDownInactiveGlyph`|  
|![フォーカスされず押されたタイトル バー ボタン](../extensibility/ux-guidelines/media/0303-101-titlebarbuttonunfocusedpressed.png "0303-101_TitleBarButtonUnfocusedPressed")<br /><br /> **フォーカスされていない**|境界線|`Environment.ToolWindowButtonDownBorder`|  
  
#### <a name="tool-window-tabs"></a>ツール ウィンドウ タブ  
 ![[ツールウィンドウ] タブ赤線](../extensibility/ux-guidelines/media/0303-102-toolwindowtabredline.png "0303-102_ToolWindowTabRedline")  
  
 使用するケース  
 ツール ウィンドウと一致させる UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
 **選択されているタブ**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされた [ツール ウィンドウ] タブ](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br /><br /> **選択され、フォーカスされたツール ウィンドウ タブ**|背景|`Environment.ToolWindowTabSelectedTab`|  
|![フォーカスされた [ツール ウィンドウ] タブ](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br /><br /> **選択され、フォーカスされたツール ウィンドウ タブ**|前景 (テキスト)|`Environment.ToolWindowTabSelectedActiveText`|  
|![フォーカスされた [ツール ウィンドウ] タブ](../extensibility/ux-guidelines/media/0303-103-toolwindowtabfocused.png "0303-103_ToolWindowTabFocused")<br /><br /> **選択され、フォーカスされたツール ウィンドウ タブ**|境界線|`Environment.ToolWindowTabSelectedBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされていない [ツール ウィンドウ] タブ](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br /><br /> **選択され、フォーカスされていないツール ウィンドウ タブ**|背景|`Environment.ToolWindowTabSelectedTab`|  
|![フォーカスされていない [ツール ウィンドウ] タブ](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br /><br /> **選択され、フォーカスされていないツール ウィンドウ タブ**|前景 (テキスト)|`Environment.ToolWindowTabSelectedText`|  
|![フォーカスされていない [ツール ウィンドウ] タブ](../extensibility/ux-guidelines/media/0303-104-toolwindowtabunfocused.png "0303-104_ToolWindowTabUnfocused")<br /><br /> **選択され、フォーカスされていないツール ウィンドウ タブ**|境界線|`Environment.ToolWindowTabSelectedBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
 **背景タブ**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![[ツール ウィンドウの背景] タブ](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br /><br /> **背景ツール ウィンドウ タブ**|背景|`Environment.ToolWindowTabGradientBegin`<br /><br /> グラデーション境界は、Visual Studio 2013 で同じ色の値に設定されます。<br /><br /> `Environment.ToolWindowTabGradientEnd`<br /><br /> グラデーション境界は、Visual Studio 2013 で同じ色の値に設定されます。|  
|![[ツール ウィンドウの背景] タブ](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br /><br /> **背景ツール ウィンドウ タブ**|前景 (テキスト)|`Environment.ToolWindowTabText`|  
|![[ツール ウィンドウの背景] タブ](../extensibility/ux-guidelines/media/0303-105-toolwindowbackgroundtab.png "0303-105_ToolWindowBackgroundTab")<br /><br /> **背景ツール ウィンドウ タブ**|境界線|`Environment.ToolWindowTabBorder`|  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時の [ツール ウィンドウの背景] タブ](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br /><br /> **ホバー時の背景ツール ウィンドウ タブ**|背景|`Environment.ToolWindowTabMouseOverBackgroundBegin`<br /><br /> グラデーション境界は、Visual Studio 2013 で同じ色の値に設定されます。<br /><br /> `Environment.ToolWindowTabMouseOverBackgroundEnd`<br /><br /> グラデーション境界は、Visual Studio 2013 で同じ色の値に設定されます。|  
|![ホバー時の [ツール ウィンドウの背景] タブ](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br /><br /> **ホバー時の背景ツール ウィンドウ タブ**|前景 (テキスト)|`Environment.ToolWindowTabMouseOverText`|  
|![ホバー時の [ツール ウィンドウの背景] タブ](../extensibility/ux-guidelines/media/0303-106-toolwindowbackgroundtabhover.png "0303-106_ToolWindowBackgroundTabHover")<br /><br /> **ホバー時の背景ツール ウィンドウ タブ**|境界線|`Environment.ToolWindowTabMouseOverBorder`<br /><br /> 背景と同じ色に設定されます。|  
  
#### <a name="auto-hide-tabs"></a>自動非表示タブ  
 ![自動&#45;非表示赤線](../extensibility/ux-guidelines/media/0303-107-autohideredline.png "0303-107_AutoHideRedline")  
  
 使用するケース  
 自動非表示ツール ウィンドウ タブと一致させる UI を作成するすべての場所。  
  
 使用しないケース  
 シェルにテーマの更新がある場合に自動的に変更しない UI。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![自動&#45;[非表示] タブ](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303-108_AutoHideTab")<br /><br /> **既定の自動非表示タブ**|背景|`Environment.AutoHideTabBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![自動&#45;[非表示] タブ](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303-108_AutoHideTab")<br /><br /> **既定の自動非表示タブ**|前景 (テキスト)|`Environment.AutoHideTabText`|  
|![自動&#45;[非表示] タブ](../extensibility/ux-guidelines/media/0303-108-autohidetab.png "0303-108_AutoHideTab")<br /><br /> **既定の自動非表示タブ**|境界線|`Environment.AutoHideTabBorder`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時に自動&#45;タブを非表示にする](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303-109_AutoHideTabHover")<br /><br /> **ホバー時の [自動非表示] タブ**|背景|`Environment.AutoHideTabMouseOverBackgroundBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時に自動&#45;タブを非表示にする](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303-109_AutoHideTabHover")<br /><br /> **ホバー時の [自動非表示] タブ**|前景 (テキスト)|`Environment.AutoHideTabMouseOverText`|  
|![ホバー時に自動&#45;タブを非表示にする](../extensibility/ux-guidelines/media/0303-109-autohidetabhover.png "0303-109_AutoHideTabHover")<br /><br /> **ホバー時の [自動非表示] タブ**|境界線|`Environment.AutoHideTabMouseOverBorder`|  
  
### <a name="common-shared-controls"></a>コモン共有コントロール  
 標準の Visual Studio のコマンド バーを機能で使用する場合、スタイル設定されたシェル コントロールにアクセスでき、これらのコモン コントロールを再テンプレート化する必要はありません。 ただし、カスタム コマンド バーを作成する必要がある場合は、カスタム コントロールも構築することが必要な場合があります。 その場合は、UI が Visual Studio の他の部分と一貫性を持つように、次の各コントロールに正しいトークン名を使用してください。  
  
#### <a name="search-box"></a>検索ボックス  
 可能な場合は常に、Visual Studio 環境で提供されるコモン検索コントロールを使用します。 検索ボックスの色は、入力フィールド、動作設定ボタン、ドロップダウン ボタン、ドロップダウン メニューのトークン名が格納されている **ShellColors.pkgdef** ファイルの "SearchControl" カテゴリにあります。  
  
 検索ボックスは次の複数の状態のいずれかの場合があり、一部の状態は相互に排他的です。  
  
- "フォーカスされている" または "フォーカスされていない" は、カーソルがテキスト ボックス内にあるかどうかを示します。  
  
- "アクティブ" または "非アクティブ" は、ユーザーがテキスト ボックスに検索クエリを入力したかどうかを示します。  
  
- "ホバー" は、ユーザーがマウスを使用して検索ボックスの上にマウス ポインターを置いたことを意味します (この状態は他のすべての状態よりもオーバーライドされます)。  
  
- "無効" は、現在のコンテキストに対して検索機能がオフになっていることを意味します。  
  
  ![検索ボックスの赤線](../extensibility/ux-guidelines/media/0303-110-searchboxredline.png "0303-110_SearchBoxRedline")  
  
  使用するケース  
  カスタム検索ボックスを設計する場合。  
  
  使用しないケース  
  - 検索ボックス以外のすべてのもの。  
  
- 検索ボックスの UI と常に一致させるわけではないすべてのもの。  
  
  **Focused**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **入力フィールド**|背景|`SearchControl.FocusedBackground`|  
|![フォーカスされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **入力フィールド**|前景 (テキスト)|`SearchControl.FocusedBackground`|  
|![フォーカスされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **入力フィールド**|境界線|`SearchControl.FocusedBorder`|  
|![フォーカスされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-111-searchinputfieldfocused.png "0303-111_SearchInputFieldFocused")<br /><br /> **入力フィールド**|区切り記号|`SearchControl.FocusedDropDownSeparator`|  
|![フォーカスされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **[アクション] ボタン**|背景|なし|  
|![フォーカスされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **[アクション] ボタン**|前景 (検索グリフ)|`SearchControl.SearchGlyph`|  
|![フォーカスされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **[アクション] ボタン**|前景 (停止グリフ)|`SearchControl.StopGlyph`|  
|![フォーカスされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **[アクション] ボタン**|前景 (クリア グリフ)|`SearchControl.ClearGlyph`|  
|![フォーカスされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-112-searchactionbuttonfocused.png "0303-112_SearchActionButtonFocused")<br /><br /> **[アクション] ボタン**|境界線|該当なし|  
|![検索ドロップダウン&#45;フォーカスを絞ったボタン](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br /><br /> **ドロップダウン ボックス**|背景|`SearchControl.FocusedDropDownButton`|  
|![検索ドロップダウン&#45;フォーカスを絞ったボタン](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`SearchControl.FocusedDropDownButtonGlyph`|  
|![検索ドロップダウン&#45;フォーカスを絞ったボタン](../extensibility/ux-guidelines/media/0303-113-searchdropdownbuttonfocused.png "0303-113_SearchDropdownButtonFocused")<br /><br /> **ドロップダウン ボックス**|境界線|`SearchControl.FocusedDropDownButtonBorder`|  
  
 **フォーカスされていない**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされていない検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **アクティブな入力フィールド**|背景|`SearchControl.SearchActiveBackground`|  
|![フォーカスされていない検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **アクティブな入力フィールド**|前景 (テキスト)|`SearchControl.SearchActiveBackground`|  
|![フォーカスされていない検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **アクティブな入力フィールド**|境界線|`SearchControl.UnfocusedBorder`|  
|![フォーカスされていない検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-searchinputfieldunfocused.png "0303-114_SearchInputFieldUnfocused")<br /><br /> **アクティブな入力フィールド**|区切り記号|`SearchControl.DropDownSeparator`|  
|![フォーカスされず非アクティブな検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **非アクティブな入力フィールド**|背景|`SearchControl.Unfocused`|  
|![フォーカスされず非アクティブな検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **非アクティブな入力フィールド**|前景 (テキスト)|`SearchControl.Unfocused`|  
|![フォーカスされず非アクティブな検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **非アクティブな入力フィールド**|境界線|`SearchControl.UnfocusedBorder`|  
|![フォーカスされず非アクティブな検索入力フィールド](../extensibility/ux-guidelines/media/0303-114-1-searchinputfieldunfocusedinactive.png "0303-114-1_SearchInputFieldUnfocusedInactive")<br /><br /> **非アクティブな入力フィールド**|区切り記号|`SearchControl.DropDownSeparator`|  
|![フォーカスされていない検索操作ボタン](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **[アクション] ボタン**|背景|該当なし|  
|![フォーカスされていない検索操作ボタン](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **[アクション] ボタン**|前景 (検索グリフ)|`SearchControl.SearchGlyph`|  
|![フォーカスされていない検索操作ボタン](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **[アクション] ボタン**|前景 (停止グリフ)|`SearchControl.StopGlyph`|  
|![フォーカスされていない検索操作ボタン](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **[アクション] ボタン**|前景 (クリア グリフ)|`SearchControl.ClearGlyph`|  
|![フォーカスされていない検索操作ボタン](../extensibility/ux-guidelines/media/0303-115-searchactionbuttonunfocused.png "0303-115_SearchActionButtonUnfocused")<br /><br /> **[アクション] ボタン**|境界線|該当なし|  
|![検索&#45;ドロップダウンボタン見る](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br /><br /> **ドロップダウン ボックス**|背景|`SearchControl.UnfocusedDropDownButton`|  
|![検索&#45;ドロップダウンボタン見る](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`SearchControl.UnfocusedDropDownButtonGlyph`|  
|![検索&#45;ドロップダウンボタン見る](../extensibility/ux-guidelines/media/0303-116-searchdropdownbuttonunfocused.png "0303-116_SearchDropdownButtonUnfocused")<br /><br /> **ドロップダウン ボックス**|境界線|`SearchControl.UnfocusedDropDownButtonBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押された検索操作ボタン](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br /><br /> **[アクション] ボタン**|背景|`SearchControl.ActionButtonMouseDown`|  
|![押された検索操作ボタン](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br /><br /> **[アクション] ボタン**|前景 (グリフ)|`SearchControl.ActionButtonMouseDownGlyph`|  
|![押された検索操作ボタン](../extensibility/ux-guidelines/media/0303-116-1-searchactionbuttonpressed.png "0303-116-1_SearchActionButtonPressed")<br /><br /> **[アクション] ボタン**|境界線|`SearchControl.ActionButtonMouseDownBorder`|  
|![押された&#45;下へ移動ボタン](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|背景|`SearchControl.MouseDownDropDownButton`|  
|![押された&#45;下へ移動ボタン](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`SearchControl.MouseDownDropDownButtonGlyph`|  
|![押された&#45;下へ移動ボタン](../extensibility/ux-guidelines/media/0303-116-2-searchdropdownbuttonpressed.png "0303-116-2_SearchDropdownButtonPressed")<br /><br /> **ドロップダウン ボックス**|境界線|`SearchControl.MouseDownDropDownButtonBorder`|  
  
 **強調表示 (テキストのみ)**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![強調表示された検索入力フィールド](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **テキストが強調表示された入力フィールド**|背景|`SearchControl.Selection`|  
|![強調表示された検索入力フィールド](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **テキストが強調表示された入力フィールド**|前景 (テキスト)|`SearchControl.FocusedBackground`|  
|![強調表示された検索入力フィールド](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **テキストが強調表示された入力フィールド**|境界線|なし|  
|![強調表示された検索入力フィールド](../extensibility/ux-guidelines/media/0303-120-searchinputfieldhighlight.png "0303-120_SearchInputFieldHighlight")<br /><br /> **テキストが強調表示された入力フィールド**|区切り記号|`SearchControl.FocusedDropDownSeparator`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効にされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **入力フィールド**|背景|`SearchControl.Disabled`|  
|![無効にされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **入力フィールド**|前景 (テキスト)|`SearchControl.Disabled`|  
|![無効にされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **入力フィールド**|境界線|`SearchControl.DisabledBorder`|  
|![無効にされた検索入力フィールド](../extensibility/ux-guidelines/media/0303-121-searchinputfielddisabled.png "0303-121_SearchInputFieldDisabled")<br /><br /> **入力フィールド**|区切り記号|`SearchControl.DropDownSeparator`|  
|![無効にされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br /><br /> **[アクション] ボタン**|背景|なし|  
|![無効にされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br /><br /> **[アクション] ボタン**|前景 (グリフ)|`SearchControl.ActionButtonDisabledGlyph`|  
|![無効にされた検索操作ボタン](../extensibility/ux-guidelines/media/0303-122-searchactionbuttondisabled.png "0303-122_SearchActionButtonDisabled")<br /><br /> **[アクション] ボタン**|境界線|なし|  
|![[検索] ドロップダウンボタンが無効になっている&#45;](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br /><br /> **ドロップダウン ボックス**|背景|なし|  
|![[検索] ドロップダウンボタンが無効になっている&#45;](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br /><br /> **ドロップダウン ボックス**|前景 (グリフ)|`SearchControl.DisabledDownButtonGlyph`|  
|![[検索] ドロップダウンボタンが無効になっている&#45;](../extensibility/ux-guidelines/media/0303-123-searchdropdownbuttondisabled.png "0303-123_SearchDropdownButtonDisabled")<br /><br /> **ドロップダウン ボックス**|境界線|なし|  
  
##### <a name="search-drop-down-lists"></a>検索ドロップダウン リスト  
 検索ボックスのドロップダウン メニューは、Visual Studio の他のドロップダウン メニューより少し複雑になる可能性があります。 "提案される検索" と "検索オプション" の各セクションは、メニューに単独または一緒に表示され、それぞれに別の色が付けられます。 これらの 2 つのセクションが一緒に表示される場合は線で区切られ、ドロップダウン メニュー全体が境界線で囲まれます。  
  
 ![検索&#45;ダウン赤線](../extensibility/ux-guidelines/media/0303-124-searchdropdownredline.png "0303-124_SearchDropdownRedline")  
  
使用するケース  
- カスタム検索ドロップダウン リストを作成する場合。  

- 正しいリスト コンポーネントの正しいトークン名。  

使用しないケース  
- 他のコンテキストで表示されるドロップダウン リスト。  

- 指定以外の背景と前景の組み合わせ。  
  
  **既定 (他の状態はありません)**  
  
|要素|トークン名: Category.color|  
|-------------|--------------------------------|  
|境界線|`SearchControl.PopupBorder`|  
|区切り記号|`SearchControl.PopupSectionHeaderSeparator`|  
|シャドウ|`Environment.DropShadowBackground`|  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![推奨される検索](../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303-125_SearchSuggested")<br /><br /> **提案される検索**|背景|`SearchControl.PopupItemsListBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![推奨される検索](../extensibility/ux-guidelines/media/0303-125-searchsuggested.png "0303-125_SearchSuggested")<br /><br /> **提案される検索**|前景 (テキスト)|`SearchControl.PopupItemText`|  
|![検索チェック ボックス](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **検索オプション (チェック ボックス)**|背景|`SearchControl.PopupSectionBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![［検索のオプション］](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **検索オプション (リンク)**|背景|`SearchControl.PopupSectionBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![検索チェック ボックス](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **検索オプション (チェック ボックス)**|前景 (チェック ボックス テキスト)|`SearchControl.PopupCheckboxText`|  
|![［検索のオプション］](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **検索オプション (リンク)**|前景 (チェック ボックス テキスト)|`SearchControl.PopupCheckboxText`|  
|![検索チェック ボックス](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **検索オプション (チェック ボックス)**|前景 (リンク テキスト)|`SearchControl.PopupButtonText`|  
|![［検索のオプション］](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **検索オプション (リンク)**|前景 (リンク テキスト)|`SearchControl.PopupButtonText`|  
|![検索チェック ボックス](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **検索オプション (チェック ボックス)**|ヘッダーの背景|`SearchControl.PopupSectionHeaderGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![［検索のオプション］](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **検索オプション (リンク)**|ヘッダーの背景|`SearchControl.PopupSectionHeaderGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![検索チェック ボックス](../extensibility/ux-guidelines/media/0303-126-searchcheckbox.png "0303-126_SearchCheckbox")<br /><br /> **検索オプション (チェック ボックス)**|前景 (ヘッダー テキスト)|`SearchControl.PopupSectionHeaderText`|  
|![［検索のオプション］](../extensibility/ux-guidelines/media/0303-127-searchoptions.png "0303-127_SearchOptions")<br /><br /> **検索オプション (リンク)**|前景 (ヘッダー テキスト)|`SearchControl.PopupSectionHeaderText`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時の推奨される検索](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br /><br /> **提案される検索**|背景|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時の推奨される検索](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br /><br /> **提案される検索**|前景 (テキスト)|`SearchControl.PopupMouseOverItemText`|  
|![ホバー時の推奨される検索](../extensibility/ux-guidelines/media/0303-128-searchsuggestedhover.png "0303-128_SearchSuggestedHover")<br /><br /> **提案される検索**|境界線|`SearchControl.PopupControlMouseOverBorder`|  
|![ホバー時の検索チェック ボックス](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **提案される検索 (チェック ボックス)**|背景|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時の検索オプション](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **［検索のオプション］**|背景|`SearchControl.PopupControlMouseOverBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![ホバー時の検索チェック ボックス](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **提案される検索 (チェック ボックス)**|前景 (チェック ボックス テキスト)|`SearchControl.PopupCheckboxMouseDownText`|  
|![ホバー時の検索オプション](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **［検索のオプション］**|前景 (チェック ボックス テキスト)|`SearchControl.PopupCheckboxMouseDownText`|  
|![ホバー時の検索チェック ボックス](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **提案される検索 (チェック ボックス)**|前景 (リンク テキスト)|`SearchControl.PopupButtonMouseDownText`|  
|![ホバー時の検索オプション](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **［検索のオプション］**|前景 (リンク テキスト)|`SearchControl.PopupButtonMouseDownText`|  
|![ホバー時の検索チェック ボックス](../extensibility/ux-guidelines/media/0303-129-searchcheckboxhover.png "0303-129_SearchCheckboxHover")<br /><br /> **提案される検索 (チェック ボックス)**|境界線|`SearchControl.PopupControlMouseOverBorder`|  
|![ホバー時の検索オプション](../extensibility/ux-guidelines/media/0303-130-searchoptionshover.png "0303-130_SearchOptionsHover")<br /><br /> **［検索のオプション］**|境界線|`SearchControl.PopupControlMouseOverBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押された推奨される検索](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **提案される検索 (チェック ボックス)**|チェック ボックスの背景|`SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された検索オプション](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **［検索のオプション］**|チェック ボックスの背景|`SearchControl.PopupControlMouseDownBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された推奨される検索](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **提案される検索 (チェック ボックス)**|チェック ボックスの背景|`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された検索オプション](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **［検索のオプション］**|チェック ボックスの背景|`SearchControl.PopupControlMouseDownBackgroundGradientEnd`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された推奨される検索](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **提案される検索 (チェック ボックス)**|前景 (チェック ボックス テキスト)|`SearchControl.PopupCheckboxMouseDownText`|  
|![押された検索オプション](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **［検索のオプション］**|前景 (チェック ボックス テキスト)|`SearchControl.PopupCheckboxMouseDownText`|  
|![押された推奨される検索](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **提案される検索 (チェック ボックス)**|リンクの背景|`SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された検索オプション](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **［検索のオプション］**|リンクの背景|`SearchControl.PopupButtonMouseDownBackgroundGradientBegin`<br /><br /> 最新のテーマの UI では使用されませんが、この背景にはグラデーション境界と値があります。|  
|![押された推奨される検索](../extensibility/ux-guidelines/media/0303-131-searchsuggestedpressed.png "0303-131_SearchSuggestedPressed")<br /><br /> **提案される検索 (チェック ボックス)**|前景 (リンク テキスト)|`SearchControl.PopupButtonMouseDownText`|  
|![押された検索オプション](../extensibility/ux-guidelines/media/0303-132-searchoptionspressed.png "0303-132_SearchOptionsPressed")<br /><br /> **［検索のオプション］**|前景 (リンク テキスト)|`SearchControl.PopupButtonMouseDownText`|  
  
#### <a name="hyperlink"></a>ハイパーリンク  
 ハイパーリンクは、前景と背景の組み合わせがない 1 つのコントロールです。 すべての場合において、ハイパーリンクの前景色を使用します。この色は濃色、灰色、白の背景で正しく表示されます。 ハイパーリンク コントロールの色トークンを使用しない場合、"押されている" ことを示す既定のシステム カラー (明るい赤) が表示されます。 これは、コントロールで適切な環境の色トークンが使用されていないことを示します。  
  
 ![ハイパーリンクの赤線](../extensibility/ux-guidelines/media/0303-133-hyperlinkredline.png "0303-133_HyperlinkRedline")  
  
 使用するケース  
 カスタム ハイパーリンクを作成する必要がある場合。  
  
 使用しないケース  
 ハイパーリンク以外のすべてのもの。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ハイパーリンクの既定値](../extensibility/ux-guidelines/media/0303-134-hyperlink.png "0303-134_Hyperlink")|前景 (テキスト)|`Environment.PanelHyperlink`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のハイパーリンク](../extensibility/ux-guidelines/media/0303-135-hyperlinkhover.png "0303-135_HyperlinkHover")|前景 (テキスト)|`Environment.PanelHyperlinkHover`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたハイパーリンク](../extensibility/ux-guidelines/media/0303-136-hyperlinkpressed.png "0303-136_HyperlinkPressed")|前景 (テキスト)|`Environment.PanelHyperlinkPressed`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効にされたハイパーリンク](../extensibility/ux-guidelines/media/0303-137-hyperlinkdisabled.png "0303-137_HyperlinkDisabled")|前景 (テキスト)|`Environment.PanelHyperlinkDisabled`|  
  
#### <a name="infobar"></a>情報バー  
 情報バーは該当するコンテキストの詳細を提供するために使用され、常にドキュメント ウィンドウまたはツール ウィンドウの上部に表示されます。  
  
 ![情報バーの赤線](../extensibility/ux-guidelines/media/0303-138-infobarredline.png "0303-138_InfobarRedline")  
  
 使用するケース  
 カスタム情報バーを作成する場合。  
  
 使用しないケース  
 情報バーに類似していない UI 要素。  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![情報バー](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **情報バー**|背景|`Environment.InfoBackground`|  
|![情報バー](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **情報バー**|前景 (テキスト)|`Environment.InfoText`|  
|![情報バー](../extensibility/ux-guidelines/media/0303-139-infobar.png "0303-139_Infobar")<br /><br /> **情報バー**|境界線|`Environment.ToolWindowBorder`|  
  
#### <a name="scroll-bar"></a>スクロール バー  
 スクロール バーは Visual Studio 環境によってスタイルが設定され、テーマを指定する必要はありません。 ただし、UI が Visual Studio 環境のこの部分と常に一致するように、スクロールバーで使用する色を利用することもできます。  
  
 ![スクロール バーの赤線](../extensibility/ux-guidelines/media/0303-140-scrollbarredline.png "0303-140_ScrollbarRedline")  
  
 使用するケース  
 Visual Studio のスクロール バーと一致させる UI を作成する場合。  
  
 使用しないケース  
 スクロール バーの UI と常に一致させるわけではないすべてのもの。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![スクロール バー](../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303-141_Scrollbar")<br /><br /> **Scrollbar**|スクロール バー|`Environment.ScrollBarBackground`|  
|![スクロール バー](../extensibility/ux-guidelines/media/0303-141-scrollbar.png "0303-141_Scrollbar")<br /><br /> **Scrollbar**|前景 (つまみ)|`Environment.ScrollBarThumbBackground`|  
|![スクロール バーの矢印](../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303-142_ScrollbarArrow")<br /><br /> **スクロール矢印**|背景|`Environment.ScrollBarArrowBackground`<br /><br /> スクロール バーと同じ色に設定されます。|  
|![スクロール バーの矢印](../extensibility/ux-guidelines/media/0303-142-scrollbararrow.png "0303-142_ScrollbarArrow")<br /><br /> **スクロール矢印**|前景 (グリフ)|`Environment.ScrollBarArrowGlyph`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のスクロール バー](../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303-143_ScrollbarHover")<br /><br /> **Scrollbar**|スクロール バー|`Environment.ScrollBarBackground`|  
|![ホバー時のスクロール バー](../extensibility/ux-guidelines/media/0303-143-scrollbarhover.png "0303-143_ScrollbarHover")<br /><br /> **Scrollbar**|前景 (つまみ)|`Environment.ScrollBarThumbMouseOverBackground`|  
|![ホバー時のスクロール バーの矢印](../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br /><br /> **スクロール矢印**|背景|`Environment.ScrollBarArrowMouseOverBackground`<br /><br /> スクロール バーと同じ色に設定されます。|  
|![ホバー時のスクロール バーの矢印](../extensibility/ux-guidelines/media/0303-144-scrollbararrowhover.png "0303-144_ScrollbarArrowHover")<br /><br /> **スクロール矢印**|前景 (グリフ)|`Environment.ScrollBarArrowGlyphMouseOver`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたスクロール バー](../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303-145_ScrollbarPressed")<br /><br /> **Scrollbar**|スクロール バー|`Environment.ScrollBarBackground`|  
|![押されたスクロール バー](../extensibility/ux-guidelines/media/0303-145-scrollbarpressed.png "0303-145_ScrollbarPressed")<br /><br /> **Scrollbar**|前景 (つまみ)|`Environment.ScrollBarThumbPressedBackground`|  
|![押されたスクロール バーの矢印](../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br /><br /> **スクロール矢印**|背景|`Environment.ScrollBarArrowPressedBackground`<br /><br /> スクロール バーと同じ色に設定されます。|  
|![押されたスクロール バーの矢印](../extensibility/ux-guidelines/media/0303-146-scrollbararrowpressed.png "0303-146_ScrollbarArrowPressed")<br /><br /> **スクロール矢印**|前景 (グリフ)|`Environment.ScrollBarArrowGlyphPressed`|  
  
#### <a name="tree-view"></a><a name="BKMK_TreeView"></a> ツリービュー  
 ソリューション エクスプローラー、サーバー エクスプローラー、クラス ビューなど、いくつかのツール ウィンドウでは、色が TreeView カテゴリの色の名前によって制御される階層組織スキームが実装されます。 ツリー ビューのすべての項目に背景色とテキスト色があります。 入れ子にされた子要素がある項目には、項目が展開されているか折りたたまれているかを示すグリフもあります。  
  
 ![ツリー ビューの赤線](../extensibility/ux-guidelines/media/0303-147-treeviewredline.png "0303-147_TreeViewRedline")  
  
 使用するケース  
 階層組織ビューを実装する必要があるすべての場所。  
  
使用しないケース  
- ツリー ビューに類似していないすべてのもの。  

- 指定以外の背景と前景の組み合わせ。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ツリー ビュー](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|背景|`TreeView.Background`|  
|![ツリー ビュー](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|前景 (テキスト)|`TreeView.Background`|  
|![ツリー ビュー](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|前景 (グリフ)|`TreeView.Glyph`|  
|![ツリー ビュー](../extensibility/ux-guidelines/media/0303-148-treeview.png "0303-148_TreeView")|境界線|なし|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のツリー ビュー](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|背景|`TreeView.Background`|  
|![ホバー時のツリー ビュー](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|前景 (テキスト)|`TreeView.Background`|  
|![ホバー時のツリー ビュー](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|前景 (グリフ)|`TreeView.GlyphMouseOver`|  
|![ホバー時のツリー ビュー](../extensibility/ux-guidelines/media/0303-149-treeviewhover.png "0303-149_TreeViewHover")|境界線|なし|  
  
 **上でドラッグする**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドラッグされたツリー ビュー](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|背景|`TreeView.DragOverItem`|  
|![ドラッグされたツリー ビュー](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|前景 (テキスト)|`TreeView.DragOverItem`|  
|![ドラッグされたツリー ビュー](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|前景 (グリフ)|`TreeView.DragOverItemGlyph`|  
|![ドラッグされたツリー ビュー](../extensibility/ux-guidelines/media/0303-150-treeviewdragover.png "0303-150_TreeViewDragOver")|境界線|なし|  
  
 **Selected**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|背景|`TreeView.SelectedItemActive`|  
|![フォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|前景 (テキスト)|`TreeView.SelectedItemActive`|  
|![フォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|前景 (グリフ)|`TreeView.SelectedItemActiveGlyph`|  
|![フォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-151-treeviewfocused.png "0303-151_TreeViewFocused")<br /><br /> **Focused**|境界線|`TreeView.FocusVisualBorder`|  
|![フォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **フォーカスされていない**|背景|`TreeView.SelectedItemInactive`|  
|![フォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **フォーカスされていない**|前景 (テキスト)|`TreeView.SelectedItemInactive`|  
|![フォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **フォーカスされていない**|前景 (グリフ)|`TreeView.SelectedItemInactiveGlyph`|  
|![フォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-152-treeviewunfocused.png "0303-152_TreeViewUnfocused")<br /><br /> **フォーカスされていない**|境界線|なし|  
  
 **選択したものの上をホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のフォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|背景|`TreeView.SelectedItemActive`|  
|![ホバー時のフォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|前景 (テキスト)|`TreeView.SelectedItemActive`|  
|![ホバー時のフォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|前景 (グリフ)|`TreeView.SelectedItemActiveGlyphMouseOver`|  
|![ホバー時のフォーカスされたツリー ビュー](../extensibility/ux-guidelines/media/0303-153-treeviewfocusedhover.png "0303-153_TreeViewFocusedHover")<br /><br /> **Focused**|境界線|なし`TreeView.FocusVisualBorder`|  
|![ホバー時のフォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **フォーカスされていない**|背景|`TreeView.SelectedItemInactive`|  
|![ホバー時のフォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **フォーカスされていない**|前景 (テキスト)|`TreeView.SelectedItemInactive`|  
|![ホバー時のフォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **フォーカスされていない**|前景 (グリフ)|`TreeView.SelectedItemActiveGlyphMouseOver`|  
|![ホバー時のフォーカスされていないツリー ビュー](../extensibility/ux-guidelines/media/0303-154-treeviewunfocusedhover.png "0303-154_TreeViewUnfocusedHover")<br /><br /> **フォーカスされていない**|境界線|なし|  
  
#### <a name="button-controls"></a>ボタン コントロール  
 ![ボタン コントロールの赤線](../extensibility/ux-guidelines/media/0303-155-buttoncontrolredline.png "0303-155_ButtonControlRedline")  
  
 使用するケース  
 Visual Studio のテーマ (淡色、濃色、青、またはシステムのハイコントラスト テーマ) と統合するドキュメント ウェル内のボタン。  
  
 使用しないケース  
 Visual Studio のテーマの一部でないカスタム背景に対して表示されるボタン。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![Button](../extensibility/ux-guidelines/media/0303-156-button.png "0303-156_Button")|Button|`CommonControls.Button`|  
|![Button](../extensibility/ux-guidelines/media/0303-156-button.png "0303-156_Button")|ボタンの境界線|`CommonControls.ButtonBorder`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効にされたボタン](../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303-157_ButtonDisabled")|Button|`CommonControls.ButtonDisabled`|  
|![無効にされたボタン](../extensibility/ux-guidelines/media/0303-157-buttondisabled.png "0303-157_ButtonDisabled")|ボタンの境界線|`CommonControls.ButtonBorderDisabled`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のボタン](../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303-158_ButtonHover")|Button|`CommonControls.ButtonHover`|  
|![ホバー時のボタン](../extensibility/ux-guidelines/media/0303-158-buttonhover.png "0303-158_ButtonHover")|ボタンの境界線|`CommonControls.ButtonBorderHover`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたボタン](../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303-159_ButtonPressed")|Button|`CommonControls.ButtonPressed`|  
|![押されたボタン](../extensibility/ux-guidelines/media/0303-159-buttonpressed.png "0303-159_ButtonPressed")|ボタンの境界線|`CommonControls.ButtonBorderPressed`|  
  
 **Focused**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたボタン](../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303-160_ButtonFocused")|Button|`CommonControls.ButtonFocused`|  
|![フォーカスされたボタン](../extensibility/ux-guidelines/media/0303-160-buttonfocused.png "0303-160_ButtonFocused")|ボタンの境界線|`CommonControls.ButtonBorderFocused`|  
  
#### <a name="check-box-controls"></a>チェック ボックス コントロール  
 ![チェック ボックスの赤線](../extensibility/ux-guidelines/media/0303-161-checkboxredline.png "0303-161_CheckboxRedline")  
  
 使用するケース  
 ドキュメント ウェル内に含まれるチェック ボックス コントロール。  
  
 使用しないケース  
 チェック ボックス コントロールでない UI。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![チェック ボックス](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|背景|`CommonControls.CheckBoxBackground`|  
|![チェック ボックス](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|境界線|`CommonControls.CheckBoxBorder`|  
|![チェック ボックス](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|Text|`CommonControls.CheckBoxText`|  
|![チェック ボックス](../extensibility/ux-guidelines/media/0303-162-checkbox.png "0303-162_Checkbox")|グリフ|`CommonControls.CheckBoxGlyph`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![無効にされたチェック ボックス](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|背景|`CommonControls.CheckBoxBackgroundDisabled`|  
|![無効にされたチェック ボックス](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|境界線|`CommonControls.CheckBoxBorderDisabled`|  
|![無効にされたチェック ボックス](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|Text|`CommonControls.CheckBoxTextDisabled`|  
|![無効にされたチェック ボックス](../extensibility/ux-guidelines/media/0303-163-checkboxdisabled.png "0303-163_CheckboxDisabled")|グリフ|`CommonControls.CheckBoxGlyphDisabled`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のチェック ボックス](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|背景|`CommonControls.CheckBoxBackgroundHover`|  
|![ホバー時のチェック ボックス](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|境界線|`CommonControls.CheckBoxBorderHover`|  
|![ホバー時のチェック ボックス](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|Text|`CommonControls.CheckBoxTextHover`|  
|![ホバー時のチェック ボックス](../extensibility/ux-guidelines/media/0303-164-checkboxhover.png "0303-164_CheckboxHover")|グリフ|`CommonControls.CheckBoxGlyphHover`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押されたチェック ボックス](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|背景|`CommonControls.CheckBoxBackgroundPressed`|  
|![押されたチェック ボックス](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|境界線|`CommonControls.CheckBoxBorderPressed`|  
|![押されたチェック ボックス](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|Text|`CommonControls.CheckBoxTextPressed`|  
|![押されたチェック ボックス](../extensibility/ux-guidelines/media/0303-165-checkboxpressed.png "0303-165_CheckboxPressed")|グリフ|`CommonControls.CheckBoxGlyphPressed`|  
  
 **Focused**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたチェック ボックス](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|背景|`CommonControls.CheckBoxBackgroundFocused`|  
|![フォーカスされたチェック ボックス](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|境界線|`CommonControls.CheckBoxBorderFocused`|  
|![フォーカスされたチェック ボックス](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|Text|`CommonControls.CheckBoxTextFocused`|  
|![フォーカスされたチェック ボックス](../extensibility/ux-guidelines/media/0303-166-checkboxfocused.png "0303-166_CheckboxFocused")|グリフ|`CommonControls.CheckBoxGlyphFocused`|  
  
#### <a name="drop-boxcombo-box-controls"></a>ドロップ ボックス/コンボ ボックス コントロール  
 ![ドロップダウン&#45;&#47;コンボボックス赤線](../extensibility/ux-guidelines/media/0303-167-dropdowncomboboxredline.png "0303-167_DropDownComboBoxRedline")  
  
使用するケース  
ドキュメント ウェルに含まれるドロップダウンとコンボ ボックス。  

使用しないケース  
- ドロップダウンまたはコンボ ボックスでない UI。  

- コマンド バーの [Drop-down](../misc/shared-colors.md#BKMK_CommandDropDown) または [Combo box](../misc/shared-colors.md#BKMK_CommandComboBox) 。  
  
  **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドロップダウン&#45;&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|背景|`CommonControls.ComboBoxBackground`|  
|![ドロップダウン&#45;&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|境界線|`CommonControls.ComboBoxBorder`|  
|![ドロップダウン&#45;&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|Text|`CommonControls.ComboBoxText`|  
|![ドロップダウン&#45;&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|区切り記号|`CommonControls.ComboBoxSeparator`|  
|![ドロップダウン&#45;&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|グリフ|`CommonControls.ComboBoxGlyph`|  
|![ドロップダウン&#45;&#47;コンボボックス](../extensibility/ux-guidelines/media/0303-168-dropdowncombobox.png "0303-168_DropDownComboBox")|グリフの背景|`CommonControls.ComboBoxGlyphBackground`|  
  
 **Disabled**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドロップダウン&#47;コンボボックスを無効に&#45;](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|背景|`CommonControls.ComboBoxBackgroundDisabled`|  
|![ドロップダウン&#47;コンボボックスを無効に&#45;](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|境界線|`CommonControls.ComboBoxBorderDisabled`|  
|![ドロップダウン&#47;コンボボックスを無効に&#45;](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|Text|`CommonControls.ComboBoxTextDisabled`|  
|![ドロップダウン&#47;コンボボックスを無効に&#45;](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|区切り記号|`CommonControls.ComboBoxSeparatorDisabled`|  
|![ドロップダウン&#47;コンボボックスを無効に&#45;](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|グリフ|`CommonControls.ComboBoxGlyphDisabled`|  
|![ドロップダウン&#47;コンボボックスを無効に&#45;](../extensibility/ux-guidelines/media/0303-169-dropdowncomboboxdisabled.png "0303-169_DropDownComboBoxDisabled")|グリフの背景|`CommonControls.ComboBoxGlyphBackgroundDisabled`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時に&#45;ダウン&#47;コンボボックスをドロップします](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|背景|`CommonControls.ComboBoxBackgroundHover`|  
|![ホバー時に&#45;ダウン&#47;コンボボックスをドロップします](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|境界線|`CommonControls.ComboBoxBorderHover`|  
|![ホバー時に&#45;ダウン&#47;コンボボックスをドロップします](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|Text|`CommonControls.ComboBoxTextHover`|  
|![ホバー時に&#45;ダウン&#47;コンボボックスをドロップします](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|区切り記号|`CommonControls.ComboBoxSeparatorHover`|  
|![ホバー時に&#45;ダウン&#47;コンボボックスをドロップします](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|グリフ|`CommonControls.ComboBoxGlyphHover`|  
|![ホバー時に&#45;ダウン&#47;コンボボックスをドロップします](../extensibility/ux-guidelines/media/0303-170-dropdowncomboboxhover.png "0303-170_DropDownComboBoxHover")|グリフの背景|`CommonControls.ComboBoxGlyphBackgroundHover`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押された&#47;コンボボックス&#45;ドロップダウン](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|背景|`CommonControls.ComboBoxBackgroundPressed`|  
|![押された&#47;コンボボックス&#45;ドロップダウン](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|境界線|`CommonControls.ComboBoxBorderPressed`|  
|![押された&#47;コンボボックス&#45;ドロップダウン](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|Text|`CommonControls.ComboBoxTextPressed`|  
|![押された&#47;コンボボックス&#45;ドロップダウン](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|区切り記号|`CommonControls.ComboBoxSeparatorPressed`|  
|![押された&#47;コンボボックス&#45;ドロップダウン](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|グリフ|`CommonControls.ComboBoxGlyphPressed`|  
|![押された&#47;コンボボックス&#45;ドロップダウン](../extensibility/ux-guidelines/media/0303-171-dropdowncomboboxpressed.png "0303-171_DropDownComboBoxPressed")|グリフの背景|`CommonControls.ComboBoxGlyphBackgroundPressed`|  
  
 **Focused**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスがあるコンボボックス&#47;ドロップダウン&#45;](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|背景|`CommonControls.ComboBoxBackgroundFocused`|  
|![フォーカスがあるコンボボックス&#47;ドロップダウン&#45;](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|境界線|`CommonControls.ComboBoxBorderFocused`|  
|![フォーカスがあるコンボボックス&#47;ドロップダウン&#45;](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|Text|`CommonControls.ComboBoxTextFocused`|  
|![フォーカスがあるコンボボックス&#47;ドロップダウン&#45;](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|区切り記号|`CommonControls.ComboBoxSeparatorFocused`|  
|![フォーカスがあるコンボボックス&#47;ドロップダウン&#45;](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|グリフ|`CommonControls.ComboBoxGlyphFocused`|  
|![フォーカスがあるコンボボックス&#47;ドロップダウン&#45;](../extensibility/ux-guidelines/media/0303-172-dropdowncomboboxfocused.png "0303-172_DropDownComboBoxFocused")|グリフの背景|`CommonControls.ComboBoxGlyphBackgroundFocused`|  
  
 **テキスト入力選択**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ドロップダウン&#47;コンボボックスのテキスト入力&#45;](../extensibility/ux-guidelines/media/0303-173-dropdowncomboboxtextinput.png "0303-173_DropDownComboBoxTextInput")|強調表示|`CommonControls.ComboBoxTextInputSelection`|  
  
 **押されている - リスト項目ビュー**  
  
|コンポーネント|要素|トークン名: Color.category|  
|---------------|-------------|--------------------------------|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListBackground`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListBackgroundHover`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListItemBackgroundPressed`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|背景|`CommonControls.ComboBoxListItemBackgroundFocused`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|境界線|`CommonControls.ComboBoxListBorder`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|境界線|`CommonControls.ComboBoxListBorderHover`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|境界線|`CommonControls.ComboBoxListBorderPressed`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|境界線|`CommonControls.ComboBoxListBorderFocused`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|項目のテキスト|`CommonControls.ComboBoxListItemText`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|項目のテキスト|`CommonControls.ComboBoxListItemTextHover`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|項目のテキスト|`CommonControls.ComboBoxListItemTextPressed`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|項目のテキスト|`CommonControls.ComboBoxListItemTextFocused`|  
|![ドロップダウン&#47;コンボボックスリストビュー&#45;](../extensibility/ux-guidelines/media/0303-174-dropdowncomboboxlistview.png "0303-174_DropDownComboBoxListView")|背景の影|`CommonControls.ComboBoxListBackgroundShadow`|  
  
#### <a name="tabular-data-grid-controls"></a>表形式のデータ (グリッド) コントロール  
 表形式のデータ コントロール (グリッド コントロールとも呼ばれる) は、複数列の大量のデータを表示するために使用する Visual Studio のコモン コントロールです。 標準の表形式のデータ コントロールは、[エラー一覧] ツール ウィンドウ、IntelliTrace レポート、メモリ ヒープ ビューなど、Visual Studio 内の複数の場所にあります。 提供される標準の表形式のデータ コントロールを常に使用します。 まれに、標準の表形式のデータ コントロールにアクセスできないことがあります。 このような場合は、次のトークン名を使用して、UI が Visual Studio の他の表形式のデータ コントロールと一貫性を保つようにします。  
  
 ![表形式データ &#40;グリッドコントロール&#41; 赤線](../extensibility/ux-guidelines/media/0303-197-tabulardatagridcontrolredline.png "0303-197_TabularDataGridControlRedline")  
  
 使用するケース  
 表形式コントロールまたはグリッド コントロール。  
  
 使用しないケース  
 表形式またはグリッド コントロール以外の UI。  
  
##### <a name="column-headers"></a>列見出し  
 列ヘッダーは、背景、境界線、タイトル テキスト、およびグリッドがその列で並べ替えられたときに通常使用されるオプションのグリフで構成されます。  
  
|State|要素|トークン名: Category.color|  
|-----------|-------------|--------------------------------|  
|Default|背景|`Header.Default`|  
|Default|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|Default|前景 (グリフ)|`Header.Glyph`|  
|Default|境界線|`Header.SeparatorLine`|  
|ホバー|背景|`Header.MouseOver`|  
|ホバー|前景 (テキスト)|`Environment.CommandBarTextHover`|  
|ホバー|前景 (グリフ)|`Header.MouseOverGlyph`|  
|ホバー|境界線|`Header.SeparatorLine`|  
|押されている|背景|`CommonControls.CheckBoxBackgroundPressed`|  
|押されている|前景 (テキスト)|`CommonControls.CheckBoxBorderPressed`|  
|押されている|前景 (グリフ)|`CommonControls.CheckBoxTextPressed`|  
|押されている|境界線|`CommonControls.CheckBoxGlyphPressed`|  
  
##### <a name="list-view-items"></a>リスト ビュー項目  
 リスト ビュー項目は、背景とコンテンツで構成されます。 コンテンツは、テキスト、アイコン、またはその両方の場合があります。  
  
|State|要素|トークン名: Category.color|  
|-----------|-------------|--------------------------------|  
|Default|背景|透明|  
|Default|前景 (テキスト)|`Environment.CommandBarTextActive`|  
|Default|境界線|なし|  
|選択済み (アクティブ)|背景|`TreeView.SelectedItemActive`|  
|選択済み (アクティブ)|前景 (テキスト)|`TreeView.SelectedItemActiveText`|  
|選択済み (アクティブ)|境界線|なし|  
|選択済み (非アクティブ)|背景|`TreeView.SelectedItemInactive`|  
|選択済み (非アクティブ)|前景 (テキスト)|`TreeView.SelectedItemInactiveText`|  
|選択済み (非アクティブ)|境界線|なし|  
  
### <a name="manifest-designer"></a>マニフェスト デザイナー  
 マニフェスト デザイナーは、Windows 8 および Windows Phone 8 プロジェクトのマニフェスト ファイルを編集しやすくするための手段として設計されています。 使用可能な共有フレームワークはありませんが、向き/ナビゲーション タブと全体的な構造のデザイン レイアウトおよび色を一致させることが適切な場合があります。 レイアウトの詳細については、「 [Layout for Visual Studio](../extensibility/ux-guidelines/layout-for-visual-studio.md)」を参照してください。  
  
 ![マニフェスト デザイナーの赤線](../extensibility/ux-guidelines/media/0303-175-manifestdesignerredline.png "0303-175_ManifestDesignerRedline")  
  
使用するケース  
- マニフェスト デザイナーと同様のデザイナー。  

- ドキュメント ウェル内のエディターの上部でコモン タブ コントロールを使用する代わり。  

使用しないケース  
- 7 つ以上のタブがある場合。  

- マニフェスト デザイナーのように構造化されていないすべての UI。  
  
|State|コンポーネント|要素|トークン名: Category.color|  
|-----------|---------------|-------------|--------------------------------|  
|既定 (選択済み)|タブ|背景|`ManifestDesigner.TabActive`|  
|既定 (選択済み)|タブ|境界線|なし|  
|既定 (選択済み)|説明ペイン|背景|`ManifestDesigner.DescriptionPane`|  
|既定 (選択済み)|コンテンツ ページ|背景|`ManifestDesigner.Background`|  
|既定 (選択済み)|コンテンツ ページ|ダイアログ ヘルパー テキスト|`ManifestDesigner.WatermarkText`<br /><br /> このトークン名はその機能に一致しません。|  
|選択されていない|タブ|背景|`ManifestDesigner.Tab.Inactive`|  
|ホバー|タブ|背景|`ManifestDesigner.Tab.Mouseover`|  
  
### <a name="tagging"></a>タグ付け  
 Visual Studio は、タグ付けをサポートしています。タグ付けにより、ユーザーは追跡のために検索可能なキーワードを宣言できます。 たとえば、プロジェクト マネージャーと開発者は、Team Foundation Server (TFS) を使用して作業項目にタグを付けることができます。 次の表に、タグ自体と、ホバー時および選択済み状態で表示される "アイコンを閉じる" グリフの両方の色の名前を示します。  
  
 ![タグ付けの赤線](../extensibility/ux-guidelines/media/0303-176-taggingredline.png "0303-176_TaggingRedline")  
  
 使用するケース  
 タグ付けをサポートする UI。  
  
 使用しないケース  
 他の種類の UI。  
  
#### <a name="tag"></a>タグ  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![Tag](../extensibility/ux-guidelines/media/0303-177-tag.png "0303-177_Tag")<br /><br /> **既定**|背景|`Tag.Background`|  
|![Tag](../extensibility/ux-guidelines/media/0303-177-tag.png "0303-177_Tag")<br /><br /> **既定**|前景 (テキスト)|`Tag.Background`|  
|![ホバー時のタグ](../extensibility/ux-guidelines/media/0303-178-taghover.png "0303-178_TagHover")<br /><br /> **ホバー**|背景|`Tag.HoverBackground`|  
|![ホバー時のタグ](../extensibility/ux-guidelines/media/0303-178-taghover.png "0303-178_TagHover")<br /><br /> **ホバー**|前景 (テキスト)|`Tag.HoverBackgroundText`|  
|![押されたタグ](../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303-179_TagPressed")<br /><br /> **Pressed**|背景|`Tag.PressedBackground`|  
|![押されたタグ](../extensibility/ux-guidelines/media/0303-179-tagpressed.png "0303-179_TagPressed")<br /><br /> **Pressed**|前景 (テキスト)|`Tag.PressedBackgroundText`|  
|![選択されたタグ](../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303-180_TagSelected")<br /><br /> **Selected**|背景|`Tag.SelectedBackground`|  
|![選択されたタグ](../extensibility/ux-guidelines/media/0303-180-tagselected.png "0303-180_TagSelected")<br /><br /> **Selected**|前景 (テキスト)|`Tag.SelectedBackgroundText`|  
  
#### <a name="glyph-close-icon"></a>グリフ (アイコンを閉じる)  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![タグ &#40;グリフ&#41;](../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303-181_TagGlyph")<br /><br /> **既定 (既定タグ)**|背景|該当なし|  
|![タグ &#40;グリフ&#41;](../extensibility/ux-guidelines/media/0303-181-tagglyph.png "0303-181_TagGlyph")<br /><br /> **既定 (既定タグ)**|前景 (グリフ)|`Tag.TagHoverGlyph`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時に &#40;グリフ&#41; にタグを付ける](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303-182_TagGlyphHover")<br /><br /> **ホバー (既定タグ)**|背景|`Tag.TagHoverGlyphHoverBackground`|  
|![ホバー時に &#40;グリフ&#41; にタグを付ける](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303-182_TagGlyphHover")<br /><br /> **ホバー (既定タグ)**|前景 (グリフ)|`Tag.TagHoverGlyphHover`|  
|![ホバー時に &#40;グリフ&#41; にタグを付ける](../extensibility/ux-guidelines/media/0303-182-tagglyphhover.png "0303-182_TagGlyphHover")<br /><br /> **ホバー (既定タグ)**|境界線|`Tag.TagHoverGlyphHoverBorder`|  
  
 **Pressed**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![タグ &#40;&#41; が押されました](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303-183_TagGlyphPressed")<br /><br /> **押されている (既定タグ)**|背景|`Tag.TagHoverGlyphPressedBackground`|  
|![タグ &#40;&#41; が押されました](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303-183_TagGlyphPressed")<br /><br /> **押されている (既定タグ)**|前景 (グリフ)|`Tag.TagHoverGlyphPressed`|  
|![タグ &#40;&#41; が押されました](../extensibility/ux-guidelines/media/0303-183-tagglyphpressed.png "0303-183_TagGlyphPressed")<br /><br /> **押されている (既定タグ)**|境界線|`Tag.TagHoverGlyphPressedBorder`|  
  
 **選択されたタグ/既定グリフ**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![選択されたタグ](../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303-184_TagSelected")<br /><br /> **既定 (選択されたタグ)**|背景|該当なし|  
|![選択されたタグ](../extensibility/ux-guidelines/media/0303-184-tagselected.png "0303-184_TagSelected")<br /><br /> **既定 (選択されたタグ)**|前景 (グリフ)|`Tag.TagSelectedGlyph`|  
  
 **選択されたタグ/グリフ ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時の選択されたタグ](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303-185_TagSelectedHover")<br /><br /> **ホバー (選択されたタグ)**|背景|`Tag.TagSelectedGlyphHoverBackground`|  
|![ホバー時の選択されたタグ](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303-185_TagSelectedHover")<br /><br /> **ホバー (選択されたタグ)**|前景 (グリフ)|`Tag.TagSelectedGlyphHover`|  
|![ホバー時の選択されたタグ](../extensibility/ux-guidelines/media/0303-185-tagselectedhover.png "0303-185_TagSelectedHover")<br /><br /> **ホバー (選択されたタグ)**|境界線|`Tag.TagSelectedGlyphHoverBorder`|  
  
 **選択されたタグ/押されているグリフ**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![押された選択済みのタグ](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303-186_TagSelectedPressed")<br /><br /> **押されている (選択されたタグ)**|背景|`Tag.TagSelectedGlyphPressedBackground`|  
|![押された選択済みのタグ](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303-186_TagSelectedPressed")<br /><br /> **押されている (選択されたタグ)**|前景 (グリフ)|`Tag.TagSelectedGlyphPressed`|  
|![押された選択済みのタグ](../extensibility/ux-guidelines/media/0303-186-tagselectedpressed.png "0303-186_TagSelectedPressed")<br /><br /> **押されている (選択されたタグ)**|境界線|`Tag.TagSelectedGlyphPressedBorder`|  
  
### <a name="shell"></a>Shell  
  
#### <a name="background"></a>背景  
 環境の背景色は、2 つのレイヤーで構成されます。 下部レイヤーは、IDE 全体にわたる単色です。 上部レイヤーは、コマンド シェルフの下、および IDE の左端と右端のツール ウィンドウ自動非表示チャネルの間に収まります。 Visual Studio 2013 の時点で、上部と下部の背景レイヤーは、ライト テーマとダーク テーマで同じ色に設定されます。  
  
 ![シェル バックグラウンドの赤線](../extensibility/ux-guidelines/media/0303-187-shellbackgroundredline.png "0303-187_ShellBackgroundRedline")  
  
 使用するケース  
 Visual Studio 環境の背景を一致させる場所。  
  
使用しないケース  
- 背景サーフェイスではない場所の塗りつぶし。  

- 前景要素を配置する背景。  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|下部レイヤー|背景|`Environment.EnvironmentBackground`|  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|上部レイヤー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.EnvironmentBackgroundGradientBegin`|  
|上部レイヤー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.EnvironmentBackgroundGradientEnd`|  
|上部レイヤー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.EnvironmentBackgroundGradientMiddle1`|  
|上部レイヤー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.EnvironmentBackgroundGradientMiddle2`|  
  
#### <a name="command-shelf"></a>コマンド シェルフ  
 コマンド シェルフの背景には 2 セットのトークン名が使用されます。1 セットはメニュー バーが位置する場所、もう 1 セットはコマンド バーが位置する場所に使用されます。 個々のコマンド バー グループには、独自の背景色値があります。これについては「コマンド バー」セクションで詳しく説明しています。 メニュー バーとコマンド バーのテキストについては、それぞれメニューとコマンド バーのセクションで説明しています。  
  
 ![コマンド シェルフの赤線](../extensibility/ux-guidelines/media/0303-188-commandshelfredline.png "0303-188_CommandShelfRedline")  
  
使用するケース  
- メニューまたはツール バーを配置する領域。  

- 正しい背景/フォアグラウンドトークン名の組み合わせで指定します。  
  
  使用しないケース  
  コマンド シェルフに類似していない領域。  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|メニュー バー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.CommandShelfHighlightGradientBegin`|  
|メニュー バー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.CommandShelfHighlightGradientMiddle`|  
|メニュー バー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.CommandShelfHighlightGradientEnd`|  
|コマンド バー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.CommandShelfBackgroundGradientBegin`|  
|コマンド バー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.CommandShelfBackgroundGradientMiddle`|  
|コマンド バー|背景<br /><br /> *グラデーション境界は、Visual Studio 2013 のライト テーマとダーク テーマで同じ色の値に設定されます。*|`Environment.CommandShelfBackgroundGradientEnd`|  
  
### <a name="toolbox"></a>ツールボックス  
 ツールボックスは、Visual Studio で最も頻繁に使用されるコモン ツール ウィンドウの 1 つです。 これは基本的に、特別なテーマとスタイルが適用されたツリー コントロールです。  
  
 ![ツールボックスの赤線](../extensibility/ux-guidelines/media/0303-189-toolboxredline.png "0303-189_ToolboxRedline")  
  
 使用するケース  
 常にシェル ツールボックスと一貫性を維持するツール ウィンドウを設計する場合。  
  
 使用しないケース  
 ツールボックス UI と類似していないすべてのもの、またはシェル ツールボックスの色を変更した場合に UI に問題が発生するかどうか不明な場合。  
  
 **既定**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **親ノード**|背景|`Environment.ToolboxContent`<br /><br /> 見出し<br /><br /> `Environment.ToolWindowBackground`<br /><br /> 個々の項目、または利用可能なコントロールがない場合はウィンドウ全体|  
|![ツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **子ノード**|背景|`Environment.ToolboxContent`<br /><br /> 見出し<br /><br /> `Environment.ToolWindowBackground`<br /><br /> 個々の項目、または利用可能なコントロールがない場合はウィンドウ全体|  
|![ツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **親ノード**|境界線|なし|  
|![ツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **子ノード**|境界線|なし|  
|![ツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **親ノード**|前景 (グリフ)|`Environment.ToolboxContent`|  
|![ツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **子ノード**|前景 (グリフ)|`Environment.ToolboxContent`|  
|![ツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-190-toolboxparentnode.png "0303-190_ToolboxParentNode")<br /><br /> **親ノード**|前景 (テキスト)|`Environment.ToolboxContent`|  
|![ツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-191-toolboxchildnode.png "0303-191_ToolboxChildNode")<br /><br /> **子ノード**|前景 (テキスト)|`Environment.ToolboxContent`|  
  
 **ホバー**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![ホバー時のツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br /><br /> **子ノードにホバー時のツールボックス**|背景|`Environment.ToolboxContentMouseOver`<br /><br /> 個々の項目のみ|  
|![ホバー時のツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br /><br /> **子ノードにホバー時のツールボックス**|境界線|なし|  
|![ホバー時のツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-192-toolboxchildnodehover.png "0303-192_ToolboxChildNodeHover")<br /><br /> **子ノードにホバー時のツールボックス**|前景 (テキスト)|`Environment.ToolboxContentMouseOver`<br /><br /> 個々の項目のみ|  
  
 **Selected**  
  
|コンポーネント|要素|トークン名: Category.color|  
|---------------|-------------|--------------------------------|  
|![フォーカスされたツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **フォーカスされた親ノード**|背景|`TreeView.SelectedItemActive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **フォーカスされた子ノード**|背景|`TreeView.SelectedItemActive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **フォーカスされた親ノード**|境界線|`TreeView.FocusVisualBorder`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **フォーカスされた子ノード**|境界線|`TreeView.FocusVisualBorder`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **フォーカスされた親ノード**|前景 (グリフ)|`TreeView.SelectedItemActive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **フォーカスされた子ノード**|前景 (グリフ)|`TreeView.SelectedItemActive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-193-toolboxparentnodefocused.png "0303-193_ToolboxParentNodeFocused")<br /><br /> **フォーカスされた親ノード**|前景 (テキスト)|`TreeView.SelectedItemActive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされたツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-194-toolboxchildnodefocused.png "0303-194_ToolboxChildNodeFocused")<br /><br /> **フォーカスされた子ノード**|前景 (テキスト)|`TreeView.SelectedItemActive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされていないツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **フォーカスされていない親ノード**|背景|`TreeView.SelectedItemInactive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされていないツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **フォーカスされていない子ノード**|背景|`TreeView.SelectedItemInactive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされていないツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **フォーカスされていない親ノード**|境界線|なし|  
|![フォーカスされていないツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **フォーカスされていない子ノード**|境界線|なし|  
|![フォーカスされていないツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **フォーカスされていない親ノード**|前景 (グリフ)|`TreeView.SelectedItemInactive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされていないツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **フォーカスされていない子ノード**|前景 (グリフ)|`TreeView.SelectedItemInactive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされていないツールボックスの親ノード](../extensibility/ux-guidelines/media/0303-195-toolboxparentnodeunfocused.png "0303-195_ToolboxParentNodeUnfocused")<br /><br /> **フォーカスされていない親ノード**|前景 (テキスト)|`TreeView.SelectedItemInactive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
|![フォーカスされていないツールボックスの子ノード](../extensibility/ux-guidelines/media/0303-196-toolboxchildnodeunfocused.png "0303-196_ToolboxChildNodeUnfocused")<br /><br /> **フォーカスされていない子ノード**|前景 (テキスト)|`TreeView.SelectedItemInactive`<br /><br /> [Tree view](../misc/shared-colors.md#BKMK_TreeView) カテゴリから|  
  
## <a name="color-value-reference"></a>カラー値の参照  
  
|コンポーネント|パーツ|要素|State|淡色|濃色|青|ハイコントラスト|
|---------|----|-------|-----|-----|----|----|----|  
|区切り線|||Default|FFEEEEF2|FF2D2D30|FFEEEEF2|ControlDark|  
|展開グリフ||フォアグラウンド|Default|||||  
|展開グリフ||フォアグラウンド|ホバー|||||  
|展開グリフ||背景|Default|||||  
|展開グリフ||背景|ホバー|||||  
|展開グリフ||境界線|Default|||||  
|展開グリフ||境界線|ホバー|||||