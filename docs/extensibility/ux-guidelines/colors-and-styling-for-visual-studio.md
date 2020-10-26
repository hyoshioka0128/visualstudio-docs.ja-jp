---
title: Visual Studio の色とスタイル |Microsoft Docs
ms.date: 07/31/2017
ms.topic: conceptual
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f1ba6e9af922a7a7ab4dffe555aa55d3ab7bb9dd
ms.sourcegitcommit: 4b29efeb3a5f05888422417c4ee236e07197fb94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90012101"
---
# <a name="colors-and-styling-for-visual-studio"></a>Visual Studio の色とスタイル

## <a name="use-color-in-visual-studio"></a>Visual Studio での色の使用

Visual Studio では、色は主に装飾としてではなく、通信ツールとして使用されます。 色を最小にして、次のような状況で予約します。

- 意味または所属 (プラットフォームや言語の修飾子など) の通信

- 注目 (状態の変化を示すなど)

- 読みやすさを向上させ、UI 内を移動するための目印を提供する

- 魅力を増やす

Visual Studio の UI 要素に色を割り当てるには、いくつかのオプションがあります。 場合によっては、使用するオプションや、正しく使用する方法を判断するのが困難な場合があります。 このトピックでは、次のことについて説明します。

- Visual Studio での色の定義に使用されるさまざまなサービスとシステムについて説明します。

- 特定の要素に対して適切なオプションを選択します。

- 選択したオプションを正しく使用してください。

> [!NOTE]
> 16進数、RGB、またはシステムカラーを UI 要素にハードコーディングしないでください。 サービスを使用すると、色合いを柔軟に調整できます。 さらに、サービスがないと、 [VSColor サービス](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)のテーマ切り替え機能を利用できなくなります。

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>Visual Studio のインターフェイス要素に色を割り当てる方法

UI 要素に最適な方法を選択します。

| UI | Method | それらは何ですか? |
| --- | --- | --- |
| ダイアログボックスが埋め込まれています。 | **システムカラー** | オペレーティングシステムが UI 要素の色と外観を定義できるシステム名 (コモンダイアログコントロールなど)。 |
| VS 環境全体と一貫性を持たせ、共有トークンのカテゴリとセマンティックの意味に一致する UI 要素があるカスタム UI があること。 | **共通の共有色** | 特定の UI 要素の既存の定義済みの色のトークン名 |
| 個々の機能または機能グループがあり、類似の要素に対して共有色はありません。 | **[作成した色]** | 領域に固有であり、他の UI と共有することを意図していない色トークン名 |
| エンドユーザーが UI またはコンテンツ (たとえば、テキストエディターや特殊なデザイナーウィンドウなど) をカスタマイズできるようにする。 | **エンドユーザーのカスタマイズ**<br /><br />**(ツール &gt; オプションダイアログ)** | [ **ツール &gt; オプション** ] ダイアログの [フォントおよび色] ページ、または1つの UI 機能に固有の特殊なページで定義された設定。 |

### <a name="visual-studio-themes"></a>Visual Studio のテーマ

Visual Studio には、3つの異なる色のテーマ (明るい、暗い、および blue) が用意されています。 また、ハイコントラストモードも検出されます。これは、ユーザー補助向けに設計されたシステム全体の配色テーマです。

ユーザーは、Visual Studio の初回使用時にテーマを選択するよう求められ、後で [ **ツール] [ &gt; オプション] [ &gt; 環境] &gt; [全般** ] に移動して、[配色テーマ] ドロップダウンメニューから新しいテーマを選択することで、テーマを切り替えることができます。

また、ユーザーはコントロールパネルを使用して、システム全体をいくつかのハイコントラストテーマのいずれかに切り替えることもできます。 ユーザーがハイコントラストテーマを選択した場合、visual studio の配色テーマセレクターは Visual Studio の色に影響しなくなります。ただし、ユーザーがハイコントラストモードを終了すると、テーマの変更は保存されます。 ハイコントラストモードの詳細については、「 [ハイコントラスト色の選択](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors)」を参照してください。

