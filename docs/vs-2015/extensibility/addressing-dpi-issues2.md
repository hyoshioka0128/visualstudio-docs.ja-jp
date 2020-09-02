---
title: 対応する DPI Issues2 |Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9b8bc5963ba9263d72800cc473cfa56324884ace
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65699264"
---
# <a name="addressing-dpi-issues"></a>DPI 問題への対応
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

"高解像度" の画面で出荷されるデバイスの数が増えています。 これらの画面は、通常、200ピクセル/インチ (ppi) を超えています。 これらのコンピューターでアプリケーションを使用する場合、コンテンツを表示するための要件を満たすために、デバイスの通常の表示距離でコンテンツを拡大する必要があります。 2014のうち、高密度ディスプレイのプライマリターゲットは、モバイルコンピューティングデバイス (タブレット、clamshell ラップトップ、および携帯電話) です。  
  
 Windows 8.1 以降では、これらのマシンがディスプレイと環境で動作するようにするための機能がいくつか用意されています。これらのマシンは、高密度と標準密度の両方のディスプレイに接続されています。  
  
- Windows では、[テキストとその他の項目のサイズを変更する] 設定 (Windows XP 以降で使用可能) を使用して、デバイスにコンテンツをスケーリングできます。  
  
- Windows 8.1 以降では、ほとんどのアプリケーションのコンテンツが自動的に拡張され、異なるピクセル密度のディスプレイ間を移動したときに一貫性が保たれます。 プライマリディスプレイが高密度 (200% scaling) で、2番目のディスプレイが標準密度 (100%) の場合、Windows は、アプリケーションウィンドウのコンテンツを2番目のディスプレイに自動的にスケールします (アプリケーションによって表示される4ピクセルごとに1ピクセルが表示されます)。  
  
- Windows では、ピクセル密度とディスプレイ距離 (Windows 7 以降、OEM が構成可能) に対する適切なスケーリングが既定で設定されます。  
  
- Windows では、280 ppi (Windows 8.1 S14) を超える新しいデバイスで、最大250% のコンテンツを自動的にスケールできます。  
  
  Windows では、ピクセル数の増加を活用するために、UI のスケールアップを処理することができます。 アプリケーションは、それ自体を "システム DPI 対応" と宣言することで、このシステムを認識します。 この処理を行わないアプリケーションは、システムによってスケールアップされます。 これにより、アプリケーション全体が幅が均等に伸縮される "あいまいな" ユーザーエクスペリエンスが発生する可能性があります。 次に例を示します。  
  
  ![DPI 問題 (ファジー)](../extensibility/media/dpi-issues-fuzzy.png "DPI 問題 (ファジー)")  
  
  Visual Studio では、DPI スケール対応になっているため、"仮想化" されません。  
  
  Windows (および Visual Studio) は、複数の UI テクノロジを利用しています。これには、システムによって設定されたスケールファクターを処理するさまざまな方法があります。 次に例を示します。  
  
- WPF は、デバイスに依存しない方法 (ピクセルではなく単位) でコントロールを測定します。 WPF UI は、現在の DPI に合わせて自動的にスケールアップします。  
  
- UI フレームワークに関係なく、すべてのテキストサイズはポイント単位で表現されるため、システムによって DPI に依存しないものとして扱われます。 Win32、WinForms、WPF のテキストは、ディスプレイデバイスに描画するときに、既に適切にスケールアップされています。  
  
- Win32/WinForms のダイアログとウィンドウには、グリッド、フロー、テーブルのレイアウトパネルなど、テキストでサイズを変更するレイアウトを有効にする手段があります。 これにより、フォントサイズの増加に合わせてスケーリングされない、ハードコーディングされたピクセル位置を回避できます。  
  
- システムメトリックに基づいてシステムまたはリソースによって提供されるアイコン (SM_CXICON や SM_CXSMICON など) は、既にスケールアップされています。  
  
## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>以前の Win32 (GDI、GDI +) と WinForms ベースの UI  
 WPF は既に高 DPI 対応ですが、Win32/GDI ベースのコードの多くは、最初は DPI 認識を考慮して記述されていませんでした。 Windows には、DPI スケーリング Api が用意されています。 Win32 の問題の修正プログラムは、これらの製品全体で一貫して使用する必要があります。 Visual Studio には、機能の複製を回避し、製品全体の一貫性を確保するためのヘルパークラスライブラリが用意されています。  
  
## <a name="high-resolution-images"></a>高解像度のイメージ  
 このセクションは、主に Visual Studio 2013 を拡張する開発者を対象としています。 Visual Studio 2015 では、Visual Studio に組み込まれているイメージサービスを使用します。 また、Visual Studio の多くのバージョンをサポート/対象とする必要があるため、2015でイメージサービスを使用することは、以前のバージョンには存在しないため、選択肢ではありません。 ここでも、このセクションについて説明します。  
  
