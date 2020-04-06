---
title: DPI 問題への対処 2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 80f16c5b17a41d1f95b9bcb70e90eb8de46ad69d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740106"
---
# <a name="address-dpi-issues"></a>DPI の問題に対処する
「高解像度」画面で出荷されるデバイスが増えています。 これらの画面は、通常、1 インチあたり 200 ピクセル (ppi) を超えています。 これらのコンピュータでアプリケーションを操作するには、デバイスの通常の表示距離でコンテンツを表示するニーズを満たすために、コンテンツをスケールアップする必要があります。 2014 年現在、高密度ディスプレイの主なターゲットはモバイル コンピューティング デバイス (タブレット、クラムシェル ラップトップ、および電話) です。

Windows 8.1 以降には、これらのマシンがディスプレイと、高密度ディスプレイと標準密度ディスプレイの両方に同時に接続されている環境で動作する機能がいくつか含まれています。

- Windows では、"テキストやその他の項目を大きくまたは小さくする" 設定 (Windows XP 以降で利用可能) を使用して、コンテンツをデバイスに合わせてスケーリングできます。

- Windows 8.1 以降では、ピクセル密度の異なるディスプレイ間を移動すると、ほとんどのアプリケーションでコンテンツが一貫性を保つように自動的にスケーリングされます。 プライマリ ディスプレイが高密度 (200% スケーリング) で、セカンダリ ディスプレイが標準密度 (100%) の場合、Windows はセカンダリ ディスプレイ上でアプリケーション ウィンドウの内容を自動的に縮小します (アプリケーションによってレンダリングされる 4 ピクセルごとに 1 ピクセル表示されます)。

- Windows は、ディスプレイのピクセル密度と表示距離に対して、既定で適切なスケーリングを行います (Windows 7 以上の OEM が構成可能)。

- Windows では、280 ppi を超える新しいデバイスでコンテンツを 250% まで自動的に拡大できます (Windows 8.1 S14 の時点)。

  Windows には、増加したピクセル数を利用する UI のスケール アップを処理する方法があります。 アプリケーションは、それ自体を「システム DPI 認識」と宣言することによって、このシステムにオプトインします。 これを行わないアプリケーションは、システムによってスケールアップされます。 これにより、アプリケーション全体が均一にピクセルストレッチされる「ファジー」ユーザーエクスペリエンスが生じる可能性があります。 次に例を示します。

  ![DPI 問題 (ファジー)](../extensibility/media/dpi-issues-fuzzy.png "DPI 問題 (ファジー)")

  Visual Studio は DPI スケーリングを認識することを選択しているため、「仮想化」されません。

  Windows (および Visual Studio) では、システムによって設定されたスケーリング要因に対処する方法が異なる、いくつかの UI テクノロジが利用されます。 次に例を示します。

- WPF は、デバイスに依存しない方法 (ピクセルではなく単位) でコントロールを測定します。 WPF UI は、現在の DPI に合わせて自動的にスケールアップします。

- UI フレームワークに関係なく、すべてのテキスト サイズはポイントで表され、DPI 非依存としてシステムによって扱われます。 Win32、WinForms、および WPF のテキストは、表示デバイスに描画されると、既に正しくスケールアップされています。

- Win32/WinForms ダイアログボックスとウィンドウには、テキストでサイズ変更するレイアウトを有効にする手段があります (グリッド、フロー、テーブルレイアウトパネルなど)。 これらのオプションを使用すると、フォント サイズが大きくなると拡大されない、ハードコードされたピクセル位置を回避できます。

- システムメトリックに基づいてシステムまたはリソースによって提供されるアイコン (SM_CXICONやSM_CXSMICONなど) は、すでにスケールアップされています。

## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>古い Win32 (GDI、GDI+) および WinForms ベースの UI
WPF は既に DPI を認識していますが、Win32/GDI ベースのコードの多くは、もともと DPI 認識を念頭に置いて記述されていませんでした。 Windows は DPI スケーリング API を提供しています。 Win32 の問題を修正する場合は、製品全体でこれらを一貫して使用する必要があります。 Visual Studio には、機能の重複を回避し、製品全体の一貫性を確保するためのヘルパー クラス ライブラリが用意されています。

