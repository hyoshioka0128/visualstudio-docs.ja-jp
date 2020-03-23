---
title: ビジュアルスタジオの色とスタイル |マイクロソフトドキュメント
ms.date: 07/31/2017
ms.topic: conceptual
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ceea00a3fa77a9c1106f24f28ac1d5890437b41
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301561"
---
# <a name="colors-and-styling-for-visual-studio"></a>Visual Studio の色とスタイル

## <a name="use-color-in-visual-studio"></a>ビジュアル スタジオで色を使用する

Visual Studio では、色は、装飾としてだけでなく、通信ツールとして主に使用されます。 色を最小限にして使用し、次のような状況に備え、予約を行います。

- 意味または所属を伝える (プラットフォームや言語の修飾子など)

- 注目を集める (たとえば、ステータスの変更を示す)

- 読みやすさを向上させ、UI をナビゲートするためのランドマークを提供する

- 望ましさを高める

Visual Studio の UI 要素に色を割り当てるためのオプションがいくつかあります。 どのオプションを使用するか、または正しく使用する方法を把握することが難しい場合があります。 このトピックは、次のトピックで役立ちます。

- Visual Studio で色を定義するために使用されるさまざまなサービスとシステムについて理解する。

- 特定の要素に対して正しいオプションを選択します。

- 選択したオプションを正しく使用します。

> [!NOTE]
> UI 要素に対して、16 進、RGB、またはシステム カラーをハードコードしないでください。 サービスを使用すると、柔軟に調色を調整できます。 また、サービスがないと[、VSColor サービス](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)のテーマ切り替え機能を利用できなくなります。

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>Visual Studio インターフェイス要素に色を割り当てるメソッド

UI 要素に最適な方法を選択します。

| Your UI | Method | 彼らは何ですか? |
| --- | --- | --- |
| 埋め込みまたはスタンドアロンのダイアログ ボックスがあります。 | **システムカラー** | オペレーティング システムが UI 要素の色と外観を定義できるようにするシステム名 。.一般的なダイアログ コントロールなど。 |
| VS 環境全体と一貫性を保つカスタム UI があり、共有トークンのカテゴリと意味に一致する UI 要素があります。 | **共通の共有色** | 特定の UI 要素の既存の定義済みカラー トークン名 |
| 個々のフィーチャまたはフィーチャ グループがあり、類似した要素に対して共有色はありません。 | **[作成した色]** | 領域に固有で、他の UI と共有することを意図していない色のトークン名 |
| エンド ユーザーが UI やコンテンツをカスタマイズできるようにする場合 (たとえば、テキスト エディターや特殊なデザイナー ウィンドウの場合)。 | **エンド ユーザーのカスタマイズ**<br /><br />**([&gt;ツール オプション]ダイアログ)** | **[&gt;ツール オプション]** ダイアログの [フォントと色] ページ、または 1 つの UI 機能に固有の特殊なページで定義された設定。 |

### <a name="visual-studio-themes"></a>ビジュアルスタジオのテーマ

Visual Studio には、明るい色、暗い色、青の 3 つの異なる色のテーマがあります。 また、アクセシビリティのために設計されたシステム全体のカラーテーマであるハイコントラストモードも検出します。

ユーザーは Visual Studio の最初の使用時にテーマを選択するように求められ、後で **[ツール&gt;オプション環境&gt;&gt;全般]** に移動し、[色のテーマ] ドロップダウン メニューから新しいテーマを選択することでテーマを切り替えることができます。

また、コントロール パネルを使用して、システム全体をハイ コントラスト テーマの 1 つに切り替えることもできます。 ユーザーがハイ コントラスト テーマを選択すると、Visual Studio の色テーマ セレクターは Visual Studio の色に影響を与えなくなります。 ハイ コントラスト モードの詳細については、「[ハイ コントラスト 色の選択](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors)」を参照してください。

### <a name="the-vscolor-service"></a>VS カラー サービス

