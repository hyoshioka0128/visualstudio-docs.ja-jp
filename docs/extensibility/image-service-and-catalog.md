---
title: イメージサービスとカタログ |マイクロソフトドキュメント
ms.date: 04/01/2019
ms.topic: conceptual
ms.assetid: 34990c37-ae98-4140-9b1e-a91c192220d9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 79e1ccfad2a678656bcf09e37852532a8b28eb0e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710384"
---
# <a name="image-service-and-catalog"></a>イメージ サービスとカタログ
このクックブックには、Visual Studio 2015 で導入された Visual Studio イメージ サービスとイメージ カタログを採用するためのガイダンスとベスト プラクティスが含まれています。

 Visual Studio 2015 で導入されたイメージ サービスを使用すると、開発者は、デバイスとユーザーが選択したテーマに最適なイメージを取得して、表示されるコンテキストのテーマを修正するなど、イメージを表示できます。 イメージ サービスを採用することで、資産のメンテナンス、HDPI スケーリング、テーマに関連する主要な問題点を排除できます。

|||
|-|-|
|**今日の問題**|**ソリューション**|
|背景色のブレンド|組み込みのアルファブレンディング|
|テーマ(一部)画像|テーマメタデータ|
|ハイコントラスト モード|代替ハイコントラスト リソース|
|異なるDPIモードに複数のリソースが必要|ベクターベースのフォールバックを使用して選択可能なリソース|
|重複した画像|イメージコンセプトごとに1つの識別子|

 なぜイメージサービスを採用するのですか?

- 常に Visual Studio から最新の "ピクセルパーフェクト" イメージを取得します。

- 自分の画像を送信して使用できます

- Windows が新しい DPI スケーリングを追加するときにイメージをテストする必要はありません。

- 実装における古いアーキテクチャのハードルに対処する

  イメージ サービスを使用する前後の Visual Studio シェル ツール バー:

  ![前後のイメージ サービス](../extensibility/media/image-service-before-and-after.png "前後のイメージ サービス")

## <a name="how-it-works"></a>しくみ
 イメージ サービスは、サポートされている UI フレームワークに適したビットマップ イメージを提供できます。

- WPF: ビットマップソース

- ウィンフォーム: システム.ドローイング.ビットマップ

- Win32: HBITMAP

  イメージ サービス フロー図

  ![イメージ サービスのフロー ダイアグラム](../extensibility/media/image-service-flow-diagram.png "イメージ サービスのフロー ダイアグラム")

  **イメージモニカー**

  イメージ モニカー (略してモニカー) は、イメージ ライブラリ内のイメージ アセットまたはイメージ リスト アセットを一意に識別する GUID/ID ペアです。

  **既知のモニカー**

  Visual Studio イメージ カタログに含まれ、Visual Studio のコンポーネントまたは拡張機能によって一般に消費可能なイメージ モニカーのセット。

  **イメージ マニフェスト ファイル**

  イメージ マニフェスト (*.imagemanifest*) ファイルは、イメージ アセットのセット、それらのアセットを表すモニカー、および各アセットを表す実イメージを定義する XML ファイルです。 イメージ マニフェストは、従来の UI サポート用のスタンドアロン イメージまたはイメージ リストを定義できます。 また、アセットまたは各アセットの背後にある個々のイメージに設定して、アセットの表示時期と表示方法を変更できる属性もあります。

  **イメージ マニフェスト スキーマ**

  完全なイメージ マニフェストは次のようになります。

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

 **Symbols**

 イメージ マニフェストは、読みやすさと保守の助けとして、属性値のシンボルを使用できます。 シンボルは次のように定義されます。

```xml
<Symbols>
      <Import Manifest="manifest" />
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />
      <ID Name="cmdidSaveAll" Value="1000" />
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />
</Symbols>
```

|||
|-|-|
|**サブ要素**|**定義**|
|[インポート]|現在のマニフェストで使用するために、指定されたマニフェスト ファイルのシンボルをインポートします。|
|Guid|シンボルは GUID を表し、GUID の書式設定と一致する必要があります|
|id|シンボルは ID を表し、負でない整数でなければなりません|
|String|シンボルは任意の文字列値を表します。|

 シンボルは大文字と小文字を区別し、$(symbol-name) 構文を使用して参照されます。

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 一部のシンボルは、すべてのマニフェストに対して事前定義されています。 これらは、\<ソース>または\<インポート>要素の Uri 属性でローカル コンピューター上のパスを参照するために使用できます。