## <a name="scaling-up-images-that-are-too-small"></a>スケールアップイメージが小さすぎる  
 小さすぎるイメージは、いくつかの一般的な方法を使用して "スケールアップ" し、GDI と WPF でレンダリングできます。 マネージ DPI ヘルパークラスは、拡大/縮小アイコン、ビットマップ、imagestrips、および imagelists に対応するために、内部および外部の Visual Studio インテグレーターが使用できます。 Win32 ベースのネイティブ C/C + + ヘルパーは、HICON、HBITMAP、HIMAGELIST、組み込み vsui:: GdiplusImage のスケーリングに使用できます。 通常、ビットマップのスケーリングでは、ヘルパーライブラリへの参照を含めた後に1行の変更が必要になります。 次に例を示します。  
  
```cpp  
(Unmanaged)  VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);  
```  
  
```csharp  
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);  
```  
  
 Imagelist のスケーリングは、imagelist が読み込み時に完了したか、実行時に追加されたかによって異なります。 読み込み時に完了した場合は、ビットマップの場合と同じように、imagelist を使用して LogicalToDeviceUnits () を呼び出します。 Imagelist を作成する前に、コードで個々のビットマップを読み込む必要がある場合は、imagelist のイメージサイズを必ず拡大してください。  
  
```csharp  
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);  
```  
  
 ネイティブコードでは、次のように、imagelist を作成するときにディメンションをスケーリングできます。  
  
```cpp  
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);  
```  
  
 ライブラリ内の関数を使用すると、サイズ変更アルゴリズムを指定できます。 Imagelists に配置されるようにイメージをスケーリングする場合は、透明度に使用する背景色を指定します。または、NearestNeighbor スケーリングを使用します (これにより、125% と150%) でゆがみが発生します)。  
  
 MSDN のドキュメントを参照してください <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> 。  
  
 次の表は、対応する DPI スケールファクターでイメージをスケーリングする方法の例を示しています。 緑の画像は、Visual Studio 2013 (100%-200% DPI スケーリング) のようなベストプラクティスを示しています。  
  
 ![DPI 問題 (スケーリング)](../extensibility/media/dpi-issues-scaling.png "DPI 問題 (スケーリング)")  
  
## <a name="layout-issues"></a>レイアウトの問題  
 一般的なレイアウトの問題を回避するには、主に絶対位置 (ピクセル単位) を使用するのではなく、UI 内のポイントをスケーリングして相対的に調整します。 次に例を示します。  
  
- レイアウト/テキストの位置を調整して、スケールアップされたイメージを考慮する必要があります。  
  
- グリッド内の列には、スケールアップされたテキストの幅を調整する必要があります。  
  
- ハードコーディングされたサイズまたは要素間のスペースもスケールアップする必要があります。 フォントは自動的にスケールアップされるので、テキストディメンションだけに基づくサイズは通常は問題ありません。  
  
  クラスでは、 <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> X 軸と Y 軸のスケーリングを可能にするヘルパー関数を使用できます。  
  
- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (関数は X/Y 軸でのスケーリングを可能にします)  
  
- int space = DpiHelper. LogicalToDeviceUnitsX (10);  
  
- int height = 組み込み vsui::D piHelper:: LogicalToDeviceUnitsY (5);  
  
  LogicalToDeviceUnits オーバーロードを使用すると、四角形、ポイント、サイズなどのオブジェクトのスケーリングを行うことができます。  
  
## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>DPIHelper ライブラリ/クラスを使用したイメージとレイアウトのスケーリング  
 Visual Studio DPI ヘルパーライブラリはネイティブでもマネージ形式でも使用でき、他のアプリケーションによって Visual Studio シェルの外部で使用できます。  
  
 ライブラリを使用するには、 [Visual Studio の VSSDK 拡張機能のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples) にアクセスし、高 DPI_Images_Icons サンプルを複製します。  
  
 ソースファイルで、VsUIDpiHelper .h をインクルードし、組み込み vsui::D piHelper クラスの静的関数を呼び出します。  
  
```cpp  
#include "VsUIDpiHelper.h"  
  
int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);  
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);  
  
```  
  
> [!NOTE]
> モジュールレベルまたはクラスレベルの静的変数では、ヘルパー関数を使用しないでください。 また、このライブラリはスレッドの同期にスタティックを使用するため、順序の初期化の問題が発生する可能性があります。 これらの静的変数を非静的メンバー変数に変換するか、関数にラップします (そのため、最初のアクセス時に構築されます)。  
  
 Visual Studio 環境内で実行されるマネージコードから DPI ヘルパー関数にアクセスするには、次の操作を行います。  
  