### <a name="the-vscolor-service"></a>VSColor サービス

Visual Studio には、VSColor サービスと呼ばれる環境カラーサービスが用意されています。これにより、UI 要素の色の値を、Visual Studio の各テーマの色の値を含む名前付きのエントリにバインドできます。 これにより、現在のユーザーが選択したテーマまたはシステムハイコントラストモードを反映するように、色が自動的に変更されます。 サービスを使用することは、テーマに関連するすべての色の変更の実装が1か所で処理されることを意味します。また、サービスから共通の共有色を使用している場合、今後のバージョンの Visual Studio では、UI に新しいテーマが自動的に反映されます。

### <a name="implementation"></a>実装

Visual Studio のソースコードには、トークン名のリストと各テーマのそれぞれの色の値を含む、いくつかのパッケージ定義ファイルが含まれています。 カラーサービスは、これらのパッケージ定義ファイルで定義されている VSColors を読み取ります。 これらの色は、XAML マークアップまたはコードで参照された後、 `IVsUIShell5.GetThemedColor` メソッドまたは DynamicResource マッピングによって読み込まれます。

### <a name="system-colors"></a>システムカラー

コモンコントロールは、既定でシステムカラーを参照します。 埋め込みまたはスタンドアロンのダイアログを作成する場合のように、UI でシステムカラーを使用する場合は、何もする必要はありません。

### <a name="common-shared-colors-in-the-vscolor-service"></a>VSColor サービスの共通共有色

インターフェイス要素は、Visual Studio 環境全体を反映している必要があります。 デザインする UI コンポーネントに適した共通の共有色を再利用することによって、インターフェイスが他の Visual Studio インターフェイスと一貫性があること、およびテーマが追加または更新されたときに色が自動的に更新されることを確認します。

共通の共有色を使用する前に、それらを正しく使用する方法を理解しておく必要があります。 共通の共有色が不適切に使用されていると、ユーザーのエクスペリエンスが一貫していないか、混乱を招く可能性があります。

### <a name="user-customizable-colors"></a>ユーザーがカスタマイズ可能な色