Visual Studio には、VSColor サービスと呼ばれる環境の色サービスが用意されており、各 Visual Studio テーマの色の値を含む名前付きエントリに UI 要素の色の値をバインドできます。 これにより、現在のユーザーが選択したテーマまたはシステムのハイ コントラスト モードを反映して、色が自動的に変更されます。 このサービスを使用すると、テーマに関連するすべての色の変更の実装が 1 か所で処理され、サービスの共通の共有色を使用している場合、UI は将来のバージョンの Visual Studio で新しいテーマを自動的に反映します。

### <a name="implementation"></a>実装

Visual Studio のソース コードには、トークン名のリストと各テーマのそれぞれの色の値を含む複数のパッケージ定義ファイルが含まれています。 カラー サービスは、これらのパッケージ定義ファイルで定義されている VSColors を読み取ります。 これらの色は XAML マークアップまたはコードで参照され、メソッドまたは DynamicResource マッピングを`IVsUIShell5.GetThemedColor`通じて読み込まれます。

### <a name="system-colors"></a>システムカラー

コモン コントロールは、既定でシステム カラーを参照します。 埋め込みダイアログやスタンドアロン ダイアログを作成する場合など、UI でシステム カラーを使用する場合は、何もする必要はありません。

### <a name="common-shared-colors-in-the-vscolor-service"></a>VSColor サービスで共通の共有色

インターフェイス要素は、Visual Studio 環境全体を反映している必要があります。 デザインしている UI コンポーネントに適した共通の共有色を再利用することで、インターフェイスが他の Visual Studio インターフェイスと一致し、テーマが追加または更新されたときに色が自動的に更新されるようにします。

共通の共有色を使用する前に、それらを正しく使用する方法を理解していることを確認してください。 共通の共有色を誤って使用すると、ユーザーの一貫性、イライラ、混乱を招く可能性があります。

### <a name="user-customizable-colors"></a>ユーザーがカスタマイズ可能な色

