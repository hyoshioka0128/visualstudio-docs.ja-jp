---
title: イメージライブラリビューアー |Microsoft Docs
description: イメージマニフェストを読み込んで検索する Visual Studio イメージライブラリビューアーツールについて説明します。これにより、イメージの属性を表示および操作できるようになります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 9d9c7fbb-ebae-4b20-9dd8-3c9070c0d0d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d60443e97bc557bc964d59750417b2662e4c3c8f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085976"
---
# <a name="image-library-viewer"></a>イメージ ライブラリ ビューア
Visual Studio のイメージライブラリビューアーツールでは、イメージマニフェストを読み込んで検索することができます。これにより、Visual Studio の場合と同じ方法でユーザーが操作できるようになります。 ユーザーは、背景、サイズ、DPI、ハイコントラストなどの設定を変更できます。 このツールでは、各イメージマニフェストの読み込み情報も表示され、イメージマニフェスト内の各イメージのソース情報が表示されます。 このツールは、次の場合に役立ちます。

1. エラーの診断

2. カスタムイメージマニフェストで属性が正しく設定されていることを確認する

3. Visual studio の拡張機能が visual studio のスタイルに適合するイメージを使用できるように、Visual Studio のイメージカタログ内のイメージを検索する

   ![イメージ ライブラリ ビューアーのヒーロー](../../extensibility/internals/media/image-library-viewer-hero.png "イメージ ライブラリ ビューアーのヒーロー")

   **イメージモニカー**

   イメージモニカー (または short のモニカー) は、イメージライブラリ内のイメージアセットまたはイメージリスト資産を一意に識別する GUID: ID ペアです。

   **イメージマニフェストファイル**

   イメージマニフェスト (imagemanifest) ファイルは、一連のイメージアセット、それらのアセットを表すモニカー、および各資産を表す実際のイメージまたはイメージを定義する XML ファイルです。 イメージマニフェストでは、レガシ UI をサポートするために、スタンドアロンイメージまたはイメージリストを定義できます。 また、資産または各資産の背後にある個々の画像に対して設定できる属性があり、これらのアセットがどのように表示されるかや方法を変更できます。

   **イメージマニフェストスキーマ**

   イメージマニフェスト全体は次のようになります。

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Guid, ID, or String elements -->
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
|Guid|シンボルは GUID を表し、GUID の書式設定と一致する必要があります。|
|id|シンボルは ID を表し、負でない整数である必要があります。|
|String|シンボルは、任意の文字列値を表します。|

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
|システム|Windows\System32 フォルダー|
|WinDir|% WinDir% 環境変数の値|

 **Image**

 要素は、 \<Image> モニカーによって参照できるイメージを定義します。 イメージモニカーを形成する GUID と ID。 イメージのモニカーは、イメージライブラリ全体で一意である必要があります。 複数のイメージに特定のモニカーが含まれている場合は、ライブラリのビルド中に最初に検出されたものが保持されます。

 少なくとも1つのソースが含まれている必要があります。 サイズに依存しないソースは幅広いサイズで最適な結果を得られますが、必須ではありません。 サービスが要素で定義されていないサイズのイメージを要求され、 \<Image> サイズに依存しないソースが存在しない場合、サービスは最適なサイズ固有のソースを選択し、要求されたサイズにスケーリングします。

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|**属性**|**定義**|
|-|-|
|Guid|必要イメージモニカーの GUID 部分|
|id|必要イメージモニカーの ID 部分|
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
|Uri|必要イメージの読み込み元となる場所を定義する URI。 次のいずれかを指定できます。<br /><br /> -Application:///機関を使用する[パック URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf)<br /><br /> -コンポーネントの絶対リソース参照<br /><br /> -ネイティブリソースを含むファイルへのパス|
|バックグラウンド|Optionalソースの使用を想定している背景の種類を示します。<br /><br /> 次のいずれかを指定できます。<br /><br /> - *Light*: 光源はライトバックで使用できます。<br /><br /> - *ダーク*: ソースは、濃色の背景で使用できます。<br /><br /> - *Systeminformation.highcontrast*: ソースはハイコントラストモードの任意のバックグラウンドで使用できます。<br /><br /> - *HighContrastLight*: ソースはハイコントラストモードのライトバックで使用できます。<br /><br /> -*HighContrastDark*: ソースはハイコントラストモードでダークバックグラウンドで使用できます。<br /><br /> **Background** 属性が省略されている場合は、任意のバックグラウンドでソースを使用できます。<br /><br /> **Background** 、 *Dark*、 *HighContrastLight*、または *HighContrastDark**の場合*、ソースの色は反転されません。 **Background** が省略されている場合、または *systeminformation.highcontrast* に設定されている場合、ソースの色の反転は、イメージの **allowcolorinversion** 属性によって制御されます。|

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
|id|必要ネイティブリソースの整数の ID 部分|

 **ImageList**

 要素は、 \<ImageList> 1 つのストリップで返すことができるイメージのコレクションを定義します。 ストリップは必要に応じて構築されます。

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|**属性**|**定義**|
|-|-|
|Guid|必要イメージモニカーの GUID 部分|
|id|必要イメージモニカーの ID 部分|
|外部|[省略可能、既定値は false]イメージモニカーが現在のマニフェスト内のイメージを参照しているかどうかを示します。|

 含まれているイメージのモニカーは、現在のマニフェストで定義されているイメージを参照する必要がありません。 含まれているイメージがイメージライブラリに見つからない場合は、空白のプレースホルダーイメージが代わりに使用されます。

