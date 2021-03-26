---
title: VSIX カラーエディター |Microsoft Docs
description: Visual studio 拡張機能のカラーエディターツールについて説明します。このツールでは、Visual Studio のカスタム色を作成および編集したり、テーマリソースキーを生成したりできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 70879c5d-e0f0-4845-993c-2f4229869706
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bfd6ff388119d829c2e5994c0fa78d01958326bc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069284"
---
# <a name="vsix-color-editor"></a>VSIX カラー エディター
Visual Studio 拡張機能のカラーエディターツールでは、Visual Studio のカスタム色を作成および編集できます。 ツールでは、色をコードで使用できるように、テーマリソースキーを生成することもできます。 このツールは、テーマをサポートする Visual Studio 拡張機能の色を作成する場合に便利です。 このツールでは、pkgdef ファイルと .xml ファイルを開くことができます。 Visual studio のテーマ (vstheme ファイル) は、ファイル拡張子を .xml に変更することで、Visual Studio 拡張機能のカラーエディターと共に使用できます。 また、vstheme ファイルを現在の .xml ファイルにインポートすることもできます。

 ![VSIX カラー エディターのヒーロー](../../extensibility/internals/media/vsix-color-editor-hero.png "VSIX カラー エディターのヒーロー")

 **パッケージ定義ファイル**

 パッケージ定義 (pkgdef) ファイルは、テーマを定義するファイルです。 色自体は、pkgdef ファイルにコンパイルされるテーマの色 .xml ファイルに格納されます。 Pkgdef ファイルは、Visual Studio の検索可能な場所に配置され、実行時に処理されて、テーマを定義するために結合されます。

 **色トークン**

 色トークンは、次の4つの要素で構成されます。

- **カテゴリ名:** 一連の色を論理的にグループ化したもの。 必要な UI 要素または UI 要素のグループに固有の色が既に存在する場合は、既存のカテゴリ名を使用します。

- **トークン名:** 色トークンとトークンセットのわかりやすい名前。 設定には、バックグラウンドおよびフォアグラウンド (テキスト) トークンの名前とそのすべての状態が含まれます。これらの名前は、ペアとそれらが適用される状態を簡単に識別できるように、という名前にする必要があります。

- **色の値 (または色相):** 配色テーマごとに必要です。 背景とテキストの色の値は、常にペアで作成します。 色は背景と前景のペアになっているため、描画される背景色に対してテキスト (前景) の色を常に読み取ることができます。 これらの色はリンクされており、UI で一緒に使用されます。 背景がテキストで使用することを意図していない場合は、前景色を定義しないでください。

- **システムカラー名:** ハイコントラストディスプレイで使用します。

## <a name="how-to-use-the-tool"></a>ツールの使用方法
 可能な限り、必要に応じて、既存の Visual Studio の色を新しいものにする代わりに再利用する必要があります。 ただし、適切な色が定義されていない場合は、拡張機能のテーマとの互換性を維持するためにカスタムの色を作成する必要があります。

 **新しい色のトークンの作成**

 Visual Studio 拡張機能のカラーエディターを使用してカスタムの色を作成するには、次の手順を実行します。

1. 新しいカラートークンのカテゴリ名とトークン名を決定します。

2. UI 要素が各テーマに使用する色相とハイコントラストのシステムカラーを選択します。

3. カラーエディターを使用して、新しいカラートークンを作成します。

4. Visual Studio 拡張機能で色を使用します。

5. Visual Studio で変更をテストします。

   **手順 1: 新しいカラートークンのカテゴリ名とトークン名を決定します。**

   VSColor の推奨される名前付けスキームは **[Category] [UI type] [State]** です。 VSColor 名には冗長であるため、"color" という語は使用しないでください。

   カテゴリ名は論理グループを提供します。可能な限り狭くするように定義する必要があります。 たとえば、単一のツールウィンドウの名前はカテゴリ名にすることができますが、ビジネスユニットまたはプロジェクトチーム全体の名前は同じではありません。 エントリをカテゴリにグループ化すると、同じ名前の色が混同されるのを防ぐことができます。

   トークン名は、要素の種類と、その色が適用される状況 ("状態") を明確に示す必要があります。 たとえば、アクティブなデータヒントの **[UI 型]** に "**DataTip**" という名前を付け、 **[State]** に "**active**" という名前を付けて、"**DataTipActive**" という色の名前を付けることができます。 データヒントにはテキストが含まれているため、前景色と背景色の両方を定義する必要があります。 背景/前景のペアリングを使用すると、カラーエディターによって背景の色 "**DataTipActive**" と前景の "**DataTipActiveText**" が自動的に作成されます。

   UI の部分に状態が1つしかない場合は、名前の **[state]** 部分を省略できます。 たとえば、検索ボックスに境界線があり、境界線の色に影響する状態の変更がない場合、境界線の色トークンの名前は単に "**Searchboxborder**" と呼ばれます。

   一般的な状態名には次のものがあります。