|||
|-|-|
|**シンボル**|**説明**|
|CommonProgramFiles|環境変数の値|
|ローカルアプリケーションデータ|環境変数 %LocalAppData% の値|
|マニフェストフォルダー|マニフェスト ファイルを含むフォルダー|
|マイドキュメント|現在のユーザーのマイ ドキュメント フォルダの完全パス|
|ProgramFiles|環境変数 %ProgramFiles% の値|
|システム|*ウィンドウズ\システム32*フォルダ|
|Windir|%WinDir% 環境変数の値|

 **イメージ**

 イメージ\<>要素は、モニカーによって参照できるイメージを定義します。 GUID と ID は、イメージ モニカーを形成します。 イメージのモニカーは、イメージ ライブラリ全体で一意である必要があります。 複数のイメージに特定のモニカーがある場合、ライブラリのビルド中に最初に検出されたイメージは保持されます。

 少なくとも 1 つのソースが含まれている必要があります。 サイズに依存しないソースは、幅広いサイズで最良の結果を得ることができますが、必須ではありません。 サービスが Image> 要素で定義されていないサイズのイメージを\<要求され、サイズに依存しないソースがない場合、サービスは最適なサイズ固有のソースを選択し、要求されたサイズにスケーリングします。

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|||
|-|-|
|**属性**|**定義**|
|Guid|[必須]イメージ モニカーの GUID 部分|
|id|[必須]イメージ モニカーの ID 部分|
|許可色反転|[オプション、デフォルトは true]暗い背景で使用する場合、イメージの色をプログラムによって反転できるかどうかを示します。|

 **ソース**

 ソース\<>要素は、単一のイメージ ソース アセット (XAML および PNG) を定義します。

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|||
|-|-|
|**属性**|**定義**|
|Uri|[必須]イメージの読み込み元を定義する URI。 次のいずれかを指定できます。<br /><br /> - application:///権限を使用する[パック URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf)<br />- 絶対コンポーネントリソース参照<br />- ネイティブ リソースを含むファイルへのパス|
|バックグラウンド|[オプション]ソースが使用される背景の種類を示します。<br /><br /> 次のいずれかを指定できます。<br /><br /> *ライト:* 光源は、明るい背景で使用できます。<br /><br /> *暗い:* ソースは暗い背景で使用できます。<br /><br /> *ハイコントラスト:* ソースはハイ コントラスト モードで任意の背景で使用できます。<br /><br /> *ハイコントラストライト:* 光源はハイ コントラスト モードの明るい背景で使用できます。<br /><br /> *ハイコントラストダーク:* ソースは、ハイ コントラスト モードで暗い背景で使用できます。<br /><br /> 背景属性を省略すると、任意のバックグラウンドでソースを使用できます。<br /><br /> 背景が*明るい*、*暗い*、*ハイコントラストライト*、または*ハイコントラストダーク*の場合、ソースの色は反転しません。 背景を省略するか *、ハイコントラスト*に設定すると、ソースの色の反転はイメージの**AllowColorInversion**属性によって制御されます。|

\<ソース>要素は、次のオプションのサブ要素のうち 1 つだけを持つことができます。

||||
|-|-|-|
|**要素**|**属性 (すべて必須)**|**定義**|
|\<サイズ>|[値]|ソースは、指定されたサイズのイメージ (デバイス単位) に使用されます。 画像は正方形になります。|
|\<サイズ範囲>|最小サイズ、最大サイズ|ソースは、MinSize から MaxSize (デバイス単位) までのイメージに使用されます。 画像は正方形になります。|
|\<分析コード>|Width、Height|ソースは、指定された幅と高さのイメージ (デバイス単位) に使用されます。|
|\<ディメンション範囲>|最小幅、最小高さ、<br /><br /> 最大幅、最大高さ|ソースは、最小幅/高さから最大幅/高さ (デバイス単位) までの画像に使用されます。|

 ソース>要素には、マネージ アセンブリ\<ではなくネイティブ アセンブリから読み込まれる\<ソース>を定義するオプションの NativeResource> サブ要素を含めることもできます。 \<

```xml
<NativeResource Type="type" ID="int" />
```

|||
|-|-|
|**属性**|**定義**|
|種類|[必須]ネイティブ リソースの種類 (XAML または PNG)|
|id|[必須]ネイティブ リソースの整数 ID 部分|

 **Imagelist**

 ImageList>要素は\<、単一のストリップで返すことができるイメージのコレクションを定義します。 ストリップは必要に応じて、オンデマンドで構築されます。

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|||
|-|-|
|**属性**|**定義**|
|Guid|[必須]イメージ モニカーの GUID 部分|
|id|[必須]イメージ モニカーの ID 部分|
|外部|[オプション、デフォルトの false]イメージ モニカーが現在のマニフェスト内のイメージを参照するかどうかを示します。|

 含まれているイメージのモニカーは、現在のマニフェストで定義されているイメージを参照する必要はありません。 含まれているイメージがイメージ ライブラリに見つからない場合は、その場所に空白のプレースホルダー イメージが使用されます。

## <a name="using-the-image-service"></a>イメージ サービスの使用

### <a name="first-steps-managed"></a>最初のステップ (管理)
 イメージ サービスを使用するには、プロジェクトに次のアセンブリの一部またはすべてを参照する必要があります。

- *をクリックします。*

  - 組み込みのイメージ カタログ**KnownMonikers**を使用する場合は必須です。

- *Microsoft.VisualStudio.Imaging.dll*

  - あなたのWPF UIで**クリスプイメージ**と**画像をテーマにユーティリティを使用する**場合に必要です。

- *相互運用性.14.0.デザインタイム.dll*

  - **イメージモニカ**ーと**イメージ属性**の型を使用する場合は必須です。

  - **埋め込み相互運用性の種類**を true に設定する必要があります。

- *デザインタイム*

  - **IVsImageService2**型を使用する場合は必須です。

  - **埋め込み相互運用性の種類**を true に設定する必要があります。

- *ユーティリティ.dll*

  - WPF UI で**イメージテリングユーティリティに****ブラシを**使用する場合に必要です。

- *をクリックします。\<vsバージョン>.0*

  - **IVsUI オブジェクト**型を使用する場合は必須です。

- *10.0.dll*

  - WinForms 関連の UI ヘルパーを使用する場合は必須です。

  - **埋め込み相互運用性の種類**を true に設定する必要があります。

### <a name="first-steps-native"></a>最初のステップ (ネイティブ)
 イメージ サービスを使用するには、プロジェクトに次のヘッダーの一部またはすべてを含める必要があります。

- **既知のイメージIds.h**

  - 組み込みのイメージ カタログ**KnownMonikers**を使用する場合は必須ですが **、IVsHierarchy GetGuidProperty**または**GetProperty**呼び出しから値を返す場合など **、ImageMoniker**型を使用することはできません。

- **既知のモニカーズ.h**

  - 組み込みのイメージ カタログ**KnownMonikers**を使用する場合は必須です。

- **イメージパラメーター140.h**

  - **イメージモニカ**ーと**イメージ属性**の型を使用する場合は必須です。

- **VSShell140.h**

  - **IVsImageService2**型を使用する場合は必須です。

- **ユーティリティ.h**

  - イメージ サービスでテーマを処理できない場合に必要です。

  - イメージ サービスがイメージテーマを処理できる場合は、このヘッダーを使用しないでください。