## <a name="high-resolution-images"></a>高解像度の画像
このセクションは、主に Visual Studio 2013 を拡張する開発者向けです。 Visual Studio 2015 の場合は、Visual Studio に組み込まれているイメージ サービスを使用します。 また、Visual Studio の多くのバージョンをサポート/対象とする必要があるため、2015 年のイメージ サービスの使用は、以前のバージョンには存在しないため、オプションではありません。 このセクションは、その後、あなたのためです。

## <a name="scaling-up-images-that-are-too-small"></a>小さすぎる画像のスケールアップ
小さすぎるイメージは、一般的なメソッドを使用して GDI および WPF でスケールアップおよびレンダリングできます。 マネージ DPI ヘルパー クラスは、スケーリング アイコン、ビットマップ、イメージトリップ、およびイメージリストに対応するために、内部および外部の Visual Studio インテグレーターで使用できます。 Win32 ベースのネイティブ C/C++ヘルパーは、HICON、HBITMAP、ヒマージュリスト、および VsUI::GdiplusImage のスケーリングに使用できます。 ビットマップのスケーリングは、通常、ヘルパー ライブラリへの参照を含めた後、1 行の変更のみが必要です。 次に例を示します。

```cpp
(Unmanaged) VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);
```

```csharp
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);
```

イメージリストのスケーリングは、イメージリストがロード時に完了したか、実行時に追加されるかによって異なります。 読み込み時に完了`LogicalToDeviceUnits()`した場合は、ビットマップと同じイメージリストを使用して呼び出します。 イメージリストを作成する前に、コードで個々のビットマップを読み込む必要がある場合は、イメージリストのイメージサイズを必ず拡大縮小してください。

```csharp
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);
```

ネイティブ コードでは、イメージリストを作成するときに次のように寸法をスケーリングできます。

```cpp
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);
```

ライブラリ内の関数では、サイズ変更アルゴリズムを指定できます。 イメージリストに配置するイメージをスケーリングする場合は、透過性に使用する背景色を指定するか、NearestNeighbor の拡大縮小 (125% と 150% で歪みが発生します) を使用してください。

MSDN<xref:Microsoft.VisualStudio.PlatformUI.DpiHelper>のドキュメントを参照してください。

次の表は、対応する DPI スケーリング係数で画像をスケーリングする方法の例を示しています。 オレンジ色で説明した画像は、Visual Studio 2013 (100%-200% DPI スケーリング) のベスト プラクティスを示しています。

![DPI 問題 (スケーリング)](../extensibility/media/dpi-issues-scaling.png "DPI 問題 (スケーリング)")

## <a name="layout-issues"></a>レイアウトの問題
レイアウトの一般的な問題は、絶対位置 (特にピクセル単位) を使用するのではなく、UI のポイントを互いにスケーリングし、相対的に保つことによって、主に回避できます。 次に例を示します。

- レイアウト/テキストの位置は、スケールアップされた画像を考慮して調整する必要があります。

- グリッド内の列は、スケールアップされたテキストの幅を調整する必要があります。

- ハードコーディングされたサイズや要素間のスペースもスケールアップする必要があります。 フォントは自動的に拡大されるため、テキストサイズのみに基づくサイズは通常は問題ありません。

  ヘルパー関数は、X<xref:Microsoft.VisualStudio.PlatformUI.DpiHelper>軸と Y 軸でのスケーリングを許可するクラスで使用できます。

- 論理デバイスユニットX/論理デバイスユニットY(関数はX/Y軸のスケーリングを可能にする)

- イントスペース = Dpiヘルパー.論理デバイスユニットX (10);

- イントの高さ = vsUI::Dpi ヘルパー::論理デバイスユニットY(5);

  Rect、Point、サイズなどのスケーリングオブジェクトを許可する LogicalToDeviceUnits オーバーロードがあります。

## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>DPIHelper ライブラリ/クラスを使用したイメージとレイアウトの拡大縮小
Visual Studio DPI ヘルパー ライブラリは、ネイティブフォームとマネージ フォームで使用でき、他のアプリケーションで Visual Studio シェルの外部で使用できます。

ライブラリを使用するには[、Visual Studio VSSDK の機能拡張サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)に移動し、DPI_Images_Iconsのサンプルを複製します。