- アクティブ

- 非アクティブ

- MouseOver

- MouseDown

- オン

- フォーカスされている

  リスト項目コントロールの一部に対するいくつかのトークン名の例を次に示します。

- ListItem

- ListItemBorder

- ListItemMouseOver

- ListItemMouseOverBorder

- ListItemSelected

- ListItemSelectedBorder

- ListItemDisabled

- ListItemDisabledBorder

  **手順 2: UI 要素が各テーマに使用する色相とハイコントラストのシステムカラーを選択します。**

  UI に対してカスタム色を選択する場合は、同様の既存の UI 要素を選択し、その色をベースとして使用します。 インボックスの UI 要素の色は、レビューとテストが行われているため、適切に表示され、すべてのテーマで正しく動作します。

  **手順 3: カラーエディターを使用して、新しいカラートークンを作成します。**

  カラーエディターを起動し、新しいカスタムテーマ色の .xml ファイルを開くか、作成します。 メニューから [ **編集 > 新しい色** ] を選択します。 これにより、カテゴリと、そのカテゴリ内の色エントリの1つ以上の名前を指定するためのダイアログが表示されます。

  ![VSIX カラー エディターの新しい色](../../extensibility/internals/media/vsix-color-editor-new-color.png "VSIX カラー エディターの新しい色")

  既存のカテゴリを選択するか、[ **新しいカテゴリ** ] を選択して新しいカテゴリを作成します。 別のダイアログが開き、新しいカテゴリ名が作成されます。

  ![VSIX カラー エディターの新しいカテゴリ](../../extensibility/internals/media/vsix-color-editor-new-category.png "VSIX カラー エディターの新しいカテゴリ")

  新しいカテゴリは、[ **新しい色** のカテゴリ] ドロップダウンメニューで使用できるようになります。 カテゴリを選択したら、新しい色トークンごとに1行に1つの名前を入力し、完了したら [作成] を選択します。

  ![VSIX カラー エディターの新しい色 (塗りつぶし)](../../extensibility/internals/media/vsix-color-editor-new-color-filled.png "VSIX カラー エディターの新しい色 (塗りつぶし)")

  色の値は、背景と前景のペアで表示されます。色が定義されていないことを示す "None" が付いています。 注: 色にテキストの色と背景の色のペアがない場合は、背景のみを定義する必要があります。

  ![VSIX カラー エディターのカラー値](../../extensibility/internals/media/vsix-color-editor-color-values.png "VSIX カラー エディターのカラー値")

  色トークンを編集するには、そのトークンのテーマ (列) の色エントリを選択します。 色の値を追加するには、8桁の ARGB 形式で16進数の色の値を入力するか、セルにシステムの色の名前を入力するか、ドロップダウンメニューを使用して、一連の色スライダーまたはシステムカラーの一覧から目的の色を選択します。

  ![VSIX カラー エディターの色の編集](../../extensibility/internals/media/vsix-color-editor-edit-color.png "VSIX カラー エディターの色の編集")

  ![VSIX カラー エディターの背景](../../extensibility/internals/media/vsix-color-editor-background.png "VSIX カラー エディターの背景")

  テキストを表示する必要がないコンポーネントの場合は、色の値を1つだけ入力します。背景色です。 それ以外の場合は、[背景] と [テキストの色] の両方の値をスラッシュで区切って入力します。

  ハイコントラストの値を入力するときに、Windows システムの有効な色の名前を入力します。 ハードコードされた ARGB 値は入力しないでください。 有効なシステムカラー名の一覧を表示するには、[色の値] ドロップダウンメニューから [背景: システム] または [前景: システム] を選択します。 テキストコンポーネントを含む要素を作成する場合は、適切な背景/テキストシステムの色のペアを使用するか、テキストを判読できない可能性があります。

  色トークンの作成、設定、および編集が完了したら、必要な .xml または pkgdef 形式に保存します。 背景も前景にも設定されていないカラートークンは、.xml 形式で空の色として保存されますが、pkgdef 形式では破棄されます。 空の色を pkgdef ファイルに保存しようとすると、色が失われる可能性があることを示すダイアログが表示されます。

  **手順 4: Visual Studio 拡張機能で色を使用します。**

  新しい色トークンを定義した後、[ビルドアクション] を [コンテンツ] に設定し、[True] に設定して、[プロジェクトファイルに pkgdef] を追加します。

  ![VSIX カラー エディターの pkgdef](../../extensibility/internals/media/vsix-color-editor-pkgdef.png "VSIX カラー エディターの pkgdef")

  Visual Studio 拡張機能のカラーエディターで、[ファイル > 表示] をクリックして、WPF ベースの UI でカスタムカラーにアクセスするために使用するコードを表示します。

  ![VSIX カラー エディターのリソース コード ビューアー](../../extensibility/internals/media/vsix-color-editor-resource-code-viewer.png "VSIX カラー エディターのリソース コード ビューアー")

  このコードをプロジェクトの静的クラスに含めます。 VisualStudio への参照をプロジェクトに追加して、 **\<VSVersion>.0.dll** **eresourcekey** 型を使用する必要があります。

