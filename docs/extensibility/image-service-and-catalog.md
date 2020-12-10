---
title: Image Service と Catalog |Microsoft Docs
description: この記事には、Visual Studio イメージサービスとイメージカタログを採用するためのガイダンスとベストプラクティスが記載されています。
ms.custom: SEO-VS-2020
ms.date: 04/01/2019
ms.topic: conceptual
ms.assetid: 34990c37-ae98-4140-9b1e-a91c192220d9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 41adcbe97f9d0779fbad465bac673a3f7cf086c7
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96993537"
---
# <a name="image-service-and-catalog"></a>イメージサービスとカタログ
このクックブックには、visual studio イメージサービスと Visual Studio 2015 で導入されたイメージカタログを採用するためのガイダンスとベストプラクティスが含まれています。

 Visual Studio 2015 で導入されたイメージサービスを使用すると、開発者は、表示されているコンテキストの正しいテーマを含めて、デバイスとユーザーが選択したテーマに最適なイメージを取得できます。 イメージサービスを採用すると、資産のメンテナンス、HDPI スケーリング、およびテーマに関連する主要な問題点を排除するのに役立ちます。

|**現在の問題**|**ソリューション**|
|-|-|
|背景色のブレンド|組み込みのアルファブレンド|
|テーマ (some) イメージ|テーマのメタデータ|
|ハイコントラストモード|代替ハイコントラストリソース|
|DPI モードごとに複数のリソースが必要|ベクターベースのフォールバックを使用した選択可能なリソース|
|イメージの複製|イメージごとの識別子1つの概念|

 イメージサービスを採用する理由

- 常に最新の "ピクセル完全な" イメージを Visual Studio から取得する

- 独自のイメージを送信して使用することができます。

- Windows が新しい DPI スケーリングを追加したときにイメージをテストする必要はありません

- 実装における以前のアーキテクチャの課題に対処する

  イメージサービスを使用する前と後の Visual Studio シェルツールバー:

  ![前後のイメージ サービス](../extensibility/media/image-service-before-and-after.png "前後のイメージ サービス")

## <a name="how-it-works"></a>しくみ
 イメージサービスは、サポートされているすべての UI フレームワークに適したビットマップイメージを提供できます。

- WPF: BitmapSource

- WinForms: system.string

- Win32: HBITMAP

  イメージサービスのフローダイアグラム

  ![イメージ サービスのフロー ダイアグラム](../extensibility/media/image-service-flow-diagram.png "イメージ サービスのフロー ダイアグラム")

  **イメージモニカー**

  イメージモニカー (または short のモニカー) は、イメージライブラリ内のイメージアセットまたはイメージリスト資産を一意に識別する GUID/ID のペアです。

  **既知のモニカー**

  Visual Studio イメージカタログに格納され、Visual Studio のコンポーネントまたは拡張機能によって一般に利用できるイメージモニカーのセット。

  **イメージマニフェストファイル**

  イメージマニフェスト (*imagemanifest*) ファイルは、一連のイメージアセット、それらのアセットを表すモニカー、および各資産を表す実際のイメージまたはイメージを定義する XML ファイルです。 イメージマニフェストでは、レガシ UI をサポートするために、スタンドアロンイメージまたはイメージリストを定義できます。 また、資産または各資産の背後にある個々の画像に対して設定できる属性があり、これらのアセットがどのように表示されるかや方法を変更できます。

  **イメージマニフェストスキーマ**

  イメージマニフェスト全体は次のようになります。

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Import, Guid, ID, or String elements -->
      </Symbols>
      <!-- zero or one Images elements -->
      <Images>
        <!-- zero or more Image elements -->
      </Images>
      <!-- zero or one ImageLists elements -->
      <ImageLists>
        <!-- zero or more ImageList elements -->
      </ImageLists>