::: moniker range="vs-2017"
- **を使用します。**

  - DPI ヘルパーを使用して現在の DPI を取得する場合は必須です。

::: moniker-end

::: moniker range=">=vs-2019"
- **フズピアウェアネス.h**

  - DPI 認識ヘルパーを使用して現在の DPI を取得する場合は必須です。

::: moniker-end

## <a name="how-do-i-write-new-wpf-ui"></a>新しい WPF UI を記述する方法

1. まず、上記の最初の手順のセクションで必要なアセンブリ参照をプロジェクトに追加します。 すべてのファイルを追加する必要はありませんので、必要な参照だけを追加してください。 (注:**ブラシ**の代わりに**色**を使用している場合や、アクセス権がある場合は、コンバータは必要ないので **、ユーティリティ**への参照をスキップできます。

2. 目的の画像を選択し、そのモニカーを取得します。 既知の画像やモニカーがある場合は、既知**のモニカ**ーを使用するか、独自のイメージを使用します。

3. **XAML にクリスプイメージズ**を追加します。 (以下の例を参照してください。

4. UI 階層で**イメージを設定します**。 (これは、**必ずしもCrispImage**上ではなく、背景色が既知の場所に設定する必要があります。(以下の例を参照してください。

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

 **既存の WPF UI を更新する方法**

 既存の WPF UI の更新は、3 つの基本的な手順で構成される比較的単純なプロセスです。

1. UI\<内のすべてのイメージ>要素を\<CrispImage>要素に置き換えます。

2. すべてのソース属性をモニカー属性に変更します。

    - イメージが変更されずに**KnownMonikers**を使用している場合は、そのプロパティを**KnownMoniker**に静的にバインドします。 (上記の例を参照してください。

    - イメージが変更されず、独自のカスタム イメージを使用している場合は、独自のモニカーに静的にバインドします。

    - イメージが変更できる場合は、プロパティの変更を通知するコード プロパティに Moniker 属性をバインドします。

3. UI 階層のどこかで、色の反転が正しく動作するように**イメージテーマユーティリティ.ImageBackgroundColor**を設定します。

    - この場合 **、クラスを**使用する必要があります。 (上記の例を参照してください。

## <a name="how-do-i-update-win32-ui"></a>Win32 UI を更新する方法
 イメージの未加工の読み込みを置き換えるために、適切な場所に次のコードを追加します。 必要に応じて、HBITMAPs 対 HICON 対 HIMAGELIST を返す値を切り替えます。

 **イメージ サービスを取得する**

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

## <a name="how-do-i-update-winforms-ui"></a>WinForms UI を更新する方法
 イメージの未加工の読み込みを置き換えるために、適切な場所に次のコードを追加します。 必要に応じて、ビットマップとアイコンを返す値を切り替えます。

 **ステートメントの使用に役立ちます**

```csharp
using GelUtilities = Microsoft.Internal.VisualStudio.PlatformUI.Utilities;
```

 **イメージ サービスを取得する**

```csharp
// This or your preferred way of querying for Visual Studio services
IVsImageService2 imageService = (IVsImageService2)Package.GetGlobalService(typeof(SVsImageService));

```

 **画像をリクエストする**

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

## <a name="how-do-i-use-image-monikers-in-a-new-tool-window"></a>新しいツール ウィンドウでイメージ モニカを使用する方法
 VSIX パッケージ プロジェクト テンプレートが更新されました。 新しいツール ウィンドウを作成するには、VSIX プロジェクトを右クリックし、[**新しい項目**の**追加** > ] (**Ctrl**+**Shift**+**A**) を選択します。 プロジェクト言語の [機能拡張] ノードで、[**カスタム ツール ウィンドウ**] を選択し、ツール ウィンドウに名前を付けて **[追加**] ボタンをクリックします。

 これらは、ツール ウィンドウでモニカーを使用する重要な場所です。 それぞれの手順に従います。

1. タブが十分に小さくなったときのツール ウィンドウ タブ **(Ctrl**+**タブ**ウィンドウ スイッチャーでも使用)。

    次の行を **、ToolWindowPane**型から派生するクラスのコンストラクターに追加します。

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   this.BitmapImageMoniker = KnownMonikers.Blank;
   ```

2. ツール ウィンドウを開くコマンド。

    パッケージの *.vsct*ファイルで、ツール ウィンドウのコマンド ボタンを編集します。

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

   **既存のツール ウィンドウでイメージ モニカを使用する方法**

   イメージ モニカーを使用するように既存のツール ウィンドウを更新する手順は、新しいツール ウィンドウを作成する手順に似ています。

   これらは、ツール ウィンドウでモニカーを使用する重要な場所です。 それぞれの手順に従います。

3. タブが十分に小さくなったときのツール ウィンドウ タブ **(Ctrl**+**タブ**ウィンドウ スイッチャーでも使用)。

   1. **ToolWindowPane**型から派生するクラスのコンストラクターで、次の行 (存在する場合) を削除します。

       ```csharp
       this.BitmapResourceID = <Value>;
       this.BitmapIndex = <Value>;
       ```

   2. 「新しいツール ウィンドウでイメージ モニカを使用する方法」の手順#1を参照してください。 上のセクション。

4. ツール ウィンドウを開くコマンド。

   - 「新しいツール ウィンドウでイメージ モニカを使用する方法」の手順#2を参照してください。 上のセクション。

## <a name="how-do-i-use-image-monikers-in-a-vsct-file"></a>vsct ファイルでイメージ モニカを使用する方法
 以下のコメント行で示されているように *、.vsct*ファイルを更新します。

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

 **以前のバージョンの Visual Studio でファイルを読み取る必要がある場合は、どうなりますか?**

 以前のバージョンの Visual Studio では **、IconIsMoniker**コマンド フラグは認識されません。 イメージ サービスのイメージは、イメージ サービスをサポートするバージョンの Visual Studio で使用できますが、古いバージョンの Visual Studio では引き続き古いスタイルのイメージを使用できます。 これを行うには *、.vsct*ファイルを変更せずに (したがって、Visual Studio の古いバージョンと互換性があります)、.vsct ファイルの\<ビットマップ>要素で定義された GUID と ID *.vsct*のペアからイメージ モニカーの GUID/ID ペアにマップする CSV (コンマ区切り値) ファイルを作成します。

 マッピング CSV ファイルの形式は次のとおりです。

```
Icon guid, Icon id, Moniker guid, Moniker id
b714fcf7-855e-4e4c-802a-1fd87144ccad,1,fda30684-682d-421c-8be4-650a2967058e,100
b714fcf7-855e-4e4c-802a-1fd87144ccad,2,fda30684-682d-421c-8be4-650a2967058e,200
```

 CSV ファイルはパッケージと共に配置され、その場所は **、パッケージ**属性の**アイコン マッピング ファイル名**プロパティで指定されます。

```csharp
[ProvideMenuResource("MyPackage.ctmenu", 1, IconMappingFilename="IconMappings.csv")]
```

 **IconMappingFilename**は、暗黙的に $PackageFolder$ にルートされる相対パス (上記の例のように) か、環境変数によって定義されたディレクトリに明示的にルートされている絶対パスです *。*

## <a name="how-do-i-port-a-project-system"></a>プロジェクト システムを移植する方法
 **プロジェクトに ImageMonikers を提供する方法**

1. プロジェクトの**IVsHierarchy**に**VSHPROPID_SupportsIconMonikers**を実装し、true を返します。

2. **VSHPROPID_IconMonikerImageList** (元のプロジェクト**が VSHPROPID_IconImgList**使用されている場合) または**VSHPROPID_IconMonikerGuid**、 **VSHPROPID_IconMonikerId**、 **VSHPROPID_OpenFolderIconMonikerGuid VSHPROPID_OpenFolderIconMonikerId**( 元のプロジェクトが**VSHPROPID_IconHandle**使用されている場合は**VSHPROPID_OpenFolderIconHandle**) を実装します 。 **VSHPROPID_OpenFolderIconMonikerId**

3. アイコンの元の VSHPROPID の実装を変更して、拡張ポイントが要求する場合は、アイコンの「レガシー」バージョンを作成します。 **IVsImageService2**は、これらのアイコンを取得するために必要な機能を提供します。

   **VB/C# プロジェクト フレーバーに関する追加要件**

   プロジェクトが**最も外側のフレーバー**であることを検出した場合にのみ **、VSHPROPID_SupportsIconMonikers**を実装します。 そうしないと、実際の最も外側のフレーバーがイメージモニカーを実際にサポートしないことがあり、あなたの基本フレーバーは、カスタマイズされた画像を効果的に「隠す」可能性があります。

   **CPSでイメージモニカーを使用するにはどうすればよいですか?**

   CPS (共通プロジェクト システム) のカスタム イメージの設定は、手動で行うか、プロジェクト システム拡張機能 SDK に付属の項目テンプレートを使用して行うことができます。

   **プロジェクト システム拡張機能 SDK の使用**

   CPS イメージをカスタマイズするには、「[プロジェクトの種類/項目の種類にカスタム アイコンを指定](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/scenario/provide_custom_icons_for_the_project_or_item_type.md)する」の手順に従います。 CPS の詳細については[、Visual Studio プロジェクト システムの機能拡張に関するドキュメントを参照してください。](https://github.com/Microsoft/VSProjectSystem)

   **イメージモニカーを手動で使用する**

4. プロジェクト システムで**IProjectTreeModifier**インターフェイスを実装およびエクスポートします。

5. 使用する**既知のモニカ**ーまたはカスタム イメージ モニカーを決定します。

6. **ApplyModifications**メソッドで、次の例のように、新しいツリーを返す前に、メソッド内の次の操作を行います。

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   tree = tree.SetIcon(KnownMonikers.Blank.ToProjectSystemType());
   ```

7. 新しいツリーを作成する場合は、次の例のように、目的のモニカーを NewTree メソッドに渡してカスタム イメージを設定できます。

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

## <a name="how-do-i-convert-from-a-real-image-strip-to-a-moniker-based-image-strip"></a>実際のイメージ ストリップからモニカー ベースのイメージ ストリップに変換する方法
 **私はヒマゲリスをサポートする必要があります**

 イメージ サービスを使用するために更新するコードの既存のイメージ ストリップが既にあるが、イメージ リストを渡す必要がある API によって制約されている場合でも、イメージ サービスの利点を得ることができます。 モニカーベースのイメージ ストリップを作成するには、次の手順に従って、既存のモニカーからマニフェストを作成します。

1. イメージ ストリップを渡して、**マニフェストリソース**ツールを実行します。 これにより、ストリップのマニフェストが生成されます。

   - 推奨: マニフェストの使用法に合わせて既定以外の名前を指定してください。

2. を使用している場合は、**次**の操作を行います。

   - マニフェストの\<[イメージ>] セクション\<を[イメージ/>に置き換えます。

   - すべてのサブイメージ ID を削除します (\<イメージトリップ名>_##)。

   - 推奨: 使用法に合わせて AssetsGuid シンボルとイメージ ストリップ シンボルの名前を変更します。

   - 各**包含イメージ**の GUID を $(ImageCatalogGuid) に置き換え、各**包含イメージ**の ID を $(\<モニカ>)に置き換え、各包含イメージに外部="true" 属性を追加**します。**

       - \<モニカー>は、画像に一致する**KnownMoniker**に置き換える必要がありますが、「既知のモニカー」に置き換える必要があります。 名前から削除されます。

   - <インポート マニフェストを追加します="$(\\マニフェストフォルダー)<相対インストール\>ディレクトリ パスに * \VisualStudio.ImageCatalog.imagemanifest" /\*> をシンボル> セクションの先頭に追加します。 \<

       - 相対パスは、マニフェストのセットアップ オーサリングで定義された配置場所によって決まります。

3. 既存のコードがイメージ ストリップのイメージ サービスを照会するために使用できるモニカーを持つラッパーを生成するには **、ManifestToCode**ツールを実行します。

   - 推奨: ラッパーと名前空間の使用法に合わせて、デフォルト以外の名前を指定してください。

4. イメージ サービスと新しいファイルを操作するために、すべての追加、オーサリング/配置、およびその他のコードの変更を行います。

   内部と外部の両方のイメージを含むマニフェストのサンプルは、次のようになります。

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

 **私はヒマゲリスをサポートする必要はありません**

1. 画像ストリップ内の画像に一致する**KnownMonikers**のセットを決定するか、画像ストリップ内の画像用に独自のモニカーを作成します。

2. イメージ ストリップの必要なインデックスでイメージを取得するために使用したマッピングを更新して、モニカーを使用します。

3. 更新されたマッピングを介してモニカーを要求するイメージ サービスを使用するコードを更新します。 (これは、マネージ コード用の**CrispImages**に更新するか、イメージ サービスから HBITMAPs または HICON を要求してネイティブ コードに渡すことを意味します)。

## <a name="testing-your-images"></a>画像のテスト
 イメージ ライブラリ ビューアー ツールを使用して、イメージ マニフェストをテストして、すべてが正しく作成されていることを確認できます。 このツールは[、Visual Studio 2015 SDK](visual-studio-sdk.md)で見つけることができます。 このツールおよびその他のドキュメントは[、こちら](/visualstudio/extensibility/internals/vssdk-utilities?view=vs-2015)にあります。

## <a name="additional-resources"></a>その他のリソース

### <a name="samples"></a>サンプル
 GitHub の Visual Studio サンプルの一部が更新され、さまざまな Visual Studio の機能拡張ポイントの一部としてイメージ サービスを使用する方法が示されました。

 最新[http://github.com/Microsoft/VSSDK-Extensibility-Samples](https://github.com/Microsoft/VSSDK-Extensibility-Samples)のサンプルを確認します。

### <a name="tooling"></a>ツール
 イメージ サービスで動作する UI の作成と更新を支援するために、イメージ サービスのサポート ツールのセットが作成されました。 各ツールの詳細については、ツールに付属のマニュアルを参照してください。 ツールは[、Visual Studio 2015 SDK](visual-studio-sdk.md)の一部として含まれています。

 **リソースからマニフェスト**

 リソースからのマニフェスト ツールは、イメージ リソース (PNG または XAML) の一覧を取得し、イメージ サービスでそれらのイメージを使用するためのイメージ マニフェスト ファイルを生成します。

 **マニフェストコード**

 マニフェストからコードへのツールは、イメージ マニフェスト ファイルを受け取り、コード (C++、C#、または VB) または *.vsct*ファイルでマニフェスト値を参照するためのラッパー ファイルを生成します。

 **イメージライブラリビューア**

 イメージ ライブラリ ビューアー ツールは、イメージ マニフェストを読み込み、ユーザーが Visual Studio でマニフェストが正しく作成されていることを確認するのと同じ方法で、それらを操作できるようにします。 ユーザーは、背景、サイズ、DPI 設定、ハイ コントラスト、およびその他の設定を変更できます。 また、マニフェストでエラーを検出するための読み込み情報を表示し、マニフェスト内の各イメージのソース情報を表示します。

## <a name="faq"></a>よく寄せられる質問

- 参照の組み込み="VisualStudio.*を読み込むとき\<に含める必要がある依存関係はありますか。相互運用.14.0.デザインタイム"/>?

  - すべての相互運用 DLL に対して埋め込み相互運用性タイプ="true" を設定します。

- 拡張機能を使用してイメージ マニフェストを配置するにはどうすればよいですか。

  - プロジェクトに *.imagemanifest*ファイルを追加します。

  - "VSIX に含める" を True に設定します。

- CPSプロジェクトシステムを更新しています。 **イメージネーム**と**ストックアイコンサービスはどうなりました**か?

  - これらは、モニカーを使用するように CPS が更新されたときに削除されました。 必要な呼び出しをする必要はありません、 **StockIconService**、 CPS ユーティリティの**ToProjectSystemType()** 拡張メソッドを使用してメソッドまたはプロパティに目的の**既知のモニカ**ーを渡すだけです。 **イメージ名**から**既知のモニカー**へのマッピングは以下のとおりです。

    |||
    |-|-|
    |**ImageName**|**既知のモニカー**|
    |イメージ名.オフラインウェブアプリ|既知のイメージId.Web|
    |フォルダ|既知のイメージId.Web|
    |フォルダを開く|フォルダーが開きました|
    |ファイル名を指定します。|既知のイメージId.リファレンス|
    |参照|既知のイメージId.リファレンス|
    |イメージネーム.Sdlウェブリファレンス|既知のイメージId.Web 参照フォルダー|
    |イメージネーム.ディスコウェブリファレンス|既知のイメージId.動的証拠開示ドキュメント|
    |フォルダ|フォルダークローズ|
    |フォルダを開く|フォルダーが開きました|
    |除外フォルダ|既知のイメージId.隠しフォルダ閉じました|
    |ファイル名をクリックします。|既知のイメージId.隠しフォルダが開かれました|
    |除外ファイル|ファイルの種類|
    |ファイルに依存するファイル|ファイルを生成します。|
    |ファイルが見つかりません。|既知のイメージId.ドキュメント警告|
    |ウィンドウズフォーム|既知のイメージ Id.ウィンドウズ フォーム|
    |コントロール|既知のイメージId.ユーザー コントロール|
    |をクリックします。|コンポーネントファイル|
    |Xml スキーマ|既知のイメージId.XML スキーマ|
    |ファイル名|ファイル|
    |ウェブフォーム|既知のイメージId.Web|
    |イメージネーム.ウェブサービス|既知のイメージId.Web サービス|
    |コントロール|既知のイメージId.Web ユーザー コントロール|
    |コントロール|コントロールを使用します。|
    |イメージ名.AspPage|既知のイメージId.ASP ファイル|
    |クラス名|ファイルを指定します。|
    |ウェブコンフィグ|構成ファイル|
    |イメージ名.Html ページ|ファイルを見る|
    |スタイルシート|スタイルシート|
    |ファイル名|既知のイメージId.JS スクリプト|
    |テキストファイル|既知のイメージId.ドキュメント|
    |設定ファイル|設定|
    |リソース名|既知のイメージId.ドキュメント グループ|
    |ビットマップ|イメージ|
    |アイコン|アイコンファイル|
    |イメージ名.イメージ|イメージ|
    |イメージネーム.イメージマップ|イメージマップ ファイル|
    |イメージネーム.Xワールド|既知のイメージId.Xワールドファイル|
    |オーディオ|サウンドを認識しています。|
    |ビデオ|メディアを認識しています。|
    |イメージ名.キャブ|既知のイメージId.CAB プロジェクト|
    |イメージ名.ジャー|既知のイメージId.JAR ファイル|
    |データ環境|データテーブル|
    |ファイル名|レポート|
    |イメージネーム.ダングルリファレンス|既知のイメージId.参照警告|
    |ファイル名|既知のイメージId.XSL 変換|
    |カーソル|カーソルを置くファイル|
    |を指定します。|プロパティ|
    |データ名|データベース|
    |アプリケーション名|アプリケーション|
    |データセット|データベース グループ|
    |イメージ名.Pfx|証明書|
    |イメージネーム.Snk|ルールを認識しています。|
    |イメージ名.ビジュアルベーシックプロジェクト|既知のイメージ Id.VB プロジェクト ノード|
    |イメージ名.CSharpプロジェクト|既知のイメージ Id.CS プロジェクト ノード|
    |空のイメージ名|既知のイメージIds.ブランク|
    |フォルダが見つかりません。|フォルダーオフライン|
    |参照を共有します。|共有プロジェクト|
    |イメージ名.共有投影|既知のイメージId.CSシェアードプロジェクト|
    |を共有します。|既知のイメージId.CPPシェアードプロジェクト|
    |共有プロジェクト|プロジェクトを認識します。|
    |ファイル名|を指定します。|
    |ファイル名を指定します。|ファイルノード|

  - 完了リスト のプロバイダを更新しています。 既知**のモニカーが**古い**標準グリフグループと標準グリフ**の値に一致**するもの**は何ですか?

    ||||
    |-|-|-|
    |クラス|アイテムを公開する|クラスパブリック|
    |クラス|内部のアイテム|クラス内部|
    |クラス|アイテムフレンド|クラス内部|
    |クラス|保護されたアイテム|クラスプロテクト|
    |クラス|プライベートなアイテム|クラスプライベート|
    |クラス|ショートカット|クラスショートカット|
    |定数|アイテムを公開する|定数公開|
    |定数|内部のアイテム|コンスタント内部|
    |定数|アイテムフレンド|コンスタント内部|
    |定数|保護されたアイテム|定数プロテクト|
    |定数|プライベートなアイテム|コンスタントプライベート|
    |定数|ショートカット|定数ショートカット|
    |グループデリゲート|アイテムを公開する|代理人公開|
    |グループデリゲート|内部のアイテム|内部委任|
    |グループデリゲート|アイテムフレンド|内部委任|
    |グループデリゲート|保護されたアイテム|デリゲートプロテクト|
    |グループデリゲート|プライベートなアイテム|プライベートデリゲート|
    |グループデリゲート|ショートカット|委任ショートカット|
    |グループ列挙|アイテムを公開する|列挙体公開|
    |グループ列挙|内部のアイテム|列挙内部|
    |グループ列挙|アイテムフレンド|列挙内部|
    |グループ列挙|保護されたアイテム|列挙プロテクト|
    |グループ列挙|プライベートなアイテム|列挙プライベート|
    |グループ列挙|ショートカット|列挙ショートカット|
    |メンバーを構成します。|アイテムを公開する|列挙項目のパブリック|
    |メンバーを構成します。|内部のアイテム|列挙項目内部|
    |メンバーを構成します。|アイテムフレンド|列挙項目内部|
    |メンバーを構成します。|保護されたアイテム|列挙項目プロテクト|
    |メンバーを構成します。|プライベートなアイテム|列挙アイテムプライベート|
    |メンバーを構成します。|ショートカット|列挙項目ショートカット|
    |グリフグループイベント|アイテムを公開する|イベントパブリック|
    |グリフグループイベント|内部のアイテム|イベント内部|
    |グリフグループイベント|アイテムフレンド|イベント内部|
    |グリフグループイベント|保護されたアイテム|イベントプロテクト|
    |グリフグループイベント|プライベートなアイテム|イベントプライベート|
    |グリフグループイベント|ショートカット|イベントショートカット|
    |グループの例外|アイテムを公開する|例外公開|
    |グループの例外|内部のアイテム|例外内部|
    |グループの例外|アイテムフレンド|例外内部|
    |グループの例外|保護されたアイテム|例外プロテクト|
    |グループの例外|プライベートなアイテム|例外プライベート|
    |グループの例外|ショートカット|例外ショートカット|
    |グリフグループフィールド|アイテムを公開する|フィールドパブリック|
    |グリフグループフィールド|内部のアイテム|フィールド内部|
    |グリフグループフィールド|アイテムフレンド|フィールド内部|
    |グリフグループフィールド|保護されたアイテム|フィールドプロテクト|
    |グリフグループフィールド|プライベートなアイテム|フィールドプライベート|
    |グリフグループフィールド|ショートカット|フィールドショートカット|
    |グループインターフェイス|アイテムを公開する|インターフェイスパブリック|
    |グループインターフェイス|内部のアイテム|インターフェイス内部|
    |グループインターフェイス|アイテムフレンド|インターフェイス内部|
    |グループインターフェイス|保護されたアイテム|インターフェイスプロテクト|
    |グループインターフェイス|プライベートなアイテム|インターフェイスプライベート|
    |グループインターフェイス|ショートカット|インターフェイスショートカット|
    |グリフグループマクロ|アイテムを公開する|マクロパブリック|
    |グリフグループマクロ|内部のアイテム|マクロ内部|
    |グリフグループマクロ|アイテムフレンド|マクロ内部|
    |グリフグループマクロ|保護されたアイテム|マクロプロテクト|
    |グリフグループマクロ|プライベートなアイテム|マクロプライベート|
    |グリフグループマクロ|ショートカット|マクロショートカット|
    |グリフグループマップ|アイテムを公開する|マップパブリック|
    |グリフグループマップ|内部のアイテム|内部マップ|
    |グリフグループマップ|アイテムフレンド|内部マップ|
    |グリフグループマップ|保護されたアイテム|マッププロテクト|
    |グリフグループマップ|プライベートなアイテム|マッププライベート|
    |グリフグループマップ|ショートカット|マップショートカット|
    |グループマップアイテム|アイテムを公開する|アイテムの公開|
    |グループマップアイテム|内部のアイテム|内部のアイテム|
    |グループマップアイテム|アイテムフレンド|内部のアイテム|
    |グループマップアイテム|保護されたアイテム|保護されたマップアイテム|
    |グループマップアイテム|プライベートなアイテム|プライベートなアイテム|
    |グループマップアイテム|ショートカット|ショートカット|
    |メソッド|アイテムを公開する|メソッドパブリック|
    |メソッド|内部のアイテム|メソッド内部|
    |メソッド|アイテムフレンド|メソッド内部|
    |メソッド|保護されたアイテム|MethodProtected|
    |メソッド|プライベートなアイテム|メソッドプライベート|
    |メソッド|ショートカット|メソッドショートカット|
    |グループオーバーロード|アイテムを公開する|メソッドパブリック|
    |グループオーバーロード|内部のアイテム|メソッド内部|
    |グループオーバーロード|アイテムフレンド|メソッド内部|
    |グループオーバーロード|保護されたアイテム|MethodProtected|
    |グループオーバーロード|プライベートなアイテム|メソッドプライベート|
    |グループオーバーロード|ショートカット|メソッドショートカット|
    |グリフグループモジュール|アイテムを公開する|モジュールパブリック|
    |グリフグループモジュール|内部のアイテム|モジュール内部|
    |グリフグループモジュール|アイテムフレンド|モジュール内部|
    |グリフグループモジュール|保護されたアイテム|モジュールプロテクト|
    |グリフグループモジュール|プライベートなアイテム|モジュールプライベート|
    |グリフグループモジュール|ショートカット|モジュールショートカット|
    |名前空間|アイテムを公開する|名前空間パブリック|
    |名前空間|内部のアイテム|名前空間内部|
    |名前空間|アイテムフレンド|名前空間内部|
    |名前空間|保護されたアイテム|名前空間プロテクト|
    |名前空間|プライベートなアイテム|名前空間プライベート|
    |名前空間|ショートカット|名前空間ショートカット|
    |グリフグループ演算子|アイテムを公開する|オペレーター公開|
    |グリフグループ演算子|内部のアイテム|オペレータ内部|
    |グリフグループ演算子|アイテムフレンド|オペレータ内部|
    |グリフグループ演算子|保護されたアイテム|オペレータ保護|
    |グリフグループ演算子|プライベートなアイテム|オペレータープライベート|
    |グリフグループ演算子|ショートカット|オペレーターショートカット|
    |プロパティ|アイテムを公開する|プロパティパブリック|
    |プロパティ|内部のアイテム|プロパティ内部|
    |プロパティ|アイテムフレンド|プロパティ内部|
    |プロパティ|保護されたアイテム|プロパティプロテクト|
    |プロパティ|プライベートなアイテム|プロパティプライベート|
    |プロパティ|ショートカット|プロパティショートカット|
    |クラス構造|アイテムを公開する|構造体パブリック|
    |クラス構造|内部のアイテム|構造内部|
    |クラス構造|アイテムフレンド|構造内部|
    |クラス構造|保護されたアイテム|構造保護|
    |クラス構造|プライベートなアイテム|構造プライベート|
    |クラス構造|ショートカット|構造ショートカット|
    |テンプレート|アイテムを公開する|テンプレート公開|
    |テンプレート|内部のアイテム|テンプレート内部|
    |テンプレート|アイテムフレンド|テンプレート内部|
    |テンプレート|保護されたアイテム|テンプレート保護|
    |テンプレート|プライベートなアイテム|テンプレートプライベート|
    |テンプレート|ショートカット|テンプレートショートカット|
    |グリフグループタイプデフ|アイテムを公開する|パブリック|
    |グリフグループタイプデフ|内部のアイテム|内部定義|
    |グリフグループタイプデフ|アイテムフレンド|内部定義|
    |グリフグループタイプデフ|保護されたアイテム|定義プロテクト|
    |グリフグループタイプデフ|プライベートなアイテム|型定義プライベート|
    |グリフグループタイプデフ|ショートカット|ショートカット|
    |グリフグループタイプ|アイテムを公開する|タイプパブリック|
    |グリフグループタイプ|内部のアイテム|型内部|
    |グリフグループタイプ|アイテムフレンド|型内部|
    |グリフグループタイプ|保護されたアイテム|保護された型|
    |グリフグループタイプ|プライベートなアイテム|タイププライベート|
    |グリフグループタイプ|ショートカット|ショートカットの種類|
    |グリフグループユニオン|アイテムを公開する|ユニオンパブリック|
    |グリフグループユニオン|内部のアイテム|ユニオン内部|
    |グリフグループユニオン|アイテムフレンド|ユニオン内部|
    |グリフグループユニオン|保護されたアイテム|ユニオンプロテクト|
    |グリフグループユニオン|プライベートなアイテム|ユニオンプライベート|
    |グリフグループユニオン|ショートカット|ユニオンショートカット|
    |グリフグループ変数|アイテムを公開する|フィールドパブリック|
    |グリフグループ変数|内部のアイテム|フィールド内部|
    |グリフグループ変数|アイテムフレンド|フィールド内部|
    |グリフグループ変数|保護されたアイテム|フィールドプロテクト|
    |グリフグループ変数|プライベートなアイテム|フィールドプライベート|
    |グリフグループ変数|ショートカット|フィールドショートカット|
    |値型|アイテムを公開する|パブリックな値型|
    |値型|内部のアイテム|内部の値型|
    |値型|アイテムフレンド|内部の値型|
    |値型|保護されたアイテム|保護された値の種類|
    |値型|プライベートなアイテム|プライベートな値型|
    |値型|ショートカット|値の種類ショートカット|
    |組み込みグリフグループ|アイテムを公開する|オブジェクトパブリック|
    |組み込みグリフグループ|内部のアイテム|オブジェクト内部|
    |組み込みグリフグループ|アイテムフレンド|オブジェクト内部|
    |組み込みグリフグループ|保護されたアイテム|オブジェクトプロテクト|
    |組み込みグリフグループ|プライベートなアイテム|オブジェクトプライベート|
    |組み込みグリフグループ|ショートカット|オブジェクトショートカット|
    |グリフグループJシャープメソッド|アイテムを公開する|メソッドパブリック|
    |グリフグループJシャープメソッド|内部のアイテム|メソッド内部|
    |グリフグループJシャープメソッド|アイテムフレンド|メソッド内部|
    |グリフグループJシャープメソッド|保護されたアイテム|MethodProtected|
    |グリフグループJシャープメソッド|プライベートなアイテム|メソッドプライベート|
    |グリフグループJシャープメソッド|ショートカット|メソッドショートカット|
    |グリフグループJシャープフィールド|アイテムを公開する|フィールドパブリック|
    |グリフグループJシャープフィールド|内部のアイテム|フィールド内部|
    |グリフグループJシャープフィールド|アイテムフレンド|フィールド内部|
    |グリフグループJシャープフィールド|保護されたアイテム|フィールドプロテクト|
    |グリフグループJシャープフィールド|プライベートなアイテム|フィールドプライベート|
    |グリフグループJシャープフィールド|ショートカット|フィールドショートカット|
    |グリフグループJシャープクラス|アイテムを公開する|クラスパブリック|
    |グリフグループJシャープクラス|内部のアイテム|クラス内部|
    |グリフグループJシャープクラス|アイテムフレンド|クラス内部|
    |グリフグループJシャープクラス|保護されたアイテム|クラスプロテクト|
    |グリフグループJシャープクラス|プライベートなアイテム|クラスプライベート|
    |グリフグループJシャープクラス|ショートカット|クラスショートカット|
    |名前空間|アイテムを公開する|名前空間パブリック|
    |名前空間|内部のアイテム|名前空間内部|
    |名前空間|アイテムフレンド|名前空間内部|
    |名前空間|保護されたアイテム|名前空間プロテクト|
    |名前空間|プライベートなアイテム|名前空間プライベート|
    |名前空間|ショートカット|名前空間ショートカット|
    |グリフグループJシャープインターフェイス|アイテムを公開する|インターフェイスパブリック|
    |グリフグループJシャープインターフェイス|内部のアイテム|インターフェイス内部|
    |グリフグループJシャープインターフェイス|アイテムフレンド|インターフェイス内部|
    |グリフグループJシャープインターフェイス|保護されたアイテム|インターフェイスプロテクト|
    |グリフグループJシャープインターフェイス|プライベートなアイテム|インターフェイスプライベート|
    |グリフグループJシャープインターフェイス|ショートカット|インターフェイスショートカット|
    |グループエラー||StatusError|
    |グリフブスクファイル||クラスファイル|
    |グリフアセンブリ||リファレンス|
    |グリフライブラリ||ライブラリ|
    |グリフVBプロジェクト||プロジェクトノード|
    |グリフクールプロジェクト||ノード|
    |グリフクッププロジェクト||CPPプロジェクトノード|
    |ダイアログボックスID||ダイアログ|
    |グリフオープンフォルダ||フォルダ開きました|
    |グリフクローズドフォルダ||閉じたフォルダ|
    |グリフアロー||次へ|
    |グリフシャープファイル||ファイルノード|
    |グリフシャープエクスパンション||スニペット|
    |グリフキーワード||インテライセンスキーワード|
    |グリフ情報||ステータス情報|
    |グリフリファレンス||クラスメソッドリファレンス|
    |グリフレキュアション||再帰|
    |グリフXmlアイテム||タグ|
    |グリフスイシャーププロジェクト||DocumentCollection|
    |ドキュメント||ドキュメント|
    |グリフフォワードタイプ||次へ|
    |呼び出し元グラフ||コールト|
    |グリフコールグラフ||コールフロ|
    |グリフの警告||StatusWarning|
    |グリフメイファレンスリファレンス||質問マーク|
    |呼び出し元||コールト|
    |グリフメイコー||コールフロ|
    |メソッド||拡張メソッド|
    |内部の内部||拡張メソッド|
    |グリフエクステンションメソッドフレンド||拡張メソッド|
    |メソッドを追加します。||拡張メソッド|
    |メソッドをプライベートにします。||拡張メソッド|
    |ショートカットを拡張します。||拡張メソッド|
    |属性||XmlAttribute|
    |グリフXmlチャイルド||XmlElement|
    |子孫||子孫の数|
    |名前空間||XmlNamespace|
    |質問||信頼性が低い|
    |属性チェック||高信頼感|
    |質問||信頼性の低い|
    |グリフXmlチャイルドチェック||高い信頼感|
    |質問||低信頼度|
    |子孫チェック||コンフィデンス|
    |グリフ完了警告||インテリンセンス警告|