```csharp
namespace MyCustomColors
{
    public static class MyCategory
    {
        #region Autogenerated resource keys
        // These resource keys are generated by Visual Studio Extension Color Editor, and should be replaced when new colors are added to this category.
        public static readonly Guid Category = new Guid("faf7f3f9-9fe5-4dd3-9350-59679617dfbe");

        private static ThemeResourceKey _MyColor1ColorKey;
        private static ThemeResourceKey _MyColor1BrushKey;
        private static ThemeResourceKey _MyColor1TextColorKey;
        private static ThemeResourceKey _MyColor1TextBrushKey;
        public static ThemeResourceKey MyColor1ColorKey { get { return _MyColor1ColorKey ?? (_MyColor1ColorKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.BackgroundColor)); } }
        public static ThemeResourceKey MyColor1BrushKey { get { return _MyColor1BrushKey ?? (_MyColor1BrushKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.BackgroundBrush)); } }
        public static ThemeResourceKey MyColor1TextColorKey { get { return _MyColor1TextColorKey ?? (_MyColor1TextColorKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.ForegroundColor)); } }
        public static ThemeResourceKey MyColor1TextBrushKey { get { return _MyColor1TextBrushKey ?? (_MyColor1TextBrushKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.ForegroundBrush)); } }
        #endregion
    }
}
```

 これにより、XAML コードの色へのアクセスが可能になり、UI がテーマの変更に応答できるようになります。

```xaml
<UserControl x:Class="NewTestProject.TestPackageControl" Name="MyToolWindow"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:ns="clr-namespace:MyCustomColors">
  <Grid>
    <TextBlock Background="{DynamicResource {x:Static ns:MyCategory.MyColor1BrushKey}}"
               Foreground="{DynamicResource {x:Static ns:MyCategory.MyColor1TextBrushKey}}"
      >Sample Text</TextBlock>

  </Grid>
</UserControl>
```

 **手順 5: Visual Studio で変更をテストします。**

 カラーエディターは、Visual Studio の実行中のインスタンスに色トークンを一時的に適用して、拡張機能パッケージを再構築せずに、色のライブ変更を表示できます。 これを行うには、各テーマ列のヘッダーにある [このテーマを適用して Visual Studio ウィンドウを実行する] ボタンをクリックします。 この一時的なテーマは、VSIX カラーエディターを閉じたときに消えます。

 ![VSIX カラー エディターによる適用](../../extensibility/internals/media/vsix-color-editor-apply.png "VSIX カラー エディターによる適用")

 変更を永続的にするには、新しい色を pkgdef ファイルに追加し、それらの色を使用するコードを記述した後で、Visual Studio 拡張機能をリビルドして再配置します。 Visual Studio 拡張機能を再構築すると、新しい色のレジストリ値がテーマの残りの部分にマージされます。 次に、Visual Studio を再起動し、UI を表示して、新しい色が想定どおりに表示されることを確認します。

## <a name="notes"></a>メモ
 このツールは、既存の Visual Studio テーマに対してカスタムの色を作成したり、カスタム Visual Studio テーマの色を編集したりするために使用することを目的としています。 カスタム Visual Studio の完全なテーマを作成するには、visual studio 拡張機能ギャラリーから [Visual Studio 配色テーマエディター拡張機能](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.VisualStudio2015ColorThemeEditor) をダウンロードします。

## <a name="sample-output"></a>出力例
 **XML カラー出力**

 ツールによって生成される .xml ファイルは次のようになります。