- 使用中のプロジェクトは、最新バージョンの Shell MPF を参照する必要があります。 次に例を示します。  
  
    ```csharp  
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />  
    ```  
  
- プロジェクトに、system.string、**プレゼンテーションコア**、および**プレゼンテーション ui****への**参照があることを確認します。  
  
- コードでは、 **VisualStudio** 名前空間を使用し、DpiHelper クラスの静的関数を呼び出します。 サポートされている型 (ポイント、サイズ、四角形など) については、拡張された新しいオブジェクトを返す拡張関数が用意されています。 次に例を示します。  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);  
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();  
    DpiHelper.LogicalToDeviceUnits(ref bitmap);  
  
    ```  
  
## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>Zoomable UI での WPF image fuzziness の処理  
 WPF では、高品質のバイキュービックアルゴリズム (既定値) を使用して、WPF によって現在の DPI ズームレベルのビットマップのサイズが自動的に変更されます。これは、画像や大規模なスクリーンショットに適していますが、メニュー項目アイコンには適していません。これは、fuzziness が認識されるためです  
  
 推奨事項:  
  
- ロゴ画像とバナーアートワークの場合は、既定の <xref:System.Windows.Media.BitmapScalingMode> サイズ変更モードを使用できます。  
  
- メニュー項目と iconography イメージについては、を <xref:System.Windows.Media.BitmapScalingMode> 使用して、他のひずみアーティファクトによって fuzziness が削除されないようにする必要があります (200% と300%)。  
  
- •100% の倍数ではない大規模なズームレベル (250% または350%) では、iconography イメージをバイキュービックでスケーリングすると、ファジー化された非ウォッシュアウト UI になります。 最初に NearestNeighbor を使用してイメージを100% の最大倍数 (200% や300%) にスケーリングすると、より良い結果が得られます。また、そこからのバイキュービックでスケーリングします。 詳細については、「大規模な DPI レベル用に WPF イメージを事前に確認する」を参照してください。  
  
  VisualStudio 名前空間の DpiHelper クラスは、 <xref:System.Windows.Media.BitmapScalingMode> バインディングに使用できるメンバーを提供します。 これにより、Visual Studio シェルは、DPI スケールファクターに応じて、製品全体のビットマップスケーリングモードを均一に制御できるようになります。  
  
  XAML で使用するには、次のように追加します。  
  
```xaml  
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
  
<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />  
  
```  
  
 Visual Studio シェルは、トップレベルのウィンドウとダイアログでこのプロパティを既に設定しています。 Visual Studio で実行されている WPF ベースの UI は、既にそれを継承しています。 設定が UI の特定の部分に反映されない場合は、XAML/WPF UI のルート要素に設定できます。 これが発生する場所には、ポップアップ、Win32 親を持つ要素、および Blend などのプロセスが不足しているデザイナーウィンドウがあります。  
  
 一部の UI は、Visual Studio テキストエディターや WPF ベースのデザイナー (WPF デスクトップおよび Windows ストア) など、システム設定の DPI ズームレベルとは無関係に拡張できます。 このような場合は、System.windows.media.bitmapscalingmode> を使用しないでください。 エディターでこの問題を修正するために、IDE チームは System.windows.media.bitmapscalingmode> という名前のカスタムプロパティを作成しました。 システムと UI の合計ズームレベルに応じて、そのプロパティ値を HighQuality または NearestNeighbor に設定します。  
  
## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特殊なケース: 大きな DPI レベル用に WPF イメージを事前に使用する  
 100% の倍数ではない非常に大きなズームレベル (たとえば、250%、350% など) では、iconography イメージを双三次でスケーリングすると、あいまいでウォッシュアウトされた UI になります。 これらの画像の外観は、光の錯覚とほぼ同じです。 画像は目の近くに表示され、テキストに対してフォーカスが出ません。 この拡大されたサイズでのスケーリング結果は、最初に NearestNeighbor を使用してイメージを100% の最大倍数 (200% や300%) にスケーリングすることで改善できます。また、バイキュービックを使用して、残りの部分にスケーリングします (さらに50%)。  
  
 次に、結果の違いの例を示します。最初のイメージは、改善された倍精度アルゴリズム 100%->200%->250% でスケーリングされ、2番目のイメージはバイキュービック 100%->250% でスケーリングされます。  
  
 ![DPI 問題のダブルスケーリングの例](../extensibility/media/dpi-issues-double-scaling-example.png "DPI 問題のダブルスケーリングの例")  
  
 UI でこのダブルスケールを使用できるようにするには、各イメージ要素を表示するための XAML マークアップを変更する必要があります。 次の例は、DpiHelper ライブラリとシェルを使用して、Visual Studio の WPF でダブルスケールを使用する方法を示しています。 12/14。  
  
 手順 1: Prescale を使用して、イメージを200%、300% のようにします。  
  
 バインドに適用されているコンバーターか、XAML マークアップ拡張機能を使用して、イメージを Prescale します。 次に例を示します。  
  
```xaml  
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />  
  