</ImageManifest>
```

 **記号**

 読みやすく、保守を容易にするために、イメージマニフェストでは属性値にシンボルを使用できます。 シンボルは次のように定義されます。

```xml
<Symbols>
      <Import Manifest="manifest" />
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />
      <ID Name="cmdidSaveAll" Value="1000" />
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />
</Symbols>
```

|**サブ要素**|**定義**|
|-|-|
|[インポート]|現在のマニフェストで使用するために、指定されたマニフェストファイルのシンボルをインポートします。|
|GUID|シンボルは GUID を表し、GUID の書式設定と一致する必要があります|
|ID|シンボルは ID を表し、負でない整数である必要があります|
|String|シンボルは任意の文字列値を表します。|

 シンボルは大文字と小文字が区別され、$ (symbol-name) 構文を使用して参照されます。

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 一部のシンボルは、すべてのマニフェストに事前に定義されています。 これら \<Source> は、 \<Import> ローカルコンピューター上のパスを参照するために、要素または要素の Uri 属性で使用できます。

|**記号**|**説明**|
|-|-|
|CommonProgramFiles|% CommonProgramFiles% 環境変数の値|
|LocalAppData|% LocalAppData% 環境変数の値|
|ManifestFolder|マニフェストファイルを含むフォルダー|
|マイドキュメント]|現在のユーザーの [マイドキュメント] フォルダーの完全なパス|
|ProgramFiles|% ProgramFiles% 環境変数の値|
|システム|*Windows\System32* フォルダー|
|WinDir|% WinDir% 環境変数の値|

 **イメージ**

 要素は、 \<Image> モニカーによって参照できるイメージを定義します。 イメージモニカーを形成する GUID と ID。 イメージのモニカーは、イメージライブラリ全体で一意である必要があります。 複数のイメージに特定のモニカーが含まれている場合は、ライブラリのビルド中に最初に検出されたものが保持されます。

 少なくとも1つのソースが含まれている必要があります。 サイズに依存しないソースでは、さまざまなサイズの範囲で最適な結果が得られますが、必須ではありません。 サービスが要素で定義されていないサイズのイメージを要求され、 \<Image> サイズに依存しないソースが存在しない場合、サービスは最適なサイズ固有のソースを選択し、要求されたサイズにスケーリングします。

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|**属性**|**定義**|
|-|-|
|GUID|必要イメージモニカーの GUID 部分|
|ID|必要イメージモニカーの ID 部分|
|AllowColorInversion|[省略可能、既定値は true]画像の色を、濃色の背景で使用するときにプログラムによって反転するかどうかを示します。|

 **ソース**

 要素は、 \<Source> 単一のイメージソース資産 (XAML および PNG) を定義します。

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|**属性**|**定義**|
|-|-|
|Uri|必要イメージの読み込み元となる場所を定義する URI。 次のいずれかを指定できます。<br /><br /> -Application:///機関を使用する[パック URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf)<br />-コンポーネントの絶対リソース参照<br />-ネイティブリソースを含むファイルへのパス|
|バックグラウンド|Optionalソースの使用を想定している背景の種類を示します。<br /><br /> 次のいずれかを指定できます。<br /><br /> *ライト:* 光源は、ライトバックで使用できます。<br /><br /> *ダーク:* ソースは、ダーク背景で使用できます。<br /><br /> *Systeminformation.highcontrast:* ソースは、ハイコントラストモードの任意のバックグラウンドで使用できます。<br /><br /> *HighContrastLight:* ソースは、ハイコントラストモードのライトバックで使用できます。<br /><br /> *HighContrastDark:* ソースはハイコントラストモードでダークバックグラウンドで使用できます。<br /><br /> Background 属性が省略されている場合は、任意のバックグラウンドでソースを使用できます。<br /><br /> Background、 *Dark*、 *HighContrastLight*、または *HighContrastDark**の場合*、ソースの色は反転されません。 Background が省略されている場合、または *systeminformation.highcontrast* に設定されている場合、ソースの色の反転は、イメージの **allowcolorinversion** 属性によって制御されます。|

\<Source>要素は、次の省略可能なサブ要素のうち1つだけを持つことができます。

|**要素**|**属性 (すべて必須)**|**定義**|
|-|-|-|
|\<Size>|値|ソースは、指定されたサイズ (デバイス単位) のイメージに使用されます。 画像は正方形になります。|
|\<SizeRange>|MinSize、MaxSize|ソースは、MinSize から MaxSize (デバイスユニット単位) のイメージに使用されます。 画像は正方形になります。|
|\<Dimensions>|Width、Height|ソースは、指定された幅と高さ (デバイス単位) のイメージに使用されます。|
|\<DimensionRange>|MinWidth、Minwidth、<br /><br /> MaxWidth、Maxwidth|ソースは、幅/高さの最小値から最大幅/高さ (デバイス単位) までのイメージに使用されます。|

 要素には、省略可能なサブ要素 \<Source> を含めることもできます \<NativeResource> \<Source> 。これは、マネージアセンブリではなくネイティブアセンブリから読み込まれるを定義します。

```xml
<NativeResource Type="type" ID="int" />
```

|**属性**|**定義**|
|-|-|
|型|必要ネイティブリソースの型 (XAML または PNG)|
|ID|必要ネイティブリソースの整数の ID 部分|

 **リスト**

 要素は、 \<ImageList> 1 つのストリップで返すことができるイメージのコレクションを定義します。 ストリップは必要に応じて構築されます。

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|**属性**|**定義**|
|-|-|
|GUID|必要イメージモニカーの GUID 部分|
|ID|必要イメージモニカーの ID 部分|
|外部|[省略可能、既定値は false]イメージモニカーが現在のマニフェスト内のイメージを参照しているかどうかを示します。|

 含まれているイメージのモニカーは、現在のマニフェストで定義されているイメージを参照する必要がありません。 含まれているイメージがイメージライブラリに見つからない場合は、空白のプレースホルダーイメージが代わりに使用されます。

## <a name="using-the-image-service"></a>イメージサービスの使用

### <a name="first-steps-managed"></a>最初の手順 (管理)
 イメージサービスを使用するには、次のアセンブリの一部またはすべてへの参照をプロジェクトに追加する必要があります。

- *Microsoft.VisualStudio.ImageCatalog.dll*

  - 組み込みの image catalog **knownmonikers** を使用する場合は必須です。

- *Microsoft.VisualStudio.Imaging.dll*

  - WPF UI で **CrispImage** と **imageのユーティリティ** を使用する場合に必要です。

- *Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll*

  - **ImageMoniker** および **ImageAttributes** 型を使用する場合は必須です。

  - **EmbedInteropTypes** は true に設定する必要があります。

- *VisualStudio. 14.0. デザイン時.*

  - **IVsImageService2** 型を使用する場合は必須です。

  - **EmbedInteropTypes** は true に設定する必要があります。

- *Microsoft.VisualStudio.Utilities.dll*

  - WPF UI で **ImageBackgroundColor** の **BrushToColorConverter** を使用する場合に必要です。

- *VisualStudio. \<VSVersion> .0*

  - **は、ivsuiobject** 型を使用する場合は必須です。

- *Microsoft.VisualStudio.Shell.Interop.10.0.dll*

  - WinForms 関連の UI ヘルパーを使用する場合は必須です。

  - **EmbedInteropTypes** を true に設定する必要があります。

### <a name="first-steps-native"></a>最初の手順 (ネイティブ)
 イメージサービスを使用するには、次のヘッダーの一部またはすべてをプロジェクトに含める必要があります。

- **KnownImageIds. h**

  - 組み込みの image catalog **knownmonikers** を使用する場合は必須ですが、 **IVsHierarchy getguidproperty** または **GetProperty** 呼び出しから値を返す場合など、 **ImageMoniker** 型を使用することはできません。

- **KnownMonikers. h**

  - 組み込みの image catalog **knownmonikers** を使用する場合は必須です。

- **ImageParameters140**

  - **ImageMoniker** および **ImageAttributes** 型を使用する場合は必須です。

- **VSShell140**

  - **IVsImageService2** 型を使用する場合は必須です。

- **Imageutilities**

  - イメージサービスによるテーマの処理を許可しない場合は必須です。

  - イメージサービスがイメージのテーマを処理できる場合は、このヘッダーを使用しないでください。

::: moniker range="vs-2017"
- **VSUIDPIHelper. h**

  - DPI ヘルパーを使用して現在の DPI を取得する場合に必要です。

::: moniker-end

::: moniker range=">=vs-2019"
- **VsDpiAwareness. h**

  - DPI 認識ヘルパーを使用して現在の DPI を取得する場合に必要です。

::: moniker-end

## <a name="how-do-i-write-new-wpf-ui"></a>操作方法新しい WPF UI を作成しますか?

1. まず、上記の最初の手順セクションで必要なアセンブリ参照をプロジェクトに追加します。 これらのすべてを追加する必要はないため、必要な参照だけを追加します。 (注: を使用している場合や、**ブラシ** ではなく **色** にアクセスできる場合は、コンバーターが不要になるため、**ユーティリティ** への参照をスキップできます)。

2. 目的のイメージを選択し、そのモニカーを取得します。 **Knownmoniker** を使用するか、独自のカスタムイメージとモニカーがある場合は独自のモニカーを使用します。

3. **CrispImages** を XAML に追加します。 (以下の例を参照してください)。

4. UI 階層で **ImageBackgroundColor** プロパティを設定します。 (これは、必ずしも **CrispImage** ではなく、背景色が既知の場所に設定する必要があります)。(以下の例を参照してください)。

```xaml
<Window
  x:Class="WpfApplication.MainWindow"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:imaging="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:theming="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:utilities="clr-namespace:Microsoft.Internal.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:catalog="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.ImageCatalog"
  Title="MainWindow" Height="350" Width="525" UseLayoutRounding="True">
  <Window.Resources>
    <utilities:BrushToColorConverter x:Key="BrushToColorConverter"/>
  </Window.Resources>
  <StackPanel Background="White" VerticalAlignment="Center"
    theming:ImageThemingUtilities.ImageBackgroundColor="{Binding Background, RelativeSource={RelativeSource Self}, Converter={StaticResource BrushToColorConverter}}">
    <imaging:CrispImage Width="16" Height="16" Moniker="{x:Static catalog:KnownMonikers.MoveUp}" />
  </StackPanel>