```xml
<Themes>
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">
    <Category Name="CategoryName" GUID="{eee9d521-dac2-48d9-9a5e-5c625ba2040c}">
      <Color Name="ColorName1">
        <Background Type="CT_RAW" Source="FFFFFFFF" />
      </Color>
      <Color Name="ColorName2">
        <Background Type="CT_RAW" Source="FFFFFFFF" />
        <Foreground Type="CT_RAW" Source="FF000000" />
      </Color>
      <Color Name="ColorName3">
        <Background Type="CT_RAW" Source="FFFF0000" />
      </Color>
      <Color Name="ColorName4">
        <Background Type="CT_RAW" Source="FF000088" />
        <Foreground Type="CT_RAW" Source="FFFFFFFF" />
      </Color>
    </Category>
  </Theme>
  <Theme Name="Dark" GUID="{1ded0138-47ce-435e-84ef-9ec1f439b749}">...</Theme>
  <Theme Name="Blue" GUID="{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}">...</Theme>
  <Theme Name="HighContrast" GUID="{a5c004b4-2d4b-494e-bf01-45fc492522c7}">...</Theme>
</Themes>

```

 **PKGDEF カラー出力**

 このツールによって生成される pkgdef ファイルは次のようになります。

```
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\CategoryName]
"Data"=hex:78,00,00,00,0b,00,00,00,01,00,00,00,21,d5,e9,ee,c2,da,d9,48,9a,5e,5c,62,5b,a2,04,0c,04,00,00,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,31,01,ff,ff,ff,ff,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,32,01,ff,ff,ff,ff,01,00,00,00,ff,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,33,01,ff,00,00,ff,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,34,01,00,00,88,ff,01,ff,ff,ff,ff
[$RootKey$\Themes\{1ded0138-47ce-435e-84ef-9ec1f439b749}\CategoryName]
"Data"=hex:...
[$RootKey$\Themes\{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}\CategoryName]
"Data"=hex:...
[$RootKey$\Themes\{a5c004b4-2d4b-494e-bf01-45fc492522c7}\CategoryName]
"Data"=hex:...

```

 **C# リソースキーラッパー**

 ツールによって生成される色リソースキーは次のようになります。

```csharp
namespace MyNamespace
{
    public static class MyColors
    {
        #region Autogenerated resource keys
        // These resource keys are generated by Visual Studio Extension Color Editor, and should be replaced when new colors are added to this category.

        public static string ColorName1ColorKey { get { return "ColorName1ColorKey"; } }
        public static string ColorName1BrushKey { get { return "ColorName1BrushKey"; } }

        public static string ColorName2ColorKey { get { return "ColorName2ColorKey"; } }
        public static string ColorName2BrushKey { get { return "ColorName2BrushKey"; } }
        public static string ColorName2TextColorKey { get { return "ColorName2TextColorKey"; } }
        public static string ColorName2TextBrushKey { get { return "ColorName2TextBrushKey"; } }

        public static string ColorName3ColorKey { get { return "ColorName4ColorKey"; } }
        public static string ColorName3BrushKey { get { return "ColorName4BrushKey"; } }
        public static string ColorName3TextColorKey { get { return "ColorName4TextColorKey"; } }
        public static string ColorName3TextBrushKey { get { return "ColorName4TextBrushKey"; } }
        #endregion
    }
}
```

 **WPF リソースディクショナリラッパー**

 ツールによって生成される色 **ResourceDictionary** キーは、次のようになります。

```xaml
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:colors="clr-namespace:MyNamespace">

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName1BrushKey}" Color="#FFFFFFFF" />
  <Color x:Key="{x:Static colors:MyColors.ColorName1ColorKey}" A="255" R="255" G="255" B="255" />

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName2BrushKey}" Color="#FFFFFFFF" />
  <Color x:Key="{x:Static colors:MyColors.ColorName2ColorKey}" A="255" R="255" G="255" B="255" />
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName2TextBrushKey}" Color="#FF000000" />
  <Color x:Key="{x:Static colors:MyColors.ColorName2TextColorKey}" A="255" R="0" G="0" B="0" />

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName3BrushKey}" Color="#FFFF0000" />
  <Color x:Key="{x:Static colors:MyColors.ColorName3ColorKey}" A="255" R="255" G="0" B="0" />

  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName4BrushKey}" Color="#FF000088" />
  <Color x:Key="{x:Static colors:MyColors.ColorName4ColorKey}" A="255" R="0" G="0" B="136" />
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName4TextBrushKey}" Color="#FFFFFFFF" />
  <Color x:Key="{x:Static colors:MyColors.ColorName4TextColorKey}" A="255" R="255" G="255" B="255" />
</ResourceDictionary>
```