参照項目:[エンド ユーザーの色の公開](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

場合によっては、コード エディターやデザイン サーフェイスを作成するときのように、エンド ユーザーに UI のカスタマイズを許可する必要があります。 カスタマイズ可能な UI コンポーネントは、[**ツール&gt;オプション]** ダイアログの **[フォントと色**] セクションにあります。

![[&gt;ツール オプション]ダイアログ ボックス](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301-a_ToolsOptionsDialog")<br />[&gt;ツール オプション]ダイアログ ボックス

## <a name="the-vscolor-service"></a><a name="BKMK_TheVSColorService"></a>VSカラーサービス

Visual Studio には、VSColor サービスまたはシェル カラー サービスとも呼ばれる環境カラー サービスが用意されています。 このサービスを使用すると、UI 要素の色値を、各テーマの色を含む名前値の色セットにバインドできます。 VSColor サービスは、すべての UI 要素に使用して、現在のユーザーが選択したテーマを反映するように色が自動的に変更されるようにし、環境の色サービスにバインドされた UI が Visual Studio の将来のバージョンで新しいテーマと統合されるようにする必要があります。

### <a name="how-the-service-works"></a>サービスのしくみ

環境カラー サービスは、UI コンポーネントの .pkgdef で定義された VSColors を読み取ります。 これらの VSColors は、XAML マークアップまたはコードで参照され、`IVsUIShell5.GetThemedColor`または`DynamicResource`マッピングを通じて読み込まれます。

![環境の色のサービス アーキテクチャ](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302-a_EnvironmentColorServiceArchitecture")<br />環境の色のサービス アーキテクチャ

### <a name="accessing-the-service"></a>サービスへのアクセス

VSColor サービスにアクセスする方法は、使用している色のトークンの種類と、使用しているコードの種類に応じて、いくつかの異なる方法があります。

#### <a name="predefined-environment-colors"></a>定義済みの環境色

##### <a name="from-native-code"></a>ネイティブ コードから

シェルは、カラー`COLORREF`へのアクセスを提供するサービスを提供します。 サービス/インターフェイスは次のとおりです。

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

VSShell80.idl ファイルでは、列挙体`__VSSYSCOLOREX`にシェル カラー定数があります。 これを使用するには、MSDN で`enum __VSSYSCOLOREX`説明されている値の 1 つ、または Windows システム API`GetSysColor`が受け入れる通常のインデックス番号のいずれかのインデックス値として渡します。 これを行うと、2 番目のパラメーターで使用する色の RGB 値が返されます。

ペンまたはブラシを新しい色で保存する場合は、Visual Studio シェルから外してメッセージをリッスン`WM_SYSCOLORCHANGE`し`WM_THEMECHANGED`、メッセージをリッスンする必要があります`AdviseBroadcastMessages`。

ネイティブ コードでカラー サービスにアクセスするには、次のような呼び出しを行います。

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> 返`COLORREF`される`GetVSSysColorEx()`値には、テーマカラーの R、G、B コンポーネントが含まれます。 テーマエントリが透過性を使用している場合、アルファ チャネル値は戻る前に破棄されます。 したがって、透過性チャネルが重要な場所で環境の色を使用する必要がある場合は、このトピックで`IVsUIShell5.GetThemedColor`後述`IVsUIShell2::GetVSSysColorEx`するように、 の代わりにを使用する必要があります。

##### <a name="from-managed-code"></a>マネージ コードから

ネイティブ コードを使用した VSColor サービスへのアクセスは、非常に簡単です。 ただし、マネージ コードを使用している場合は、サービスの使用方法を決定するのが難しい場合があります。 このことを念頭に置いて、このプロセスを示す C# コード スニペットを次に示します。

```csharp
private void VSColorPaint(object sender, System.Windows.Forms.PaintEventArgs e)
{
    //getIVSUIShell2
    IVsUIShell2 uiShell2 = Package.GetService(typeof(SVsUIShell)) as IVsUIShell2;
    Debug.Assert (uiShell2 != null, "failed to get IVsUIShell2");

    if (uiShell2 != null)
    {
        //get the COLORREF structure
        uint win32Color;
        uiShell2.GetVSSysColorEx((int)__VSSYSCOLOREX.VSCOLOR_SMARTTAG_HOVER_FILL, out win32Color);

        //translate it to a managed Color structure
        Color myColor = ColorTranslator.FromWin32((int)win32Color);
        //use it
        e.Graphics.FillRectangle(new SolidBrush(myColor), 0, 0, 100, 100);
    }
}
```

Visual Basic で作業している場合は、次の方法を使用します。

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>WPF UI から

アプリケーションの にエクスポートされた値を使用して、Visual Studio`ResourceDictionary`の色にバインドできます。 次に、色テーブルのリソースを使用し、XAML で環境フォント データにバインドする例を示します。

```xml
<Style TargetType="{x:Type Button}">
    <Setter Property="TextBlock.FontFamily"
            Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
    <Setter Property="TextBlock.FontSize"
            Value="{DynamicResource VsFont.EnvironmentFontSize}" />
    <Setter Property="Background"
            Value="{DynamicResource VsBrush.EnvironmentBackgroundGradient}" />
</Style>
```

#### <a name="helper-classes-and-methods-for-managed-code"></a>マネージ コードのヘルパー クラスとメソッド

マネージ コードの場合、シェルのマネージ パッケージ フレームワーク`Microsoft.VisualStudio.Shell.12.0.dll`ライブラリ ( ) には、テーマカラーの使用を容易にするヘルパー クラスがいくつか含まれています。

MPF のクラス`Microsoft.VisualStudio.Shell.VsColors`のヘルパー メソッドには`GetThemedGDIColor()`、`GetThemedWPFColor()`と が含まれます。 これらのヘルパー メソッドは、WinForms または WPF `System.Drawing.Color` UI`System.Windows.Media.Color`で使用されるテーマ エントリの色の値をまたは として返します。

```csharp
IVsUIShell5 shell5;
Button button = new Button();
button.BackColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemBrushKey);
button.ForeColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemTextBrushKey);

/// <summary>
/// Gets a System.Drawing.Color value from the current theme for the given color key.
/// </summary>
/// <param name="vsUIShell">The IVsUIShell5 service, used to get the color's value.</param>
/// <param name="themeResourceKey">The key to find the color for.</param>
/// <returns>The current theme's value of the named color.</returns>
public static System.Drawing.Color GetThemedGDIColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Validate.IsNotNull(vsUIShell, "vsUIShell");
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");

   byte[] colorComponents = GetThemedColorRgba(vsUIShell, themeResourceKey);

   // Note: The Win32 color we get back from IVsUIShell5.GetThemedColor is ABGR
   return System.Drawing.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);
}

private static byte[] GetThemedColorRgba(IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Guid category = themeResourceKey.Category;
   __THEMEDCOLORTYPE colorType = __THEMEDCOLORTYPE.TCT_Foreground
   if (themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundColor || themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundBrush)
   {
      colorType = __THEMEDCOLORTYPE.TCT_Background;
   }

   // This call will throw an exception if the color is not found
   uint rgbaColor = vsUIShell.GetThemedColor(ref category, themeResourceKey.Name, (uint)colorType);
   return BitConverter.GetBytes(rgbaColor);
}
public static System.Windows.Media.Color GetThemedWPFColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Validate.IsNotNull(vsUIShell, "vsUIShell");
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");

   byte[] colorComponents = GetThemedColorComponents(vsUIShell, themeResourceKey);

    return System.Windows.Media.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);
}
```

このクラスは、特定の WPF カラー リソース キーの VSCOLOR 識別子を取得したり、その逆の場合に使用することもできます。

```csharp
public static string GetColorBaseKey(int vsSysColor);
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);
```

クラスの`VsColors`メソッドは、呼び出されるたびにカラー値を返すために VSColor サービスを照会します。 色`System.Drawing.Color`の値をとして取得するには、代わりに VSColor サービスから取得したカラー値`Microsoft.VisualStudio.PlatformUI.VSThemeColor`をキャッシュするクラスのメソッドを使用する代わりに、パフォーマンスを向上させます。 クラスは、シェル ブロードキャスト メッセージ イベントに内部的にサブスクライブし、テーマ変更イベントが発生したときにキャッシュされた値を破棄します。 また、クラスは.テーマの変更をサブスクライブする NET フレンドリーなイベント。 イベントを`ThemeChanged`使用して新しいハンドラーを追加し、メソッド`GetThemedColor()`を使用して対象のカラー値`ThemeResourceKeys`を取得します。 サンプル コードは次のようになります。

```csharp
public MyWindowPanel()
{
    InitializeComponent();

    // Subscribe to theme changes events so we can refresh the colors
    VSColorTheme.ThemeChanged += VSColorTheme_ThemeChanged;

    RefreshColors();
}

private void VSColorTheme_ThemeChanged(ThemeChangedEventArgs e)
{
    RefreshColors();

    // Also post a message to all the children so they can apply the current theme appropriately
    foreach (System.Windows.Forms.Control child in this.Controls)
    {
        NativeMethods.SendMessage(child.Handle, e.Message, IntPtr.Zero, IntPtr.Zero);
    }
}

private void RefreshColors()
{
    this.BackColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowBackgroundColorKey);
    this.ForeColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowTextColorKey);
}

protected override void Dispose(bool disposing)
{
    if (disposing)
    {
        VSColorTheme.ThemeChanged -= this.VSColorTheme_ThemeChanged;
        base.Dispose(disposing);}
}
```

## <a name="choosing-high-contrast-colors"></a><a name="BKMK_ChoosingHighContrastColors"></a>ハイコントラストカラーの選択

### <a name="overview"></a>概要

Windows では、テキスト、背景、およびイメージの色のコントラストを高める、システム レベルのハイ コントラスト テーマをいくつか使用し、画面上の要素の表示を明確にします。 ユーザー補助の理由から、ユーザーがハイ コントラスト テーマに切り替えたときに Visual Studio インターフェイス要素が正しく応答することが重要です。

ハイ コントラスト テーマには、ほんの一握りのシステム カラーしか使用できません。 システムの色名を選択する際には、次のヒントを覚えておいてください。

- **色付けする要素と同じ意味を持つシステム カラーを選択**します。 たとえば、ウィンドウ内のテキストに対してハイコントラストの色を選択する場合は、ControlText ではなく WindowText を使用します。

- **一緒に前景色と背景のペアを選択**するか、すべてのハイ コントラスト テーマで色の選択が動作することを確信していません。

- **UI のどの部分が最も重要かを判断し、コンテンツ領域が目立つようにします。** 色相の微妙な違いが通常区別されるほどの詳細が失われるため、コンテンツ領域ごとに色のバリエーションがないため、強い境界線の色を使用してコンテンツ領域を定義するのが一般的です。

### <a name="system-color-set"></a>システムカラーセット

[WPF チーム ブログ: システムカラー リファレンス](https://blogs.msdn.microsoft.com/wpf/2010/11/30/systemcolors-reference/)のテーブルは、システムカラー名の完全なセットと、各テーマに表示される対応する色相を示します。

この限られた色のセットを UI に適用すると *、「通常の」テーマに存在していた微妙な詳細が失われることが予想されます*。 ツール ウィンドウ内の領域を区別するために使用される、微妙なグレーの色を使用した UI の例を次に示します。 ハイ コントラスト モードで表示される同じウィンドウと組み合わせると、すべての背景が同じ色合いであり、それらの領域の境界線が境界線だけで示されていることがわかります。

![ハイ コントラストでの微妙な詳細の消失の例](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303-a_PropertiesWindow")<br />ハイ コントラストでの微妙な詳細の消失の例

#### <a name="choosing-text-colors-in-an-editor"></a>エディタでのテキストの色の選択

色付きテキストは、エディターまたはデザインサーフェイスで、類似した項目のグループを簡単に識別できるように、意味を示すために使用されます。 ただし、ハイ コントラスト テーマでは、3 色を超えるテキストの色を区別することはできません。 ウィンドウテキスト、グレーテキストとホットトラックテキストは、ウィンドウの背景の表面上で利用可能な唯一の色です。 3 色を超える色を使用することはできないため、ハイ コントラスト モードで表示する最も重要な相違点を慎重に選択します。

各ハイ コントラスト テーマに表示される各トークン名の色相は、エディターのサーフェスで許可されます。

![ハイ コントラスト エディターの比較](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303-b_HCEditorComparison")<br />ハイ コントラスト エディターの比較

ブルーテーマのエディタサーフェスの例:

![青のテーマでのエディター](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303-c_EditorBlue")<br />青のテーマでのエディター

![ハイコントラスト#1テーマのエディタ](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303-d_EditorHC1")<br />ハイコントラスト#1テーマのエディタ

### <a name="usage-patterns"></a>使用パターン

多くの一般的な UI 要素には、既にハイ コントラストの色が定義されています。 独自のシステムカラー名を選択する際に、これらの使用パターンを参照して、UI 要素が類似のコンポーネントと一致するようにすることができます。

| システムカラー | 使用法 |
| --- | --- |
| ActiveCaption | - ホバーして押すと、アクティブなIDEとラフティングウィンドウボタングリフ<br />- IDE とラフト ウィンドウのタイトル バーの背景<br />- デフォルトのステータスバーの背景 |
| ActiveCaptionText | - タイトルバー前景用のアクティブなIDEとラフティングウィンドウ(テキストとグリフ)<br />- ホバーと押しの上にアクティブなウィンドウボタンの背景と境界線 |
| コントロール | - コンボボックス、ドロップダウンリスト、検索コントロールのデフォルトと無効の背景(ドロップダウンボタンを含む)<br />- ドッキングターゲットボタンの背景<br />- コマンド バーの背景<br />- ツール ウィンドウの背景 |
| ControlDark | - IDE の背景<br />- メニューとコマンド バーの区切り記号<br />- コマンド バーの境界線<br />- メニューシャドウ<br />- ツール ウィンドウ タブのデフォルトとホバー境界線と区切り記号<br />- ドキュメントウェルオーバーフローボタンの背景<br />- ドッキングターゲットグリフの境界線 |
| ControlDarkDark |- フォーカスなし、選択したドキュメントタブウィンドウ |
| ControlLight |- タブの境界線を自動的に非表示にする<br />- コンボボックスとドロップダウンリストの境界線<br />- ドッキングターゲットの背景とボーダー |
| コントロールライトライト | - 選択された、焦点を当てた暫定国境 |
| コントロールテキスト | - コンボボックスとドロップダウンリストグリフ<br />- ツール ウィンドウの未選択のタブ テキスト |
| グレーテキスト |- コンボボックスとドロップダウンリスト無効の枠線、ドロップダウングリフ、テキスト、およびメニュー項目のテキスト<br />- 無効なメニューテキスト<br />- 検索コントロール '検索オプション' ヘッダーテキスト<br />- 検索制御セクション区切り記号 |
| ハイライト | - コンボボックスのドロップダウンボタンの背景とドキュメントウェルオーバーフローボタンの境界線を除き、すべてのホバーと押された背景と境界線<br />- 選択した項目の背景 |
| ハイライトテキスト | - すべてのホバーと押された前景 (テキストとグリフ)<br />- フォーカスのあるツールウィンドウとドキュメントタブウィンドウコントロールの前景<br />- フォーカスのあるツール ウィンドウのタイトル バーの境界線<br />- フォーカスが設定され、選択された暫定タブの前景<br />- ドキュメントのウェルオーバーフローボタンの境界線をホバーして押す<br />- 選択されたアイコンの境界線|
| ホットトラック | - スクロールバーの親指の背景と押しの境界線<br />- スクロールバーの矢印グリフを押す |
| 非アクティブなキャプション | - 非アクティブな IDE とラフトウィンドウボタングリフホバー<br />- IDE とラフト ウィンドウのタイトル バーの背景<br />- 無効な検索コントロールの背景 |
| 非アクティブなキャプションテキスト | - 非アクティブな IDE とラフティングウィンドウのタイトルバー前景 (テキストとグリフ)<br />- 非アクティブウィンドウボタンの背景とホバー時の境界線<br />- フォーカスのないツールウィンドウボタンの背景と枠線<br />- 無効な検索コントロールのフォアグラウンド |
| メニュー | - ドロップダウンメニューの背景<br />- チェックマークの背景と無効なチェックマークの背景 |
| メニューテキスト | - ドロップダウン メニューの境界線<br />- マークを確認する<br />- メニューグリフ<br />- ドロップダウン メニューテキスト<br />- 選択されたアイコンの境界線 |
| スクロール バー | - スクロールバーとスクロールバーの矢印の背景、すべての状態 |
| ウィンドウ | - タブの背景を自動的に隠す<br />- メニューバーとコマンドシェルフの背景<br />- 開いているタブと暫定タブの両方に対して、フォーカスを外した、または選択されていないドキュメントウィンドウの背景とドキュメントの境界線<br />- フォーカスのないツール ウィンドウのタイトル バーの背景<br />- ツール ウィンドウ タブの背景(選択済みと選択なしの両方) |
| ウィンドウフレーム | - IDE の境界線 |
| ウィンドウテキスト | - タブの前景を自動的に非表示にする<br />- 選択したツール ウィンドウ タブの前景<br />- フォーカスのないドキュメントウィンドウタブとフォーカスなしまたは未選択の暫定タブ前景<br />- ツリービューのデフォルトの前景と未選択のグリフの上にカーソルを合わせる<br />- ツール ウィンドウが選択されたタブ枠<br />- スクロールバーのサムの背景、境界線、およびグリフ |

## <a name="exposing-colors-for-end-users"></a><a name="BKMK_ExposingColorsForEndUsers"></a>エンド ユーザーの色の公開

### <a name="overview"></a>概要

コード エディターやデザイン サーフェイスを作成する場合など、エンド ユーザーに UI のカスタマイズを許可する場合があります。 この操作を行う最も一般的な方法は、[**&gt;ツール オプション]** ダイアログ ボックスを使用することです。 特殊なコントロールを必要とする高度な UI を使用しない限り、カスタマイズを表示する最も簡単な方法は、ダイアログの **[環境**] セクションの [**フォントと色**] ページを使用することです。 カスタマイズのために公開する各要素について、ユーザーは前景色、背景色、またはその両方を変更できます。

### <a name="building-a-vspackage-for-your-customizable-colors"></a>カスタマイズ可能な色の VSPackage をビルドする

VSPackage は、カスタム カテゴリを通じてフォントと色を制御し、フォントと色のプロパティ ページに項目を表示できます。 このメカニズムを使用する場合、VS パッケージは[、IVs フォントの種類と色の既定値プロバイダーインターフェイス](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider)とその関連付けられているインターフェイスを実装する必要があります。

原則として、このメカニズムを使用して、既存のすべての表示項目と、それらを含むカテゴリを変更できます。 ただし、テキスト エディターカテゴリまたはその表示項目の変更には使用しないでください。 テキスト エディタ カテゴリの詳細については、「[フォントと色の概要](/visualstudio/extensibility/font-and-color-overview?view=vs-2015)」を参照してください。

カスタム カテゴリを実装するか、アイテムを表示するには、VSPackage を必要があります。

- **レジストリ内のカテゴリを作成または識別します。** IDE の **「フォントと色」** プロパティー・ページの実装では、この情報を使用して、特定のカテゴリーをサポートするサービスを正しく照会します。

- **レジストリ内のグループを作成または識別します (オプション)。** 2 つ以上のカテゴリの和集合を表すグループを定義すると便利です。 グループが定義されている場合、IDE は自動的にサブカテゴリをマージし、グループ内に表示項目を配布します。

- **IDE サポートを実装します。**

- **フォントと色の変更を処理します。**

#### <a name="to-create-or-identify-categories"></a>カテゴリを作成または識別するには

カテゴリのローカライズされていない名前の下`[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]``<Category>`に、特殊な種類のカテゴリ レジストリ エントリを作成します。

レジストリに次の 2 つの値を設定します。

| 名前 | Type | Data | 説明 |
| --- | --- | --- | --- |
| カテゴリ | REG_SZ | GUID | カテゴリを識別するために作成された GUID |
| Package | REG_SZ | GUID | カテゴリをサポートする VSPackage サービスの GUID |

 レジストリで指定されたサービスは、対応するカテゴリの[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)の実装を提供する必要があります。

#### <a name="to-create-or-identify-groups"></a>グループを作成または識別するには

グループのローカライズされていない名前の下`[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]``<group>`に、特殊な種類のカテゴリ レジストリ エントリを作成します。

レジストリに次の 2 つの値を設定します。

| 名前 | Type | Data | 説明 |
|--- | --- | --- | --- |
| カテゴリ | REG_SZ | GUID | カテゴリを識別するために作成された GUID |
| Package | REG_SZ | GUID | カテゴリをサポートする VSPackage サービスの GUID |

レジストリで指定されたサービスは、対応するグループ<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>の 実装を提供する必要があります。

![Ivフォントアンドカラーグループの実装](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304-a_FontAndColorGroup")<br />`IVsFontAndColorGroup` の実装

### <a name="to-implement-ide-support"></a>IDE サポートを実装するには

指定された各カテゴリまたはグループ GUID の[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)インターフェイスまたは IDE への<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>インターフェイスを返す[GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject)を実装します。

サポートするすべてのカテゴリについて、VSPackage は[IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)インターフェイスの別のインスタンスを実装します。

[IVsFontAndColor を](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)介して実装されるメソッドは、IDE に次の機能を提供する必要があります。

- カテゴリ内の表示項目の一覧

- 表示項目のローカライズ可能な名前

- カテゴリの各メンバーの情報を表示します

> [!NOTE]
> 各カテゴリには、少なくとも 1 つの表示項目が含まれている必要があります。

IDE は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup>このインタフェースを使用して、複数のカテゴリの和集合を定義します。

その実装は、IDE に次の機能を提供します。

- 特定のグループを構成するカテゴリのリスト

- グループ内の各カテゴリをサポート[する IVsFontAndColorDefaults の](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)インスタンスへのアクセス

- ローカライズ可能なグループ名

#### <a name="updating-the-ide"></a>IDE の更新

IDE は、フォントと色の設定に関する情報をキャッシュします。 したがって、IDE のフォントと色の設定を変更した後、キャッシュが最新であることを確認することがベスト プラクティスです。

キャッシュの更新は[、IvsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager)インターフェイスを介して行われ、グローバルに実行することも、選択した項目に対して実行することもできます。

### <a name="handling-font-and-color-changes"></a>フォントと色の変更を処理する

VSPackage が表示するテキストの色付けを適切にサポートするには、VSPackage をサポートする色付けサービスは、フォントと色のプロパティ ページを通じて行われたユーザーが開始した変更に応答する必要があります。

これを行うには、VSPackage が必要です。

- **インターフェイスを実装して IDE によって生成されたイベント**[を](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents)処理します。 IDE は、フォントと色ページのユーザーによる変更に続いて、適切なメソッドを呼び出します。 たとえば、新しいフォントが選択されている場合[は OnFontChanged](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged)メソッドを呼び出します。

  **または**

- **IDE に変更を求めるポーリングを行います**。 これは、システムで実装された[IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)インターフェイスを介して行うことができます。 主に永続化をサポートするためですが[、GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem)メソッドは表示項目のフォントと色の情報を取得できます。 フォントと色の設定の詳細については、MSDN の記事「[保存されているフォントと色の設定にアクセスする](/visualstudio/extensibility/accessing-stored-font-and-color-settings?view=vs-2015)」を参照してください。

> [!NOTE]
> ポーリング結果が正しいことを確認するには[、IVsFontAndColorCacheManager インターフェイスを使用して、IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager)インターフェイスの取得メソッドを呼び出[IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)す前にキャッシュのフラッシュと更新が必要かどうかを判断します。

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>インターフェイスを実装せずにカスタム フォントと色カテゴリを登録する

次のコード例は、インターフェイスを実装せずにカスタム フォントと色の Category を登録する方法を示しています。

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"

    "NameID"=dword:00000064
```

このコード例では、次のようになります。

- `"NameID"`= パッケージ内のローカライズされたカテゴリ名のリソース ID
- `"ToolWindowPackage"`= パッケージ GUID
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"`は単なる例であり、実際の値は実装者によって提供される新しい GUID である可能性があります。

### <a name="set-the-font-and-color-property-category-guid"></a>フォントと色プロパティカテゴリ GUID を設定します。

次のコード例は、カテゴリ GUID の設定を示しています。

```csharp
// m_pView is your IVsTextView
IVsTextEditorPropertyCategoryContainer spPropCatContainer =
(IVsTextEditorPropertyCategoryContainer)m_pView;
if (spPropCatContainer != null)
{
IVsTextEditorPropertyContainer spPropContainer;
Guid GUID_EditPropCategory_View_MasterSettings =
new Guid("{D1756E7C-B7FD-49a8-B48E-87B14A55655A}");
hr = spPropCatContainer.GetPropertyCategory(
ref GUID_EditPropCategory_View_MasterSettings,
out spPropContainer);
if(hr == 0)
{
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_FontCategory,
catGUID);
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_ColorCategory,
catGUID);
}
}
```