</Window>
```

 **既存の WPF UI を更新操作方法には**

 既存の WPF UI の更新は、次の3つの基本的な手順で構成される比較的単純なプロセスです。

1. \<Image>UI 内のすべての要素を \<CrispImage> 要素に置き換えます。

2. すべてのソース属性をモニカー属性に変更します。

    - イメージが変更されず、 **Knownmonikers** を使用している場合は、そのプロパティを **knownmonikers** に静的にバインドします。 (上記の例を参照してください)。

    - イメージが変更されず、独自のカスタムイメージを使用している場合は、独自のモニカーに静的にバインドします。

    - イメージが変更可能な場合は、プロパティの変更を通知するコードプロパティにモニカー属性をバインドします。

3. UI 階層内の任意の場所で、 **ImageBackgroundColor** を設定して、色の反転が正しく機能することを確認します。

    - このためには、 **BrushToColorConverter** クラスの使用が必要になることがあります。 (上記の例を参照してください)。

## <a name="how-do-i-update-win32-ui"></a>Win32 UI 操作方法更新しますか?
 適切な場所にあるコードに次のコードを追加して、イメージの未加工の読み込みを置き換えます。 必要に応じて HBITMAPs、Hbitmaps、HBITMAPS を返す値を切り替えます。

 **イメージサービスを取得する**

```cpp
CComPtr<IVsImageService2> spImgSvc;
CGlobalServiceProvider::HrQueryService(SID_SVsImageService, &spImgSvc);
```

 **イメージの要求**

::: moniker range="vs-2017"

```cpp
ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = VsUI::DpiHelper::GetDeviceDpiX();
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

::: moniker range=">=vs-2019"

```cpp
UINT dpiX, dpiY;
HWND hwnd = // get the HWND where the image will be displayed
VsUI::CDpiAwareness::GetDpiForWindow(hwnd, &dpiX, &dpiY);

ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = dpiX;
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

## <a name="how-do-i-update-winforms-ui"></a>WinForms UI を更新操作方法ますか?
 適切な場所にあるコードに次のコードを追加して、イメージの未加工の読み込みを置き換えます。 必要に応じて、ビットマップとアイコンを返すように値を切り替えます。

 **役に立つ using ステートメント**

```csharp
using GelUtilities = Microsoft.Internal.VisualStudio.PlatformUI.Utilities;
```

 **イメージサービスを取得する**

```csharp
// This or your preferred way of querying for Visual Studio services
IVsImageService2 imageService = (IVsImageService2)Package.GetGlobalService(typeof(SVsImageService));

```

 **イメージを要求する**

::: moniker range="vs-2017"

```csharp
ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiHelper.DeviceDpiX;
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

::: moniker range=">=vs-2019"

```csharp
Control control = // get the control where the image will be displayed

ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiAwareness.GetWindowDpi(control.Handle);
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

## <a name="how-do-i-use-image-monikers-in-a-new-tool-window"></a>新しいツールウィンドウでイメージモニカーを使用操作方法には
 VSIX パッケージプロジェクトテンプレートが Visual Studio 2015 用に更新されました。 新しいツールウィンドウを作成するには、VSIX プロジェクトを右クリックし、 [  >  **新しい項目** の追加] (**Ctrl** + **Shift** + **a**) を選択します。 プロジェクト言語の [機能拡張] ノードで、[ **カスタムツールウィンドウ**] を選択し、ツールウィンドウに名前を付けて、[ **追加** ] をクリックします。

 これらは、ツールウィンドウでモニカーを使用するための重要な場所です。 それぞれの手順に従います。

1. タブが十分に小さく ( **Ctrl** + **tab** window スイッチャーでも使用される)、[ツールウィンドウ] タブ。

    **Createtoolwindow は toolwindowpane** 型から派生したクラスのコンストラクターに次の行を追加します。

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   this.BitmapImageMoniker = KnownMonikers.Blank;
   ```

2. ツールウィンドウを開くコマンド。

    パッケージの *vsct* ファイルで、ツールウィンドウのコマンドボタンを編集します。

   ```xml
   <Button guid="guidPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <!-- Replace this KnownMoniker with your desired ImageMoniker -->
     <Icon guid="ImageCatalogGuid" id="Blank" />
     <!-- Add this -->
     <CommandFlag>IconIsMoniker</CommandFlag>
     <Strings>
       <ButtonText>MyToolWindow</ButtonText>
     </Strings>
   </Button>
   ```

   **既存のツールウィンドウでイメージモニカーを使用操作方法には**

   イメージモニカーを使用するように既存のツールウィンドウを更新する方法は、新しいツールウィンドウを作成する手順と似ています。

   これらは、ツールウィンドウでモニカーを使用するための重要な場所です。 それぞれの手順に従います。

3. タブが十分に小さく ( **Ctrl** + **tab** window スイッチャーでも使用される)、[ツールウィンドウ] タブ。

   1. **Createtoolwindow は toolwindowpane** 型から派生したクラスのコンストラクターに、次の行が存在する場合は削除します。

       ```csharp
       this.BitmapResourceID = <Value>;
       this.BitmapIndex = <Value>;
       ```

   2. 「新しいツールウィンドウでイメージモニカーを使用する操作方法」の手順 #1 を参照してください。 セクションを参照してください。

4. ツールウィンドウを開くコマンド。

   - 「新しいツールウィンドウでイメージモニカーを使用する操作方法」の手順 #2 を参照してください。 セクションを参照してください。

## <a name="how-do-i-use-image-monikers-in-a-vsct-file"></a>操作方法、vsct ファイルでイメージモニカーを使用しますか。
 次のコメント行に示されているように、 *vsct* ファイルを更新します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <!--  Include the definitions for images included in the VS image catalog -->
  <Include href="KnownImageIds.vsct"/>
  <Commands package="guidMyPackage">
    <Buttons>
      <Button guid="guidMyCommandSet" id="cmdidMyCommand" priority="0x0000" type="Button">
        <!-- Add an Icon element, changing the attributes to match the image moniker you want to use.
             In this case, we're using the Guid for the VS image catalog.
             Change the id attribute to be the ID of the desired image moniker. -->
        <Icon guid="ImageCatalogGuid" id="OpenFolder" />
        <CommandFlag>DynamicVisibility</CommandFlag>
        <CommandFlag>DefaultInvisible</CommandFlag>
        <CommandFlag>DefaultDisabled</CommandFlag>
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>IconAndText</CommandFlag>
        <!-- Add the IconIsMoniker CommandFlag -->
        <CommandFlag>IconIsMoniker</CommandFlag>
        <Strings>
          <ButtonText>Quick Fixes...</ButtonText>
          <CommandName>Show Quick Fixes</CommandName>
          <CanonicalName>ShowQuickFixes</CanonicalName>
          <LocCanonicalName>ShowQuickFixes</LocCanonicalName>
        </Strings>
      </Button>
    </Buttons>
  </Commands>
  <!-- It is recommended that you remove <Bitmap> elements that are no longer used in the vsct file -->
  <Symbols>
    <GuidSymbol name="guidMyPackage"    value="{1491e936-6ffe-474e-8371-30e5920d8fdd}" />
    <GuidSymbol name="guidMyCommandSet" value="{10347de4-69a9-47f4-a950-d3301f6d2bc7}">
      <IDSymbol name="cmdidMyCommand" value="0x9437" />
    </GuidSymbol>
  </Symbols>
