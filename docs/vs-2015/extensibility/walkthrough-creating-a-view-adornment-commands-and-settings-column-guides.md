---
title: 'チュートリアル: ビューの表示要素、コマンド、および設定の作成 (列ガイド) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 4a2df0a3-42da-4f7b-996f-ee16a35ac922
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0cab24a373595ca1257cbdaa50c009eefa713ea7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148841"
---
# <a name="walkthrough-creating-a-view-adornment-commands-and-settings-column-guides"></a>チュートリアル: ビューの表示要素、コマンド、設定 (垂直グリッド ガイド) の作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コマンドと表示効果を使用して、Visual Studio のテキストエディターまたはコードエディターを拡張できます。 このトピックでは、一般的な拡張機能の列ガイドを使ってみる方法について説明します。 列ガイドは、特定の列の幅に合わせてコードを管理するために、テキストエディターのビューに視覚的に表示される線です。 特に書式設定されたコードは、ドキュメント、ブログの投稿、またはバグレポートに含めるサンプルにとって重要です。

このチュートリアルでは次を行います。

- VSIX プロジェクトを作成する
- エディタービューの表示要素を追加する
- 設定を保存および取得するためのサポートを追加する (列ガイドとその色を描画する場所)
- コマンドの追加 (列ガイドの追加と削除、色の変更)
- [編集] メニューおよびテキストドキュメントのショートカットメニューにコマンドを配置する
- Visual Studio のコマンドウィンドウからコマンドを呼び出すためのサポートを追加します。  
  
  この Visual Studio ギャラリーの[拡張](https://visualstudiogallery.msdn.microsoft.com/da227a0b-0e31-4a11-8f6b-3a149cf2e459?SRC=Home)機能を使用して、列ガイド機能のバージョンを試すことができます。  
  
  **注**: このチュートリアルでは、visual studio 拡張機能テンプレートによって生成されるいくつかのファイルに多くのコードを貼り付けますが、このチュートリアルでは、他の拡張機能の例と共に、GitHub で完成したソリューションを参照します。 完成したコードは、generictemplate アイコンを使用するのではなく、実際のコマンドアイコンがあると若干異なります。

## <a name="getting-started"></a>作業の開始
Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="setting-up-the-solution"></a>ソリューションの設定
まず、VSIX プロジェクトを作成し、エディタービューの表示要素を追加します。次に、コマンドを追加します (これにより、コマンドを所有する VSPackage が追加されます)。 基本的なアーキテクチャは次のとおりです。

- ビューごとにオブジェクトを作成するテキストビュー作成リスナーがあり `ColumnGuideAdornment` ます。 このオブジェクトは、ビューの変更または設定に関するイベントをリッスンします。列ガイドは必要に応じて変更、更新、または再描画します。
- `GuidesSettingsManager`Visual Studio の設定ストレージからの読み取りと書き込みを処理するがあります。 また、設定マネージャーには、ユーザーコマンド ([列の追加]、[列の削除]、[色の変更]) をサポートする設定を更新するための操作もあります。
- ユーザーコマンドを使用している場合は、VSIP パッケージが必要ですが、コマンド実装オブジェクトを初期化する定型コードにすぎません。
- `ColumnGuideCommands`ユーザーコマンドを実装し、. vsct ファイルで宣言されているコマンドのコマンドハンドラーをフックするオブジェクトがあります。
  
  **VSIX**。 **ファイル &#124; 新規作成**... コマンドを実行してプロジェクトを作成します。 左側のナビゲーションウィンドウで [C#] の [機能拡張] ノードを選択し、右側のウィンドウで [ **VSIX プロジェクト** ] を選択します。 「ColumnGuides」という名前を入力し、 **[OK]** を選択してプロジェクトを作成します。
  
  **表示要素を表示**します。 ソリューションエクスプローラーのプロジェクトノードで、右のポインターボタンを押します。 [**新しい項目の追加 &#124;** ] を選択します。 コマンドを実行して、新しいビューの表示項目を追加します。 左側のナビゲーションウィンドウで [ **機能拡張 &#124; エディター** ] を選択し、右側のウィンドウで [ **エディタービューポート** ] 表示を選択します。 [名前] 列に「column?」という名前を入力し、[ **追加** ] をクリックして追加します。
  
  この項目テンプレートでは、ColumnGuideAdornment.cs と ColumnGuideAdornmentTextViewCreationListener.cs という2つのファイルがプロジェクトに追加されていることがわかります。 テンプレートでは、ビューに紫色の四角形が描画されます。 次に、ビュー作成リスナーのいくつかの行を変更し、ColumnGuideAdornment.cs の内容を置き換えます。
  
  **コマンド**。 ソリューションエクスプローラーのプロジェクトノードで、右のポインターボタンを押します。 [**新しい項目の追加 &#124;** ] を選択します。 コマンドを実行して、新しいビューの表示項目を追加します。 左側のナビゲーションウィンドウで [ **機能拡張 &#124; VSPackage** ] を選択し、右側のウィンドウで [ **カスタムコマンド** ] を選択します。 項目名として「ColumnGuideCommands」という名前を入力し、[ **追加** ] を選択して追加します。 いくつかの参照に加えて、コマンドとパッケージを追加すると、ColumnGuideCommands.cs、ColumnGuideCommandsPackage.cs、および ColumnGuideCommandsPackage が追加されました。 次に、最初と最後のファイルの内容を置き換えて、コマンドを定義して実装します。

## <a name="setting-up-the-text-view-creation-listener"></a>テキストビュー作成リスナーの設定
エディターで ColumnGuideAdornmentTextViewCreationListener.cs を開きます。 このコードは、Visual Studio がテキストビューを作成するたびに、のハンドラーを実装します。 ビューの特性に応じてハンドラーが呼び出されるタイミングを制御する属性があります。

このコードでは、装飾レイヤーを宣言する必要もあります。 エディターによってビューが更新されると、ビューの表示要素レイヤーと、表示要素を取得するからビューが取得されます。 属性を使用して、レイヤーの順序を他のユーザーに対して相対的に宣言できます。 次の行を置き換えます。

```csharp
[Order(After = PredefinedAdornmentLayers.Caret)]
```

 次の2つの行を使用します。

```csharp
[Order(Before = PredefinedAdornmentLayers.Text)]
[TextViewRole(PredefinedTextViewRoles.Document)]
```

置き換えた行は、表示要素レイヤーを宣言する属性のグループに含まれています。  変更した最初の行が変更されるのは、列ガイドの線が表示される箇所だけです。 ビュー内のテキストの "前" に線を描画すると、テキストの背後または下に表示されます。 2番目の行は、列ガイドの修飾がドキュメントの概念に適合するテキストエンティティに適用できることを宣言しますが、たとえば、編集可能なテキストに対してのみ機能するように、表示要素を宣言できます。 詳細については[、「言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)」を参照してください。

## <a name="implementing-the-settings-manager"></a>設定マネージャーの実装
GuidesSettingsManager.cs の内容を次のコードに置き換えます (以下で説明します)。

```csharp
using Microsoft.VisualStudio.Settings;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Settings;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows.Media;

namespace ColumnGuides
{
    internal static class GuidesSettingsManager
    {
        // Because my code is always called from the UI thred, this succeeds.
        internal static SettingsManager VsManagedSettingsManager =
            new ShellSettingsManager(ServiceProvider.GlobalProvider);

        private const int _maxGuides = 5;
        private const string _collectionSettingsName = "Text Editor";
        private const string _settingName = "Guides";
        // 1000 seems reasonable since primary scenario is long lines of code
        private const int _maxColumn = 1000;

        static internal bool AddGuideline(int column)
        {
            if (! IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column",
                    "The paramenter must be between 1 and " + _maxGuides.ToString());
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            if (offsets.Count() >= _maxGuides)
                return false;
            // Check for duplicates
            if (offsets.Contains(column))
                return false;
            offsets.Add(column);
            WriteSettings(GuidesSettingsManager.GuidelinesColor, offsets);
            return true;
        }

        static internal bool RemoveGuideline(int column)
        {
            if (!IsValidColumn(column))
                throw new ArgumentOutOfRangeException(
                    "column", "The paramenter must be between 1 and 10,000");
            var columns = GuidesSettingsManager.GetColumnOffsets();
            if (! columns.Remove(column))
            {
                // Not present. Allow user to remove the last column 
                // even if they're not on the right column.
                if (columns.Count != 1)
                    return false;

                columns.Clear();
            }
            WriteSettings(GuidesSettingsManager.GuidelinesColor, columns);
            return true;
        }

        static internal bool CanAddGuideline(int column)
        {
            if (!IsValidColumn(column))
                return false;
            var offsets = GetColumnOffsets();
            if (offsets.Count >= _maxGuides)
                return false;
            return ! offsets.Contains(column);
        }

        static internal bool CanRemoveGuideline(int column)
        {
            if (! IsValidColumn(column))
                return false;
            // Allow user to remove the last guideline regardless of the column.
            // Okay to call count, we limit the number of guides.
            var offsets = GuidesSettingsManager.GetColumnOffsets();
            return offsets.Contains(column) || offsets.Count() == 1;
        }

        static internal void RemoveAllGuidelines()
        {
            WriteSettings(GuidesSettingsManager.GuidelinesColor, new int[0]);
        }

        private static bool IsValidColumn(int column)
        {
            // zero is allowed (per user request)
            return 0 <= column && column <= _maxColumn;
        }

        // This has format "RGB(<int>, <int>, <int>) <int> <int>...".
        // There can be any number of ints following the RGB part,
        // and each int is a column (char offset into line) where to draw.
        static private string _guidelinesConfiguration;
        static private string GuidelinesConfiguration
        {
            get
            {
                if (_guidelinesConfiguration == null)
                {
                    _guidelinesConfiguration =
                        GetUserSettingsString(
                            GuidesSettingsManager._collectionSettingsName,
                            GuidesSettingsManager._settingName)
                        .Trim();
                }
                return _guidelinesConfiguration;
            }

            set
            {
                if (value != _guidelinesConfiguration)
                {
                    _guidelinesConfiguration = value;
                    WriteUserSettingsString(
                        GuidesSettingsManager._collectionSettingsName,
                        GuidesSettingsManager._settingName, value);
                    // Notify ColumnGuideAdornments to update adornments in views.
                    var handler = GuidesSettingsManager.SettingsChanged;
                    if (handler != null)
                        handler();
                }
            }
        }

        internal static string GetUserSettingsString(string collection, string setting)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetReadOnlySettingsStore(SettingsScope.UserSettings);
            return store.GetString(collection, setting, "RGB(255,0,0) 80");
        }

        internal static void WriteUserSettingsString(string key, string propertyName,
                                                     string value)
        {
            var store = GuidesSettingsManager
                            .VsManagedSettingsManager
                            .GetWritableSettingsStore(SettingsScope.UserSettings);
            store.CreateCollection(key);
            store.SetString(key, propertyName, value);
        }

        // Persists settings and sets property with side effect of signaling
        // ColumnGuideAdornments to update.
        static private void WriteSettings(Color color, IEnumerable<int> columns)
        {
            string value = ComposeSettingsString(color, columns);
            GuidelinesConfiguration = value;
        }

        private static string ComposeSettingsString(Color color,
                                                    IEnumerable<int> columns)
        {
            StringBuilder sb = new StringBuilder();
            sb.AppendFormat("RGB({0},{1},{2})", color.R, color.G, color.B);
            IEnumerator<int> columnsEnumerator = columns.GetEnumerator();
            if (columnsEnumerator.MoveNext())
            {
                sb.AppendFormat(" {0}", columnsEnumerator.Current);
                while (columnsEnumerator.MoveNext())
                {
                    sb.AppendFormat(", {0}", columnsEnumerator.Current);
                }
            }
            return sb.ToString();
        }

        // Parse a color out of a string that begins like "RGB(255,0,0)"
        static internal Color GuidelinesColor
        {
            get
            {
                string config = GuidelinesConfiguration;
                if (!String.IsNullOrEmpty(config) && config.StartsWith("RGB("))
                {
                    int lastParen = config.IndexOf(')');
                    if (lastParen > 4)
                    {
                        string[] rgbs = config.Substring(4, lastParen - 4).Split(',');

                        if (rgbs.Length >= 3)
                        {
                            byte r, g, b;
                            if (byte.TryParse(rgbs[0], out r) &&
                                byte.TryParse(rgbs[1], out g) &&
                                byte.TryParse(rgbs[2], out b))
                            {
                                return Color.FromRgb(r, g, b);
                            }
                        }
                    }
                }
                return Colors.DarkRed;
            }

            set
            {
                WriteSettings(value, GetColumnOffsets());
            }
        }

        // Parse a list of integer values out of a string that looks like
        // "RGB(255,0,0) 1, 5, 10, 80"
        static internal List<int> GetColumnOffsets()
        {
            var result = new List<int>();
            string settings = GuidesSettingsManager.GuidelinesConfiguration;
            if (String.IsNullOrEmpty(settings))
                return new List<int>();

            if (!settings.StartsWith("RGB("))
                return new List<int>();

            int lastParen = settings.IndexOf(')');
            if (lastParen <= 4)
                return new List<int>();

            string[] columns = settings.Substring(lastParen + 1).Split(',');

            int columnCount = 0;
            foreach (string columnText in columns)
            {
                int column = -1;
                // VS 2008 gallery extension didn't allow zero, so per user request ...
                if (int.TryParse(columnText, out column) && column >= 0)
                {
                    columnCount++;
                    result.Add(column);
                    if (columnCount >= _maxGuides)
                        break;
                }
            }
            return result;
        }

        // Delegate and Event to fire when settings change so that ColumnGuideAdornments
        // can update. We need nothing special in this event since the settings manager
        // is statically available.
        //
        internal delegate void SettingsChangedHandler();
        static internal event SettingsChangedHandler SettingsChanged;

    }
}

```

このコードのほとんどは、"RGB ( \<int> , \<int> , \<int> ) \<int> , \<int> ,..." という設定形式を作成および解析するだけです。 最後の整数は、列ガイドを作成する1ベースの列です。 列ガイド拡張機能では、すべての設定が1つの設定値の文字列でキャプチャされます。

コードにはいくつかの部分が強調表示されています。 次のコード行は、設定ストレージの Visual Studio マネージラッパーを取得します。 ほとんどの場合、これによって Windows レジストリが抽象化されますが、この API はストレージメカニズムに依存しません。

```csharp
internal static SettingsManager VsManagedSettingsManager =
    new ShellSettingsManager(ServiceProvider.GlobalProvider);
```

 Visual Studio の設定ストレージでは、カテゴリ識別子と設定識別子を使用して、すべての設定を一意に識別します。

```csharp
private const string _collectionSettingsName = "Text Editor";
private const string _settingName = "Guides";
```

をカテゴリ名として使用する必要はなく、 `“Text Editor”` 好きなものを選択することもできます。

最初のいくつかの関数は、設定を変更するためのエントリポイントです。 これらは、許可されているガイドの最大数などの高レベルの制約を確認します。 次に、 `WriteSettings` は、設定文字列を構成し、プロパティを設定するを呼び出します `GuideLinesConfiguration` 。 このプロパティを設定すると、設定の値が Visual Studio の設定ストアに保存され、イベントが発生して、 `SettingsChanged` `ColumnGuideAdornment` それぞれがテキストビューに関連付けられているすべてのオブジェクトが更新されます。

`CanAddGuideline`設定を変更するコマンドの実装に使用されるエントリポイント関数 (など) がいくつかあります。 Visual Studio にメニューが表示されている場合は、コマンドの実装に対してクエリを実行し、コマンドが現在有効になっているかどうか、およびその名前を確認します。次に、これらのエントリポイントをコマンド実装用にフックする方法について説明します。 コマンドの詳細については [、「メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md) 」を参照してください。

## <a name="implementing-the-columnguideadornment-class"></a>Columnを実装しています。 column? の装飾クラス
クラスは、 `ColumnGuideAdornment` 修飾を持つことができる各テキストビューに対してインスタンス化されます。 このクラスは、ビューの変更または設定に関するイベントをリッスンします。列ガイドは必要に応じて変更、更新、または再描画します。

ColumnGuideAdornment.cs の内容を次のコードに置き換えます (以下で説明します)。

```csharp
using System;
using System.Windows.Media;
using Microsoft.VisualStudio.Text.Editor;
using System.Collections.Generic;
using System.Windows.Shapes;
using Microsoft.VisualStudio.Text.Formatting;
using System.Windows;

namespace ColumnGuides
{
    /// <summary>
    /// Adornment class, one instance per text view that draws a guides on the viewport
    /// </summary>
    internal sealed class ColumnGuideAdornment
    {
        private const double _lineThickness = 1.0;
        private IList<Line> _guidelines;
        private IWpfTextView _view;
        private double _baseIndentation;
        private double _columnWidth;

        /// <summary>
        /// Creates editor column guidelines
        /// </summary>
        /// <param name="view">The <see cref="IWpfTextView"/> upon
        /// which the adornment will be drawn</param>
        public ColumnGuideAdornment(IWpfTextView view)
        {
            _view = view;
            _guidelines = CreateGuidelines();
            GuidesSettingsManager.SettingsChanged +=
                new GuidesSettingsManager.SettingsChangedHandler(SettingsChanged);
            view.LayoutChanged +=
                new EventHandler<TextViewLayoutChangedEventArgs>(OnViewLayoutChanged);
            _view.Closed += new EventHandler(OnViewClosed);
        }

        void SettingsChanged()
        {
            _guidelines = CreateGuidelines();
            UpdatePositions();
            AddGuidelinesToAdornmentLayer();
        }

        void OnViewClosed(object sender, EventArgs e)
        {
            _view.LayoutChanged -= OnViewLayoutChanged;
            _view.Closed -= OnViewClosed;
            GuidesSettingsManager.SettingsChanged -= SettingsChanged;
        }

        private bool _firstLayoutDone;

        void OnViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)
        {
            bool fUpdatePositions = false;

            IFormattedLineSource lineSource = _view.FormattedLineSource;
            if (lineSource == null)
            {
                return;
            }
            if (_columnWidth != lineSource.ColumnWidth)
            {
                _columnWidth = lineSource.ColumnWidth;
                fUpdatePositions = true;
            }
            if (_baseIndentation != lineSource.BaseIndentation)
            {
                _baseIndentation = lineSource.BaseIndentation;
                fUpdatePositions = true;
            }
            if (fUpdatePositions ||
                e.VerticalTranslation ||
                e.NewViewState.ViewportTop != e.OldViewState.ViewportTop ||
                e.NewViewState.ViewportBottom != e.OldViewState.ViewportBottom)
            {
                UpdatePositions();
            }
            if (!_firstLayoutDone)
            {
                AddGuidelinesToAdornmentLayer();
                _firstLayoutDone = true;
            }
        }

        private static IList<Line> CreateGuidelines()
        {
            Brush lineBrush = new SolidColorBrush(GuidesSettingsManager.GuidelinesColor);
            DoubleCollection dashArray = new DoubleCollection(new double[] { 1.0, 3.0 });
            IList<Line> result = new List<Line>();
            foreach (int column in GuidesSettingsManager.GetColumnOffsets())
            {
                Line line = new Line()
                {
                    // Use the DataContext slot as a cookie to hold the column
                    DataContext = column,
                    Stroke = lineBrush,
                    StrokeThickness = _lineThickness,
                    StrokeDashArray = dashArray
                };
                result.Add(line);
            }
            return result;
        }

        void UpdatePositions()
        {
            foreach (Line line in _guidelines)
            {
                int column = (int)line.DataContext;
                line.X2 = _baseIndentation + 0.5 + column * _columnWidth;
                line.X1 = line.X2;
                line.Y1 = _view.ViewportTop;
                line.Y2 = _view.ViewportBottom;
            }
        }

        void AddGuidelinesToAdornmentLayer()
        {
            // Grab a reference to the adornment layer that this adornment
            // should be added to
            // Must match exported name in ColumnGuideAdornmentTextViewCreationListener
            IAdornmentLayer adornmentLayer =
                _view.GetAdornmentLayer("ColumnGuideAdornment");
            if (adornmentLayer == null)
                return;
            adornmentLayer.RemoveAllAdornments();
            // Add the guidelines to the adornment layer and make them relative
            // to the viewport
            foreach (UIElement element in _guidelines)
                adornmentLayer.AddAdornment(AdornmentPositioningBehavior.OwnerControlled,
                                            null, null, element, null);
        }
    }

}
```

このクラスのインスタンスは、関連付けられている <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> およびビューに描画されたオブジェクトのリストに保持され `Line` ます。

( `ColumnGuideAdornmentTextViewCreationListener` Visual Studio が新しいビューを作成するときにから呼び出される) コンストラクターは、列ガイドオブジェクトを作成し `Line` ます。 また、コンストラクターは、 `SettingsChanged` イベント (で定義される `GuidesSettingsManager` ) およびビューイベント (および) のハンドラーも追加し `LayoutChanged` `Closed` ます。

イベントは、 `LayoutChanged` Visual Studio がビューを作成するときなど、ビューのいくつかの種類の変更によって発生します。 `OnViewLayoutChanged`ハンドラーがを呼び出すと、が実行さ `AddGuidelinesToAdornmentLayer` れます。 のコードによっ `OnViewLayoutChanged` て、フォントサイズの変更、ビューのとじしろ、水平スクロールなどの変更に基づいて行の位置を更新する必要があるかどうかが決まります。 のコードを実行 `UpdatePositions` すると、テキスト行の指定された文字オフセットにあるテキストの列の直後にガイド行が描画されます。

設定を変更するたびに、 `SettingsChanged` すべての `Line` オブジェクトが新しい設定で再作成されます。 行の位置を設定した後、コードは、すべての前の `Line` オブジェクトを装飾レイヤーから削除し、新しいオブジェクトを `ColumnGuideAdornment` 追加します。

## <a name="defining-the-commands-menus-and-menu-placements"></a>コマンド、メニュー、およびメニューの配置の定義
コマンドやメニューを宣言したり、他のさまざまなメニューにコマンドやメニューのグループを配置したり、コマンドハンドラーをフックしたりすることは、多くの場合があります。 このチュートリアルでは、この拡張機能でのコマンドの動作について説明しますが、詳細については、「 [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)」を参照してください。

### <a name="introduction-to-the-code"></a>コードの概要
列ガイドの拡張機能では、まとめられたコマンドのグループ ([列の追加]、[列の削除]、[行の色の変更]) を宣言し、そのグループをエディターのコンテキストメニューのサブメニューに配置します。 また、列ガイドの拡張機能では、メインの [ **編集** ] メニューにコマンドが追加されますが、以下の一般的なパターンとして示されているように見えません。

コマンドの実装には、ColumnGuideCommandsPackage.cs、ColumnGuideCommandsPackage、および ColumnGuideCommands.cs の3つの部分があります。 テンプレートによって生成されるコードは、ダイアログボックスを実装としてポップするコマンドを [ **ツール** ] メニューに配置します。 これは非常に簡単であるため、ColumnGuideCommands.cs ファイルでの実装方法を確認できます。 これらのファイルのコードは次のように置き換えます。

パッケージコードは、拡張機能がコマンドとコマンドの配置場所を提供することを Visual Studio が検出するために必要な定型宣言です。 パッケージが初期化されると、commands 実装クラスがインスタンス化されます。 コマンドに関連するパッケージの詳細については、上記のコマンドのリンクを参照してください。

### <a name="a-common-commands-pattern"></a>一般的なコマンドパターン
列ガイドの拡張機能のコマンドは、Visual Studio の非常に一般的なパターンの一例です。 関連するコマンドをグループに配置し、そのグループをメインメニューに配置します。多くの場合、 `<CommandFlag>CommandWellOnly</CommandFlag>` コマンドを非表示にするように設定されています。 この方法でメインメニュー ([**編集**] など) にコマンドを配置すると、[**ツール] オプション**でキーバインドを再割り当てするときにコマンドを検索したり、**コマンドウィンドウ**からコマンドを起動するときに使用できるように**なります。**

次に、ユーザーがコマンドを使用することが予想されるコンテキストメニューまたはサブメニューに、コマンドのグループを追加します。 Visual Studio `CommandWellOnly` では、メインメニューの非表示フラグとして扱われます。 コンテキストメニューまたはサブメニューに同じコマンドグループを配置すると、コマンドが表示されます。

一般的なパターンの一部として、列ガイドの拡張機能によって、1つのサブメニューを保持する2番目のグループが作成されます。 サブメニューには、4つの列ガイドコマンドを含む最初のグループが含まれます。 サブメニューを保持する2番目のグループは、さまざまなコンテキストメニューに配置する再利用可能なアセットで、これらのコンテキストメニューにサブメニューが配置されます。

### <a name="the-vsct-file"></a>Vsct ファイル
この vsct ファイルでは、コマンドと、それらのコマンドがアイコンなどを使用して宣言されています。 次に説明するように、vsct ファイルの内容を次のコードに置き換えます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">

  <!--  This is the file that defines the actual layout and type of the commands.
        It is divided in different sections (e.g. command definition, command
        placement, ...), with each defining a specific set of properties.
        See the comment before each section for more details about how to
        use it. -->

  <!--  The VSCT compiler (the tool that translates this file into the binary
        format that VisualStudio will consume) has the ability to run a preprocessor
        on the vsct file; this preprocessor is (usually) the C++ preprocessor, so
        it is possible to define includes and macros with the same syntax used
        in C++ files. Using this ability of the compiler here, we include some files
        defining some of the constants that we will use inside the file. -->

  <!--This is the file that defines the IDs for all the commands exposed by
      VisualStudio. -->
  <Extern href="stdidcmd.h"/>

  <!--This header contains the command ids for the menus provided by the shell. -->
  <Extern href="vsshlids.h"/>

  <!--The Commands section is where commands, menus, and menu groups are defined.
      This section uses a Guid to identify the package that provides the command
      defined inside it. -->
  <Commands package="guidColumnGuideCommandsPkg">
    <!-- Inside this section we have different sub-sections: one for the menus, another
    for the menu groups, one for the buttons (the actual commands), one for the combos
    and the last one for the bitmaps used. Each element is identified by a command id
    that is a unique pair of guid and numeric identifier; the guid part of the identifier
    is usually called "command set" and is used to group different command inside a
    logically related group; your package should define its own command set in order to
    avoid collisions with command ids defined by other packages. -->

    <!-- In this section you can define new menu groups. A menu group is a container for
         other menus or buttons (commands); from a visual point of view you can see the
         group as the part of a menu contained between two lines. The parent of a group
         must be a menu. -->
    <Groups>

      <!-- The main group is parented to the edit menu. All the buttons within the group
           have the "CommandWellOnly" flag, so they're actually invisible, but it means
           they get canonical names that begin with "Edit". Using placements, the group
           is also placed in the GuidesSubMenu group. -->
      <!-- The priority 0xB801 is chosen so it goes just after
           IDG_VS_EDIT_COMMANDWELL -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

      <!-- Group for holding the "Guidelines" sub-menu anchor (the item on the menu that
           drops the sub menu). The group is parented to
           the context menu for code windows. That takes care of most editors, but it's
           also placed in a couple of other windows using Placements -->
      <Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_CTXT_CODEWIN" />
      </Group>

    </Groups>

    <Menus>
      <Menu guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" priority="0x1000"
            type="Menu">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup" />
        <Strings>
          <ButtonText>&Column Guides</ButtonText>
        </Strings>
      </Menu>
    </Menus>

    <!--Buttons section. -->
    <!--This section defines the elements the user can interact with, like a menu command or a button
        or combo box in a toolbar. -->
    <Buttons>
      <!--To define a menu group you have to specify its ID, the parent menu and its
          display priority.
          The command is visible and enabled by default. If you need to change the
          visibility, status, etc, you can use the CommandFlag node.
          You can add more than one CommandFlag node e.g.:
              <CommandFlag>DefaultInvisible</CommandFlag>
              <CommandFlag>DynamicVisibility</CommandFlag>
          If you do not want an image next to your command, remove the Icon node or
          set it to <Icon guid="guidOfficeIcon" id="msotcidNoIcon" /> -->

      <Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
              priority="0x0100" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicAddGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Add Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveColumnGuide"
              priority="0x0101" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicRemoveGuide" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>AllowParams</CommandFlag>
        <Strings>
          <ButtonText>&Remove Column Guide</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidChooseGuideColor"
              priority="0x0103" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <Icon guid="guidImages" id="bmpPicChooseColor" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Column Guide &Color...</ButtonText>
        </Strings>
      </Button>

      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveAllColumnGuides"
              priority="0x0102" type="Button">
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
        <CommandFlag>CommandWellOnly</CommandFlag>
        <Strings>
          <ButtonText>Remove A&ll Columns</ButtonText>
        </Strings>
      </Button>
    </Buttons>

    <!--The bitmaps section is used to define the bitmaps that are used for the
        commands.-->
    <Bitmaps>
      <!--  The bitmap id is defined in a way that is a little bit different from the
            others:
            the declaration starts with a guid for the bitmap strip, then there is the
            resource id of the bitmap strip containing the bitmaps and then there are
            the numeric ids of the elements used inside a button definition. An important
            aspect of this declaration is that the element id
            must be the actual index (1-based) of the bitmap inside the bitmap strip. -->
      <Bitmap guid="guidImages" href="Resources\ColumnGuideCommands.png"
              usedList="bmpPicAddGuide, bmpPicRemoveGuide, bmpPicChooseColor" />
    </Bitmaps>

  </Commands>

  <CommandPlacements>

    <!-- Define secondary placements for our groups -->

    <!-- Place the group containing the three commands in the sub-menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                      priority="0x0100">
      <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
    </CommandPlacement>

    <!-- The HTML editor context menu, for some reason, redefines its own groups
         so we need to place a copy of our context menu there too. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_HTML" />
    </CommandPlacement>

    <!-- The HTML context menu in Dev12 changed. -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp_Dev12" id="IDMX_HTM_SOURCE_HTML_Dev12" />
    </CommandPlacement>

    <!-- Similarly for Script -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_SCRIPT" />
    </CommandPlacement>

    <!-- Similarly for ASPX  -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x1001">
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_ASPX" />
    </CommandPlacement>

    <!-- Similarly for the XAML editor context menu -->
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
                      priority="0x0600">
      <Parent guid="guidXamlUiCmds" id="IDM_XAML_EDITOR" />
    </CommandPlacement>

  </CommandPlacements>

  <!-- This defines the identifiers and their values used above to index resources
       and specify commands. -->
  <Symbols>
    <!-- This is the package guid. -->
    <GuidSymbol name="guidColumnGuideCommandsPkg"
                value="{e914e5de-0851-4904-b361-1a3a9d449704}" />

    <!-- This is the guid used to group the menu commands together -->
    <GuidSymbol name="guidColumnGuidesCommandSet"
                value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
      <IDSymbol name="GuidesContextMenuGroup" value="0x1020" />
      <IDSymbol name="GuidesMenuItemsGroup" value="0x1021" />
      <IDSymbol name="GuidesSubMenu" value="0x1022" />
      <IDSymbol name="cmdidAddColumnGuide" value="0x0100" />
      <IDSymbol name="cmdidRemoveColumnGuide" value="0x0101" />
      <IDSymbol name="cmdidChooseGuideColor" value="0x0102" />
      <IDSymbol name="cmdidRemoveAllColumnGuides" value="0x0103" />
    </GuidSymbol>

    <GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
      <IDSymbol name="bmpPicAddGuide" value="1" />
      <IDSymbol name="bmpPicRemoveGuide" value="2" />
      <IDSymbol name="bmpPicChooseColor" value="3" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp_Dev12"
                value="{78F03954-2FB8-4087-8CE7-59D71710B3BB}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML_Dev12" value="0x1" />
    </GuidSymbol>

    <GuidSymbol name="CMDSETID_HtmEdGrp" value="{d7e8c5e1-bdb8-11d0-9c88-0000f8040a53}">
      <IDSymbol name="IDMX_HTM_SOURCE_HTML" value="0x33" />
      <IDSymbol name="IDMX_HTM_SOURCE_SCRIPT" value="0x34" />
      <IDSymbol name="IDMX_HTM_SOURCE_ASPX" value="0x35" />
    </GuidSymbol>

    <GuidSymbol name="guidXamlUiCmds" value="{4c87b692-1202-46aa-b64c-ef01faec53da}">
      <IDSymbol name="IDM_XAML_EDITOR" value="0x103" />
    </GuidSymbol>
  </Symbols>

</CommandTable>

```

**Guid**。 Visual Studio でコマンドハンドラーを検索して呼び出すには、(プロジェクト項目テンプレートから生成された) ColumnGuideCommandsPackage.cs ファイルで宣言されているパッケージ GUID が、(上からコピーした) vsct ファイルで宣言されているパッケージ GUID と一致していることを確認する必要があります。 このサンプルコードを再利用する場合は、このコードをコピーした他のユーザーと競合しないように、別の GUID を使用していることを確認する必要があります。

ColumnGuideCommandsPackage.cs で次の行を検索し、引用符の間に GUID をコピーします。

```csharp
public const string PackageGuidString = "ef726849-5447-4f73-8de5-01b9e930f7cd";
```

次に、この GUID を. vsct ファイルに貼り付けて、宣言に次の行を記述し `Symbols` ます。

```xml
<GuidSymbol name="guidColumnGuideCommandsPkg" 
            value="{ef726849-5447-4f73-8de5-01b9e930f7cd}" />
```

コマンドセットの Guid とビットマップイメージファイルは、拡張機能に対しても一意である必要があります。

```xml
<GuidSymbol name="guidColumnGuidesCommandSet"
            value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
<GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
```

ただし、コードを機能させるには、このチュートリアルでコマンドセットとビットマップイメージの Guid を変更する必要はありません。 コマンドセット GUID は、ColumnGuideCommands.cs ファイル内の宣言と一致している必要がありますが、そのファイルの内容も置換されます。そのため、Guid が一致します。

. Vsct ファイル内の他の Guid によって、列ガイドのコマンドが追加される既存のメニューが特定されるため、変更されることはありません。

**ファイルのセクション**。 Vsct には、コマンド、配置、および記号という3つの外部セクションがあります。 Commands セクションでは、コマンドグループ、メニュー、ボタン、メニュー項目、およびアイコンのビットマップが定義されています。 配置セクションでは、メニューのどこに移動するか、または既存のメニューへの追加配置を宣言します。 シンボルセクションでは、. vsct ファイル内で使用されている識別子を宣言します。これにより、Guid と16進数値をどこでも読みやすくすることができます。

**コマンドセクション「グループの定義」を参照**してください。 Commands セクションでは、まずコマンドグループを定義します。 コマンドのグループは、メニューに表示されるコマンドであり、グループを分割してわずかに灰色の線が付いています。 この例のように、グループはサブメニュー全体を埋めることもできます。この場合、灰色の区切り線は表示されません。 この vsct ファイルは、2つのグループを宣言します。これは、 `GuidesMenuItemsGroup` `IDM_VS_MENU_EDIT` (メインの [ **編集** ] メニュー) と、 `GuidesContextMenuGroup` `IDM_VS_CTXT_CODEWIN` (コードエディターのコンテキストメニュー) を親とするです。

2番目のグループ宣言には `0x0600` 優先順位があります。

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
```

ヒントとして、[列ガイド] サブメニューをショートカットメニューの最後に配置して、サブメニューグループを追加します。 ただし、最もよく知られていないことを前提にして、サブメニューを常に優先度の高いものにすることをお勧めし `0xFFFF` ます。 この数値を使用して、サブメニューが配置されているコンテキストメニューに表示されている場所を確認する必要があります。 この場合、 `0x0600` 表示できる限り、メニューの最後に配置するのは十分ですが、必要に応じて、他のユーザーがその拡張機能を列ガイド拡張機能よりも低いものになるように設計する余地はありません。

**コマンドセクション、メニュー定義**。 次に、コマンドセクションは、を親とするサブメニューを定義し `GuidesSubMenu` `GuidesContextMenuGroup` ます。 は、 `GuidesContextMenuGroup` 関連するすべてのコンテキストメニューに追加するグループです。 配置セクションでは、コードによって、このサブメニューに4つの列ガイドコマンドがグループ化されます。

**コマンドセクション、ボタンの定義**。 Commands セクションでは、4つの列ガイドのコマンドであるメニュー項目またはボタンを定義します。 `CommandWellOnly`は、上で説明したように、メインメニューに配置されたときにコマンドが非表示になることを意味します。 メニュー項目ボタンの宣言 ([ガイドの追加] と [ガイドの削除]) には、次の2つのフラグもあり `AllowParams` ます。

```xml
<CommandFlag>AllowParams</CommandFlag>
```

このフラグにより、メインメニューが配置され、Visual Studio がコマンドハンドラーを呼び出すときに引数を受け取るコマンドが有効になります。 ユーザーがコマンドウィンドウからコマンドを呼び出すと、引数はイベント引数のコマンドハンドラーに渡されます。

**コマンドセクション、ビットマップの定義**。 最後に、コマンドセクションでは、コマンドに使用するビットマップまたはアイコンを宣言します。 これは、プロジェクトリソースを識別する単純な宣言であり、使用済みアイコンの1から始まるインデックスを一覧表示します。 . Vsct ファイルのシンボルセクションは、インデックスとして使用される識別子の値を宣言します。 このチュートリアルでは、プロジェクトに追加されたカスタムコマンド項目テンプレートに用意されているビットマップストリップを使用します。

配置**セクション**。 コマンドセクションが配置セクションになります。 最初の例では、上記で説明した最初のグループをコードで追加し、コマンドが表示されるサブメニューに4つの列ガイドコマンドを保持します。

```xml
<CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                  priority="0x0100">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
</CommandPlacement>
```

他のすべての配置では、 `GuidesContextMenuGroup` (を含む `GuidesSubMenu` ) を他のエディターコンテキストメニューに追加します。 コードがを宣言すると `GuidesContextMenuGroup` 、コードエディターのコンテキストメニューが親になりました。 そのため、コードエディターのコンテキストメニューの配置が表示されません。

**シンボルセクション**。 前述のように、シンボルセクションでは、. vsct ファイル内で使用されている識別子を宣言します。これにより、Guid と16進数値をすべての場所で使用するよりも、vsct コードをより読みやすくすることができます。 このセクションの重要な点は、パッケージの GUID が package クラスの宣言と一致する必要があり、コマンドセット GUID が command 実装クラスの宣言と一致する必要があることです。

## <a name="implementing-the-commands"></a>コマンドの実装
ColumnGuideCommands.cs ファイルは、コマンドを実装し、ハンドラーをフックします。 Visual Studio によってパッケージが読み込まれて初期化されると、パッケージは `Initialize` commands 実装クラスを呼び出します。 コマンドの初期化では、クラスをインスタンス化するだけで、コンストラクターはすべてのコマンドハンドラーをフックします。

ColumnGuideCommands.cs ファイルの内容を次のコードに置き換えます (以下で説明します)。

```csharp
using System;
using System.ComponentModel.Design;
using System.Globalization;
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;
using Microsoft.VisualStudio.TextManager.Interop;
using Microsoft.VisualStudio.Text.Editor;
using Microsoft.VisualStudio;

namespace ColumnGuides
{
    /// <summary>
    /// Command handler
    /// </summary>
    internal sealed class ColumnGuideCommands
    {

        const int cmdidAddColumnGuide = 0x0100;
        const int cmdidRemoveColumnGuide = 0x0101;
        const int cmdidChooseGuideColor = 0x0102;
        const int cmdidRemoveAllColumnGuides = 0x0103;

        /// <summary>
        /// Command menu group (command set GUID).
        /// </summary>
        static readonly Guid CommandSet =
            new Guid("c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e");

        /// <summary>
        /// VS Package that provides this command, not null.
        /// </summary>
        private readonly Package package;

        OleMenuCommand _addGuidelineCommand;
        OleMenuCommand _removeGuidelineCommand;

        /// <summary>
        /// Initializes the singleton instance of the command.
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        public static void Initialize(Package package)
        {
            Instance = new ColumnGuideCommands(package);
        }

        /// <summary>
        /// Gets the instance of the command.
        /// </summary>
        public static ColumnGuideCommands Instance
        {
            get;
            private set;
        }

        /// <summary>
        /// Initializes a new instance of the <see cref="ColumnGuideCommands"/> class.
        /// Adds our command handlers for menu (commands must exist in the command
        /// table file)
        /// </summary>
        /// <param name="package">Owner package, not null.</param>
        private ColumnGuideCommands(Package package)
        {
            if (package == null)
            {
                throw new ArgumentNullException("package");
            }

            this.package = package;

            // Add our command handlers for menu (commands must exist in the .vsct file)

            OleMenuCommandService commandService =
                this.ServiceProvider.GetService(typeof(IMenuCommandService))
                    as OleMenuCommandService;
            if (commandService != null)
            {
                // Add guide
                _addGuidelineCommand =
                    new OleMenuCommand(AddColumnGuideExecuted, null,
                                       AddColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidAddColumnGuide));
                _addGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_addGuidelineCommand);
                // Remove guide
                _removeGuidelineCommand =
                    new OleMenuCommand(RemoveColumnGuideExecuted, null,
                                       RemoveColumnGuideBeforeQueryStatus,
                                       new CommandID(ColumnGuideCommands.CommandSet,
                                                     cmdidRemoveColumnGuide));
                _removeGuidelineCommand.ParametersDescription = "<column>";
                commandService.AddCommand(_removeGuidelineCommand);
                // Choose color
                commandService.AddCommand(
                    new MenuCommand(ChooseGuideColorExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidChooseGuideColor)));
                // Remove all
                commandService.AddCommand(
                    new MenuCommand(RemoveAllGuidelinesExecuted,
                                    new CommandID(ColumnGuideCommands.CommandSet,
                                                  cmdidRemoveAllColumnGuides)));
            }
        }

        /// <summary>
        /// Gets the service provider from the owner package.
        /// </summary>
        private IServiceProvider ServiceProvider
        {
            get
            {
                return this.package;
            }
        }

        private void AddColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _addGuidelineCommand.Enabled =
                GuidesSettingsManager.CanAddGuideline(currentColumn);
        }

        private void RemoveColumnGuideBeforeQueryStatus(object sender, EventArgs e)
        {
            int currentColumn = GetCurrentEditorColumn();
            _removeGuidelineCommand.Enabled =
                GuidesSettingsManager.CanRemoveGuideline(currentColumn);
        }

        private int GetCurrentEditorColumn()
        {
            IVsTextView view = GetActiveTextView();
            if (view == null)
            {
                return -1;
            }

            try
            {
                IWpfTextView textView = GetTextViewFromVsTextView(view);
                int column = GetCaretColumn(textView);

                // Note: GetCaretColumn returns 0-based positions. Guidelines are 1-based
                // positions.
                // However, do not subtract one here since the caret is positioned to the
                // left of
                // the given column and the guidelines are positioned to the right. We
                // want the
                // guideline to line up with the current caret position. e.g. When the
                // caret is
                // at position 1 (zero-based), the status bar says column 2. We want to
                // add a
                // guideline for column 1 since that will place the guideline where the
                // caret is.
                return column;
            }
            catch (InvalidOperationException)
            {
                return -1;
            }
        }

        /// <summary>
        /// Find the active text view (if any) in the active document.
        /// </summary>
        /// <returns>The IVsTextView of the active view, or null if there is no active
        /// document or the
        /// active view in the active document is not a text view.</returns>
        private IVsTextView GetActiveTextView()
        {
            IVsMonitorSelection selection =
                this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
                                                    as IVsMonitorSelection;
            object frameObj = null;
            ErrorHandler.ThrowOnFailure(
                selection.GetCurrentElementValue(
                    (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame, out frameObj));

            IVsWindowFrame frame = frameObj as IVsWindowFrame;
            if (frame == null)
            {
                return null;
            }

            return GetActiveView(frame);
        }

        private static IVsTextView GetActiveView(IVsWindowFrame windowFrame)
        {
            if (windowFrame == null)
            {
                throw new ArgumentException("windowFrame");
            }

            object pvar;
            ErrorHandler.ThrowOnFailure(
                windowFrame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView, out pvar));

            IVsTextView textView = pvar as IVsTextView;
            if (textView == null)
            {
                IVsCodeWindow codeWin = pvar as IVsCodeWindow;
                if (codeWin != null)
                {
                    ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
                }
            }
            return textView;
        }

        private static IWpfTextView GetTextViewFromVsTextView(IVsTextView view)
        {

            if (view == null)
            {
                throw new ArgumentNullException("view");
            }

            IVsUserData userData = view as IVsUserData;
            if (userData == null)
            {
                throw new InvalidOperationException();
            }

            object objTextViewHost;
            if (VSConstants.S_OK
                   != userData.GetData(Microsoft.VisualStudio
                                                .Editor
                                                .DefGuidList.guidIWpfTextViewHost,
                                       out objTextViewHost))
            {
                throw new InvalidOperationException();
            }

            IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
            if (textViewHost == null)
            {
                throw new InvalidOperationException();
            }

            return textViewHost.TextView;
        }

        /// <summary>
        /// Given an IWpfTextView, find the position of the caret and report its column
        /// number. The column number is 0-based
        /// </summary>
        /// <param name="textView">The text view containing the caret</param>
        /// <returns>The column number of the caret's position. When the caret is at the
        /// leftmost column, the return value is zero.</returns>
        private static int GetCaretColumn(IWpfTextView textView)
        {
            // This is the code the editor uses to populate the status bar.
            Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
                textView.Caret.ContainingTextViewLine;
            double columnWidth = textView.FormattedLineSource.ColumnWidth;
            return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                       / columnWidth));
        }

        /// <summary>
        /// Determine the applicable column number for an add or remove command.
        /// The column is parsed from command arguments, if present. Otherwise
        /// the current position of the caret is used to determine the column.
        /// </summary>
        /// <param name="e">Event args passed to the command handler.</param>
        /// <returns>The column number. May be negative to indicate the column number is
        /// unavailable.</returns>
        /// <exception cref="ArgumentException">The column number parsed from event args
        /// was not a valid integer.</exception>
        private int GetApplicableColumn(EventArgs e)
        {
            var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
            if (!string.IsNullOrEmpty(inValue))
            {
                int column;
                if (!int.TryParse(inValue, out column) || column < 0)
                    throw new ArgumentException("Invalid column");
                return column;
            }

            return GetCurrentEditorColumn();
        }

        /// <summary>
        /// This function is the callback used to execute a command when the a menu item
        /// is clicked. See the Initialize method to see how the menu item is associated
        /// to this function using the OleMenuCommandService service and the MenuCommand
        /// class.
        /// </summary>
        private void AddColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.AddGuideline(column);
            }
        }

        private void RemoveColumnGuideExecuted(object sender, EventArgs e)
        {
            int column = GetApplicableColumn(e);
            if (column >= 0)
            {
                GuidesSettingsManager.RemoveGuideline(column);
            }
        }

        private void RemoveAllGuidelinesExecuted(object sender, EventArgs e)
        {
            GuidesSettingsManager.RemoveAllGuidelines();
        }

        private void ChooseGuideColorExecuted(object sender, EventArgs e)
        {
            System.Windows.Media.Color color = GuidesSettingsManager.GuidelinesColor;

            using (System.Windows.Forms.ColorDialog picker =
                new System.Windows.Forms.ColorDialog())
            {
                picker.Color = System.Drawing.Color.FromArgb(255, color.R, color.G,
                                                             color.B);
                if (picker.ShowDialog() == System.Windows.Forms.DialogResult.OK)
                {
                    GuidesSettingsManager.GuidelinesColor =
                        System.Windows.Media.Color.FromRgb(picker.Color.R,
                                                           picker.Color.G,
                                                           picker.Color.B);
                }
            }
        }

    }
}

```

**参照を修正**します。 この時点で参照がありません。 ソリューションエクスプローラーの [参照] ノードで、右のポインターボタンを押します。 [**追加**] を選択します。 コマンドを実行して、ヘルプを表示してください。 [ **参照の追加** ] ダイアログには、右上隅に [検索] ボックスがあります。 「Editor」と入力します (二重引用符は使用しません)。 **VisualStudio**項目を選択し (項目を選択するだけでなく、項目の左側のチェックボックスをオンにする必要があります)、[ **OK]** をクリックして参照を追加します。

**[初期化]** 。 パッケージクラスが初期化されると、 `Initialize` commands 実装クラスでが呼び出されます。 初期化では、クラスがインスタンス化され、クラス `ColumnGuideCommands` インスタンスとパッケージ参照がクラスメンバーに保存されます。

クラスコンストラクターから、コマンドハンドラーのフックの1つを見てみましょう。

```csharp
_addGuidelineCommand =
    new OleMenuCommand(AddColumnGuideExecuted, null,
                       AddColumnGuideBeforeQueryStatus,
                       new CommandID(ColumnGuideCommands.CommandSet,
                                     cmdidAddColumnGuide));

```

を作成し `OleMenuCommand` ます。 Visual Studio では、Microsoft Office コマンドシステムが使用されます。 OleMenuCommand をインスタンス化するときのキー引数は、コマンド () を実装する関数、 `AddColumnGuideExecuted` Visual Studio がコマンド () を使用してメニューを表示したときに呼び出す関数、 `AddColumnGuideBeforeQueryStatus` およびコマンド ID です。 Visual studio は、メニューにコマンドを表示する前に query status 関数を呼び出します。これにより、メニューの特定の表示 (たとえば、選択されていない場合に **コピー** を無効にする)、アイコンの変更、名前の変更 (たとえば、何かを削除するなど) を行うことができます。 コマンド ID は、vsct ファイルで宣言されているコマンド ID と一致している必要があります。 コマンドセットと列ガイドの add コマンドの文字列は、vsct ファイルと ColumnGuideCommands.cs の間で一致している必要があります。

次の行は、ユーザーがコマンドウィンドウ (以下で説明) を使用してコマンドを起動する場合のサポートを提供します。

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";
```

**クエリの状態**。 クエリの状態は `AddColumnGuideBeforeQueryStatus` 、 `RemoveColumnGuideBeforeQueryStatus` いくつかの設定 ([ガイドの最大数] や [最大の列] など)、または削除する列ガイドがあるかどうかを確認します。 条件が適切な場合は、コマンドを有効にします。 クエリの状態関数は、Visual Studio がメニューを表示するたびにメニューの各コマンドに対して実行されるため、非常に効率的である必要があります。

**Addcolumnに実行**された関数。 ガイドを追加する際の興味深い点は、現在のエディタービューとキャレットの位置を理解することです。 まず、 `GetApplicableColumn` コマンドハンドラーのイベント引数にユーザーが指定した引数があるかどうかを確認し、存在しない場合はエディターのビューをチェックします。

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

    return GetCurrentEditorColumn();
}

```

`GetCurrentEditorColumn` コードのビューを取得するために、少し掘り下げていく必要があり <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> ます。 、、およびを使用してトレースする場合は、 `GetActiveTextView` `GetActiveView` `GetTextViewFromVsTextView` その方法を確認できます。 次に示すのは、現在の選択範囲から開始し、選択したフレームを取得してから、フレームの DocView をとして取得し、次に <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> IVsTextView からを取得して、ビューホストを取得し、最後に IWpfTextView を取得する、関連するコードです <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> 。

```csharp
   IVsMonitorSelection selection =
       this.ServiceProvider.GetService(typeof(IVsMonitorSelection))
           as IVsMonitorSelection;
   object frameObj = null;

ErrorHandler.ThrowOnFailure(selection.GetCurrentElementValue(
                                (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame,
                                out frameObj));

   IVsWindowFrame frame = frameObj as IVsWindowFrame;
   if (frame == null)
       <<do nothing>>;

...
   object pvar;
   ErrorHandler.ThrowOnFailure(frame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView,
                                                  out pvar));

   IVsTextView textView = pvar as IVsTextView;
   if (textView == null)
   {
       IVsCodeWindow codeWin = pvar as IVsCodeWindow;
       if (codeWin != null)
       {
           ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));
       }
   }

...
   if (textView == null)
       <<do nothing>>

   IVsUserData userData = textView as IVsUserData;
   if (userData == null)
       <<do nothing>>

   object objTextViewHost;
   if (VSConstants.S_OK
           != userData.GetData(Microsoft.VisualStudio.Editor.DefGuidList
                                                            .guidIWpfTextViewHost,
                                out objTextViewHost))
   {
       <<do nothing>>
   }

   IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;
   if (textViewHost == null)
       <<do nothing>>

   IWpfTextView textView = textViewHost.TextView;

```

IWpfTextView を取得したら、カレットがある列を取得できます。

```csharp
private static int GetCaretColumn(IWpfTextView textView)
{
    // This is the code the editor uses to populate the status bar.
    Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =
        textView.Caret.ContainingTextViewLine;
    double columnWidth = textView.FormattedLineSource.ColumnWidth;
    return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)
                                / columnWidth));
}

```

ユーザーがクリックした位置にある現在の列を使用して、コードは設定マネージャーでを呼び出して列を追加または削除します。 設定マネージャーは、すべてのオブジェクトがリッスンするイベントを発生させ `ColumnGuideAdornment` ます。 イベントが発生すると、これらのオブジェクトは、関連付けられているテキストビューを新しい列ガイドの設定で更新します。

## <a name="invoking-command-from-the-command-window"></a>コマンドウィンドウからのコマンドの呼び出し
列ガイドのサンプルを使用すると、ユーザーはコマンドウィンドウから2つのコマンドを拡張機能として呼び出すことができます。 [ **他の Windows &#124; コマンドウィンドウを表示 &#124;** ] コマンドを使用すると、コマンドウィンドウが表示されます。 コマンドウィンドウを操作するには、「edit」と入力し、コマンド名 completion を入力して引数120を指定します。これには、次のものがあります。

```
> Edit.AddColumnGuide 120
>
```

これを有効にするサンプルの部分は、vsct ファイル宣言、 `ColumnGuideCommands` コマンドハンドラーをフックするときのクラスコンストラクター、およびイベント引数をチェックするコマンドハンドラーの実装に含まれています。

[ `<CommandFlag>CommandWellOnly</CommandFlag>` **編集** ] メニューの UI にコマンドを表示しない場合でも、vsct ファイルに "" が表示され、メインメニューの [編集] が表示されます。 メインの [編集] メニューを使用すると、 **edit. AddColumnGuide**などの名前が付けられます。 次の4つのコマンドを保持するコマンドグループ宣言は、[編集] メニューにグループを直接配置したものです。

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

```

ボタンのセクションでは、メインメニューに表示されないようにするコマンドを後で宣言し、次のように宣言してい `CommandWellOnly` `AllowParams` ます。

```xml
<Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide" 
        priority="0x0100" type="Button">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
  <Icon guid="guidImages" id="bmpPicAddGuide" />
  <CommandFlag>CommandWellOnly</CommandFlag>
  <CommandFlag>AllowParams</CommandFlag>

```

クラスコンストラクターで、許可されている `ColumnGuideCommands` パラメーターの説明を指定して、コマンドハンドラーのフックコードをフックしていることを確認しました。

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";

```

`GetApplicableColumn` `OleMenuCmdEventArgs` 現在の列に対してエディターのビューをチェックする前に、関数によって値がチェックされていることを確認しました。

```csharp
private int GetApplicableColumn(EventArgs e)
{
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;
    if (!string.IsNullOrEmpty(inValue))
    {
        int column;
        if (!int.TryParse(inValue, out column) || column < 0)
            throw new ArgumentException("Invalid column");
        return column;
    }

```

## <a name="trying-your-extension"></a>拡張機能を試しています
これで、 **F5** キーを押して、列ガイド拡張機能を実行できます。 テキストファイルを開き、エディターのコンテキストメニューを使用して、ガイドラインの追加、削除、および色の変更を行います。 列ガイドを追加するには、テキスト内をクリックする必要があります (行の末尾に空白文字が渡されません)。または、エディターによって行の最後の列に追加されます。 コマンドウィンドウを使用して引数を指定してコマンドを呼び出す場合は、任意の場所に列ガイドを追加できます。

さまざまなコマンドの配置、名前の変更、アイコンの変更などを試して、Visual Studio で最新のコードをメニューに表示しているときに問題が発生した場合は、デバッグ中の実験的な hive をリセットできます。 Windows の [ **スタート] メニュー** を開き、「リセット」と入力します。 **次の Visual Studio の実験的なインスタンスをリセット**するコマンドを探して起動します。 これにより、すべての拡張コンポーネントの実験的なレジストリハイブがクリーンアップされます。 コンポーネントから設定が消去されることはありません。そのため、Visual Studio の実験的な hive をシャットダウンしたときのガイドは、コードが次回の起動時に設定ストアを読み取るときに引き続き表示されます。

## <a name="finished-code-project"></a>完成したコードプロジェクト
近日中に Visual Studio 機能拡張サンプルの GitHub プロジェクトが完成し、完成したプロジェクトがそこに配置されます。 この問題が発生した時点で、このトピックを更新します。 完成したサンプルプロジェクトには guid が異なる場合があり、コマンドアイコンに対して異なるビットマップストリップが使用されます。

この Visual Studio ギャラリーの[拡張](https://visualstudiogallery.msdn.microsoft.com/da227a0b-0e31-4a11-8f6b-3a149cf2e459?SRC=Home)機能を使用して、列ガイド機能のバージョンを試すことができます。

## <a name="see-also"></a>参照
[エディター内](../extensibility/inside-the-editor.md) 
[エディターと言語サービス](../extensibility/extending-the-editor-and-language-services.md) 
 の拡張[言語サービスとエディターの拡張点](../extensibility/language-service-and-editor-extension-points.md) 
[メニューとコマンド](../extensibility/extending-menus-and-commands.md) 
 の拡張メニューへの[サブメニューの追加](../extensibility/adding-a-submenu-to-a-menu.md) 
[エディター項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)