参照: [エンドユーザーの色の公開](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

場合によっては、コードエディターやデザインサーフェイスを作成するときなど、エンドユーザーが UI をカスタマイズできるようにする必要があります。 カスタマイズ可能な UI コンポーネントは、[ツール] の [ ** &gt; オプション**] ダイアログボックスの [**フォントおよび色**] セクションにあります。ユーザーは、前景色、背景色、またはその両方を変更できます。

![ツールの &gt; オプションダイアログ](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301-a_ToolsOptionsDialog")<br />ツールの &gt; オプションダイアログ

## <a name="the-vscolor-service"></a><a name="BKMK_TheVSColorService"></a> VSColor サービス

Visual Studio には、VSColor サービスまたはシェルカラーサービスとも呼ばれる環境カラーサービスが用意されています。 このサービスを使用すると、UI 要素の色の値を、各テーマの色を含む名前と値の色セットにバインドできます。 すべての UI 要素に対して VSColor サービスを使用する必要があります。これにより、現在のユーザーが選択したテーマを反映するように色が自動的に変更されるようになります。また、環境カラーサービスにバインドされた UI は、今後のバージョンの Visual Studio で新しいテーマと統合されるようになります。

### <a name="how-the-service-works"></a>サービスのしくみ

環境カラーサービスは、UI コンポーネントの pkgdef で定義されている VSColors を読み取ります。 これらの VSColors は、XAML マークアップまたはコードで参照され、またはのいずれかのマッピングによって読み込まれ `IVsUIShell5.GetThemedColor` `DynamicResource` ます。

![環境の色のサービス アーキテクチャ](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302-a_EnvironmentColorServiceArchitecture")<br />環境の色のサービス アーキテクチャ

### <a name="accessing-the-service"></a>サービスへのアクセス

VSColor サービスにアクセスするには、使用している色トークンの種類と使用しているコードの種類に応じて、さまざまな方法があります。

#### <a name="predefined-environment-colors"></a>定義済みの環境の色

##### <a name="from-native-code"></a>ネイティブコードから

シェルには、色のへのアクセスを提供するサービスが用意されて `COLORREF` います。 サービス/インターフェイスは次のとおりです。

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

VSShell80 ファイルでは、列挙体に `__VSSYSCOLOREX` シェルカラー定数が含まれています。 これを使用するには、MSDN に記載されているの値のいずれか、または Windows システム API によって受け入れられる標準のインデックス番号で、インデックス値として渡し `enum __VSSYSCOLOREX` `GetSysColor` ます。 この操作を行うと、2番目のパラメーターで使用する色の RGB 値が返されます。

ペンまたはブラシを新しい色で格納する場合は、 `AdviseBroadcastMessages` (Visual Studio シェルの) を使用して、メッセージとメッセージをリッスンする必要があり `WM_SYSCOLORCHANGE` `WM_THEMECHANGED` ます。

ネイティブコードで color service にアクセスするには、次のような呼び出しを行います。

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> `COLORREF`によって返される値には、 `GetVSSysColorEx()` テーマの色の R、G、B のコンポーネントだけが含まれています。 テーマエントリで透明度を使用している場合は、を返す前にアルファチャネル値が破棄されます。 したがって、必要な環境の色を透明度チャネルが重要な場所で使用する必要がある場合は、 `IVsUIShell5.GetThemedColor` `IVsUIShell2::GetVSSysColorEx` このトピックの後半で説明するように、の代わりにを使用する必要があります。

##### <a name="from-managed-code"></a>マネージコードから

ネイティブコードを介して VSColor サービスにアクセスするのは非常に簡単です。 ただし、マネージコードを使用して作業している場合は、サービスの使用方法を決定するのが難しい場合があります。 この点を念頭に置いて、このプロセスをデモンストレーションする C# コードスニペットを次に示します。

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

Visual Basic で作業している場合は、次を使用します。

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>WPF UI から

アプリケーションのにエクスポートされた値を使用して、Visual Studio の色にバインドでき `ResourceDictionary` ます。 次の例では、color テーブルのリソースと、XAML の環境フォントデータへのバインドを使用します。

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

#### <a name="helper-classes-and-methods-for-managed-code"></a>マネージコードのヘルパークラスとヘルパーメソッド

マネージコードの場合、シェルのマネージパッケージフレームワークライブラリ () には、テーマが適用された `Microsoft.VisualStudio.Shell.12.0.dll` 色の使用を容易にするヘルパークラスがいくつか含まれています。

MPF のクラスのヘルパーメソッドには、 `Microsoft.VisualStudio.Shell.VsColors` とが含まれ `GetThemedGDIColor()` `GetThemedWPFColor()` ます。 これらのヘルパーメソッド `System.Drawing.Color` は、 `System.Windows.Media.Color` WinForms または WPF UI で使用されるテーマエントリの色の値をまたはとして返します。

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

クラスを使用して、指定された WPF 色リソースキーの VSCOLOR 識別子を取得することもできます。また、その逆も可能です。

```csharp
public static string GetColorBaseKey(int vsSysColor);
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);
```

クラスのメソッドは、呼び出されるたび `VsColors` に色の値を返すように VSColor サービスに対してクエリを実行します。 色の値をとして取得するに `System.Drawing.Color` は、代わりに、パフォーマンスを向上させる代わりに、 `Microsoft.VisualStudio.PlatformUI.VSThemeColor` vscolor サービスから取得した色の値をキャッシュするクラスのメソッドを使用します。 クラスは、シェルブロードキャストメッセージイベントに対して内部でサブスクライブし、テーマ変更イベントが発生したときにキャッシュされた値を破棄します。 また、クラスにはが用意されています。テーマの変更をサブスクライブするための NET 対応イベント。 イベントを使用して `ThemeChanged` 新しいハンドラーを追加し、メソッドを使用して `GetThemedColor()` 目的のの色の値を取得し `ThemeResourceKeys` ます。 サンプルコードは次のようになります。

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

## <a name="choosing-high-contrast-colors"></a><a name="BKMK_ChoosingHighContrastColors"></a> ハイコントラスト色の選択

### <a name="overview"></a>概要

Windows では、テキスト、背景、およびイメージの色のコントラストを向上させる、ハイコントラストのシステムレベルのテーマをいくつか使用しています。これにより、要素が画面上でより明確に表示されるようになります。 ユーザー補助の理由により、ユーザーがハイコントラストテーマに切り替えたときに、Visual Studio のインターフェイス要素が正しく応答することが重要です。

ハイコントラストのテーマに使用できるシステムカラーは少数です。 システムの色の名前を選択するときは、次のヒントに注意してください。

- 色付けする要素と**同じセマンティックの意味を持つシステムカラーを選択し**ます。 たとえば、ウィンドウ内のテキストのハイコントラスト色を選択する場合は、ControlText ではなく WindowText を使用します。

- **前景色と背景の組み合わせを選択** するか、またはすべてのハイコントラストテーマで色の選択が機能することを確信できません。

- **UI のどの部分が最も重要であるかを判断し、コンテンツ領域が確実に表示されるようにします。** 色の色合いの微妙な違いは通常は区別されないので、さまざまなコンテンツ領域の色のバリエーションが存在しないので、強い境界線の色を使用するとコンテンツ領域を定義するのが一般的です。

### <a name="system-color-set"></a>システムカラーセット

[「WPF チームブログ: SystemColors リファレンス](/archive/blogs/wpf/systemcolors-reference)」の表は、システムカラー名の完全なセットと、各テーマに表示される対応する色相を示しています。

この限られた色のセットを UI に適用する場合 *は、"通常の" テーマに含まれていた微妙な詳細が失われることが予想さ*れます。 次に示すのは、ツールウィンドウ内の領域を区別するために使用される細い灰色の色を持つ UI の例です。 ハイコントラストモードで表示されている同じウィンドウと組み合わせて使用すると、すべての背景が同じ色合いであり、それらの領域の枠線が境界線だけで示されていることがわかります。

![ハイコントラストでの微妙な詳細の消失の例](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303-a_PropertiesWindow")<br />ハイコントラストでの微妙な詳細の消失の例

#### <a name="choosing-text-colors-in-an-editor"></a>エディターでのテキストの色の選択

色分けされたテキストは、エディターまたはデザインサーフェイスで、類似した項目のグループを簡単に識別できるように、意味を示すために使用されます。 ただし、ハイコントラストのテーマでは、3つ以上のテキスト色を区別する機能がありません。 Windowtext サーフェイスで使用できるのは、WindowText、グレーのテキスト、およびホットトラックテキストのみです。 3色以上を使用することはできないため、ハイコントラストモードでは、表示する最も重要な違いを慎重に選択してください。

各ハイコントラストテーマに表示される、エディター画面で使用できる各トークン名の色相。

![ハイ コントラスト エディターの比較](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303-b_HCEditorComparison")<br />ハイ コントラスト エディターの比較

青のテーマでのエディター画面の例を次に示します。

![青のテーマでのエディター](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303-c_EditorBlue")<br />青のテーマでのエディター

![ハイコントラスト #1 テーマのエディター](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303-d_EditorHC1")<br />ハイコントラスト #1 テーマのエディター

### <a name="usage-patterns"></a>使用パターン

多くの一般的な UI 要素にはハイコントラストの色が既に定義されています。 独自のシステムカラー名を選択するときに、これらの使用パターンを参照して、UI 要素と同様のコンポーネントとの一貫性を保つことができます。

| システムカラー | 使用法 |
| --- | --- |
| ActiveCaption | -ホバー時のアクティブな IDE と rafted のウィンドウボタンのグリフ<br />-IDE および rafted ウィンドウのタイトルバーの背景<br />-既定のステータスバーの背景 |
| ActiveCaptionText | -アクティブな IDE および rafted ウィンドウ (タイトルバーの前景) (テキストとグリフ)<br />-ホバー時と押したときのアクティブなウィンドウボタンの背景と境界線 |
| コントロール | -コンボボックス、ドロップダウンリスト、および検索コントロールの既定値と無効な背景 (ドロップダウンボタンを含む)<br />-ドッキングターゲットボタンの背景<br />-コマンドバーの背景<br />-ツールウィンドウの背景 |
| ControlDark | -IDE の背景<br />-メニューとコマンドバーの区切り記号<br />-コマンドバーの境界線<br />-メニューの影<br />-ツールウィンドウタブの既定とホバーの境界線と区切り記号<br />-ドキュメントウェルオーバーフローボタンの背景<br />-ドックターゲットのグリフの境界線 |
| ControlDarkDark |-見る、選択したドキュメントタブウィンドウ |
| ControlLight |-[自動的に隠す] タブの枠線<br />-コンボボックスとドロップダウンリストの境界線<br />-ドッキングターゲットの背景と境界線 |
| Control電球 | -選択、フォーカスされた仮罫線 |
| ControlText | -コンボボックスとドロップダウンリストのグリフ<br />-ツールウィンドウの選択が解除したタブのテキスト |
| グレーのテキスト |-コンボボックスおよびドロップダウンリストが無効になっている境界線、ドロップダウングリフ、テキスト、およびメニュー項目のテキスト<br />-無効になったメニューテキスト<br />-検索コントロールの ' 検索オプション ' ヘッダーテキスト<br />-検索コントロールセクション区切り記号 |
| 強調表示 | -ホバーと押されたすべての背景と境界線 (コンボボックスのドロップダウンボタンの背景とドキュメントウェルオーバーフローボタンの境界線を除く)<br />-選択された項目の背景 |
| HighlightText | -すべてのホバーと押された foregrounds (テキストとグリフ)<br />フォーカスされているツールウィンドウとドキュメントタブウィンドウコントロールの前景<br />-フォーカスがあるツールウィンドウのタイトルバーの境界線<br />フォーカス、選択された一時的なタブの前景<br />-マウスポインターを置いて押すと、ドキュメントウェルのオーバーフローボタンの境界線<br />-選択されたアイコンの境界線|
| ホットトラック | -押されたときのスクロールバーのつまみの背景と境界線<br />-押されるときのスクロールバーの矢印グリフ |
| Inactivecap | -非アクティブな IDE と rafted のウィンドウボタンのグリフ (ホバー時)<br />-IDE および rafted ウィンドウのタイトルバーの背景<br />-無効になった検索コントロールの背景 |
| InactiveCaptionText | -非アクティブな IDE および rafted windows タイトルバーの前景 (テキストとグリフ)<br />-非アクティブウィンドウボタンの背景およびホバー時の境界線<br />-見るツールウィンドウボタンの背景と境界線<br />-無効になった検索コントロールの前景 |
| メニュー | -ドロップダウンメニューの背景<br />-Checked および disabled チェックマークの背景 |
| MenuText | -ドロップダウンメニューの枠線<br />-チェックマーク<br />-メニューグリフ<br />-ドロップダウンメニューのテキスト<br />-選択されたアイコンの境界線 |
| スクロール バー | -スクロールバーとスクロールバーの矢印の背景、すべての状態 |
| ウィンドウ | -[自動的に隠す] タブの背景<br />-メニューバーとコマンドシェルフの背景<br />-見るまたは選択されていないドキュメントウィンドウタブの背景とドキュメントの境界線 (開いているタブと仮のタブの両方)<br />-見るツールウィンドウのタイトルバーの背景<br />-ツールウィンドウタブの背景 (選択されているか選択されていません) |
| WindowFrame | -IDE の境界線 |
| WindowText | -[自動的に隠す] タブの前景<br />-選択したツールウィンドウタブの前景<br />-見るドキュメントウィンドウのタブと見るまたは選択されていない一時的なタブの前景<br />-ツリービューの既定の前景と選択されていないグリフにマウスポインターを合わせる<br />-ツールウィンドウの選択したタブの枠線<br />-スクロールバーのつまみの背景、罫線、およびグリフ |

## <a name="exposing-colors-for-end-users"></a><a name="BKMK_ExposingColorsForEndUsers"></a> 公開 (エンドユーザーの色を)

### <a name="overview"></a>概要

場合によっては、コードエディターやデザインサーフェイスを作成するときのように、エンドユーザーが UI をカスタマイズできるようにする必要があります。 これを行う最も一般的な方法は、[ツール] [ ** &gt; オプション** ] ダイアログを使用することです。 特別な制御を必要とする高度に特殊化された UI がない限り、カスタマイズを表示する最も簡単な方法は、ダイアログの [**環境**] セクション内の [**フォントおよび色**] ページを使用することです。 カスタマイズのために公開する要素ごとに、ユーザーは前景色、背景色、またはその両方を変更することができます。

### <a name="building-a-vspackage-for-your-customizable-colors"></a>カスタマイズ可能な色のための VSPackage の構築

VSPackage は、カスタムカテゴリを使用してフォントや色を制御したり、[フォントおよび色] プロパティページで項目を表示したりできます。 このメカニズムを使用する場合、Vspackage は [IVsFontAndColorDefaultsProvider](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider) インターフェイスとそれに関連するインターフェイスを実装する必要があります。

原則として、このメカニズムを使用して、既存のすべての表示項目とそれらを含むカテゴリを変更できます。 ただし、テキストエディターのカテゴリまたはその表示項目の変更には使用しないでください。 [テキストエディター] カテゴリの詳細については、「 [フォントおよび色の概要](../../vs-2015/extensibility/font-and-color-overview.md?view=vs-2015)」を参照してください。

カスタムカテゴリまたは表示項目を実装するには、VSPackage が次の条件を満たす必要があります。

- **レジストリでカテゴリを作成または識別します。** IDE の [ **フォントおよび色** ] プロパティページの実装では、この情報を使用して、特定のカテゴリをサポートするサービスを正しく照会します。

- **レジストリでグループを作成または指定します (省略可能)。** 2つ以上のカテゴリの和集合を表すグループを定義すると便利な場合があります。 グループが定義されている場合、IDE はサブカテゴリを自動的にマージし、グループ内の表示項目を配布します。

- **IDE サポートを実装します。**

- **フォントと色の変更を処理します。**

#### <a name="to-create-or-identify-categories"></a>カテゴリを作成または識別するには

の下に特別な種類のカテゴリレジストリエントリを構築し `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]` `<Category>` ます。は、カテゴリのローカライズされていない名前です。

次の2つの値を使用してレジストリを設定します。

| 名前 | 種類 | Data | 説明 |
| --- | --- | --- | --- |
| カテゴリ | REG_SZ | GUID | カテゴリを識別するために作成された GUID |
| Package | REG_SZ | GUID | カテゴリをサポートする VSPackage サービスの GUID |

 レジストリに指定されたサービスは、対応するカテゴリの [Ivsfontandcolordefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) の実装を提供する必要があります。

#### <a name="to-create-or-identify-groups"></a>グループを作成または識別するには

の下に特別な種類のカテゴリレジストリエントリを構築 `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]` `<group>` します。はグループのローカライズされていない名前です。

次の2つの値を使用してレジストリを設定します。

| 名前 | 種類 | Data | 説明 |
|--- | --- | --- | --- |
| カテゴリ | REG_SZ | GUID | カテゴリを識別するために作成された GUID |
| Package | REG_SZ | GUID | カテゴリをサポートする VSPackage サービスの GUID |

レジストリに指定されたサービスは、対応するグループのの実装を提供する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> ます。

![IVsFontAndColorGroup の実装](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304-a_FontAndColorGroup")<br />`IVsFontAndColorGroup` の実装

### <a name="to-implement-ide-support"></a>IDE サポートを実装するには

[GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject)を実装します。これにより、指定されたカテゴリまたはグループ GUID ごとに[Ivsfontandcolordefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)インターフェイスまたは <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> IDE へのインターフェイスのいずれかが返されます。

サポートされているすべてのカテゴリに対して、VSPackage は [Ivsfontandcolordefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) インターフェイスの個別のインスタンスを実装します。

[Ivsfontandcolordefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)を使用して実装されたメソッドは、IDE に次のものを提供する必要があります。

- カテゴリ内の表示項目の一覧

- 表示項目のローカライズ可能な名前

- カテゴリの各メンバーの情報を表示する

> [!NOTE]
> すべてのカテゴリには、少なくとも1つの表示項目を含める必要があります。

IDE では、インターフェイスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> 複数のカテゴリの和集合を定義します。

この実装では、IDE を次のように提供します。

- 特定のグループを構成するカテゴリの一覧

- グループ内の各カテゴリをサポートしている [Ivsfontandcolordefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) のインスタンスへのアクセス

- ローカライズ可能なグループ名

#### <a name="updating-the-ide"></a>IDE の更新

IDE では、フォントおよび色の設定に関する情報がキャッシュされます。 そのため、IDE のフォントと色の構成を変更した後は、キャッシュが最新であることを確認することをお勧めします。

キャッシュの更新は [Ivsfontandcolorcachemanager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) インターフェイスを介して行われ、グローバルに、または選択した項目でのみ実行できます。

### <a name="handling-font-and-color-changes"></a>フォントと色の変更の処理

VSPackage によって表示されるテキストの色付けを適切にサポートするには、VSPackage をサポートする色付けサービスが、[フォントおよび色] プロパティページでユーザーが開始した変更に応答する必要があります。

これを行うには、VSPackage で次の操作を行う必要があります。

- [Ivsfontandcolorevents](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents)インターフェイスを実装して、 **IDE によって生成されたイベントを処理**します。 IDE は、[フォントおよび色] ページをユーザーが変更した後、適切なメソッドを呼び出します。 たとえば、新しいフォントが選択されている場合、 [Onfontchanged](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged) メソッドを呼び出します。

  **OR**

- **変更については、IDE をポーリング**します。 これは、システムによって実装された [Ivsfontandcolorstorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) インターフェイスを使用して実行できます。 主に永続化のサポートのために、 [GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem) メソッドは表示項目のフォントと色の情報を取得できます。 フォントと色の設定の詳細については、MSDN の記事「格納されている [フォントと色の設定にアクセス](../../vs-2015/extensibility/accessing-stored-font-and-color-settings.md?view=vs-2015)する」を参照してください。

> [!NOTE]
> ポーリング結果が正しいことを確認するには、 [Ivsfontandcolorcachemanager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) インターフェイスを使用して、 [Ivsfontandcolorcachemanager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) インターフェイスの取得メソッドを呼び出す前に、キャッシュフラッシュと更新が必要かどうかを判断します。

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>インターフェイスを実装せずにカスタムフォントおよびカラーカテゴリを登録する

次のコード例は、インターフェイスを実装せずにカスタムフォントおよびカラーカテゴリを登録する方法を示しています。

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"

    "NameID"=dword:00000064
```

このコード例では、次のようになります。

- `"NameID"` = パッケージ内のローカライズされたカテゴリ名のリソース ID
- `"ToolWindowPackage"` = パッケージ GUID
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"` は一例であり、実際の値は、実装者が提供する新しい GUID にすることができます。

### <a name="set-the-font-and-color-property-category-guid"></a>フォントと色のプロパティカテゴリ GUID を設定する

次のコード例は、カテゴリ Guid の設定を示しています。

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