</CommandTable>
```

 **以前のバージョンの Visual Studio でも、vsct ファイルを読み取る必要がある場合はどうすればよいでしょうか。**

 以前のバージョンの Visual Studio では、 **Iconismoniker** コマンドフラグは認識されません。 イメージサービスのイメージは、それをサポートするバージョンの Visual Studio で使用できますが、以前のバージョンの Visual Studio では引き続き古い形式のイメージを使用できます。 これを行うには、(そのため、以前のバージョンの Visual Studio と互換性がある) *vsct* ファイルを変更せずに、 *vsct* ファイルの要素で定義されている guid と id のペアから \<Bitmaps> イメージモニカー guid/ID ペアにマップする CSV (コンマ区切り値) ファイルを作成します。

 マッピング CSV ファイルの形式は次のとおりです。

```
Icon guid, Icon id, Moniker guid, Moniker id
b714fcf7-855e-4e4c-802a-1fd87144ccad,1,fda30684-682d-421c-8be4-650a2967058e,100
b714fcf7-855e-4e4c-802a-1fd87144ccad,2,fda30684-682d-421c-8be4-650a2967058e,200
```

 CSV ファイルはパッケージと共に配置され、その場所は、**次のよう** に指定されます。

```csharp
[ProvideMenuResource("MyPackage.ctmenu", 1, IconMappingFilename="IconMappings.csv")]
```

 **Iconmappingfilename** は $PackageFolder $ (上の例のように) で暗黙的にルート化された相対パスか、または環境変数によって定義されたディレクトリ ( *@ "% UserProfile% \dir1\dir2\MyMappingFile.csv"* など) を明示的にルートとした絶対パスです。

## <a name="how-do-i-port-a-project-system"></a>プロジェクトシステムを操作方法ポート
 **プロジェクトの ImageMonikers を指定する方法**

1. プロジェクトの **IVsHierarchy** に **VSHPROPID_SupportsIconMonikers** を実装し、true を返します。

2. **VSHPROPID_IconMonikerImageList** (元のプロジェクトが **VSHPROPID_IconImgList** 使用されている場合) または **VSHPROPID_IconMonikerGuid**、 **VSHPROPID_IconMonikerId**、 **VSHPROPID_OpenFolderIconMonikerGuid**、 **VSHPROPID_OpenFolderIconMonikerId** を実装します (元のプロジェクトが **VSHPROPID_IconHandle** と **VSHPROPID_OpenFolderIconHandle** を使用していた場合)。

3. 拡張ポイントが要求した場合、アイコンの元の VSHPROPIDs の実装を変更して、アイコンの "レガシ" バージョンを作成します。 **IVsImageService2** は、これらのアイコンを取得するために必要な機能を提供します。

   **VB/C# プロジェクトフレーバーの追加要件**

   プロジェクトが **最も外側のフレーバー** であることを検出した場合にのみ、 **VSHPROPID_SupportsIconMonikers** を実装します。 そうしないと、実際には最も外側のフレーバーによってイメージモニカーがサポートされず、基本フレーバーでは、カスタマイズされたイメージを効果的に "隠す" ことができます。

   **CPS でイメージモニカーを使用操作方法には**

   CPS でのカスタムイメージの設定 (Common Project System) は、手動で行うことも、プロジェクトシステム拡張 SDK に付属する項目テンプレートを使用して行うこともできます。

   **プロジェクトシステム機能拡張 SDK の使用**

   [「プロジェクトの種類/項目の種類のカスタムアイコンを指定](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/scenario/provide_custom_icons_for_the_project_or_item_type.md)する」の手順に従って、CPS イメージをカスタマイズします。 CPS の詳細については、 [Visual Studio プロジェクトシステムの機能拡張](https://github.com/Microsoft/VSProjectSystem)に関するドキュメントを参照してください。

   **ImageMonikers を手動で使用する**

4. プロジェクトシステムに **Iprojecttreemodifier** インターフェイスを実装してエクスポートします。

5. 使用する **knownmoniker** またはカスタムイメージモニカーを決定します。

6. **Applymodifications** メソッドで、次の例のように、新しいツリーを返す前に、メソッドのどこかで次の操作を実行します。

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   tree = tree.SetIcon(KnownMonikers.Blank.ToProjectSystemType());
   ```