<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />  
  
<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />  
  
```  
  
 画像にもテーマを適用する必要がある場合 (ほとんどの場合、すべてではない場合)、マークアップでは、最初にイメージのテーマを行う別のコンバーターを使用してから、前にスケーリングを行うことができます。 マークアップは、 <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter> 目的の <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter> 変換出力に応じて、またはを使用できます。  
  
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
  
 手順 2: 現在の DPI に対して最終的なサイズが正しいことを確認します。  
  
 WPF は、UIElement で設定された System.windows.media.bitmapscalingmode> プロパティを使用して現在の DPI の UI をスケールするため、ソースとしての prescaled イメージを使用したイメージコントロールは、2 ~ 3 倍のサイズで表示されます。 この効果に対抗するためのいくつかの方法を次に示します。  
  
- 元のイメージの次元が100% であることがわかっている場合は、イメージコントロールの正確なサイズを指定できます。 これらのサイズは、スケーリングが適用される前に UI のサイズを反映します。  
  
    ```xaml  
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />  
    ```  
  
- 元のイメージのサイズが不明な場合は、LayoutTransform を使用して最終的なイメージオブジェクトをスケールダウンできます。 次に例を示します。  
  
    ```xaml  
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >  
        <Image.LayoutTransform>  
         <ScaleTransform  
             ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"  
             ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />  
        </Image.LayoutTransform>  
    </Image>  
    ```  
  
## <a name="enabling-hdpi-support-to-the-weboc"></a>WebOC の HDPI サポートを有効にする  
 既定では、WebOC コントロール (WPF の WebBrowser コントロールや IWebBrowser2 インターフェイスなど) は、HDPI の検出とサポートを有効にしません。 結果は、高解像度表示では小さすぎる表示コンテンツを含む埋め込みコントロールになります。 以下では、特定の web WebOC インスタンスで高 DPI のサポートを有効にする方法について説明します。  
  
 IDocHostUIHandler インターフェイスを実装します ( [IDocHostUIHandler](https://msdn.microsoft.com/library/aa753260.aspx) インターフェイスに関する MSDN の記事を参照してください)。  
  
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
  
 必要に応じて、ICustomDoc インターフェイスを実装します ( [ICustomDoc](https://msdn.microsoft.com/library/aa753272.aspx) インターフェイスに関する MSDN の記事を参照してください)。  
  
```idl  
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),  
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]  
public interface ICustomDoc  
{  
    void SetUIHandler(IDocHostUIHandler pUIHandler);  
}   
```  
  
 IDocHostUIHandler を実装するクラスを WebOC のドキュメントに関連付けます。 上記の ICustomDoc インターフェイスを実装した場合は、WebOC の document プロパティが有効になるとすぐに、ICustomDoc にキャストし、IDocHostUIHandler を実装するクラスを渡して SetUIHandler メソッドを呼び出します。  
  
```csharp  
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface  
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;  
customDoc.SetUIHandler(this);  
  
```  
  
 ICustomDoc インターフェイスを実装していない場合は、WebOC のドキュメントプロパティが有効になるとすぐに、IOleObject にキャストし、IDocHostUIHandler を実装するクラスを渡して SetClientSite メソッドを呼び出す必要があります。 GetHostInfo メソッドの呼び出しに渡される DOCHOSTUIINFO の DOCHOSTUIFLAG_DPI_AWARE フラグを設定します。  
  
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
  
 これは、WebOC コントロールを利用して、HPDI をサポートするために必要な操作です。  
  
## <a name="tips"></a>ヒント  
  
1. WebOC コントロールの document プロパティが変更された場合は、ドキュメントを IDocHostUIHandler クラスに再関連付けする必要がある場合があります。  
  
2. 上記の問題が解決しない場合は、WebOC が DPI フラグへの変更を選択しないという既知の問題があります。 これを解決する最も信頼性の高い方法は、WebOC の光学ズームを切り替えることです。これは、ズームの比率として2つの異なる値を持つ2つの呼び出しを意味します。 また、この回避策が必要な場合は、すべての navigate 呼び出しで実行する必要があります。  
  
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