## <a name="how-to-use-the-tool"></a>ツールの使用方法
 **カスタムイメージマニフェストの検証**

 カスタムマニフェストを作成するには、ManifestFromResources ツールを使用してマニフェストを自動生成することをお勧めします。 カスタムマニフェストを検証するには、イメージライブラリビューアーを起動し、[ファイル] > [パスの設定...] を選択します。を選択すると、[ディレクトリの検索] ダイアログボックスが開きます。 このツールでは、検索ディレクトリを使用してイメージマニフェストを読み込みますが、それを使用してマニフェスト内のイメージを含む .dll ファイルを検索します。そのため、このダイアログにはマニフェストと DLL の両方のディレクトリが含まれている必要があります。

 ![イメージ ライブラリ ビューアーの検索](../../extensibility/internals/media/image-library-viewer-search.png "イメージ ライブラリ ビューアーの検索")

 [ **追加** ] をクリックして新しい検索ディレクトリを選択し、マニフェストとそれに対応する dll を検索します。 このツールでは、これらの検索ディレクトリが記憶され、ディレクトリのチェックボックスをオンまたはオフにすることで、これらのディレクトリを有効または無効にすることができます。

 既定では、ツールは Visual Studio のインストールディレクトリを検索し、これらのディレクトリを検索ディレクトリの一覧に追加しようとします。 ツールによって検出されないディレクトリを手動で追加することができます。

 すべてのマニフェストが読み込まれたら、ツールを使用してイメージの **背景** 色、 **DPI**、 **ハイコントラスト**、または **グレースケール** を切り替えることができます。これにより、ユーザーはイメージ資産を視覚的に調べて、さまざまな設定に対して正しくレンダリングされていることを確認できます。

 ![イメージ ライブラリ ビューアーの背景](../../extensibility/internals/media/image-library-viewer-background.png "イメージ ライブラリ ビューアーの背景")

 背景色は、ライト、ダーク、またはカスタム値に設定できます。 [ユーザー設定の色] を選択すると、色の選択ダイアログが開き、後で簡単に再呼び出しできるように、[背景] コンボボックスの下部にそのカスタム色が追加されます。

 ![イメージ ライブラリ ビューアーのカスタム色](../../extensibility/internals/media/image-library-viewer-custom-color.png "イメージ ライブラリ ビューアーのカスタム色")

 イメージモニカーを選択すると、右側の [イメージの詳細] ウィンドウにモニカーの背後にある各実際のイメージの情報が表示されます。 このウィンドウでは、ユーザーが名前または未加工の GUID: ID 値を使用してモニカーをコピーすることもできます。

 ![イメージ ライブラリ ビューアーのイメージの詳細](../../extensibility/internals/media/image-library-viewer-image-details.png "イメージ ライブラリ ビューアーのイメージの詳細")

 各イメージソースに対して表示される情報には、表示する背景の種類、テーマを使用できるかハイコントラストサポートするか、またはサイズに依存しないかどうか、およびイメージがネイティブアセンブリから取得されるかどうかが含まれます。

 ![イメージ ライブラリ ビューアーにテーマを設定可能](../../extensibility/internals/media/image-library-viewer-can-theme.png "イメージ ライブラリ ビューアーにテーマを設定可能")

 イメージマニフェストを検証するときは、実際の場所にマニフェストとイメージ DLL を配置することをお勧めします。 これにより、相対パスが正常に機能していること、およびイメージライブラリがマニフェストとイメージの DLL を見つけて読み込むことができることが確認されます。

 **イメージカタログ KnownMonikers を検索しています**

 Visual studio のスタイルに適合するように、visual studio 拡張機能では、独自のを作成して使用するのではなく、visual Studio のイメージカタログのイメージを使用できます。 これには、これらのイメージを維持する必要がなく、Visual Studio でサポートされているすべての DPI 設定で適切に見えるように、イメージが高 DPI のバッキングイメージを持つことが保証されるという利点があります。

 イメージライブラリビューアーでは、ユーザーがイメージアセットを表すモニカーを見つけて、そのモニカーをコードで使用できるように、マニフェストを検索できます。 画像を検索するには、検索ボックスに目的の検索語句を入力し、enter キーを押します。 下部のステータスバーには、すべてのマニフェストの合計イメージから見つかった一致の数が表示されます。

 ![イメージ ライブラリ ビューアーのフィルター](../../extensibility/internals/media/image-library-viewer-filter.png "イメージ ライブラリ ビューアーのフィルター")

 既存のマニフェストでイメージモニカーを検索する場合は、Visual Studio イメージカタログのモニカー、他の意図的にパブリックにアクセスできるモニカー、または独自のカスタムモニカーだけを検索して使用することをお勧めします。 非パブリックモニカーを使用すると、カスタム UI が破損したり、非パブリックモニカーやイメージが変更または更新されたりした場合に、予期しない方法でイメージが変更される可能性があります。

 また、GUID で検索することもできます。 この種の検索は、リストを1つのマニフェストにフィルター処理する場合、またはマニフェストに複数の Guid が含まれている場合にマニフェストのサブセクションを絞り込む場合に便利です。

 ![イメージ ライブラリ ビューアーのフィルター GUID](../../extensibility/internals/media/image-library-viewer-filter-guid.png "イメージ ライブラリ ビューアーのフィルター GUID")

 最後に、ID で検索することもできます。

 ![イメージ ライブラリ ビューアーのフィルター ID](../../extensibility/internals/media/image-library-viewer-filter-id.png "イメージ ライブラリ ビューアーのフィルター ID")

## <a name="notes"></a>メモ

- 既定では、ツールは Visual Studio のインストールディレクトリに存在する複数のイメージマニフェストを取得します。 一般公開されているモニカーを持つ唯一のものは、 **VisualStudio ImageCatalog** マニフェストです。 GUID: ae27a6b0-e345-4288-96df-5eaf394ee369 (カスタムマニフェストでこの GUID をオーバーライドし **ません** ) 型: knownmonikers

- 検出されたすべてのイメージマニフェストを読み込むために起動が試行されるため、アプリケーションが実際に表示されるまでに数秒かかることがあります。 マニフェストの読み込み中に、処理速度が低下したり、応答しなくなったりすることもあります。

## <a name="sample-output"></a>出力例
 このツールでは、出力は生成されません。