7. 新しいツリーを作成する場合は、次の例のように、目的のモニカーを NewTree メソッドに渡してカスタムイメージを設定できます。

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   ProjectImageMoniker icon         = KnownMonikers.FolderClosed.ToProjectSystemType();
   ProjectImageMoniker expandedIcon = KnownMonikers.FolderOpened.ToProjectSystemType();

   return this.ProjectTreeFactory.Value.NewTree(/*caption*/<value>,
                                                /*filePath*/<value>,
                                                /*browseObjectProperties*/<value>,
                                                icon,
                                                expandedIcon);
   ```

## <a name="how-do-i-convert-from-a-real-image-strip-to-a-moniker-based-image-strip"></a>実際のイメージストリップからモニカーベースのイメージストリップに変換操作方法ますか。
 **HIMAGELISTs をサポートする必要があります**

 イメージサービスを使用するために更新するコードの既存のイメージストリップが既に存在する場合、イメージリストを渡す必要がある Api によって制限されている場合でも、イメージサービスの利点を得ることができます。 モニカーベースのイメージストリップを作成するには、次の手順に従って、既存のモニカーからマニフェストを作成します。

1. **Manifestfromresources** ツールを実行し、イメージストリップを渡します。 これにより、ストリップのマニフェストが生成されます。

   - 推奨: マニフェストの使用に合わせて既定以外の名前を指定します。

2. **Knownmonikers** のみを使用している場合は、次の手順を実行します。

   - \<Images>マニフェストのセクションをに置き換え \<Images/> ます。

   - すべてのサブイメージ Id (_ # # ですべてのもの) を削除 \<imagestrip name> します。

   - 推奨: Asセット Guid シンボルとイメージストリップシンボルの使用方法に合わせて名前を変更します。

   - 各文字列 **の GUID** を $ (ImageCatalogGuid) に置き換え **、各** 文字列の ID を $ () に置き換え、 \<moniker> 外部 = "true" 属性を各型の型に追加します。

       - \<moniker> は、イメージと一致するが、" **Knownmoniker** " で置き換えられます。 名前から削除されます。

   - <インポートマニフェスト = "$ (ManifestFolder) \\<相対インストールディレクトリパスを * \> \Microsoft.VisualStudio.ImageCatalog.imagemanifest"/> に追加し \* て、セクションの先頭に追加し \<Symbols> ます。

       - 相対パスは、マニフェストのセットアップ作成で定義されている配置場所によって決まります。

3. **Manifesttocode** ツールを実行してラッパーを生成します。これにより、既存のコードに、イメージストリップのイメージサービスを照会するために使用できるモニカーが含まれるようになります。

   - 推奨: ラッパーと名前空間の使用法に合わせて、既定以外の名前を指定します。

4. イメージサービスと新しいファイルを操作するために、追加、セットアップの作成/配置、およびその他のコード変更をすべて実行します。

   内部イメージと外部イメージの両方を含むサンプルマニフェストは、次のように表示されます。

```xml
<?xml version="1.0"?>
<ImageManifest
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">

  <Symbols>
    <!-- This needs to be the relative path from your manifest to the ImageCatalog's manifest
         where $(ManifestFolder) is the deployed location of this manifest. -->
    <Import Manifest="$(ManifestFolder)\<RelPath>\Microsoft.VisualStudio.ImageCatalog.imagemanifest" />

    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/ImageStrip" />
    <Guid Name="ImageGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />
    <Guid Name="ImageStripGuid" Value="{9c84a570-d9a7-4052-a340-188fb276f973}" />
    <ID Name="MyImage_0" Value="100" />
    <ID Name="MyImage_1" Value="101" />
    <ID Name="InternalList" Value="1001" />
    <ID Name="ExternalList" Value="1002" />
  </Symbols>

  <Images>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_0)">
      <Source Uri="$(Resources)/MyImage_0.png">
        <Size Value="16" />
      </Source>
    </Image>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_1)">
      <Source Uri="$(Resources)/MyImage_1.png">
        <Size Value="16" />
      </Source>
    </Image>
  </Images>

  <ImageLists>
    <ImageList Guid="$(ImageStripGuid)" ID="$(InternalList)">
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_0)" />
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_1)" />
    </ImageList>
    <ImageList Guid="$(ImageStripGuid)" ID="$(ExternalList)">
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusError)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusWarning)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusInformation)" External="true" />
    </ImageList>
  </ImageLists>