ソース ファイルには *、VsUIDpiHelper.h*を含め、クラス`VsUI::DpiHelper`の静的関数を呼び出します。

```cpp
#include "VsUIDpiHelper.h"

int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);

```

> [!NOTE]
> モジュール レベルまたはクラス レベルの静的変数では、ヘルパー関数を使用しないでください。 また、このライブラリはスレッド同期に静的を使用するため、順序初期化の問題が発生する可能性があります。 これらの静的変数を非静的メンバー変数に変換するか、関数にラップします (最初のアクセス時に構築されます)。

Visual Studio 環境内で実行されるマネージ コードから DPI ヘルパー関数にアクセスするには、次の手順を実行します。

- 使用するプロジェクトは、シェル MPF の最新バージョンを参照する必要があります。 次に例を示します。

    ```csharp
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />
    ```

- プロジェクトに**System.Windows.Forms**、**プレゼンテーションコア**、および**プレゼンテーション UI**への参照があることを確認します。

- コードでは **、名前空間を**使用し、DpiHelper クラスの静的関数を呼び出します。 サポートされている型 (ポイント、サイズ、四角形など) の場合、新しいスケーリングされたオブジェクトを返す拡張関数が用意されています。 次に例を示します。

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();
    DpiHelper.LogicalToDeviceUnits(ref bitmap);

    ```

## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>拡大可能な UI での WPF イメージファジーの処理
WPF では、ビットマップは、画像や大きなスクリーンショットに適した高品質の 2 キュービック アルゴリズム (既定) を使用して、現在の DPI ズーム レベルの WPF によって自動的にサイズ変更されますが、認識されるファジーを導入するため、メニュー項目のアイコンには不適切です。

推奨事項:

- ロゴ画像とバナーアートワークの場合、デフォルト<xref:System.Windows.Media.BitmapScalingMode>のサイズ変更モードを使用できます。

- メニュー項目と図像画像の場合、<xref:System.Windows.Media.BitmapScalingMode>他の歪みアーティファクトがファジーを排除しない場合は、(200%と300%)使用する必要があります。

- 大きなズーム レベルが 100% の倍数ではない (たとえば、250% または 350%) 場合、バイキュービックで図像画像をスケーリングすると、あいまいで洗い流された UI が生成されます。 より良い結果は、最初にNearestNeighborを使用して100%の最大倍数(たとえば、200%または300%)に画像をスケーリングすることによって得られますそこからバイキュービックでスケーリングします。 詳細については、「特殊なケース: 大きな DPI レベルの WPF イメージをプリスケーリングする」を参照してください。

  名前空間の DpiHelper クラスは、バインディングに使用できるメンバー<xref:System.Windows.Media.BitmapScalingMode>を提供します。 これにより、DPI スケーリング係数に応じて、Visual Studio シェルが製品全体でビットマップスケーリングモードを一様に制御できるようになります。

  XAML で使用するには、次の項目を追加します。

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"

<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />

```

Visual Studio シェルは、トップレベルウィンドウとダイアログにこのプロパティを既に設定しています。 Visual Studio で実行されている WPF ベースの UI は既に継承されます。 設定が特定の UI に反映されない場合は、XAML/WPF UI のルート要素に設定できます。 この状況は、ポップアップ、Win32 の親要素、Blend などのプロセスが不足しているデザイナー ウィンドウなどです。

一部の UI は、Visual Studio テキスト エディターや WPF ベースのデザイナー (WPF デスクトップおよび Windows ストア) など、システム設定の DPI ズーム レベルとは別にスケールできます。 このような場合は、DpiHelper.BitmapScaling モードを使用しないでください。 エディターでこの問題を解決するために、IDE チームは RenderOptions.BitmapScalingMode というカスタム プロパティを作成しました。 システムと UI のズーム レベルを組み合わせた値に応じて、そのプロパティ値を [高画質] または [最も近い近傍] に設定します。

## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特殊なケース: 大きな DPI レベルの WPF イメージをプリスケーリングする
100% の倍数ではない非常に大きなズーム レベル (たとえば、250%、350%など) の場合、二次的な図像をスケーリングすると、あいまいで洗い流された UI が生成されます。 鮮明なテキストと一緒にこれらの画像の印象は、錯視の感じです。 画像は、テキストに対して目に近づき、焦点が合っていないように見えます。 この拡大サイズのスケーリング結果は、最初にNearestNeighborで画像を100%の最大倍数(たとえば、200%または300%)にスケーリングすることで改善できます。残り (追加の 50%) に二次的にスケーリングします。

次に示す結果の違いの例では、最初の画像は改良された倍精度アルゴリズムで100%->200%->250%、2番目の画像は250%>250%です。

![DPI はダブル スケーリングの例を発行します。](../extensibility/media/dpi-issues-double-scaling-example.png "DPI はダブル スケーリングの例を発行します。")

UI でこの倍精度浮動小数点数を使用できるようにするには、各 Image 要素を表示するための XAML マークアップを変更する必要があります。 次の例では、DpiHelper ライブラリと Shell.12/14 を使用して Visual Studio で WPF でダブルスケーリングを使用する方法を示します。

手順 1: NearestNeighbor を使用して、画像を 200%、300%に事前に調整します。

バインディングに適用されたコンバーターまたは XAML マークアップ拡張機能を使用してイメージを事前にスケーリングします。 次に例を示します。

```xaml
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />

<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />

<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />

```

イメージをテーマにする必要がある場合 (ほとんどが、すべてではない場合は、必要があります)、マークアップは、最初にイメージをテーマにしてから、事前スケーリングを行う別のコンバーターを使用できます。 マークアップは、目的の<xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter>変換<xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter>出力に応じて、 または を使用できます。

```xaml
<vsui:DpiPrescaleThemedImageSourceConverter x:Key="DpiPrescaleThemedImageSourceConverter" />

<Image Width="16" Height="16">
  <Image.Source>
    <MultiBinding Converter="{StaticResource DpiPrescaleThemedImageSourceConverter}">
      <Binding Path="Icon" />
      <Binding Path="(vsui:ImageThemingUtilities.ImageBackgroundColor)"
               RelativeSource="{RelativeSource Self}" />
      <Binding Source="{x:Static vsui:Boxes.BooleanTrue}" />
    </MultiBinding>
  </Image.Source>
</Image>
```

ステップ 2: 最終サイズが現在の DPI に対して正しいことを確認します。

WPF は、UIElement に設定された BitmapScalingMode プロパティを使用して現在の DPI の UI をスケーリングするため、プリスケーリングされたイメージをソースとして使用する Image コントロールは、必要な 2 ~ 3 倍の大きさになります。 この効果に対抗する方法を次に示します。

- 元のイメージのサイズが 100% である場合は、Image コントロールの正確なサイズを指定できます。 これらのサイズは、スケーリングが適用される前の UI のサイズを反映します。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />
    ```

- 元のイメージのサイズが不明な場合は、LayoutTransform を使用して最終的な Image オブジェクトを縮小できます。 次に例を示します。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >
        <Image.LayoutTransform>
            <ScaleTransform
                ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"
                ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />
        </Image.LayoutTransform>
    </Image>
    ```

## <a name="enabling-hdpi-support-to-the-weboc"></a>WebOC への HDPI サポートの有効化
既定では、WebOC コントロール (WPF の WebBrowser コントロールや IWebBrowser2 インターフェイスなど) は、HDPI の検出とサポートを有効にしません。 結果として、高解像度ディスプレイでは小さすぎる表示コンテンツを含む埋め込みコントロールが作成されます。 以下では、特定の WebOC インスタンスで高 DPI サポートを有効にする方法について説明します。

インターフェイスを実装します (次の MSDN の記事を[参照してください](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85))。

