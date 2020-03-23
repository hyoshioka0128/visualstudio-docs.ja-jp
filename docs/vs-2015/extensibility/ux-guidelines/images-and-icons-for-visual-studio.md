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
ms.openlocfilehash: 843829c56fcbd2f5c558d7c4a8b14a660a431eac
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301327"
---
# <a name="images-and-icons-for-visual-studio"></a>Visual Studio のイメージとアイコン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="image-use-in-visual-studio"></a><a name="BKMK_ImageUseInVisualStudio"></a>イメージの使用
 アートワークを作成する前に[、Visual Studio イメージ ライブラリ](https://www.microsoft.com/download/details.aspx?id=35825)で 1,000 以上のイメージを使用することを検討してください。

### <a name="types-of-images"></a>画像の種類

- **アイコン**. コマンド、階層、テンプレートなどで表示される小さなイメージ。 Visual Studio で使用される既定のアイコン サイズは 16 x 16 PNG です。 イメージ サービスによって生成されたアイコンは、HDPI サポート用の XAML 形式を自動的に生成します。

     **注:** イメージはメニュー システムで使用されますが、すべてのコマンドに対してアイコンを作成しないでください。 [Visual Studio のメニューとコマンドを](../../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)参照して、コマンドがアイコンを取得する必要があるかどうかを確認します。

- **サムネイル。** [新しいプロジェクト]ダイアログなど、ダイアログのプレビュー領域で使用されるイメージ。

- **ダイアログ イメージ。** ダイアログまたはウィザードに表示される画像(説明的なグラフィックまたはメッセージインジケータ)。 難しい概念を説明したり、ユーザーの注意を引くために必要な場合にのみ使用する (警告、警告)。

- **アニメーション画像。** 進捗状況インジケーター、ステータス バー、および操作ダイアログで使用されます。

- **カーソル。** マウスを使用して操作を許可するかどうか、オブジェクトをドロップできる場所などを示します。

## <a name="icon-design"></a><a name="BKMK_IconDesign"></a>アイコンデザイン

### <a name="overview"></a>概要
 Visual Studio では、クリーンなジオメトリと正/負 (明/暗) の 50/50 バランスを持ち、直接的でわかりやすいメタファを使用するモダンなスタイルのアイコンを使用します。 重要なアイコン設計ポイントは、明確性、単純化、およびコンテキストを中心にしています。

- **クラリティ:** アイコンにその意味と個性を与えるコア比喩に焦点を当てます。

- **単純化:** アイコンをコアの意味に縮小する - 必要な要素だけで、フリルなしでテーマを理解してください。

- **コンテキスト:** アイコンのコアメタファーを構成する要素を決定する際に重要な概念開発中に、アイコンの役割のすべての側面を考慮します。

  アイコンを使用すると、避けるべき設計ポイントが多数あります。

- UI 要素を示すアイコンは、必要な場合以外は使用しないでください。 UI 要素が一般的で、明らかでも一意でもない場合は、より抽象的または象徴的なアプローチを選択します。

- ドキュメント、フォルダ、矢印、虫眼鏡などの一般的な要素を過度に使用しないでください。 アイコンの意味に不可欠な場合にのみ、このような要素を使用します。 たとえば、右向きの虫眼鏡は、検索、参照、検索のみを示します。

- 一部の従来のアイコン要素はパースペクティブの使用を維持しますが、要素がそれなしで明確にならなければ、パースペクティブを持つ新しいアイコンを作成しないでください。

- アイコンにあまり多くの情報を詰め込まないでください。 認識しやすいシンボルとして簡単に認識または学習できる単純な画像は、複雑な画像よりもはるかに便利です。 アイコンは全体のストーリーを伝えることはできません。

### <a name="icon-creation"></a>アイコンの作成

#### <a name="concept-development"></a>コンセプト開発
 Visual Studio には、さまざまな種類のアイコンが UI に含まれています。 開発時にはアイコンの種類を慎重に検討してください。 アイコン要素に対して、不明な UI オブジェクトや珍しい UI オブジェクトを使用しないでください。 スマート タグ アイコンなど、このような場合は記号を選択します。 左側の抽象タグの意味は、右の曖昧なUIベースのバージョンよりも明確であることに注意してください。

|||
|-|-|
|**記号画像の正しい使用**|**記号画像の誤使用**|
|![正しい [スマート タグ] アイコン](../../extensibility/ux-guidelines/media/0404-01-smarttagcorrect.png "0404-01_SmartTagCorrect")|![正しくない [スマート タグ] アイコン](../../extensibility/ux-guidelines/media/0404-02-smarttagincorrect.png "0404-02_SmartTagIncorrect")|

 標準の簡単に認識できる UI 要素がアイコンに適したインスタンスがあります。 ウィンドウの追加は、そのような例の1つです。

|||
|-|-|
|**アイコン内の UI 要素を修正する**|**アイコン内の不適切な UI 要素**|
|![正しい [ウィンドウの追加] アイコン](../../extensibility/ux-guidelines/media/0404-03-addwindowcorrect.png "0404-03_AddWindowCorrect")|![正しくない [ウィンドウの追加] アイコン](../../extensibility/ux-guidelines/media/0404-04-addwindowincorrect.png "0404-04_AddWindowIncorrect")|

 アイコンの意味に不可欠な場合を除き、ドキュメントを基本要素として使用しないでください。 [ドキュメントの追加(下)のドキュメント要素がない場合、意味は失われますが、[ドキュメントを更新]を使用すると、その意味を伝える必要はありません。

|||
|-|-|
|**ドキュメントアイコンの正しい使用**|**ドキュメント アイコンの不適切な使用**|
|![正しい [ドキュメント] アイコン](../../extensibility/ux-guidelines/media/0404-05-documenticoncorrect.png "0404-05_DocumentIconCorrect")|![正しくない [ドキュメント] アイコン](../../extensibility/ux-guidelines/media/0404-06-documenticonincorrect.png "0404-06_DocumentIconIncorrect")|

 「show」の概念は、「すべてのファイルを表示」の例のように、表示されているものを最もよく示すアイコンで表す必要があります。 レンズメタファーは、リソース ビューの例のように、必要に応じて"ビュー"の概念を示すために使用できます。

|||
|-|-|
|**「ショー」**|**"見る"**|
|![表示アイコン](../../extensibility/ux-guidelines/media/0404-07-show.png "0404-07_Show")|![ビュー アイコン](../../extensibility/ux-guidelines/media/0404-08-view.png "0404-08_View")|

 右向きの虫眼鏡アイコンは、検索、検索、参照のみを表します。 プラス記号またはマイナス記号を持つ左向きのバリアントは、ズームイン/ズームアウトのみを表します。

|||
|-|-|
|**"検索"**|**"ズーム"**|
|![[検索] アイコン](../../extensibility/ux-guidelines/media/0404-09-search.png "0404-09_Search")|![ズーム アイコン](../../extensibility/ux-guidelines/media/0404-10-zoom.png "0404-10_Zoom")|

 ツリービューでは、フォルダアイコンとモディファイヤの両方を使用しないでください。 使用可能な場合は、モディファイヤのみを使用します。

|||
|-|-|
|**正しいツリービューアイコン**|**ツリー 表示アイコンが正しくありません**|
|![正しいツリー ビュー アイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-11-treeviewcorrect1.png "0404-11_TreeViewCorrect1") ![正しいツリー ビュー アイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-12-treeviewcorrect2.png "0404-12_TreeViewCorrect2")|![正しくないツリー ビュー アイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-13-treeviewincorrect1.png "0404-13_TreeViewIncorrect1") ![正しくないツリー ビュー アイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-14-treeviewincorrect2.png "0404-14_TreeViewIncorrect2")|

### <a name="style-details"></a>スタイルの詳細

#### <a name="layout"></a>[レイアウト]
 標準の 16x16 アイコンに示すように、スタック要素:

 ![16 x 16 のアイコンのレイアウト スタック](../../extensibility/ux-guidelines/media/0404-15-layoutstack.png "0404-15_LayoutStack")

 **16 x 16 のアイコンのレイアウト スタック**

 ステータス通知要素は、スタンドアロンのアイコンとして使用する方が良いです。 ただし、タスク完了アイコンなど、基本要素に通知をスタックするコンテキストがあります。

 ![Visual Studio でのスタンドアロン通知](../../extensibility/ux-guidelines/media/0404-16-standalonenotificationicons.png "0404-16_StandaloneNotificationIcons")

 **スタンドアロン通知アイコン**

 ![[タスクの完了] アイコン](../../extensibility/ux-guidelines/media/0404-17-taskcomplete.png "0404-17_TaskComplete")

 **タスク完了アイコン**

 プロジェクト アイコンは、通常、複数のサイズを含む .ico ファイルです。 ほとんどの 16 x 16 アイコンには、同じ要素が含まれています。 32x32 バージョンには、該当する場合はプロジェクトの種類を含む詳細があります。

 ![Visual Studio での [プロジェクト] アイコン](../../extensibility/ux-guidelines/media/0404-18-iconprojectthreesizes.png "0404-18_IconProjectThreeSizes")

 **VB Windows コントロール ライブラリ プロジェクト アイコン、16x16 および 32x32**

 アイコンをピクセル フレーム内に中央揃げします。 それが不可能な場合は、フレームの上部または右にアイコンを配置します。

 ![ピクセル フレーム内に中央揃えで配置されたアイコン](../../extensibility/ux-guidelines/media/0404-19-iconcentered.png "0404-19_IconCentered")

 **ピクセル フレーム内に中央揃えで配置されたアイコン**

 ![ピクセル フレームの右上に配置されたアイコン](../../extensibility/ux-guidelines/media/0404-20-icontopright.png "0404-20_IconTopRight")

 **フレームの右上に整列したアイコン**

 ![ピクセル フレームの上部中央揃えで配置されたアイコン](../../extensibility/ux-guidelines/media/0404-21-icontopalign.png "0404-21_IconTopAlign")

 **フレームの上部に合わせて中央揃えのアイコン**

 理想的な配置とバランスを実現するには、アクショングリフでアイコンの基本要素を妨げないようにします。 基本要素の左上近くにグリフを配置します。 要素を追加する場合は、アイコンの配置とバランスを考慮します。

|||
|-|-|
|**配置とバランスの修正**|**正しくない配置とバランス**|
|![正しいアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-22-alignbalancecorrect.png "0404-22_AlignBalanceCorrect")|![正しくないアイコンの分散と配置](../../extensibility/ux-guidelines/media/0404-23-alignbalanceincorrect.png "0404-23_AlignBalanceIncorrect")|

 要素を共有し、セットで使用されるアイコンのサイズ パリティを確認します。 正しくない組み合わせでは、円と矢印が大きくなり、一致しません。

|||
|-|-|
|**正しいサイズのパリティ**|**正しくないサイズのパリティ**|
|![正しいアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-24-sizeparitycorrect.png "0404-24_SizeParityCorrect")|![正しくないアイコンのサイズとパリティ](../../extensibility/ux-guidelines/media/0404-25-sizeparityincorrect.png "0404-25_SizeParityIncorrect")|

 一貫した線と視覚的な太さを使用します。 ビルドするアイコンと他のアイコンとの比較を評価するには、並べて比較します。 16x16 フレーム全体を使用しない、15x15 以下を使用します。 負対正(暗対光)比は 50/50 である必要があります。

|||
|-|-|
|**正しい負対正比**|**負対正比が正しくありません**|
|![1&#41;&#40;アイコンの表示ウェイトを修正する](../../extensibility/ux-guidelines/media/0404-26-visualweightcorrect1.png "0404-26_VisualWeightCorrect1")<br /><br /> ![アイコンの視覚的な重みを修正&#40;2&#41;](../../extensibility/ux-guidelines/media/0404-27-visualweightcorrect2.png "0404-27_VisualWeightCorrect2")<br /><br /> ![3&#41;&#40;アイコンの表示ウェイトを修正する](../../extensibility/ux-guidelines/media/0404-28-visualweightcorrect3.png "0404-28_VisualWeightCorrect3")|![アイコンの正しくない視覚的なウェイト](../../extensibility/ux-guidelines/media/0404-29-visualweightincorrect.png "0404-29_VisualWeightIncorrect")|

 要素の整合性を犠牲にすることなく、簡単で、同等の形状と補完的な角度を使用して要素を構築します。 可能な限り45°または90°の角度を使用してください。

 ![正しいアイコンの角度](../../extensibility/ux-guidelines/media/0404-30-iconanglescorrect.png "0404-30_IconAnglesCorrect")

#### <a name="perspective"></a>パースペクティブ
 アイコンを明確かつわかりやすいままにします。 必要な場合のみ、遠近法と光源を使用します。 アイコン要素のパースペクティブを使用することは避けるべきですが、一部の要素はそれなしでは認識できません。 このような場合、定型化されたパースペクティブは要素の明瞭さを伝えます。

 ![3&#45;点の視点](../../extensibility/ux-guidelines/media/0404-31-3pointperspective.png "0404-31_3PointPerspective")

 **3 点透視投影**

 ![1&#45;点の視点](../../extensibility/ux-guidelines/media/0404-32-1pointperspective.png "0404-32_1PointPerspective")

 **1 点透視投影**

 ほとんどの要素は、右向きまたは角度を付ける必要があります。

 ![右に傾いたアイコン](../../extensibility/ux-guidelines/media/0404-33-angledright.png "0404-33_AngledRight")

 光源は、オブジェクトに必要な明瞭さを追加する場合にのみ使用します。

|||
|-|-|
|**正しい光源**|**光源が正しくない**|
|![正しいアイコンの光源](../../extensibility/ux-guidelines/media/0404-34-lightsourcescorrect.png "0404-34_LightSourcesCorrect")|![正しくないアイコンの光源](../../extensibility/ux-guidelines/media/0404-35-lightsourcesincorrect.png "0404-35_LightSourcesIncorrect")|

 アウトラインは、読みやすさを高めるか、メタファーをより良く伝えるためにのみ使用します。 負の正(暗い光)のバランスは50/50でなければなりません。

|||
|-|-|
|**アウトラインの正しい使用**|**アウトラインの誤った使用**|
|![正しいアウトライン](../../extensibility/ux-guidelines/media/0404-36-outlinescorrect.png "0404-36_OutlinesCorrect")|![正しくないアウトライン](../../extensibility/ux-guidelines/media/0404-37-outlinesincorrect.png "0404-37_OutlinesIncorrect")|

#### <a name="icon-types"></a>アイコンの種類
 **シェルとコマンド バー**のアイコンは、次の要素のうち、1 つのベース、1 つのモディファイヤ、1 つのアクション、または 1 つのステータスのうち 3 つ以下で構成されます。

 ![シェルおよびコマンド バーのアイコン](../../extensibility/ux-guidelines/media/0404-38-shellicons.png "0404-38_ShellIcons")

 **シェルおよびコマンド バーアイコンの例**

 **ツール ウィンドウのコマンド バー**アイコンは、次の要素のうち、1 つのベース、1 つのモディファイヤ、1 つのアクション、または 1 つのステータスのうち 3 つ以下で構成されます。

 ![[ツール] ウィンドウのコマンド バー アイコン](../../extensibility/ux-guidelines/media/0404-39-toolwindowcommandbaricons.png "0404-39_ToolWindowCommandBarIcons")

 **ツール ウィンドウのコマンド バー アイコンの例**

 **ツリー ビューの曖昧さ回避アイコン**は、ベース、1 つのモディファイヤ、1 つのアクション、または 1 つのステータスの 3 つ以下の要素で構成されます。

 ![ツリー ビューの曖昧性解消子のアイコン](../../extensibility/ux-guidelines/media/0404-40-treeviewicons.png "0404-40_TreeViewIcons")

 **ツリー ビューの曖昧さ回避アイコンの例**

 **状態ベースの値**分類アイコンは、アクティブ、アクティブ無効、および無効の非アクティブ状態にあります。

 ![分類値アイコンに基づく状態&#45;](../../extensibility/ux-guidelines/media/0404-41-statebasedtaxonomy.png "0404-41_StateBasedTaxonomy")

 **州ベースの値分類アイコンの例**

 **IntelliSense**アイコンは、次の要素のうち、1 つのベース、1 つの修飾子、および 1 つのステータスのうち 3 つ以下で構成されます。

 ![IntelliSense アイコン](../../extensibility/ux-guidelines/media/0404-42-intellisenseicons.png "0404-42_IntelliSenseIcons")

 **インテリセンス アイコンの例**

 **小さな (16x16) プロジェクト**アイコンには、2 つの要素 (1 つのベースと 1 つの修飾子) を含めるべきではありません。

 ![16x16 プロジェクト アイコン &#40;1&#41;](../../extensibility/ux-guidelines/media/0404-43-16x16project1.png "0404-43_16x16Project1") ![16x16 プロジェクト アイコン &#40;2&#41;](../../extensibility/ux-guidelines/media/0404-44-16x16project2.png "0404-44_16x16Project2") ![16x16 プロジェクト アイコン &#40;3&#41;](../../extensibility/ux-guidelines/media/0404-45-16x16project3.png "0404-45_16x16Project3")

 **小さい (16x16) プロジェクト アイコンの例**

 **大きい (32x32) プロジェクト**アイコンは、次の 4 つ以下の要素で構成されます: 1 つのベース、1 ~ 2 つの修飾子、および 1 つの言語オーバーレイ。

 ![32 x 32 プロジェクト アイコン](../../extensibility/ux-guidelines/media/0404-46-32x32project.png "0404-46_32x32Project")

 **大きい (32x32) プロジェクト アイコンの例**

### <a name="production-details"></a>生産の詳細
 すべての新しい UI 要素は、Windows プレゼンテーション ファンデーション (WPF) を使用して作成する必要があり、WPF のすべての新しいアイコンは 32 ビット PNG 形式である必要があります。 24 ビット PNG は、透明をサポートしない従来の形式であるため、アイコンにはお勧めできません。

 解像度を 96 DPI で保存します。

#### <a name="file-types"></a>ファイルの種類

- **32 ビット PNG:** アイコンの推奨形式。 単一のラスター (ピクセル) 画像を格納できる、無損失なデータ圧縮ファイル形式。 32 ビット PNG ファイルは、アルファ チャネルの透過性、ガンマ補正、インターレースをサポートします。

- **32 ビット BMP:** 非 WPF コントロールの場合。 32 ビット BMP は、RGB/A イメージ形式であり、アルファ チャネルの透過性を持つ真のカラー イメージです。 アルファチャンネルは Adobe Photoshop で指定された透明層で、ビットマップ内に追加の(4 番目の)カラーチャンネルとして保存されます。 黒の背景は、すべての 32 ビット BMP ファイルにアートワーク制作中に追加され、色深度に関する簡単な視覚的な手掛かりを提供します。 この黒の背景は、UI でマスクされる領域を表します。

- **32 ビットの ICO:** プロジェクト アイコンと項目の追加。 すべてのICOファイルは、アルファチャンネルの透明度(RGB / A)を持つ32ビットの真の色です。 ICOファイルは複数のサイズと色深度を格納できるため、Vistaアイコンは16x16、32x32、48x48、256x256の画像サイズを含むICO形式で表示されることがよくあります。 Windows エクスプローラで正しく表示するには、各イメージ サイズの 24 ビットおよび 8 ビットの色深度に、ICO ファイルを保存する必要があります。

- **XAML:** デザイン サーフェイスと Windows 装飾用。 XAML アイコンは、スケーリング、回転、ファイリング、および透過性をサポートするベクター ベースのイメージ ファイルです。 現在の Visual Studio では一般的ではありませんが、柔軟性のために人気が高まっています。

- **SVG**

- **24 ビット BMP:** Visual Studio コマンド バーの場合。 真の RGB イメージ形式である 24 ビット BMP は、マスゼンタ (R=255、 G=0、B= 255) をノックアウト透過性レイヤーのカラーキーとして使用して、透過性のレイヤーを作成するアイコン規則です。 24 ビット BMP では、すべてのマゼンタ サーフェスが背景色を使用して表示されます。

- **24 ビット GIF:** Visual Studio コマンド バーの場合。 透過性をサポートする、真のカラー RGB イメージ形式。 GIF ファイルは、ウィザードのアートワークや GIF アニメーションでよく使用されます。

### <a name="icon-construction"></a>アイコン構造
 Visual Studio の最小アイコン サイズは 16 x 16 です。 一般的な使用の最大の 32x32 です。 アイコンをデザインする際は、16x16、24x24、32x32 フレーム全体が埋め尽くされないことに注意してください。 読みやすい、均一なアイコンの構造は、ユーザーの認識に不可欠です。 アイコンを作成する際は、次の点に従ってください。

- アイコンは明確で理解でき、一貫性があるはずです。

- ステータス通知要素を単一のアイコンとして使用し、アイコンの基本要素の上に重ね合わせて使用しないことをおやめください。 特定のコンテキストでは、UI は、基本要素とペアリングする状態要素を必要があります。

- プロジェクト アイコンは、通常、いくつかのサイズを含む .ico ファイルです。 更新されるのは、16x16、24x24、および 32x32 のアイコンのみです。 ほとんどの 16x16 と 24x24 のアイコンには、同じ要素が含まれます。 32x32 アイコンには、プロジェクト言語の種類 (該当する場合) など、詳細が含まれています。

- 32x32 アイコンの場合、基本要素は通常 2 ピクセルの線の太さになります。 1 ピクセルまたは 2 ピクセルの線の太さを詳細要素に使用できます。 どちらがより適しているかを判断するためにあなたの最善の判断を使用してください。

- 16x16 と 24 x 24 のアイコンの要素間の間隔が少なくとも 1 ピクセルです。 32 x 32 アイコンの場合、要素間とモディファイヤと基本要素の間に 2 ピクセルの間隔を使用します。

  ![16x16、24x24、および 32x32 アイコンの要素間スペース](../../extensibility/ux-guidelines/media/0404-47-elementspacing.png "0404-47_ElementSpacing")

  **16x16、24x24、および32x32のサイズのアイコンの要素間隔**

#### <a name="color-and-accessibility"></a>色とアクセシビリティ
 Visual Studio の準拠ガイドラインでは、製品内のすべてのアイコンが色とコントラストのアクセシビリティ要件を満たす必要があります。 これはアイコンの反転によって実現され、設計する際には、製品内でプログラムによって反転されることを認識しておく必要があります。

 Visual Studio アイコンでの色の使用の詳細については、「[イメージでの色の使用](../../extensibility/ux-guidelines/images-and-icons-for-visual-studio.md#BKMK_UsingColorInImages)」を参照してください。

## <a name="using-color-in-images"></a><a name="BKMK_UsingColorInImages"></a>画像の色を使用する

### <a name="overview"></a>概要
 Visual Studio のアイコンは、主に単色です。 色は、特定の情報を伝えるために予約され、装飾のために決してありません。 色が使用されます。

- アクションを示す

- ステータス通知をユーザーに通知する

- 言語の所属を指定する

- IntelliSense 内の項目を区別する

### <a name="accessibility"></a>アクセシビリティ
 Visual Studio の準拠ガイドラインでは、製品にチェックインされているすべてのアイコンが色とコントラストのアクセシビリティ要件を満たす必要があります。 ビジュアル言語パレットの色がテストされ、これらの要件を満たしています。

#### <a name="color-inversion-for-dark-themes"></a>暗いテーマの色反転
 Visual Studio の暗いテーマで正しいコントラスト比でアイコンを表示するために、プログラムによって反転が適用されます。 このガイドの色は、正しく反転するように部分的に選択されています。 色の使用をこのパレットに制限するか、反転が適用されると予測できない結果が得られます。

 ![色が反転されているアイコンの例](../../extensibility/ux-guidelines/media/0405-01-darkthemeinversion.png "0405-01_DarkThemeInversion")

 **色が反転したアイコンの例**

### <a name="base-palette"></a>ベースパレット
 すべての標準アイコンには、3 つの基本色が含まれています。 アイコンにはグラデーションやドロップ シャドウは含まれておらず、3D ツール アイコンの場合は 1 つまたは 2 つの例外があります。

|使用法|名前|値(ライトテーマ)|スウォッチ|例|
|-----------|----------|---------------------------|------------|-------------|
|背景/暗い|VS BG|424242 / 66,66,66|![見本 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|![基本パレットの例](../../extensibility/ux-guidelines/media/0405-02-basepaletteexample.png "0405-02_BasePaletteExample")|
|前景/光|VS FG|F0EFF1 / 240,239,241|![見本 F0EFF1](../../extensibility/ux-guidelines/media/0405-f0eff1.png "0405_F0EFF1")||
|[外枠]|VS アウト|F6F6F6 / 246,246,246|![見本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")||

 基本色に加えて、各アイコンには拡張パレットから 1 つの追加の色が含まれる場合があります。

### <a name="extended-palette"></a>拡張パレット

#### <a name="action-modifiers"></a>アクション修飾子
 以下の 4 つの色は、アクション修飾子で必要なアクションの種類を示しています。

|使用法|名前|価値(すべてのテーマ)|スウォッチ|
|-----------|----------|--------------------------|------------|
|Positive|VS アクショングリーン|388A34 / 56,138,52|![見本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|Negative|VS アクション レッド|A1260D / 161,38,13|![見本 A1260D](../../extensibility/ux-guidelines/media/0405-a1260d.png "0405_A1260D")|
|中立|VS アクションブルー|00539C / 0,83,156|![見本 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|作成/新規|VS アクションオレンジ|C27D1A / 194,156,26|![見本 C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|

##### <a name="examples"></a>例
 緑色は、「追加」、「実行」、「再生」、「検証」などのポジティブなアクション修飾子に使用されます。

|||||
|-|-|-|-|
|![アイコンを実行](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405-03_ActionModifierRun")**します 実行**|![クエリの実行アイコン](../../extensibility/ux-guidelines/media/0405-04-executequery.png "0405-04_ExecuteQuery")**クエリの実行**|![すべてのステップを再生アイコン](../../extensibility/ux-guidelines/media/0405-05-playallsteps.png "0405-05_PlayAllSteps")**すべてのステップを再生**|![コントロールの追加アイコン](../../extensibility/ux-guidelines/media/0405-06-addcontrol.png "0405-06_AddControl")**コントロールの追加**|

 赤は、「削除」、「停止」、「キャンセル」、「閉じる」などの負のアクション修飾子に使用されます。

|||||
|-|-|-|-|
|![リレーションシップの削除アイコン](../../extensibility/ux-guidelines/media/0405-07-deleterelationship.png "0405-07_DeleteRelationship") **[リレーションシップの削除]**|![列の削除アイコン](../../extensibility/ux-guidelines/media/0405-08-deletecolumn.png "0405-08_DeleteColumn")**列の削除**|![クエリの停止アイコン](../../extensibility/ux-guidelines/media/0405-09-stopquery.png "0405-09_StopQuery")**クエリの停止**|![接続オフラインアイコン](../../extensibility/ux-guidelines/media/0405-10-connectionoffline.png "0405-10_ConnectionOffline")**接続オフライン**|

 青は、最も一般的に矢印として表されるニュートラル アクション修飾子 ("開く""""次"、"前へ"、"インポート"、"エクスポート" など) に適用されます。

|||||
|-|-|-|-|
|![フィールドアイコンに移動](../../extensibility/ux-guidelines/media/0405-11-gotofield.png "0405-11_GoToField")**Go to Field**|![バッチチェックイン&#45;アイコン](../../extensibility/ux-guidelines/media/0405-12-batchedcheckin.png "0405-12_BatchedCheckIn")**バッチチェックイン**|![アドレス エディタ アイコン](../../extensibility/ux-guidelines/media/0405-13-addresseditor.png "0405-13_AddressEditor")**アドレス エディタ**|![アソシエーション エディタ アイコン](../../extensibility/ux-guidelines/media/0405-14-associationeditor.png "0405-14_AssociationEditor")**アソシエーション エディタ**|

 ダークゴールドは、主に「新規」モディファイヤに使用されます。

|||||
|-|-|-|-|
|![新しいプロジェクト アイコン](../../extensibility/ux-guidelines/media/0405-15-newproject.png "0405-15_NewProject")**新しいプロジェクト**|![新しいグラフの作成アイコン](../../extensibility/ux-guidelines/media/0405-16-createnewgraph.png "0405-16_CreateNewGraph")**新しいグラフを作成**|![新しい単体テスト アイコン](../../extensibility/ux-guidelines/media/0405-17-newunittest.png "0405-17_NewUnitTest")**新しい単体テスト**|![新しいリスト アイテム アイコン](../../extensibility/ux-guidelines/media/0405-18-newlistitem.png "0405-18_NewListItem") **[新しいリスト アイテム]**|

#### <a name="special-cases"></a>特殊なケース
 特殊な場合、色付きアクション修飾子は独立してスタンドアロン アイコンとして使用できます。 アイコンに使用される色は、アイコンが関連付けられているアクションを反映します。 この使用は、次のアイコンを含む小さなサブセットに限定されます。

||||||
|-|-|-|-|-|
|![アイコンを実行](../../extensibility/ux-guidelines/media/0405-03-actionmodifierrun.png "0405-03_ActionModifierRun")**します 実行**|![停止アイコン](../../extensibility/ux-guidelines/media/0405-19-stop.png "0405-19_Stop")**停止**|![削除アイコン](../../extensibility/ux-guidelines/media/0405-20-delete.png "0405-20_Delete")**削除**|![保存アイコン](../../extensibility/ux-guidelines/media/0405-21-save.png "0405-21_Save")**保存**|![戻るアイコン](../../extensibility/ux-guidelines/media/0405-22-navigateback.png "0405-22_NavigateBack")**のナビゲート 戻る**|

### <a name="code-hierarchy-palette"></a>コード階層パレット

#### <a name="folder"></a>Folder

|使用法|名前|価値(すべてのテーマ)|スウォッチ|例|
|-----------|----------|--------------------------|------------|-------------|
|Folders|Folder|DCB67A / 220,182,122|![見本 DCB67A](../../extensibility/ux-guidelines/media/0405-dcb67a.png "0405_DCB67A")|![フォルダーの色のアイコン](../../extensibility/ux-guidelines/media/0405-23-foldercolor.png "0405-23_FolderColor")|

#### <a name="visual-studio-languages"></a>Visual Studio の言語
 Visual Studio で使用できる共通の言語またはプラットフォームのそれぞれに、色が関連付けられます。 これらの色は、基本アイコン、または複合アイコンの右上隅に表示される言語修飾子に使用されます。

|使用法|名前|価値(すべてのテーマ)|スウォッチ|
|-----------|----------|--------------------------|------------|
|ASP、 HTML、 WPF|ASP HTML WPF ブルー|0095D7 / 0,149,215|![見本 0095D7](../../extensibility/ux-guidelines/media/0405-0096d7.png "0405_0096D7")|
|C++|CPPパープル|9B4F96 / 155,79,150|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|C#|CS グリーン (VS アクショングリーン)|388A34 / 56,138,52|![見本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|CSS|CSSレッド|BD1E2D / 189,30,45|![見本 BD1E2D](../../extensibility/ux-guidelines/media/0405-bd1e2d.png "0405_BD1E2D")|
|F#|FSパープル|672878 / 103,40,120|![見本 672878](../../extensibility/ux-guidelines/media/0405-672878.png "0405_672878")|
|JavaScript|JSオレンジ|F16421 / 241,100,33|![見本 F16421](../../extensibility/ux-guidelines/media/0405-f16421.png "0405_F16421")|
|VB|VB ブルー (VS アクションブルー)|00539C / 0,83,156|![見本 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|TypeScript|TSオレンジ|E04C06 / 224,76,6|![見本 E04C06](../../extensibility/ux-guidelines/media/0405-e04c06.png "0405_E04C06")|
|Python|PYグリーン|879636 / 135,150,54|![見本 879636](../../extensibility/ux-guidelines/media/0405-879636.png "0405_879636")|

##### <a name="examples-of-icons-with-language-modifiers"></a>言語修飾子を含むアイコンの例

|||||||
|-|-|-|-|-|-|
|![ビジュアル ベーシック アイコン](../../extensibility/ux-guidelines/media/0405-25-vb.png "0405-25_VB") **VB**|![C&#35; アイコン](../../extensibility/ux-guidelines/media/0405-26-csharp.png "0405-26_CSharp") **C#**|![C&#43;&#43; アイコン](../../extensibility/ux-guidelines/media/0405-27-cplusplus.png "0405-27_CPlusPlus") **C++**|![F&#35; アイコン](../../extensibility/ux-guidelines/media/0405-28-fsharp.png "0405-28_FSharp") **F#**|![Javaスクリプトアイコン](../../extensibility/ux-guidelines/media/0405-29-javascript.png "0405-29_JavaScript")**JavaScript**|![Python アイコン](../../extensibility/ux-guidelines/media/0405-30-python.png "0405-30_Python") **Python**|
|![HTML アイコン](../../extensibility/ux-guidelines/media/0405-31-html.png "0405-31_HTML") **HTML**|![WPF アイコン](../../extensibility/ux-guidelines/media/0405-32-wpf.png "0405-32_WPF") **WPF**|![ASP アイコン](../../extensibility/ux-guidelines/media/0405-33-asp.png "0405-33_ASP") **ASP**|![CSS アイコン](../../extensibility/ux-guidelines/media/0405-34-css.png "0405-34_CSS") **CSS**|![タイプスクリプトアイコン](../../extensibility/ux-guidelines/media/0405-35-typescript.png "0405-35_TypeScript")**タイプスクリプト**||

#### <a name="intellisense"></a>IntelliSense
 IntelliSense アイコンは、専用のカラー パレットを使用します。 これらの色は、ユーザーが IntelliSense ポップアップ リスト内のさまざまな項目をすばやく区別するために使用されます。

|使用法|名前|価値(すべてのテーマ)|スウォッチ|
|-----------|----------|--------------------------|------------|
|クラス,イベント|VS アクションオレンジ|C27D1A / 194,125,26|![見本 C27D1A](../../extensibility/ux-guidelines/media/0405-c27d1a.png "0405_C27D1A")|
|拡張メソッド、メソッド、モジュール、デリゲート|VS アクションパープル|652D90 / 101,45,144|![見本 652D90](../../extensibility/ux-guidelines/media/0405-652d90.png "0405_652D90")|
|フィールド、列挙項目、マクロ、構造体、共用体値型、演算子、インタフェース|VS アクションブルー|00539C / 0,83,156|![見本 00539C](../../extensibility/ux-guidelines/media/0405-00539c.png "0405_00539C")|
|Object|VS アクショングリーン|388A34 / 56,138,52|![見本 388A34](../../extensibility/ux-guidelines/media/0405-388a34.png "0405_388A34")|
|定数、例外、列挙項目、マップ、マップ項目、名前空間、テンプレート、型定義|背景 (VS BG)|424242 / 66,66,66|![見本 424242](../../extensibility/ux-guidelines/media/0405-424242.png "0405_424242")|

##### <a name="examples-of-intellisense-icons"></a>インテリセンス アイコンの例

||||||
|-|-|-|-|-|
|![クラスアイコン クラス](../../extensibility/ux-guidelines/media/0405-36-intellisenseclass.png "0405-36_IntelliSenseClass")**Class**|![プライベート イベント アイコン プライベート](../../extensibility/ux-guidelines/media/0405-37-intellisenseprivateevent.png "0405-37_IntelliSensePrivateEvent")**イベント**|![インテリセンス デリゲート アイコン](../../extensibility/ux-guidelines/media/0405-38-intellisensedelegate.png "0405-38_IntelliSenseDelegate")**デリゲート**|![メソッドのフレンド アイコン](../../extensibility/ux-guidelines/media/0405-39-intellisensemethodfriend.png "0405-39_IntelliSenseMethodFriend")**メソッド フレンド**|![フィールド アイコン](../../extensibility/ux-guidelines/media/0405-40-field.png "0405-40_Field")**フィールド**|
|![IntelliSense プロテクト列挙型項目アイコン](../../extensibility/ux-guidelines/media/0405-41-intellisenseprotectedenumitem.png "0405-41_IntelliSenseProtectedEnumItem")**保護された列挙項目**|![オブジェクト アイコン](../../extensibility/ux-guidelines/media/0405-42-intellisenseobject.png "0405-42_IntelliSenseObject")**オブジェクト**|![IntelliSense テンプレート アイコン](../../extensibility/ux-guidelines/media/0405-43-intellisensetemplate.png "0405-43_IntelliSenseTemplate")**テンプレート**|![IntelliSense 例外のショートカット アイコン](../../extensibility/ux-guidelines/media/0405-44-intellisenseexceptionshortcut.png "0405-44_IntelliSenseExceptionShortcut")**例外のショートカット**||

### <a name="notifications"></a>通知
 Visual Studio での通知は、状態を示すために使用されます。 通知パレットでは、次の 4 色と黒または白の前景塗りつぶしオプションを使用して、次のステータス レベルで通知を定義します。

|使用法|名前|価値(すべてのテーマ)|スウォッチ|
|-----------|----------|--------------------------|------------|
|ステータス: ニュートラル|通知青(VSブルー)|1BA1E2 / 27,161,226|![見本 1BA1E2](../../extensibility/ux-guidelines/media/0405-1ba1e2.png "0405_1BA1E2")|
|ステータス: 正の値|通知グリーン (VS グリーン)|339933 / 51,153,51|![見本 339933](../../extensibility/ux-guidelines/media/0405-339933.png "0405_339933")|
|ステータス: 負|通知赤 (VS レッド)|E51400 / 229,20,0|![見本 E51400](../../extensibility/ux-guidelines/media/0405-e51400.png "0405_E51400")|
|ステータス: 警告|通知黄色 (VS オレンジ色)|FFCC00 / 255,204,0|![見本 FFCC00](../../extensibility/ux-guidelines/media/0405-ffcc00.png "0405_FFCC00")|
|前景の塗りつぶし|通知黒 (黒)|000000 / 0,0,0|![スウォッチ &#35;000000](../../extensibility/ux-guidelines/media/0405-000000.png "0405_000000")|
|前景の塗りつぶし|通知白 (白)|FFFFFF / 255,255,255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|

#### <a name="examples-of-notification-icons"></a>通知アイコンの例

|||||
|-|-|-|-|
|![警告アイコン](../../extensibility/ux-guidelines/media/0405-45-alert.png "0405-45_Alert")**アラート**|![警告アイコン](../../extensibility/ux-guidelines/media/0405-48-warning.png "0405-48_Warning")**警告**|![完了アイコン](../../extensibility/ux-guidelines/media/0405-46-complete.png "0405-46_Complete")**完了**|![停止アイコン](../../extensibility/ux-guidelines/media/0405-47-stop.png "0405-47_Stop")**停止**|

### <a name="visual-studio-online"></a>Visual Studio Online
 一般に、Visual Studio オンラインは、ブラウザーでホストされる機能で構成されます。 色は環境によって異なりますが、スタイルは変わりません。

|グループ|使用法|名前|価値(すべてのテーマ)|スウォッチ|
|-----------|-----------|----------|--------------------------|------------|
|TFS|バックグラウンド|TFSO BG|656565/ 101, 101, 101|![見本 656565](../../extensibility/ux-guidelines/media/0405-656565.png "0405_656565")|
|TFS|[外枠]|TFSO アウト|FFFFFF / 255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|ナパ|バックグラウンド|White|FFFFFF / 255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|モナコ|バックグラウンド|White|FFFFFF / 255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|バックグラウンド|White|FFFFFF / 255, 255, 255|![見本 FFFFFF](../../extensibility/ux-guidelines/media/0405-ffffff.png "0405_FFFFFF")|
|F12|Normal|F12 Grey_Primary|555555 / 85, 85, 85|![見本 555555](../../extensibility/ux-guidelines/media/0405-555555.png "0405_555555")|
|F12|ホバー|F12 Blue_Hover|2279BF / 34,121,191|![見本 2279BF](../../extensibility/ux-guidelines/media/0405-2279bf.png "0405_2279BF")|
|F12|無効|F12 LtGrey_Disabled|アババック / 171,171,172|![見本 ABABAC](../../extensibility/ux-guidelines/media/0405-ababac.png "0405_ABABAC")|
|F12|ホバーの背景|ホバーbg|D9EBF7 / 217,235,247|![見本 D9EBF7](../../extensibility/ux-guidelines/media/0405-d9ebf7.png "0405_D9EBF7")|
|F12|押された背景|押されたbg|B2D7F0 / 178,215,240|![見本 B2D7F0](../../extensibility/ux-guidelines/media/0405-b2d7f0.png "0405_B2D7F0")|
|F12|[外枠]|VS アウト|F6F6F6 / 246,246,246|![見本 F6F6F6](../../extensibility/ux-guidelines/media/0405-f6f6f6.png "0405_F6F6F6")|
|F12|Information|Information|00BCF2 / 0,188,242|![見本 00BCF2](../../extensibility/ux-guidelines/media/0405-00bcf2.png "0405_00BCF2")|
|F12|警告|警告|F28300 / 242,131,0|![見本 F28300](../../extensibility/ux-guidelines/media/0405-f28300.png "0405_F28300")|
|F12|エラー/ネガティブ|Error_Negative|E81123 / 232,17,35|![見本 E81123](../../extensibility/ux-guidelines/media/0405-e81123.png "0405_E81123")|
|F12|開始/ポジティブ|Start_Positive|009E49 / 0,158,73|![見本 009E49](../../extensibility/ux-guidelines/media/0405-009e49.png "0405_009E49")|
|F12|ブレークタイプ|ブレークタイプ|9B4F96 / 155,79,150|![見本 9B4F96](../../extensibility/ux-guidelines/media/0405-9b4f96.png "0405_9B4F96")|
|F12|イベントマーク|イベントマーク|A51F00 / 165,31,0|![見本 A51F00](../../extensibility/ux-guidelines/media/0405-a51f00.png "0405_A51F00")|
|F12|ユーザー マーク|ユーザー マーク|F16220 / 241,98,32|![見本 F16220](../../extensibility/ux-guidelines/media/0405-f16220.png "0405_F16220")|

#### <a name="examples-of-visual-studio-online-icons"></a>ビジュアル スタジオ オンライン アイコンの例

|TFS オンライン||||
|----------------|-|-|-|
|![TFS オンライン チーム アイコン](../../extensibility/ux-guidelines/media/0405-49-tfsonlineteam.png "0405-49_TFSOnlineTeam")**オンライン チーム**|![TFS 情報アイコン](../../extensibility/ux-guidelines/media/0405-50-tfsinformation.png "0405-50_TFSInformation")**情報**|![TFS 履歴アイコン](../../extensibility/ux-guidelines/media/0405-51-tfshistory.png "0405-51_TFSHistory")**履歴**|![TFS ブランチ アイコン](../../extensibility/ux-guidelines/media/0405-52-tfsbranch.png "0405-52_TFSBranch")**ブランチ**|

|ナパ||||
|----------|-|-|-|
|![ナパ コンテンツ アイコン](../../extensibility/ux-guidelines/media/0405-53-napacontent.png "0405-53_NapaContent")**コンテンツ**|![ナパオフィスメールアイコン](../../extensibility/ux-guidelines/media/0405-54-napaofficemail.png "0405-54_NapaOfficeMail")**オフィスメール**|![ナパ SharePoint アイコン](../../extensibility/ux-guidelines/media/0405-55-napasharepoint.png "0405-55_NapaSharePoint")**SharePoint**|![Napa 作業ウィンドウ アイコン](../../extensibility/ux-guidelines/media/0405-56-napataskpane.png "0405-56_NapaTaskPane")**タスク ウィンドウ**|

|モナコ||||
|------------|-|-|-|
|![モナコファイルアイコン](../../extensibility/ux-guidelines/media/0405-57-monacofiles.png "0405-57_MonacoFiles")**ファイル**|![モナコ Git アイコン](../../extensibility/ux-guidelines/media/0405-58-monacogit.png "0405-58_MonacoGit") **Git**|![モナコ検索アイコン](../../extensibility/ux-guidelines/media/0405-59-monacosearch.png "0405-59_MonacoSearch")**検索**|![モナコテキストアイコン](../../extensibility/ux-guidelines/media/0405-60-monacotext.png "0405-60_MonacoText")**テキスト**|

|F12||||
|---------|-|-|-|
|![F12かなりコードアイコン](../../extensibility/ux-guidelines/media/0405-61-f12prettycode.png "0405-61_F12PrettyCode")**プリティコード**|![F12 警告アイコン](../../extensibility/ux-guidelines/media/0405-62-f12warning.png "0405-62_F12Warning")**警告**|![F12 エミュレート アイコン](../../extensibility/ux-guidelines/media/0405-63-f12emulate.png "0405-63_F12Emulate")**エミュレーション**|
