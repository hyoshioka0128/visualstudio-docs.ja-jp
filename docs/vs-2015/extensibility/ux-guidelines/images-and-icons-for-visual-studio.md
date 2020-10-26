---
title: イメージとアイコン
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: f410325e-9cf2-4f39-b6d7-b672121c2691
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cb2f209e212406fd9809ecb4bd30bce30d95a2bf
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85544795"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio のイメージとアイコン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="image-use-in-visual-studio"></a><a name="BKMK_ImageUseInVisualStudio"></a> Visual Studio でのイメージの使用
 アートワークを作成する前に、 [Visual Studio イメージライブラリ](https://www.microsoft.com/download/details.aspx?id=35825)で1000以上のイメージを使用することを検討してください。

### <a name="types-of-images"></a>画像の種類

- **アイコン**。 コマンド、階層、テンプレートなどに表示される小さい画像。 Visual Studio で使用される既定のアイコンサイズは16x16 の PNG です。 イメージサービスによって生成されるアイコンは、HDPI サポートの XAML 形式を自動的に生成します。

     **注:** イメージはメニューシステムで使用されますが、すべてのコマンドに対してアイコンを作成することはできません。 コマンドにアイコンが表示されるかどうかを確認するには、 [Visual Studio のメニューとコマンド](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md) を参照してください。

- **サムネイル.** [新しいプロジェクト] ダイアログボックスなど、ダイアログのプレビュー領域で使用される画像。

- **ダイアログイメージ。** 説明用のグラフィックまたはメッセージインジケーターとして、ダイアログまたはウィザードに表示される画像。 使用頻度が低い場合、または必要な場合にのみ使用して、困難な概念を示すか、ユーザーの注意を深めます (アラート、警告)。

- **アニメーション画像。** 進行状況インジケーター、ステータスバー、および操作ダイアログで使用されます。

- **求.** マウスを使用して操作が許可されるかどうかを示すために使用されます。オブジェクトの削除などが可能です。

## <a name="icon-design"></a><a name="BKMK_IconDesign"></a> アイコンのデザイン

### <a name="overview"></a>概要
 Visual Studio では、クリーンなジオメトリと50/50 の正/負 (明るい/濃色) のバランスを持つ最新のスタイルのアイコンが使用され、直接的でわかりやすい比喩が使用されます。 重要なアイコンデザインポイントは、わかりやすく、簡素化、およびコンテキストを中心にしています。

- **わかりやすさ:** アイコンの意味と個性を示す、主要な比喩に注目します。

- **単純化:** 必要な要素だけを使用してテーマを取得し、frills を使用せずに、その中心となる意味を持つようにアイコンを減らします。

- **コンテキスト:** アイコンの主要な比喩を構成する要素を決定するときに重要となる、概念の開発時のアイコンの役割のすべての側面を考慮します。

  アイコンを使用すると、次のようないくつかのデザインポイントを回避できます。

- 適切な場合を除き、UI 要素を示すアイコンは使用しないでください。 UI 要素が共通、明らか、または一意でない場合は、より抽象またはシンボリックアプローチを選択します。

- ドキュメント、フォルダー、矢印、虫眼鏡などの一般的な要素を使いすぎないようにしてください。 このような要素は、アイコンの意味に不可欠な場合にのみ使用してください。 たとえば、右に表示される虫眼鏡は、検索、参照、検索のみを示す必要があります。

- 一部のレガシアイコン要素ではパースペクティブの使用が維持されますが、要素の明確さが欠けていない限り、パースペクティブを持つ新しいアイコンを作成しないでください。

- 詰め込もうの情報がアイコンに多くなることはありません。 わかりやすいシンボルとして簡単に認識または学習できる単純なイメージは、非常に複雑なイメージよりもはるかに便利です。 アイコンがストーリー全体を示すことはできません。

### <a name="icon-creation"></a>アイコンの作成

#### <a name="concept-development"></a>概念開発
 Visual Studio の UI 内には、さまざまなアイコンの種類があります。 開発時にアイコンの種類を慎重に検討してください。 アイコン要素には、不明確な UI オブジェクトや一般的ではない UI オブジェクトを使用しないでください。 スマートタグアイコンなどを使用して、このような場合にシンボリックを選択します。 左側の抽象タグの意味は、右側のあいまいな UI ベースのバージョンよりも明確であることに注意してください。

|**シンボリック画像の適切な使用**|**シンボリック画像の不適切な使用**|
|-|-|
|![正しい [スマート タグ] アイコン](../../extensibility/ux-guidelines/media/0404-01-smarttagcorrect.png "0404-01_SmartTagCorrect")|![正しくない [スマート タグ] アイコン](../../extensibility/ux-guidelines/media/0404-02-smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 標準的でわかりやすい UI 要素がアイコンに適している場合があります。 ウィンドウの追加は、次の例の1つです。

|**アイコン内の正しい UI 要素**|**アイコンの UI 要素が正しくありません**|
|-|-|
|![正しい [ウィンドウの追加] アイコン](../../extensibility/ux-guidelines/media/0404-03-addwindowcorrect.png "0404-03_AddWindowCorrect")|![正しくない [ウィンドウの追加] アイコン](../../extensibility/ux-guidelines/media/0404-04-addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 アイコンの意味に不可欠でない限り、ドキュメントを基本要素として使用しないでください。 [ドキュメントの追加] にドキュメント要素がない場合 (下記)、意味は失われます。一方、[更新] を使用すると、ドキュメント要素は意味を伝える必要がありません。

|**ドキュメントアイコンの正しい使用**|**ドキュメントアイコンの不適切な使用**|
|-|-|
|![正しい [ドキュメント] アイコン](../../extensibility/ux-guidelines/media/0404-05-documenticoncorrect.png "0404-05_DocumentIconCorrect")|![正しくない [ドキュメント] アイコン](../../extensibility/ux-guidelines/media/0404-06-documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 "Show" の概念は、表示されている内容を示すアイコン ([すべてのファイルを表示] の例を含む) で表す必要があります。 レンズの比喩を使用すると、必要に応じて "view" の概念を示すことができます (リソースビューの例を参照)。

|**示**|**モード**|
|-|-|
|![表示アイコン](../../extensibility/ux-guidelines/media/0404-07-show.png "0404-07_Show")|![ビュー アイコン](../../extensibility/ux-guidelines/media/0404-08-view.png "0404-08_View")|

 右上の虫眼鏡アイコンは、検索、検索、および参照のみを表します。 正符号または負符号の付いた左側のバリアントは、ズームイン/ズームアウトのみを表します。

|**サーチ**|**倍率**|
|-|-|
|![[検索] アイコン](../../extensibility/ux-guidelines/media/0404-09-search.png "0404-09_Search")|![ズーム アイコン](../../extensibility/ux-guidelines/media/0404-10-zoom.png "0404-10_Zoom")|

 ツリービューでは、フォルダーアイコンと修飾子の両方を使用しないでください。 使用できる場合は、修飾子のみを使用します。

|**正しいツリービューのアイコン**|**ツリービューのアイコンが正しくありません**|
|-|-|
|![ツリービューの正しいアイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11-treeviewcorrect1.png "0404-11_TreeViewCorrect1") ![ツリービューの正しいアイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12-treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![無効なツリービューアイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13-treeviewincorrect1.png "0404-13_TreeViewIncorrect1") ![正しくないツリービューアイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14-treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>スタイルの詳細

#### <a name="layout"></a>Layout
 標準16x16 アイコンに表示されるスタック要素:

 ![16 x 16 のアイコンのレイアウト スタック](../../extensibility/ux-guidelines/media/0404-15-layoutstack.png "0404-15_LayoutStack")

 **16 x 16 のアイコンのレイアウト スタック**

 状態通知要素は、スタンドアロンアイコンとして使用することをお勧めします。 ただし、タスクの完了アイコンを使用するなど、基本要素で通知を積み重ねる必要があるコンテキストがあります。

 ![Visual Studio でのスタンドアロン通知](../../extensibility/ux-guidelines/media/0404-16-standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")

 **スタンドアロンの通知アイコン**

 ![[タスクの完了] アイコン](../../extensibility/ux-guidelines/media/0404-17-taskcomplete.png "0404-17_TaskComplete")

 **タスクの完了アイコン**

 プロジェクトアイコンは、通常、複数のサイズを含む .ico ファイルです。 最大16x16 のアイコンには、同じ要素が含まれています。 必要に応じて、32x32 バージョンには、プロジェクトの種類などの詳細が表示されます。

 ![Visual Studio での [プロジェクト] アイコン](../../extensibility/ux-guidelines/media/0404-18-iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")

 **VB Windows コントロールライブラリプロジェクトアイコン、16x16 および32x32**

 ピクセルフレーム内のアイコンを中央に配置します。 そうでない場合は、アイコンをフレームの上部または右に揃えます。

 ![ピクセル フレーム内に中央揃えで配置されたアイコン](../../extensibility/ux-guidelines/media/0404-19-iconcentered.png "0404-19_IconCentered")

 **ピクセル フレーム内に中央揃えで配置されたアイコン**

 ![ピクセル フレームの右上に配置されたアイコン](../../extensibility/ux-guidelines/media/0404-20-icontopright.png "0404-20_IconTopRight")

 **フレームの右上にあるアイコン**

 ![ピクセル フレームの上部中央揃えで配置されたアイコン](../../extensibility/ux-guidelines/media/0404-21-icontopalign.png "0404-21_IconTopAlign")

 **フレームの上に中央揃えで配置されたアイコン**

 最適な配置とバランスを実現するには、アイコンの基本要素にアクショングリフを obstructing ないようにします。 基本要素の左上付近にグリフを配置します。 追加の要素を追加する場合は、アイコンの配置とバランスを考慮してください。

|**正しい配置とバランス**|**配置とバランスが正しくありません**|
|-|-|
|![正しいアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-22-alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![正しくないアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-23-alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 要素を共有し、セットで使用されるアイコンのサイズパリティを確保します。 間違った組み合わせでは、円と矢印が大きすぎて一致しないことに注意してください。

|**正しいサイズのパリティ**|**サイズのパリティが正しくありません**|
|-|-|
|![正しいアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-24-sizeparitycorrect.png "0404-24_SizeParityCorrect")|![正しくないアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-25-sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 一貫した線と視覚的な重みを使用します。 ビルド中のアイコンが、並列比較を使用して他のアイコンとどのように比較されるかを評価します。 16x16 フレーム全体を使用するのではなく、15x15 以下を使用します。 負-正 (ダークから光) の比率は50/50 にする必要があります。

|**負から正の比率を修正します**|**負から正の比率が正しくありません**|
|-|-|
|![&#40;1&#41;のアイコンの視覚的な重みを修正しました ](../../extensibility/ux-guidelines/media/0404-26-visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![アイコン &#40;2&#41;の視覚的な重み付けを修正します ](../../extensibility/ux-guidelines/media/0404-27-visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![アイコン &#40;3&#41;の正しい視覚的な重み ](../../extensibility/ux-guidelines/media/0404-28-visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![アイコンの正しくない視覚的なウェイト](../../extensibility/ux-guidelines/media/0404-29-visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 要素の整合性を犠牲にせずに、単純で比較可能な図形と補完的な角度を使用して要素を構築します。 可能な場合は、45°または90°の角度を使用します。

 ![正しいアイコンの角度](../../extensibility/ux-guidelines/media/0404-30-iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>パースペクティブ
 このアイコンは明確でわかりやすいものにしてください。 必要な場合にのみ、パースペクティブと光源を使用します。 Icon 要素で perspective を使用しないようにする必要がありますが、一部の要素は認識されません。 このような場合、法を持つパースペクティブは要素のわかりやすさを伝えます。

 ![3&#45;ポイントのパースペクティブ](../../extensibility/ux-guidelines/media/0404-31-3pointperspective.png "0404-31_3PointPerspective")

 **3 点透視投影**

 ![1&#45;ポイントのパースペクティブ](../../extensibility/ux-guidelines/media/0404-32-1pointperspective.png "0404-32_1PointPerspective")

 **1 点透視投影**

 ほとんどの要素は、右に向いている必要があります。

 ![右に傾いたアイコン](../../extensibility/ux-guidelines/media/0404-33-angledright.png "0404-33_AngledRight")

 オブジェクトに必要な明確さを追加する場合にのみ、光源を使用します。

|**正しい光源**|**光源が正しくありません**|
|-|-|
|![正しいアイコンの光源](../../extensibility/ux-guidelines/media/0404-34-lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![正しくないアイコンの光源](../../extensibility/ux-guidelines/media/0404-35-lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 アウトラインを使用するのは、読みやすさを向上させたり、比喩を効果的に伝えるためだけに使用してください。 負陽性 (ダークライト) のバランスは50/50 である必要があります。

|**アウトラインの正しい使用**|**アウトラインの不適切な使用**|
|-|-|
|![正しいアウトライン](../../extensibility/ux-guidelines/media/0404-36-outlinescorrect.png "0404-36_OutlinesCorrect")|![正しくないアウトライン](../../extensibility/ux-guidelines/media/0404-37-outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>アイコンの種類
 **シェルとコマンドバー** のアイコンは、1つのベース、1つの修飾子、1つのアクション、または1つの状態の要素から構成されます。

 ![シェルおよびコマンド バーのアイコン](../../extensibility/ux-guidelines/media/0404-38-shellicons.png "0404-38_ShellIcons")

 **シェルとコマンドバーのアイコンの例**

 **ツールウィンドウのコマンドバー** アイコンは、1つのベース、1つの修飾子、1つのアクション、または1つの状態の要素から構成されます。

 ![[ツール] ウィンドウのコマンド バー アイコン](../../extensibility/ux-guidelines/media/0404-39-toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")

 **ツールウィンドウのコマンドバーのアイコンの例**

 **ツリービューの曖昧性解消** アイコンは、1つのベース、1つの修飾子、1つのアクション、または1つの状態の要素から構成されます。

 ![ツリー ビューの曖昧性解消子のアイコン](../../extensibility/ux-guidelines/media/0404-40-treeviewicons.png "0404-40_TreeViewIcons")

 **ツリービューの曖昧性解消アイコンの例**

 **状態ベースの値の分類** アイコンは、[アクティブ]、[アクティブにする]、および [非アクティブ] の状態にあります。

 ![状態&#45;ベースの分類値アイコン](../../extensibility/ux-guidelines/media/0404-41-statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")

 **状態ベースの値の分類アイコンの例**

 **IntelliSense** アイコンは、1つのベース、1つの修飾子、および1つの状態を持つ、次の3つの要素で構成されています。

 ![IntelliSense アイコン](../../extensibility/ux-guidelines/media/0404-42-intellisenseicons.png "0404-42_IntelliSenseIcons")

 **IntelliSense アイコンの例**

 **小さい (16x16) プロジェクト** アイコンには、1つのベースと1つの修飾子の2つ以上の要素を含めることはできません。

 ![16x16 プロジェクトアイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-43-16x16project1.png "0404-43_16x16Project1") ![16x16 プロジェクトアイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44-16x16project2.png "0404-44_16x16Project2") ![16x16 プロジェクトアイコン &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45-16x16project3.png "0404-45_16x16Project3")

 **小さい (16x16) プロジェクトアイコンの例**

 **Large (32x32) プロジェクト** アイコンは、1つのベース、1 ~ 2 個の修飾子、および1つの言語オーバーレイで構成されています。

 ![32 x 32 プロジェクト アイコン](../../extensibility/ux-guidelines/media/0404-46-32x32project.png "0404-46_32x32Project")

 **Large (32x32) プロジェクトアイコンの例**

### <a name="production-details"></a>実稼働の詳細
 すべての新しい UI 要素は Windows Presentation Foundation (WPF) を使用して作成する必要があり、WPF の新しいアイコンはすべて32ビットの PNG 形式である必要があります。 24ビット PNG は、透明度をサポートしていない従来の形式であるため、アイコンには推奨されません。

 解像度を 96 DPI で保存します。

#### <a name="file-types"></a>ファイルの種類

- **32-BIT PNG:** アイコンの推奨される形式。 単一のラスター (ピクセル) イメージを格納できるロスレスデータ圧縮ファイル形式。 32ビットの PNG ファイルでは、アルファチャネルの透明度、ガンマ補正、およびインターレースがサポートされています。

- **32-ビット BMP:** 非 WPF コントロールの場合。 XP または high color とも呼ばれます。32ビット BMP は、RGB/A イメージ形式で、アルファチャネル透明度を持つ実際の色の画像です。 アルファチャネルは Adobe Photoshop で指定された透明度のレイヤーであり、追加の (4) カラーチャネルとしてビットマップ内に保存されます。 アートワークの実稼働時には、すべての32ビットの BMP ファイルに黒の背景が追加され、色深度に関する簡単な視覚的な手掛かりが提供されます。 この黒の背景は、UI でマスクアウトされる領域を表します。

- **32-BIT ICO:** プロジェクトアイコンと項目の追加。 すべての .ICO ファイルは、アルファチャネル透明度 (RGB/A) を使用する32ビットの true 色です。 ICO ファイルは複数のサイズと色深度を格納できるため、Vista のアイコンは多くの場合、16x16、32x32、48 x 48、256x256 の各イメージサイズを含む ICO 形式です。 Windows エクスプローラーで適切に表示するには、イメージのサイズごとに、ICO ファイルを24ビットと8ビットの色深度に保存する必要があります。

- **XAML:** デザインサーフェイスおよび Windows ガイド用。 XAML アイコンは、拡大縮小、回転、ファイリング、透明度をサポートするベクターベースのイメージファイルです。 現在、Visual Studio では一般的ではありませんが、柔軟性が高いため、広く普及しています。

- **SVG**

- **24 ビット BMP:** Visual Studio のコマンドバー。 実際の RGB 画像形式である24ビット BMP は、抜き合わせ透明度レイヤーの色キーとしてマゼンタ (R = 255, G = 0, B = 255) を使用して透明度レイヤーを作成するアイコン規則です。 24ビット BMP では、すべてのマゼンタの表面が背景色を使用して表示されます。

- **24 ビット GIF:** Visual Studio のコマンドバー。 透明度をサポートする、真色の RGB 画像形式。 GIF ファイルは、ウィザードのアートワークと GIF アニメーションでよく使用されます。

### <a name="icon-construction"></a>アイコンの構築
 Visual Studio の最小アイコンサイズは16x16 です。 一般的に使用される最大値は32x32 です。 アイコンをデザインするときに、16x16、24 x 24、または32x32 のフレーム全体をいっぱいにしないように注意してください。 判読しやすく、一様アイコンの構築はユーザー認識に不可欠です。 アイコンを作成するときは、次の点に従います。

- アイコンは、明確でわかりやすく、一貫性のあるものである必要があります。

- ステータス通知要素をアイコンの基本要素の上に重ねて使用するのではなく、1つのアイコンとして使用することをお勧めします。 特定のコンテキストでは、UI で status 要素を基本要素と組み合わせて使用することが必要になる場合があります。

- プロジェクトアイコンは、通常、複数のサイズを含む .ico ファイルです。 16x16、24 x 24、32x32 のアイコンだけが更新されます。 最大16x16 と 24 x 24 のアイコンには、同じ要素が含まれます。 32 x 32 のアイコンには、プロジェクトの言語の種類 (該当する場合) などの詳細が含まれています。

- 32x32 のアイコンの場合、基本要素の線の太さは通常2ピクセルです。 1つまたは2ピクセルの線の太さを、詳細な要素に使用できます。 最適な方法を判断するには、適切な判断を使用します。

- 16x16 と 24 x 24 のアイコンの要素の間には、少なくとも1ピクセルの間隔が必要です。 32x32 のアイコンの場合は、要素間、および修飾子と基本要素の間に2ピクセルの間隔を使用します。

  ![16x16、24x24、および 32x32 アイコンの要素間スペース](../../extensibility/ux-guidelines/media/0404-47-elementspacing.png "0404-47_ElementSpacing")

  **アイコンサイズが 16 x 16、24 x 24、および32x32 の要素の間隔**

#### <a name="color-and-accessibility"></a>色とアクセシビリティ
 Visual Studio のコンプライアンスガイドラインでは、製品のすべてのアイコンが色とコントラストのアクセシビリティ要件を満たしている必要があります。 これはアイコンの反転によって実現されます。設計時には、製品内でプログラムによって逆になることに注意する必要があります。

 Visual Studio アイコンでの色の使用の詳細については、「 [イメージでの色の使用](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)」を参照してください。

## <a name="using-color-in-images"></a><a name="BKMK_UsingColorInImages"></a> 画像での色の使用

### <a name="overview"></a>概要
 Visual Studio のアイコンは、主にモノクロです。 色は、特定の情報を伝えるために予約されており、装飾には使用されません。 色が使用されます。

- アクションを示すには

- ユーザーに状態通知を通知するには

- 言語の関連付けを指定するには

- IntelliSense 内で項目を区別するには

### <a name="accessibility"></a>ユーザー補助
 Visual Studio のコンプライアンスガイドラインでは、製品にチェックインされているすべてのアイコンが、色とコントラストのアクセシビリティ要件を満たしている必要があります。 ビジュアル言語パレットの色はテストされており、これらの要件を満たしています。

#### <a name="color-inversion-for-dark-themes"></a>ダークテーマの色の反転
 Visual Studio のダークテーマで、適切なコントラスト比でアイコンを表示するために、逆の順序がプログラムによって適用されます。 このガイドの色は、正しく反転させるために一部選択されています。 色の使用をこのパレットに限定するか、反転が適用されたときに予測できない結果になります。

 ![色が反転されているアイコンの例](../../extensibility/ux-guidelines/media/0405-01-darkthemeinversion.png "0405-01_DarkThemeInversion")

 **色が反転したアイコンの例**

### <a name="base-palette"></a>基本パレット
 すべての標準アイコンには、3つの基本色が含まれています。 アイコンには、3D ツールアイコンに対して1つまたは2つの例外を含む、グラデーションやドロップシャドウは含まれません。

|使用法|名前|値 (明るいテーマ)|カラー|例|
|-----------|----------|---------------------------|------------|-------------|
|背景/濃色|VS BG|424242/66、66、66|![見本 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405424242")|![基本パレットの例](../../extensibility/ux-guidelines/media/0405-02-basepaletteexample.png "0405-02_BasePaletteExample")|
|前景/ライト|VS FG|F0EFF1/240239241|![見本 F0EFF1](../../extensibility/ux-guidelines/media/0405-f0eff1.png "0405_F0EFF1")||
|[外枠]|VS Out|F6F6F6/246246246|![見本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")||

 基本色に加えて、各アイコンには拡張パレットから1つの追加の色が含まれる場合があります。

### <a name="extended-palette"></a>拡張パレット

#### <a name="action-modifiers"></a>アクション修飾子
 以下の4色は、アクション修飾子で必要とされるアクションの種類を示しています。

|使用法|名前|値 (すべてのテーマ)|カラー|
|-----------|----------|--------------------------|------------|
|正|VS アクション (緑)|388A34/56138、52|![見本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|負|VS アクションの赤|A1260D/161、38、13|![見本 A1260D](../../extensibility/ux-guidelines/media/0405-a1260d.png "0405_A1260D")|
|中立|VS アクション Blue|00539C/0、83156|![見本 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|作成/新規作成|VS アクションオレンジ|C27D1A/194156、26|![見本 C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>例
 "Add"、"Run"、"Play"、"Validate" などの正のアクション修飾子には、緑色が使用されます。

|実行|クエリの実行|すべてのステップを再生する|コントロールの追加|
|-|-|-|-|
|![実行アイコン](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405-03_ActionModifierRun")|![[クエリの実行] アイコン](../../extensibility/ux-guidelines/media/0405-04-executequery.png "0405-04_ExecuteQuery")|![[すべてのステップの再生] アイコン](../../extensibility/ux-guidelines/media/0405-05-playallsteps.png "0405-05_PlayAllSteps")|![[コントロールの追加] アイコン](../../extensibility/ux-guidelines/media/0405-06-addcontrol.png "0405-06_AddControl")|

 赤は、"Delete"、"Stop"、"Cancel"、"Close" などの否定アクション修飾子に使用されます。

|リレーションシップの削除|列の削除|クエリの停止|オフライン接続|
|-|-|-|-|
|![[リレーションシップの削除] アイコン](../../extensibility/ux-guidelines/media/0405-07-deleterelationship.png "0405-07_DeleteRelationship")|![[列の削除] アイコン](../../extensibility/ux-guidelines/media/0405-08-deletecolumn.png "0405-08_DeleteColumn")|![[クエリの停止] アイコン](../../extensibility/ux-guidelines/media/0405-09-stopquery.png "0405-09_StopQuery")|![[オフラインの接続] アイコン](../../extensibility/ux-guidelines/media/0405-10-connectionoffline.png "0405-10_ConnectionOffline")|

 Blue は、"Open"、"Next"、"Previous"、"Import"、"Export" など、一般的に矢印として表されるニュートラルアクション修飾子に適用されます。

|フィールドへのジャンプ|バッチチェックイン|アドレス エディター|関連付けエディター|
|-|-|-|-|
|![[オブジェクトの選択] アイコン](../../extensibility/ux-guidelines/media/0405-11-gotofield.png "0405-11_GoToField")|![バッチチェック&#45;アイコン](../../extensibility/ux-guidelines/media/0405-12-batchedcheckin.png "0405-12_BatchedCheckIn")|![[アドレス エディター] アイコン](../../extensibility/ux-guidelines/media/0405-13-addresseditor.png "0405-13_AddressEditor")|![[関連付けエディター] アイコン](../../extensibility/ux-guidelines/media/0405-14-associationeditor.png "0405-14_AssociationEditor")|

 ダークゴールドは主に "New" 修飾子として使用されます。

|[新しいプロジェクト]|新しいグラフの作成|新しい単体テスト|新しいリスト項目|
|-|-|-|-|
|![[新しいプロジェクト] アイコン](../../extensibility/ux-guidelines/media/0405-15-newproject.png "0405-15_NewProject")|![[新しいグラフの作成] アイコン](../../extensibility/ux-guidelines/media/0405-16-createnewgraph.png "0405-16_CreateNewGraph")|![[新しい単体テスト] アイコン](../../extensibility/ux-guidelines/media/0405-17-newunittest.png "0405-17_NewUnitTest")|![[新しいリスト アイテム] アイコン](../../extensibility/ux-guidelines/media/0405-18-newlistitem.png "0405-18_NewListItem")|

#### <a name="special-cases"></a>特殊なケース
 特殊なケースでは、色分けされたアクション修飾子をスタンドアロンアイコンとして単独で使用できます。 アイコンに使用する色には、アイコンが関連付けられている操作が反映されます。 この使用は、次のような、アイコンの小さなサブセットに制限されます。

|実行|Stop|削除|保存|最近参照した場所|
|-|-|-|-|-|
|![実行アイコン](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405-03_ActionModifierRun")|![停止アイコン](../../extensibility/ux-guidelines/media/0405-19-stop.png "0405-19_Stop")|![削除アイコン](../../extensibility/ux-guidelines/media/0405-20-delete.png "0405-20_Delete")|![[Save]\(保存\) アイコン](../../extensibility/ux-guidelines/media/0405-21-save.png "0405-21_Save")|![[戻る] アイコン](../../extensibility/ux-guidelines/media/0405-22-navigateback.png "0405-22_NavigateBack")|
### <a name="code-hierarchy-palette"></a>コード階層パレット

#### <a name="folder"></a>Folder

|使用法|名前|値 (すべてのテーマ)|カラー|例|
|-----------|----------|--------------------------|------------|-------------|
|フォルダー|Folder|DCB67A/220182122|![見本 DCB67A](../../extensibility/ux-guidelines/media/0405-dcb67a.png "0405_DCB67A")|![フォルダーの色のアイコン](../../extensibility/ux-guidelines/media/0405-23-foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio の言語
 Visual Studio で使用できる各共通言語またはプラットフォームには、関連付けられた色があります。 これらの色は、基本アイコン、または複合アイコンの右上隅に表示される言語修飾子で使用されます。

|使用法|名前|値 (すべてのテーマ)|カラー|
|-----------|----------|--------------------------|------------|
|ASP、HTML、WPF|ASP HTML WPF Blue|0095D7/0149215|![見本 0095D7](../../extensibility/ux-guidelines/media/0405-0096d7.png "0405_0096D7")|
|C++|CPP 紫|9B4F96/155、79150|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|C#|CS 緑 (VS アクション緑)|388A34/56138、52|![見本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|CSS|CSS 赤|BD1E2D/189、30、45|![見本 BD1E2D](../../extensibility/ux-guidelines/media/0405-bd1e2d.png "0405_BD1E2D")|
|F#|FS 紫|672878/103、40120|![見本 672878](../../extensibility/ux-guidelines/media/0405-672878.png "0405672878")|
|JavaScript|JS オレンジ|F16421/241100、33|![見本 F16421](../../extensibility/ux-guidelines/media/0405-f16421.png "0405_F16421")|
|VB|VB Blue (VS アクション Blue)|00539C/0、83156|![見本 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|TypeScript|TS オレンジ|E04C06/224、76、6|![見本 E04C06](../../extensibility/ux-guidelines/media/0405-e04c06.png "0405_E04C06")|
|Python|.PY グリーン|879636/135150、54|![見本 879636](../../extensibility/ux-guidelines/media/0405-879636.png "040587 9636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>言語の修飾子を持つアイコンの例

|VB|C#|F#|JavaScript|Python|
|-|-|-|-|-|-|
|![Visual Basic アイコン](../../extensibility/ux-guidelines/media/0405-25-vb.png "0405-25_VB")|![C&#35; アイコン](../../extensibility/ux-guidelines/media/0405-26-csharp.png "0405-26_CSharp")|![C&#43;&#43; アイコン](../../extensibility/ux-guidelines/media/0405-27-cplusplus.png "0405-27_CPlusPlus")|![F&#35; アイコン](../../extensibility/ux-guidelines/media/0405-28-fsharp.png "0405-28_FSharp")|![JavaScript アイコン](../../extensibility/ux-guidelines/media/0405-29-javascript.png "0405-29_JavaScript")|![Python アイコン](../../extensibility/ux-guidelines/media/0405-30-python.png "0405-30_Python")|

|HTML|WPF|ASP|CSS|TypeScript|
|-|-|-|-|-|-|
|![HTML アイコン](../../extensibility/ux-guidelines/media/0405-31-html.png "0405-31_HTML")<br />HTML|![WPF アイコン](../../extensibility/ux-guidelines/media/0405-32-wpf.png "0405-32_WPF")<br />WPF|![ASP アイコン](../../extensibility/ux-guidelines/media/0405-33-asp.png "0405-33_ASP")<br />ASP|![CSS アイコン](../../extensibility/ux-guidelines/media/0405-34-css.png "0405-34_CSS")<br />CSS|![TypeScript アイコン](../../extensibility/ux-guidelines/media/0405-35-typescript.png "0405-35_TypeScript")<br />TypeScript||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense アイコンは、専用のカラーパレットを使用します。 これらの色は、ユーザーが IntelliSense ポップアップリスト内のさまざまな項目をすばやく区別できるようにするために使用されます。

|使用法|名前|値 (すべてのテーマ)|カラー|
|-----------|----------|--------------------------|------------|
|クラス、イベント|VS アクションオレンジ|C27D1A/194125、26|![見本 C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|
|拡張メソッド、メソッド、モジュール、デリゲート|VS アクション紫|652D90/101, 45144|![見本 652D90](../../extensibility/ux-guidelines/media/0405-652d90.png "0405_652D90")|
|Field、Enum Item、Macro、Structure、Union 値型、Operator、Interface|VS アクション Blue|00539C/0、83156|![見本 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|Object|VS アクション (緑)|388A34/56138、52|![見本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|定数、例外、列挙項目、マップ、マップ項目、名前空間、テンプレート、型定義|背景 (VS BG)|424242/66、66、66|![見本 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405424242")|

##### <a name="examples-of-intellisense-icons"></a>IntelliSense アイコンの例


|クラス|プライベートイベント|代理人|メソッド Friend|フィールド|
|-|-|-|-|-|
|![IntelliSense クラスのアイコン](../../extensibility/ux-guidelines/media/0405-36-intellisenseclass.png "0405-36_IntelliSenseClass")|![IntelliSense プライベート イベントのアイコン](../../extensibility/ux-guidelines/media/0405-37-intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")|![IntelliSense デリゲートのアイコン](../../extensibility/ux-guidelines/media/0405-38-intellisensedelegate.png "0405-38_IntelliSenseDelegate")|![IntelliSense メソッド フレンドのアイコン](../../extensibility/ux-guidelines/media/0405-39-intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")|![フィールドアイコン](../../extensibility/ux-guidelines/media/0405-40-field.png "0405-40_Field")|

|Protected Enum 項目|Object|Template|例外のショートカット|
|-|-|-|-|
|![IntelliSense の保護された列挙型の項目のアイコン](../../extensibility/ux-guidelines/media/0405-41-intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")|![IntelliSense オブジェクトのアイコン](../../extensibility/ux-guidelines/media/0405-42-intellisenseobject.png "0405-42_IntelliSenseObject")|![IntelliSense テンプレートのアイコン](../../extensibility/ux-guidelines/media/0405-43-intellisensetemplate.png "0405-43_IntelliSenseTemplate")|![IntelliSense の例外のショートカットのアイコン](../../extensibility/ux-guidelines/media/0405-44-intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")|

### <a name="notifications"></a>通知
 Visual Studio での通知は、状態を示すために使用されます。 通知パレットでは、次の4つの色と、白黒または白の前景の塗りつぶしオプションを使用して、次のステータスレベルで通知を定義します。

|使用法|名前|値 (すべてのテーマ)|カラー|
|-----------|----------|--------------------------|------------|
|状態: ニュートラル|青い通知 (VS Blue)|1BA1E2/27161226|![見本 1BA1E2](../../extensibility/ux-guidelines/media/0405-1ba1e2.png "0405_1BA1E2")|
|状態: 正|通知 (緑)|339933/51153、51|![見本 339933](../../extensibility/ux-guidelines/media/0405-339933.png "04053399 33")|
|状態: 負|赤の通知 (対赤)|E51400/229、20、0|![見本 E51400](../../extensibility/ux-guidelines/media/0405-e51400.png "0405_E51400")|
|状態: 警告|通知黄 (VS オレンジ)|FFCC00/255204、0|![見本 FFCC00](../../extensibility/ux-guidelines/media/0405-ffcc00.png "0405_FFCC00")|
|前景の塗りつぶし|黒の通知 (黒)|000000/0、0、0|![見本 &#35;000000](../../extensibility/ux-guidelines/media/0405-000000.png "0405000000")|
|前景の塗りつぶし|通知-白 (白)|FFFFFF/255255255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知アイコンの例

|アラート:|警告|完了|Stop|
|-|-|-|-|
|![通知アイコン](../../extensibility/ux-guidelines/media/0405-45-alert.png "0405-45_Alert")|![警告アイコン](../../extensibility/ux-guidelines/media/0405-48-warning.png "0405-48_Warning")|![完了アイコン](../../extensibility/ux-guidelines/media/0405-46-complete.png "0405-46_Complete")|![停止アイコン](../../extensibility/ux-guidelines/media/0405-47-stop.png "0405-47_Stop")|

### <a name="visual-studio-online"></a>Visual Studio Online
 一般に、Visual Studio Online は、ブラウザーでホストされている機能で構成されています。 色は環境によって異なりますが、スタイルは変わりません。

|グループ|使用法|名前|値 (すべてのテーマ)|カラー|
|-----------|-----------|----------|--------------------------|------------|
|TFS|背景|TFSO BG|656565/101、101、101|![見本 656565](../../extensibility/ux-guidelines/media/0405-656565.png "0405656565")|
|TFS|[外枠]|TFSO|FFFFFF/255、255、255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|Napa|背景|White|FFFFFF/255、255、255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|モナコ|背景|White|FFFFFF/255、255、255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|背景|White|FFFFFF/255、255、255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|標準|F12 Grey_Primary|555555/85、85、85|![見本 555555](../../extensibility/ux-guidelines/media/0405-555555.png "040555(_s)")|
|F12|ホバー|F12 Blue_Hover|2279BF/34121191|![見本 2279BF](../../extensibility/ux-guidelines/media/0405-2279bf.png "0405_2279BF")|
|F12|Disabled|F12 LtGrey_Disabled|ABABAC/171171172|![見本 ABABAC](../../extensibility/ux-guidelines/media/0405-ababac.png "0405_ABABAC")|
|F12|ホバー時の背景|ホバー (bg)|D9EBF7/217235247|![見本 D9EBF7](../../extensibility/ux-guidelines/media/0405-d9ebf7.png "0405_D9EBF7")|
|F12|押された背景|(Bg を押す)|B2D7F0/178215240|![見本 B2D7F0](../../extensibility/ux-guidelines/media/0405-b2d7f0.png "0405_B2D7F0")|
|F12|[外枠]|VS OUT|F6F6F6/246246246|![見本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")|
|F12|情報|情報|00BCF2/0188242|![見本 00BCF2](../../extensibility/ux-guidelines/media/0405-00bcf2.png "0405_00BCF2")|
|F12|警告|警告|F28300/242131、0|![見本 F28300](../../extensibility/ux-guidelines/media/0405-f28300.png "0405_F28300")|
|F12|エラー/負|Error_Negative|E81123/232、17、35|![見本 E81123](../../extensibility/ux-guidelines/media/0405-e81123.png "0405_E81123")|
|F12|開始/肯定|Start_Positive|009E49/0158、73|![見本 009E49](../../extensibility/ux-guidelines/media/0405-009e49.png "0405_009E49")|
|F12|ブレークの種類|ブレークの種類|9B4F96/155、79150|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|F12|イベントマーク|イベントマーク|A51F00/165、31、0|![見本 A51F00](../../extensibility/ux-guidelines/media/0405-a51f00.png "0405_A51F00")|
|F12|ユーザーマーク|ユーザーマーク|F16220/241、98、32|![見本 F16220](../../extensibility/ux-guidelines/media/0405-f16220.png "0405_F16220")|

#### <a name="examples-of-visual-studio-online-icons"></a>Visual Studio Online のアイコンの例

|TFS オンライン||||
|----------------|-|-|-|
|![TFS オンラインチームアイコン](../../extensibility/ux-guidelines/media/0405-49-tfsonlineteam.png "0405-49_TFSOnlineTeam")**オンラインチーム**|![TFS 情報アイコン](../../extensibility/ux-guidelines/media/0405-50-tfsinformation.png "0405-50_TFSInformation")の **情報**|![TFS 履歴アイコン](../../extensibility/ux-guidelines/media/0405-51-tfshistory.png "0405-51_TFSHistory")**履歴**|![TFS 分岐アイコン](../../extensibility/ux-guidelines/media/0405-52-tfsbranch.png "0405-52_TFSBranch")**ブランチ**|

|Napa||||
|----------|-|-|-|
|![Napa コンテンツアイコン](../../extensibility/ux-guidelines/media/0405-53-napacontent.png "0405-53_NapaContent")の **コンテンツ**|![Napa office mail アイコン](../../extensibility/ux-guidelines/media/0405-54-napaofficemail.png "0405-54_NapaOfficeMail") **office mail**|![Napa sharepoint アイコン](../../extensibility/ux-guidelines/media/0405-55-napasharepoint.png "0405-55_NapaSharePoint") **sharepoint**|![Napa 作業ウィンドウアイコン](../../extensibility/ux-guidelines/media/0405-56-napataskpane.png "0405-56_NapaTaskPane")**作業ウィンドウ**|

|モナコ||||
|------------|-|-|-|
|![モナコファイルアイコン](../../extensibility/ux-guidelines/media/0405-57-monacofiles.png "0405-57_MonacoFiles")**ファイル**|![モナコ git アイコン](../../extensibility/ux-guidelines/media/0405-58-monacogit.png "0405-58_MonacoGit") **git**|![モナコ検索アイコン](../../extensibility/ux-guidelines/media/0405-59-monacosearch.png "0405-59_MonacoSearch")**検索**|![モナコテキストアイコン](../../extensibility/ux-guidelines/media/0405-60-monacotext.png "0405-60_MonacoText")**テキスト**|

|F12||||
|---------|-|-|-|
|![F12 コードアイコン](../../extensibility/ux-guidelines/media/0405-61-f12prettycode.png "0405-61_F12PrettyCode")**かなりのコード**|![F12 警告アイコン](../../extensibility/ux-guidelines/media/0405-62-f12warning.png "0405-62_F12Warning")**警告**|![F12 エミュレートアイコン](../../extensibility/ux-guidelines/media/0405-63-f12emulate.png "0405-63_F12Emulate")**エミュレート**|