</ImageManifest>
```

 **HIMAGELISTs をサポートする必要はありません**

1. イメージストリップ内のイメージに一致する **knownmonikers** のセットを確認するか、イメージストリップ内のイメージ用に独自のモニカーを作成します。

2. イメージストリップ内の必要なインデックスにあるイメージを取得するために使用したすべてのマッピングを更新して、代わりにモニカーを使用します。

3. イメージサービスを使用して、更新されたマッピングによってモニカーを要求するようにコードを更新します。 (これは、マネージコードの **CrispImages** を更新したり、イメージサービスから hbitmaps や hbitmaps を要求したり、ネイティブコードの周囲に渡したりすることを意味します)。

## <a name="testing-your-images"></a>イメージのテスト
 イメージライブラリビューアーツールを使用すると、イメージマニフェストをテストして、すべてが正しく作成されていることを確認できます。 このツールは [Visual Studio 2015 SDK](visual-studio-sdk.md)で入手できます。 このツールとその他のドキュメントについては、 [こちら](./internals/vssdk-utilities.md?view=vs-2015&preserve-view=true)を参照してください。

## <a name="additional-resources"></a>その他のリソース

### <a name="samples"></a>サンプル
 GitHub の Visual Studio サンプルのいくつかが更新され、さまざまな Visual Studio 機能拡張ポイントの一部としてイメージサービスを使用する方法が示されるようになりました。

 [http://github.com/Microsoft/VSSDK-Extensibility-Samples](https://github.com/Microsoft/VSSDK-Extensibility-Samples)最新のサンプルを確認してください。

### <a name="tooling"></a>ツール
 イメージサービスに対応した UI を作成または更新する際に役立つ、イメージサービスの一連のサポートツールが作成されました。 各ツールの詳細については、ツールに付属のドキュメントを参照してください。 これらのツールは、 [Visual Studio 2015 SDK](visual-studio-sdk.md)の一部として含まれています。

 **ManifestFromResources**

 Manifest from Resources ツールは、イメージリソース (PNG または XAML) の一覧を取得し、イメージサービスでこれらのイメージを使用するためのイメージマニフェストファイルを生成します。

 **ManifestToCode**

 Manifest to Code ツールは、イメージマニフェストファイルを受け取り、コード (C++、C#、または VB) または *vsct* ファイルでマニフェスト値を参照するためのラッパーファイルを生成します。

 **ImageLibraryViewer**

 イメージライブラリビューアーツールでは、イメージマニフェストを読み込んで、Visual Studio がマニフェストを正しく作成するのと同じ方法でユーザーが操作できるようにすることができます。 ユーザーは、背景、サイズ、DPI 設定、ハイコントラストなどの設定を変更できます。 また、マニフェスト内のエラーを検出するための読み込み情報が表示され、マニフェスト内の各イメージのソース情報が表示されます。

## <a name="faq"></a>よく寄せられる質問

- 読み込み時に含める必要がある依存関係はあり \<Reference Include="Microsoft.VisualStudio.*.Interop.14.0.DesignTime" /> ますか。

  - すべての相互運用 Dll で EmbedInteropTypes = "true" に設定します。

- 拡張機能を使用してイメージマニフェストをデプロイ操作方法には

  - *Imagemanifest* ファイルをプロジェクトに追加します。

  - [VSIX に含める] を True に設定します。

- ここでは、CPS プロジェクトシステムを更新しています。 **ImageName** と **stockiconservice** はどうなりましたか?

  - これらは、モニカーを使用するように CPS を更新したときに削除されました。 **Stockiconservice** を呼び出す必要がなくなりました。 CPS ユーティリティで **ToProjectSystemType ()** 拡張メソッドを使用して、目的の **knownmoniker** をメソッドまたはプロパティに渡すだけです。 次のように、 **ImageName** から **knownmonikers** へのマッピングを見つけることができます。

    |**ImageName**|**KnownMoniker**|
    |-|-|
    |ImageName. OfflineWebApp|KnownImageIds. Web|
    |ImageName フォルダー|KnownImageIds. Web|
    |ImageName. OpenReferenceFolder|KnownImageIds. FolderOpened|
    |ImageName. ReferenceFolder|KnownImageIds. 参照|
    |ImageName. 参照|KnownImageIds. 参照|
    |SdlWebReference|KnownImageIds. WebReferenceFolder|
    |DiscoWebReference|KnownImageIds. DynamicDiscoveryDocument|
    |ImageName. フォルダー|KnownImageIds. FolderClosed|
    |ImageName. OpenFolder|KnownImageIds. FolderOpened|
    |ExcludedFolder|KnownImageIds|
    |OpenExcludedFolder|KnownImageIds|
    |ExcludedFile|KnownImageIds|
    |ImageName. DependentFile|KnownImageIds GenerateFile|
    |MissingFile|KnownImageIds.DocumentWarning|
    |ImageName フォーム|KnownImageIds. WindowsForm|
    |ImageName. WindowsUserControl|KnownImageIds. UserControl|
    |WindowsComponent|KnownImageIds ComponentFile|
    |ImageName.Xmlスキーマ|KnownImageIds.XMLスキーマ|
    |ImageName.Xmlファイル|KnownImageIds.XMLファイル|
    |ImageName. Web フォーム|KnownImageIds. Web|
    |ImageName. WebService|KnownImageIds. WebService|
    |ImageName. WebUserControl|KnownImageIds WebUserControl|
    |ImageName. WebCustomUserControl|KnownImageIds|
    |ImageName. AspPage|KnownImageIds ASPFile)|
    |ImageName. GlobalApplicationClass|KnownImageIds. SettingsFile|
    |ImageName. WebConfig|KnownImageIds.ConfigurationFile|
    |ImageName.HtmlPage|KnownImageIds.HTMLFile|
    |ImageName. StyleSheet|KnownImageIds. StyleSheet|
    |ScriptFile|KnownImageIds.JSスクリプト|
    |TextFile|KnownImageIds.Document|
    |ImageName ファイル。 SettingsFile|KnownImageIds. 設定|
    |ImageName. リソース|KnownImageIds.DocumentGroup|
    |ImageName. Bitmap|KnownImageIds. イメージ|
    |ImageName. アイコン|KnownImageIds. IconFile|
    |ImageName. イメージ|KnownImageIds. イメージ|
    |ImageMap|KnownImageIds|
    |ImageName. XWorld|KnownImageIds|
    |ImageName. Audio|KnownImageIds。サウンド|
    |ImageName. ビデオ|KnownImageIds。メディア|
    |ImageName.Cab|KnownImageIds.CABプロジェクト|
    |ImageName. Jar|KnownImageIds|
    |ImageName. DataEnvironment|KnownImageIds. DataTable|
    |ImageName ファイル|KnownImageIds. レポート|
    |DanglingReference|KnownImageIds. ReferenceWarning|
    |ImageName ファイル|KnownImageIds|
    |ImageName. カーソル|KnownImageIds. カーソルファイル|
    |ImageName. Appデザイナフォルダー|KnownImageIds. プロパティ|
    |ImageName. データ|KnownImageIds. データベース|
    |ImageName. アプリケーション|KnownImageIds. アプリケーション|
    |ImageName. DataSet|KnownImageIds. DatabaseGroup|
    |ImageName. .Pfx|KnownImageIds. Certificate|
    |ImageName. .Snk|KnownImageIds. ルール|
    |ImageName. VisualBasicProject|KnownImageIds. VBProjectNode|
    |CSharpProject|KnownImageIds. CSProjectNode|
    |ImageName. Empty|KnownImageIds。空白|
    |MissingFolder|KnownImageIds. FolderOffline|
    |SharedImportReference|KnownImageIds. SharedProject|
    |ImageName. SharedProjectCs|KnownImageIds. CSSharedProject|
    |ImageName. SharedProjectVc|KnownImageIds. CPPSharedProject|
    |ImageName. SharedProjectJs|SharedProject の KnownImageIds.JS|
    |CSharpCodeFile|KnownImageIds|
    |ImageName. VisualBasicCodeFile|KnownImageIds|

  - 入力候補一覧のプロバイダーを更新しています。 以前の **StandardGlyphGroup** 値と **standardglyph** 値に一致する **knownmonikers** は何ですか。

    |名前|名前|名前|
    |-|-|-|
    |GlyphGroupClass|GlyphItemPublic|ClassPublic|
    |GlyphGroupClass|GlyphItemInternal|ClassInternal|
    |GlyphGroupClass|GlyphItemFriend|ClassInternal|
    |GlyphGroupClass|GlyphItemProtected|ClassProtected|
    |GlyphGroupClass|GlyphItemPrivate|ClassPrivate|
    |GlyphGroupClass|GlyphItemShortcut|ClassShortcut|
    |GlyphGroupConstant|GlyphItemPublic|ConstantPublic|
    |GlyphGroupConstant|GlyphItemInternal|ConstantInternal|
    |GlyphGroupConstant|GlyphItemFriend|ConstantInternal|
    |GlyphGroupConstant|GlyphItemProtected|ConstantProtected|
    |GlyphGroupConstant|GlyphItemPrivate|ConstantPrivate|
    |GlyphGroupConstant|GlyphItemShortcut|ConstantShortcut|
    |GlyphGroupDelegate|GlyphItemPublic|DelegatePublic|
    |GlyphGroupDelegate|GlyphItemInternal|DelegateInternal|
    |GlyphGroupDelegate|GlyphItemFriend|DelegateInternal|
    |GlyphGroupDelegate|GlyphItemProtected|DelegateProtected|
    |GlyphGroupDelegate|GlyphItemPrivate|DelegatePrivate|
    |GlyphGroupDelegate|GlyphItemShortcut|DelegateShortcut|
    |GlyphGroupEnum|GlyphItemPublic|EnumerationPublic|
    |GlyphGroupEnum|GlyphItemInternal|EnumerationInternal|
    |GlyphGroupEnum|GlyphItemFriend|EnumerationInternal|
    |GlyphGroupEnum|GlyphItemProtected|EnumerationProtected|
    |GlyphGroupEnum|GlyphItemPrivate|EnumerationPrivate|
    |GlyphGroupEnum|GlyphItemShortcut|EnumerationShortcut|
    |GlyphGroupEnumMember|GlyphItemPublic|EnumerationItemPublic|
    |GlyphGroupEnumMember|GlyphItemInternal|EnumerationItemInternal|
    |GlyphGroupEnumMember|GlyphItemFriend|EnumerationItemInternal|
    |GlyphGroupEnumMember|GlyphItemProtected|EnumerationItemProtected|
    |GlyphGroupEnumMember|GlyphItemPrivate|EnumerationItemPrivate|
    |GlyphGroupEnumMember|GlyphItemShortcut|EnumerationItemShortcut|
    |GlyphGroupEvent|GlyphItemPublic|EventPublic|
    |GlyphGroupEvent|GlyphItemInternal|EventInternal|
    |GlyphGroupEvent|GlyphItemFriend|EventInternal|
    |GlyphGroupEvent|GlyphItemProtected|EventProtected|
    |GlyphGroupEvent|GlyphItemPrivate|EventPrivate|
    |GlyphGroupEvent|GlyphItemShortcut|EventShortcut|
    |GlyphGroupException|GlyphItemPublic|ExceptionPublic|
    |GlyphGroupException|GlyphItemInternal|ExceptionInternal|
    |GlyphGroupException|GlyphItemFriend|ExceptionInternal|
    |GlyphGroupException|GlyphItemProtected|ExceptionProtected|
    |GlyphGroupException|GlyphItemPrivate|ExceptionPrivate|
    |GlyphGroupException|GlyphItemShortcut|ExceptionShortcut|
    |GlyphGroupField|GlyphItemPublic|FieldPublic|
    |GlyphGroupField|GlyphItemInternal|FieldInternal|
    |GlyphGroupField|GlyphItemFriend|FieldInternal|
    |GlyphGroupField|GlyphItemProtected|FieldProtected|
    |GlyphGroupField|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupField|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupInterface|GlyphItemPublic|InterfacePublic|
    |GlyphGroupInterface|GlyphItemInternal|InterfaceInternal|
    |GlyphGroupInterface|GlyphItemFriend|InterfaceInternal|
    |GlyphGroupInterface|GlyphItemProtected|InterfaceProtected|
    |GlyphGroupInterface|GlyphItemPrivate|InterfacePrivate|
    |GlyphGroupInterface|GlyphItemShortcut|InterfaceShortcut|
    |GlyphGroupMacro|GlyphItemPublic|マクロパブリック|
    |GlyphGroupMacro|GlyphItemInternal|マクロ内部|
    |GlyphGroupMacro|GlyphItemFriend|マクロ内部|
    |GlyphGroupMacro|GlyphItemProtected|マクロの保護|
    |GlyphGroupMacro|GlyphItemPrivate|マクロプライベート|
    |GlyphGroupMacro|GlyphItemShortcut|マクロのショートカット|
    |GlyphGroupMap|GlyphItemPublic|MapPublic|
    |GlyphGroupMap|GlyphItemInternal|MapInternal|
    |GlyphGroupMap|GlyphItemFriend|MapInternal|
    |GlyphGroupMap|GlyphItemProtected|このようにして|
    |GlyphGroupMap|GlyphItemPrivate|MapPrivate|
    |GlyphGroupMap|GlyphItemShortcut|MapShortcut|
    |GlyphGroupMapItem|GlyphItemPublic|MapItemPublic|
    |GlyphGroupMapItem|GlyphItemInternal|MapItemInternal|
    |GlyphGroupMapItem|GlyphItemFriend|MapItemInternal|
    |GlyphGroupMapItem|GlyphItemProtected|MapItemProtected|
    |GlyphGroupMapItem|GlyphItemPrivate|MapItemPrivate|
    |GlyphGroupMapItem|GlyphItemShortcut|MapItemShortcut|
    |GlyphGroupMethod|GlyphItemPublic|MethodPublic|
    |GlyphGroupMethod|GlyphItemInternal|MethodInternal|
    |GlyphGroupMethod|GlyphItemFriend|MethodInternal|
    |GlyphGroupMethod|GlyphItemProtected|MethodProtected|
    |GlyphGroupMethod|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupMethod|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupOverload|GlyphItemPublic|MethodPublic|
    |GlyphGroupOverload|GlyphItemInternal|MethodInternal|
    |GlyphGroupOverload|GlyphItemFriend|MethodInternal|
    |GlyphGroupOverload|GlyphItemProtected|MethodProtected|
    |GlyphGroupOverload|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupOverload|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupModule|GlyphItemPublic|ModulePublic|
    |GlyphGroupModule|GlyphItemInternal|ModuleInternal|
    |GlyphGroupModule|GlyphItemFriend|ModuleInternal|
    |GlyphGroupModule|GlyphItemProtected|ModuleProtected|
    |GlyphGroupModule|GlyphItemPrivate|ModulePrivate|
    |GlyphGroupModule|GlyphItemShortcut|ModuleShortcut|
    |GlyphGroupNamespace|GlyphItemPublic|NamespacePublic|
    |GlyphGroupNamespace|GlyphItemInternal|NamespaceInternal|
    |GlyphGroupNamespace|GlyphItemFriend|NamespaceInternal|
    |GlyphGroupNamespace|GlyphItemProtected|NamespaceProtected|
    |GlyphGroupNamespace|GlyphItemPrivate|NamespacePrivate|
    |GlyphGroupNamespace|GlyphItemShortcut|NamespaceShortcut|
    |GlyphGroupOperator|GlyphItemPublic|オペレーターパブリック|
    |GlyphGroupOperator|GlyphItemInternal|演算子内部|
    |GlyphGroupOperator|GlyphItemFriend|演算子内部|
    |GlyphGroupOperator|GlyphItemProtected|保護されたオペレーター|
    |GlyphGroupOperator|GlyphItemPrivate|オペレータープライベート|
    |GlyphGroupOperator|GlyphItemShortcut|演算子のショートカット|
    |GlyphGroupProperty|GlyphItemPublic|PropertyPublic|
    |GlyphGroupProperty|GlyphItemInternal|PropertyInternal|
    |GlyphGroupProperty|GlyphItemFriend|PropertyInternal|
    |GlyphGroupProperty|GlyphItemProtected|PropertyProtected|
    |GlyphGroupProperty|GlyphItemPrivate|PropertyPrivate|
    |GlyphGroupProperty|GlyphItemShortcut|PropertyShortcut|
    |GlyphGroupStruct|GlyphItemPublic|StructurePublic|
    |GlyphGroupStruct|GlyphItemInternal|内部構造|
    |GlyphGroupStruct|GlyphItemFriend|内部構造|
    |GlyphGroupStruct|GlyphItemProtected|保護された構造|
    |GlyphGroupStruct|GlyphItemPrivate|構造体プライベート|
    |GlyphGroupStruct|GlyphItemShortcut|構造体のショートカット|
    |GlyphGroupTemplate|GlyphItemPublic|TemplatePublic|
    |GlyphGroupTemplate|GlyphItemInternal|TemplateInternal|
    |GlyphGroupTemplate|GlyphItemFriend|TemplateInternal|
    |GlyphGroupTemplate|GlyphItemProtected|TemplateProtected|
    |GlyphGroupTemplate|GlyphItemPrivate|TemplatePrivate|
    |GlyphGroupTemplate|GlyphItemShortcut|TemplateShortcut|
    |GlyphGroupTypedef|GlyphItemPublic|TypeDefinitionPublic|
    |GlyphGroupTypedef|GlyphItemInternal|TypeDefinitionInternal|
    |GlyphGroupTypedef|GlyphItemFriend|TypeDefinitionInternal|
    |GlyphGroupTypedef|GlyphItemProtected|TypeDefinitionProtected|
    |GlyphGroupTypedef|GlyphItemPrivate|TypeDefinitionPrivate|
    |GlyphGroupTypedef|GlyphItemShortcut|TypeDefinitionShortcut|
    |GlyphGroupType|GlyphItemPublic|TypePublic|
    |GlyphGroupType|GlyphItemInternal|TypeInternal|
    |GlyphGroupType|GlyphItemFriend|TypeInternal|
    |GlyphGroupType|GlyphItemProtected|TypeProtected|
    |GlyphGroupType|GlyphItemPrivate|TypePrivate|
    |GlyphGroupType|GlyphItemShortcut|TypeShortcut|
    |GlyphGroupUnion|GlyphItemPublic|UnionPublic|
    |GlyphGroupUnion|GlyphItemInternal|UnionInternal|
    |GlyphGroupUnion|GlyphItemFriend|UnionInternal|
    |GlyphGroupUnion|GlyphItemProtected|UnionProtected|
    |GlyphGroupUnion|GlyphItemPrivate|UnionPrivate|
    |GlyphGroupUnion|GlyphItemShortcut|UnionShortcut|
    |GlyphGroupVariable|GlyphItemPublic|FieldPublic|
    |GlyphGroupVariable|GlyphItemInternal|FieldInternal|
    |GlyphGroupVariable|GlyphItemFriend|FieldInternal|
    |GlyphGroupVariable|GlyphItemProtected|FieldProtected|
    |GlyphGroupVariable|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupVariable|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupValueType|GlyphItemPublic|ValueTypePublic|
    |GlyphGroupValueType|GlyphItemInternal|ValueTypeInternal|
    |GlyphGroupValueType|GlyphItemFriend|ValueTypeInternal|
    |GlyphGroupValueType|GlyphItemProtected|ValueTypeProtected|
    |GlyphGroupValueType|GlyphItemPrivate|ValueTypePrivate|
    |GlyphGroupValueType|GlyphItemShortcut|ValueTypeShortcut|
    |GlyphGroupIntrinsic|GlyphItemPublic|ObjectPublic|
    |GlyphGroupIntrinsic|GlyphItemInternal|ObjectInternal|
    |GlyphGroupIntrinsic|GlyphItemFriend|ObjectInternal|
    |GlyphGroupIntrinsic|GlyphItemProtected|ObjectProtected|
    |GlyphGroupIntrinsic|GlyphItemPrivate|ObjectPrivate|
    |GlyphGroupIntrinsic|GlyphItemShortcut|ObjectShortcut|
    |GlyphGroupJSharpMethod|GlyphItemPublic|MethodPublic|
    |GlyphGroupJSharpMethod|GlyphItemInternal|MethodInternal|
    |GlyphGroupJSharpMethod|GlyphItemFriend|MethodInternal|
    |GlyphGroupJSharpMethod|GlyphItemProtected|MethodProtected|
    |GlyphGroupJSharpMethod|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupJSharpMethod|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupJSharpField|GlyphItemPublic|FieldPublic|
    |GlyphGroupJSharpField|GlyphItemInternal|FieldInternal|
    |GlyphGroupJSharpField|GlyphItemFriend|FieldInternal|
    |GlyphGroupJSharpField|GlyphItemProtected|FieldProtected|
    |GlyphGroupJSharpField|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupJSharpField|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupJSharpClass|GlyphItemPublic|ClassPublic|
    |GlyphGroupJSharpClass|GlyphItemInternal|ClassInternal|
    |GlyphGroupJSharpClass|GlyphItemFriend|ClassInternal|
    |GlyphGroupJSharpClass|GlyphItemProtected|ClassProtected|
    |GlyphGroupJSharpClass|GlyphItemPrivate|ClassPrivate|
    |GlyphGroupJSharpClass|GlyphItemShortcut|ClassShortcut|
    |GlyphGroupJSharpNamespace|GlyphItemPublic|NamespacePublic|
    |GlyphGroupJSharpNamespace|GlyphItemInternal|NamespaceInternal|
    |GlyphGroupJSharpNamespace|GlyphItemFriend|NamespaceInternal|
    |GlyphGroupJSharpNamespace|GlyphItemProtected|NamespaceProtected|
    |GlyphGroupJSharpNamespace|GlyphItemPrivate|NamespacePrivate|
    |GlyphGroupJSharpNamespace|GlyphItemShortcut|NamespaceShortcut|
    |GlyphGroupJSharpInterface|GlyphItemPublic|InterfacePublic|
    |GlyphGroupJSharpInterface|GlyphItemInternal|InterfaceInternal|
    |GlyphGroupJSharpInterface|GlyphItemFriend|InterfaceInternal|
    |GlyphGroupJSharpInterface|GlyphItemProtected|InterfaceProtected|
    |GlyphGroupJSharpInterface|GlyphItemPrivate|InterfacePrivate|
    |GlyphGroupJSharpInterface|GlyphItemShortcut|InterfaceShortcut|
    |GlyphGroupError||StatusError|
    |GlyphBscFile||ClassFile|
    |GlyphAssembly||リファレンス|
    |GlyphLibrary||ライブラリ|
    |GlyphVBProject||VBProjectNode|
    |GlyphCoolProject||CSProjectNode|
    |GlyphCppProject||CPPProjectNode|
    |GlyphDialogId||ダイアログ|
    |GlyphOpenFolder||開かれたフォルダー|
    |GlyphClosedFolder||閉じたフォルダー|
    |GlyphArrow||GoToNext|
    |GlyphCSharpFile||CSFileNode|
    |GlyphCSharpExpansion||スニペット|
    |GlyphKeyword||IntellisenseKeyword|
    |GlyphInformation||StatusInformation|
    |GlyphReference||ClassMethodReference|
    |GlyphRecursion||再帰|
    |GlyphXmlItem||タグ|
    |GlyphJSharpProject||DocumentCollection|
    |GlyphJSharpDocument||ドキュメント|
    |GlyphForwardType||GoToNext|
    |GlyphCallersGraph||CallTo|
    |GlyphCallGraph||CallFrom|
    |GlyphWarning||StatusWarning|
    |GlyphMaybeReference||QuestionMark|
    |GlyphMaybeCaller||CallTo|
    |GlyphMaybeCall||CallFrom|
    |GlyphExtensionMethod||ExtensionMethod|
    |GlyphExtensionMethodInternal||ExtensionMethod|
    |GlyphExtensionMethodFriend||ExtensionMethod|
    |GlyphExtensionMethodProtected||ExtensionMethod|
    |GlyphExtensionMethodPrivate||ExtensionMethod|
    |GlyphExtensionMethodShortcut||ExtensionMethod|
    |GlyphXmlAttribute||XmlAttribute|
    |GlyphXmlChild||XmlElement|
    |GlyphXmlDescendant||XmlDescendant|
    |GlyphXmlNamespace||XmlNamespace|
    |GlyphXmlAttributeQuestion||XmlAttributeLowConfidence|
    |GlyphXmlAttributeCheck||XmlAttributeHighConfidence|
    |GlyphXmlChildQuestion||XmlElementLowConfidence|
    |GlyphXmlChildCheck||XmlElementHighConfidence|
    |GlyphXmlDescendantQuestion||XmlDescendantLowConfidence|
    |GlyphXmlDescendantCheck||XmlDescendantHighConfidence|
    |GlyphCompletionWarning||IntellisenseWarning|