```idl
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("BD3F23C0-D43E-11CF-893B-00AA00BDCE1A")]
public interface IDocHostUIHandler
{
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowContextMenu(
        [In, MarshalAs(UnmanagedType.U4)] int dwID,
        [In] POINT pt,
        [In, MarshalAs(UnmanagedType.Interface)] object pcmdtReserved,
        [In, MarshalAs(UnmanagedType.IDispatch)] object pdispReserved);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetHostInfo([In, Out] DOCHOSTUIINFO info);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowUI(
        [In, MarshalAs(UnmanagedType.I4)] int dwID,
        [In, MarshalAs(UnmanagedType.Interface)] object activeObject,
        [In, MarshalAs(UnmanagedType.Interface)] object commandTarget,
        [In, MarshalAs(UnmanagedType.Interface)] object frame,
        [In, MarshalAs(UnmanagedType.Interface)] object doc);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int HideUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int UpdateUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int EnableModeless([In, MarshalAs(UnmanagedType.Bool)] bool fEnable);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnDocWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnFrameWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ResizeBorder(
        [In] COMRECT rect,
        [In, MarshalAs(UnmanagedType.Interface)] object doc,
        bool fFrameWindow);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateAccelerator(
        [In] ref MSG msg,
        [In] ref Guid group,
        [In, MarshalAs(UnmanagedType.I4)] int nCmdID);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetOptionKeyPath(
        [Out, MarshalAs(UnmanagedType.LPArray)] string[] pbstrKey,
        [In, MarshalAs(UnmanagedType.U4)] int dw);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetDropTarget(
        [In, MarshalAs(UnmanagedType.Interface)] IOleDropTarget pDropTarget,
        [MarshalAs(UnmanagedType.Interface)] out IOleDropTarget ppDropTarget);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetExternal([MarshalAs(UnmanagedType.IDispatch)] out object ppDispatch);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateUrl(
        [In, MarshalAs(UnmanagedType.U4)] int dwTranslate,
        [In, MarshalAs(UnmanagedType.LPWStr)] string strURLIn,
        [MarshalAs(UnmanagedType.LPWStr)] out string pstrURLOut);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int FilterDataObject(
        IDataObject pDO,
        out IDataObject ppDORet);
    }
```

必要に応じて、ICustomDoc インターフェイスを実装します[(ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85))に関する MSDN の記事を参照してください。

```idl
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler(IDocHostUIHandler pUIHandler);
}
```

IDocHostUIHandler を実装するクラスを WebOC のドキュメントに関連付けます。 上記の ICustomDoc インターフェイスを実装した場合は、WebOC のドキュメント プロパティが有効になるとすぐに、それを ICustomDoc にキャストし、メソッドを呼び出して、IDocHostUIHandler を実装するクラスを渡します。

```csharp
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;
customDoc.SetUIHandler(this);

```

ICustomDoc インターフェイスを実装していない場合は、WebOC のドキュメント プロパティが有効になるとすぐに、IOleObject にキャストし、メソッドを`SetClientSite`呼び出して、IDocHostUIHandler を実装するクラスを渡す必要があります。 メソッド呼び出しに渡される DOCHOSTUIINFO`GetHostInfo`にDOCHOSTUIFLAG_DPI_AWAREフラグを設定します。

```csharp
public int GetHostInfo(DOCHOSTUIINFO info)
{
    // This is what the default site provides.
    info.dwFlags = (DOCHOSTUIFLAG)0x5a74012;
    // Add the DPI flag to the defaults
    info.dwFlags |=.DOCHOSTUIFLAG.DOCHOSTUIFLAG_DPI_AWARE;
    return S_OK;
}
```

HpDI をサポートするために WebOC コントロールを取得するために必要なのはこれです。

## <a name="tips"></a>ヒント

1. WebOC コントロールのドキュメント プロパティが変更された場合は、ドキュメントを IDocHostUIHandler クラスに再関連付ける必要があります。

2. 上記がうまくいかない場合は、WebOC が DPI フラグへの変更を取り込まないという既知の問題があります。 この問題を解決する最も信頼性の高い方法は、WebOC の光学ズームを切り替える方法です。 さらに、この回避策が必要な場合は、すべての navigate 呼び出しで実行する必要があります。

    ```csharp
    // browser2 is a SHDocVw.IWebBrowser2 in this case
    // EX: Call the Exec twice with DPI%-1 and then DPI% as the zoomPercent values
    IOleCommandTarget cmdTarget = browser2.Document as IOleCommandTarget;
    if (cmdTarget != null)
    {
        object commandInput = zoomPercent;
        cmdTarget.Exec(IntPtr.Zero,
                       OLECMDID_OPTICAL_ZOOM,
                       OLECMDEXECOPT_DONTPROMPTUSER,
                       ref commandInput,
                       ref commandOutput);
    }
    ```
