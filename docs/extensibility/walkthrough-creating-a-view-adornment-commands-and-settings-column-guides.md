---
title: ビューの表示表示要素、コマンド、および設定を作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4a2df0a3-42da-4f7b-996f-ee16a35ac922
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4aab9e0ede95eebe6f8f54cc3f01e7e7d5f98d1c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697647"
---
# <a name="walkthrough-create-a-view-adornment-commands-and-settings-column-guides"></a>チュートリアル: ビューの表示要素、コマンド、および設定を作成する (列ガイド)
コマンドとビュー効果を使用して、Visual Studio のテキスト/コード エディターを拡張できます。 この記事では、一般的な拡張機能のコラム ガイドを使用する方法について説明します。 列ガイドは、特定の列幅にコードを管理するために、テキスト エディターのビューに描画される視覚的に明るい線です。 具体的には、書式設定されたコードは、ドキュメント、ブログの投稿、またはバグ レポートに含めるサンプルに重要です。

このチュートリアルでは次を行います。
- VSIX プロジェクトを作成する
- エディター ビューの表示要素を追加する
- 設定の保存と取得のサポートを追加する(列ガイドとその色を描画する場所)
- コマンドを追加する(列ガイドの追加/削除、色の変更)
- [編集] メニューとテキスト ドキュメントのコンテキスト メニューにコマンドを配置する
- Visual Studio コマンド ウィンドウからコマンドを呼び出すためのサポートを追加します。

  この Visual Studio ギャラリー[拡張機能](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)を使用して、列ガイドのバージョンの機能を試すことができます。

  > [!NOTE]
  > このチュートリアルでは、Visual Studio 拡張機能テンプレートによって生成されるいくつかのファイルに大量のコードを貼り付けます。 しかし、このチュートリアルでは、すぐに他の拡張例と GitHub で完成したソリューションを参照します。 完成したコードは、汎用テンプレート アイコンを使用する代わりに実際のコマンド アイコンを持つというので、若干異なります。

## <a name="get-started"></a>はじめに
Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="set-up-the-solution"></a>ソリューションのセットアップ
まず、VSIX プロジェクトを作成し、エディター ビューの表示要素を追加し、コマンドを追加します (コマンドを所有する VSPackage を追加します)。 基本的なアーキテクチャは次のとおりです。
- ビューごとにオブジェクトを作成するテキスト ビュー作成`ColumnGuideAdornment`リスナーがあります。 このオブジェクトは、ビューの変更や設定の変更、更新、列ガイドの再描画に関するイベントを必要に応じて待機します。
- `GuidesSettingsManager` Visual Studio の設定ストレージからの読み取りと書き込みを処理するがあります。 設定マネージャーには、ユーザー コマンドをサポートする設定 (列の追加、列の削除、色の変更) の更新操作もあります。
- ユーザー コマンドがある場合に必要な VSIP パッケージがありますが、コマンド実装オブジェクトを初期化するのは単なる定型コードです。
- ユーザー コマンドを`ColumnGuideCommands`実行し *、.vsct*ファイルで宣言されたコマンドのコマンド ハンドラーをフックするオブジェクトがあります。

  **VSIX**. **ファイル &#124; New ..** コマンドを使用してプロジェクトを作成します。 左側のナビゲーション ペインの **[C#]** の下にある **[機能**拡張] ノードを選択し、右側のウィンドウで **[VSIX プロジェクト**] を選択します。 名前を入力**して、列ガイド**をクリックし **、OK**プロジェクトを作成します。

  **表示表示 :** ソリューション エクスプローラーでプロジェクト ノードの右ポインター ボタンを押します。 新しいビューの表示要素**を追加するには、[新しい項目の追加]** をクリック&#124; . 左側のナビゲーション ペインで **[機能拡張&#124; エディター** ] を選択し、右側のペインで **[エディター ビューポート表示要素**] を選択します。 項目名として**列ガイド Adornment**という名前を入力し、[**追加**] を選択して追加します。

  この項目テンプレートは **、ColumnGuideAdornment.cs**と**ColumnGuideAdornmentTextViewCreationListener.cs**の 2 つのファイル (参照など) をプロジェクトに追加したことがわかります。 テンプレートは、ビューに紫色の長方形を描画します。 次のセクションでは、ビュー作成リスナーの行をいくつか変更し **、ColumnGuideAdornment.cs**の内容を置き換えます。

  **コマンド**: **ソリューション エクスプローラー**で、プロジェクト ノードの右ポインター ボタンをクリックします。 新しいビューの表示要素**を追加するには、[新しい項目の追加]** をクリック&#124; . 左側のナビゲーション ペインで **[VSPackage &#124;機能**拡張] を選択し、右側のペインで **[カスタム コマンド**] を選択します。 項目名として**列ガイドコマンド**という名前を入力し、[**追加**] を選択します。 いくつかの参照に加えて、コマンドとパッケージを追加**すると、** ColumnGuideCommandsPackage.cs 、および**列ガイドコマンドパッケージ.vsct** **ColumnGuideCommands.cs**も追加されました。 次のセクションでは、コマンドを定義して実装するために、最初と最後のファイルの内容を置き換えます。

## <a name="set-up-the-text-view-creation-listener"></a>テキスト ビュー作成リスナーの設定
エディターで*ColumnGuideAdornmentTextViewCreationListener.cs*を開きます。 このコードは、Visual Studio がテキスト ビューを作成するたびに、ハンドラーを実装します。 ビューの特性に応じて、ハンドラーが呼び出されるタイミングを制御する属性があります。

また、このコードでは、表示要素レイヤーを宣言する必要があります。 エディターは、ビューを更新するときに、ビューの表示要素レイヤーを取得し、そこから表示要素を取得します。 属性を使用して、他のレイヤーと相対的にレイヤーの順序を宣言できます。 次の行を置き換えます。

```csharp
[Order(After = PredefinedAdornmentLayers.Caret)]
```

次の 2 行を使用します。

```csharp
[Order(Before = PredefinedAdornmentLayers.Text)]
[TextViewRole(PredefinedTextViewRoles.Document)]
```

置き換えた線は、表示要素レイヤーを宣言する属性のグループに含まれています。 変更した最初の行は、列のガイドラインが表示される位置にのみ変更されます。 ビュー内のテキストを「前」に行を描画すると、テキストの後ろまたは下に表示されます。 2 番目の行では、列ガイドの表示要素がドキュメントの概念に合ったテキスト エンティティに適用可能であると宣言していますが、たとえば、編集可能なテキストに対してのみ機能するように、表示要素を宣言できます。 [言語サービスとエディターの拡張機能ポイント](../extensibility/language-service-and-editor-extension-points.md)に関する詳細情報

## <a name="implement-the-settings-manager"></a>設定マネージャーを実装する
*GuidesSettingsManager.cs*の内容を次のコードに置き換えます(以下の説明を参照)。

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
                // Not present.  Allow user to remove the last column
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
        // can update.  We need nothing special in this event since the settings manager
        // is statically available.
        //
        internal delegate void SettingsChangedHandler();
        static internal event SettingsChangedHandler SettingsChanged;

    }
}

```

このコードのほとんどは、設定形式を作成して解析します: "RGB(int\<\<>、int\<>、int \<>) \<int>、int>.." 。  最後の整数は、列ガイドを配置する 1 から 1 から 1 つの列です。 列ガイド拡張機能は、すべての設定を 1 つの設定値文字列にキャプチャします。

強調表示する価値のあるコードの一部があります。 次のコード行は、設定ストレージの Visual Studio マネージ ラッパーを取得します。 ほとんどの場合、この方法は Windows レジストリを抽象化しますが、この API はストレージ メカニズムとは独立しています。

```csharp
internal static SettingsManager VsManagedSettingsManager =
    new ShellSettingsManager(ServiceProvider.GlobalProvider);
```

Visual Studio の設定ストレージでは、カテゴリ識別子と設定識別子を使用して、すべての設定を一意に識別します。

```csharp
private const string _collectionSettingsName = "Text Editor";
private const string _settingName = "Guides";
```

カテゴリ名として使用`"Text Editor"`する必要はありません。 あなたが好きなものを選ぶことができます。

最初のいくつかの関数は、設定を変更するためのエントリポイントです。 許可されているガイドの最大数などの高レベルの制約をチェックします。  次に、設定`WriteSettings`文字列を構成し、プロパティ`GuideLinesConfiguration`を設定する を呼び出します。 このプロパティを設定すると、設定値が Visual Studio 設定ストア`SettingsChanged`に保存され、テキスト`ColumnGuideAdornment`ビューに関連付けられているすべてのオブジェクトを更新するイベントが発生します。

設定を変更するコマンドを実装するために使用されるエントリ`CanAddGuideline`ポイント関数など、いくつかのエントリ ポイント関数があります。 Visual Studio は、メニューを表示するときに、コマンドの実装を照会して、コマンドが現在有効かどうか、コマンド名などがどのようなものかを確認します。  以下では、コマンドの実装のためにこれらのエントリポイントをフックする方法を説明します。 コマンドの詳細については、[メニューとコマンドの拡張を](../extensibility/extending-menus-and-commands.md)参照してください。

## <a name="implement-the-columnguideadornment-class"></a>クラスを実装します。
クラス`ColumnGuideAdornment`は、表示要素を持つことができる各テキスト ビューに対してインスタンス化されます。 このクラスは、ビューの変更や設定の変更に関するイベントをリッスンし、必要に応じて列ガイドの更新または再描画を行います。

*ColumnGuideAdornment.cs*の内容を次のコードに置き換えます(以下の説明を参照)。

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

このクラスのインスタンスは、ビューに描画された<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>関連付けられたオブジェクト`Line`とオブジェクトのリストに保持されます。

コンストラクター (Visual `ColumnGuideAdornmentTextViewCreationListener` Studio が新しいビューを作成するときに呼び`Line`出されます) は、列ガイド オブジェクトを作成します。  また、コンストラクターは、 で`SettingsChanged``GuidesSettingsManager`定義されているイベントとビュー イベント`LayoutChanged`および`Closed`のハンドラーも追加します。

イベント`LayoutChanged`は、Visual Studio がビューを作成するタイミングなど、ビュー内のいくつかの種類の変更によって発生します。 `OnViewLayoutChanged`実行するハンドラー`AddGuidelinesToAdornmentLayer`呼び出し。 のコードは`OnViewLayoutChanged`、フォント サイズの変更、表示のとじらぎ、水平スクロールなどの変更に基づいて行位置を更新する必要があるかどうかを判断します。 コード内`UpdatePositions`のコードでは、文字間、またはテキスト行の指定した文字オフセット内のテキスト列の直後に、ガイド線が描画されます。

設定が変更されるたびに`SettingsChanged`、新しい設定が何`Line`であれ、すべてのオブジェクトを再作成するだけです。 行の位置を設定した後、コードは、表示`Line`要素レイヤーから`ColumnGuideAdornment`以前のすべてのオブジェクトを削除し、新しいオブジェクトを追加します。

## <a name="define-the-commands-menus-and-menu-placements"></a>コマンド、メニュー、およびメニュー配置の定義
コマンドやメニューの宣言、他のさまざまなメニューへのコマンドやメニューのグループの配置、およびコマンド ハンドラーのフックは、多くの場合があります。 このチュートリアルでは、この拡張機能でのコマンドの動作について説明しますが、詳細については、「[メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)」を参照してください。

### <a name="introduction-to-the-code"></a>コードの概要
列ガイド拡張機能は、一緒に属するコマンドのグループを宣言し (列の追加、列の削除、線の色の変更)、そのグループをエディターのコンテキスト メニューのサブメニューに配置する方法を示します。  列ガイド拡張機能は、メインの**編集**メニューにもコマンドを追加しますが、以下の一般的なパターンとして説明し、それらを非表示に保ちます。

コマンドの実装には、ColumnGuideCommandsPackage.cs、列ガイドコマンドパッケージ.vsct、およびColumnGuideCommands.csの 3 つの部分があります。 テンプレートによって生成されたコードは、ツール**メニューに**コマンドを配置し、ダイアログ ボックスを実装としてポップします。 vsct ファイルと*ColumnGuideCommands.cs*ファイルでは簡単であるため *.vsct*、この方法を確認できます。 以下のファイルのコードを置き換えます。

パッケージ コードには、拡張機能がコマンドを提供していることを検出し、コマンドを配置する場所を見つけるために Visual Studio に必要な定型宣言が含まれています。 パッケージが初期化されると、コマンド実装クラスがインスタンス化されます。 コマンドに関連するパッケージの詳細については、[メニューとコマンドの拡張を](../extensibility/extending-menus-and-commands.md)参照してください。

### <a name="a-common-commands-pattern"></a>一般的なコマンド パターン
列ガイド拡張機能のコマンドは、Visual Studio で非常に一般的なパターンの例です。 関連するコマンドをグループに配置し、メイン メニュー`<CommandFlag>CommandWellOnly</CommandFlag>`にグループを配置します。  メイン メニュー (**編集**など) にコマンドを配置すると、**ツール オプション**でキー バインドを再割り当てするときにコマンドを検索する場合に便利な名前 **(Edit.AddColumnGuide**など) が表示されます。 コマンド**ウィンドウ**からコマンドを呼び出すときに、完了を取得する場合にも便利です。

次に、ユーザーがコマンドを使用するコンテキスト メニューまたはサブメニューにコマンドのグループを追加します。 Visual Studio`CommandWellOnly`は、メイン メニューのみの非表示フラグとして扱われます。 コンテキスト メニューまたはサブ メニューに同じコマンド グループを配置すると、コマンドが表示されます。

共通パターンの一部として、列ガイド拡張機能は、単一のサブメニューを保持する 2 番目のグループを作成します。 サブメニューには、4 列のガイド コマンドを含む最初のグループが含まれます。 サブメニューを保持する 2 番目のグループは、さまざまなコンテキストメニューに配置する再利用可能なアセットで、これらのコンテキストメニューにサブメニューを配置します。

### <a name="the-vsct-file"></a>vsct ファイル
*.vsct*ファイルは、コマンドとその行く場所をアイコンなどと共に宣言します。 *.vsct*ファイルの内容を次のコードに置き換えます (以下の説明を参照)。

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

**GUID .** Visual Studio でコマンド ハンドラーを検索して呼び出すには *、ColumnGuideCommandsPackage.cs*ファイルで宣言されたパッケージ GUID (プロジェクト項目テンプレートから生成) が *、.vsct*ファイルで宣言されたパッケージ GUID (上記からコピー) と一致していることを確認する必要があります。 このサンプル コードを再利用する場合は、このコードをコピーした可能性のある他のユーザーと競合しないように、別の GUID を使用していることを確認してください。

*ColumnGuideCommandsPackage.cs*で次の行を検索し、引用符の間から GUID をコピーします。

```csharp
public const string PackageGuidString = "ef726849-5447-4f73-8de5-01b9e930f7cd";
```

次に *、.vsct*ファイルに GUID を貼り付け、宣言に`Symbols`次の行を記述します。

```xml
<GuidSymbol name="guidColumnGuideCommandsPkg"
            value="{ef726849-5447-4f73-8de5-01b9e930f7cd}" />
```

コマンド セットとビットマップ イメージ ファイルの GUID は、拡張機能に対して一意である必要があります。

```xml
<GuidSymbol name="guidColumnGuidesCommandSet"
            value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">
<GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">
```

ただし、このチュートリアルでコマンド セットとビットマップ イメージの GUID を変更してコードを動作させるために必要はありません。 コマンド セット GUID は*ColumnGuideCommands.cs*ファイル内の宣言と一致する必要がありますが、そのファイルの内容も置き換えます。したがって、GUID は一致します。

*.vsct*ファイル内の他の GUID は、列ガイドコマンドが追加される既存のメニューを識別するため、変更されることはありません。

**ファイル セクション**: *vsct*には、コマンド、配置、およびシンボルの 3 つの外側のセクションがあります。 コマンド セクションでは、コマンド グループ、メニュー、ボタンまたはメニュー項目、およびアイコンのビットマップを定義します。 Placements セクションでは、グループがメニュー上に移動するか、既存のメニューに追加の配置を行うことを宣言します。 シンボル セクションでは *、.vsct*ファイル内の他の場所で使用される識別子 *.vsct*を宣言します。

**コマンド セクション、グループ定義**。 コマンド セクションでは、まずコマンド グループを定義します。 コマンドのグループは、グループを区切るわずかな灰色の線を持つメニューに表示されるコマンドです。 この例のように、グループがサブメニュー全体に表示される場合もあり、この場合は灰色の区切り線が表示されません。 *vsct*ファイルは、親の 2`GuidesMenuItemsGroup`つのグループ`IDM_VS_MENU_EDIT`を宣言します(**編集**メニューのメイン)`GuidesContextMenuGroup`と親にするグループ`IDM_VS_CTXT_CODEWIN`(コード エディターのコンテキスト メニュー)。

2 番目のグループ宣言`0x0600`には、優先順位があります。

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"
             priority="0x0600">
```

この考え方は、サブメニューグループを追加するコンテキストメニューの最後に、列ガイドサブメニューを配置することです。 しかし、あなたが最もよく知っていると仮定し、優先順位を使用してサブメニューを常に最後にする必要はありません`0xFFFF`。 サブメニューが配置されているコンテキストメニューのどこにあるかを確認するには、番号を試してみる必要があります。 この場合、`0x0600`メニューの最後に表示されるほど高いですが、必要に応じて、他のユーザーが拡張を列ガイドの拡張子よりも低く設計する余地を残します。

**コマンド セクション、 メニュー定義**。 次に、コマンド セクションで、`GuidesSubMenu`の親となるサブ`GuidesContextMenuGroup`メニューを定義します。 `GuidesContextMenuGroup`は、関連するすべてのコンテキストメニューに追加するグループです。 プレースメント セクションでは、このサブメニューに 4 列のガイド コマンドを使用してグループを配置します。

**コマンドセクション、ボタンの定義**. 次に、コマンド セクションで、4 列ガイドコマンドであるメニュー項目またはボタンを定義します。 `CommandWellOnly`上で説明した場合、メインメニューに配置するとコマンドが見えなくなるという意味です。 メニュー項目ボタン宣言の 2 つ (ガイドの追加とガイドの削除`AllowParams`) にもフラグがあります。

```xml
<CommandFlag>AllowParams</CommandFlag>
```

このフラグを使用すると、メイン メニューの配置と共に、Visual Studio がコマンド ハンドラーを呼び出したときに引数を受け取るコマンドが有効になります。  ユーザーがコマンド ウィンドウからコマンドを実行すると、引数はイベント引数のコマンド ハンドラーに渡されます。

**コマンド セクション、ビットマップ定義**。 最後に、コマンド セクションでは、コマンドに使用されるビットマップまたはアイコンを宣言します。 このセクションは、プロジェクト リソースを識別し、使用アイコンの 1 からベースのインデックスを一覧表示する単純な宣言です。 *.vsct*ファイルのシンボル セクションでは、インデックスとして使用される識別子の値を宣言します。 このチュートリアルでは、プロジェクトに追加されたカスタム コマンド項目テンプレートで提供されるビットマップ ストリップを使用します。

**[配置] セクション**。 コマンドセクションの後に配置セクションがあります。 最初の 1 つは、コマンドが表示されるサブ メニューに 4 列のガイド コマンドを保持する、上記の最初のグループを追加するコードです。

```xml
<CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
                  priority="0x0100">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />
</CommandPlacement>
```

他のすべての配置では、 (`GuidesContextMenuGroup`を含む`GuidesSubMenu`) が他のエディターコンテキストメニューに追加されます。 コードが`GuidesContextMenuGroup`を宣言したとき、コード エディターのコンテキスト メニューに親として配置されました。 そのため、コード エディターのコンテキスト メニューの配置が表示されません。

**記号セクション**。 上記のように、シンボル セクションでは *、.vsct*ファイル内の他の場所で使用される識別子を *.vsct*宣言します。 このセクションで重要な点は、パッケージ GUID がパッケージ クラスの宣言と一致する必要がある点です。 また、コマンド セット GUID は、コマンド実装クラスの宣言と一致する必要があります。

## <a name="implement-the-commands"></a>コマンドの実装
*ColumnGuideCommands.cs*ファイルは、コマンドを実装し、ハンドラーをフックします。 Visual Studio がパッケージを読み込んで初期化すると、パッケージは`Initialize`コマンド実装クラスを順番に呼び出します。 コマンドの初期化はクラスを単にインスタンス化し、コンストラクターはすべてのコマンド ハンドラーをフックします。

*ColumnGuideCommands.cs*ファイルの内容を次のコードに置き換えます (以下の説明を参照)。

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

**参照を修正**する 。 この時点で参照が見つかりません。 ソリューション エクスプローラーの [参照] ノードの右ポインター ボタンを押します。 [.. の**追加]** コマンドを選択します。 [**参照の追加]** ダイアログボックスの右上隅に検索ボックスがあります。 「エディタ」と入力します(二重引用符は使用しません)。 **項目を**選択し (項目を選択するだけでなく、項目の左側のボックスをオンにする必要があります **)、[OK] を**選択して参照を追加します。

**[初期化]**。  パッケージ クラスは初期化時に、コマンド`Initialize`実装クラスを呼び出します。 初期化`ColumnGuideCommands`では、クラスをインスタンス化し、クラスのインスタンスとクラスのメンバーにパッケージ参照を保存します。

クラスコンストラクターからコマンドハンドラーのフックアップの 1 つを見てみましょう。

```csharp
_addGuidelineCommand =
    new OleMenuCommand(AddColumnGuideExecuted, null,
                       AddColumnGuideBeforeQueryStatus,
                       new CommandID(ColumnGuideCommands.CommandSet,
                                     cmdidAddColumnGuide));

```

を作成すると`OleMenuCommand`、 が作成されます。 Office コマンド システムが使用されています。 インスタンス化時の重要な引数`OleMenuCommand`は、コマンド ( ) を実装する`AddColumnGuideExecuted`関数`AddColumnGuideBeforeQueryStatus`です。 Visual Studio は、メニューにコマンドを表示する前にクエリの状態関数を呼び出し、メニューの特定の表示に対してコマンド自体を非表示または淡色表示にしたり (たとえば、選択がない場合は **[コピー]** を無効にする)、アイコンを変更したり、名前を変更したり ([何かの追加] から[何かを削除する]など) できるようにします。 コマンド ID は *、.vsct*ファイルで宣言されているコマンド ID と一致する必要があります。 コマンド セットと列ガイドの追加コマンドの文字列は *、.vsct*ファイルと*ColumnGuideCommands.cs*の間で一致する必要があります。

次の行は、ユーザーがコマンド ウィンドウを介してコマンドを呼び出す場合の支援を提供します (以下の説明を参照)。

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";
```

 **クエリの状態**: クエリの状態は`AddColumnGuideBeforeQueryStatus`機能`RemoveColumnGuideBeforeQueryStatus`し、いくつかの設定(ガイドの最大数や最大列数など)を確認するか、削除する列ガイドがある場合に確認します。 条件が正しければ、コマンドを有効にします。  Visual Studio がメニューを表示するたびに、メニューの各コマンドに対して実行されるため、クエリの状態関数は効率的である必要があります。

 **関数を追加します**。 ガイドを追加する興味深い部分は、現在のエディタビューとキャレットの位置を把握することです。  まず、この関数は`GetApplicableColumn`、コマンド ハンドラのイベント引数にユーザ指定の引数があるかどうかをチェックし、何も存在しない場合はエディタのビューをチェックする関数を呼び出します。

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

`GetCurrentEditorColumn`コードの<xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView>ビューを取得するために少し掘り下げる必要があります。  をトレース`GetActiveTextView`すると、 `GetActiveView` `GetTextViewFromVsTextView`、 をトレースする方法がわかります。 次のコードは、現在の選択から始まり、選択したフレームを取得し、次にフレームの DocView を<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>取得し、IVsTextView<xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData>から取得し、ビュー ホストを取得し、最後に IWpfTextView を取得する関連コードを抽象化しています。

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

IWpfTextView を作成したら、キャレットが配置されている列を取得できます。

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

ユーザーがクリックした現在の列を使用すると、コードは設定マネージャーを呼び出して列を追加または削除するだけです。 設定マネージャは、すべての`ColumnGuideAdornment`オブジェクトがリッスンするイベントを起動します。 イベントが発生すると、これらのオブジェクトは、関連付けられたテキスト ビューを新しい列ガイド設定で更新します。

## <a name="invoke-command-from-the-command-window"></a>コマンド ウィンドウからのコマンドの呼び出し
列ガイドのサンプルを使用すると、ユーザーは機能拡張の形式としてコマンド ウィンドウから 2 つのコマンドを呼び出すことができます。 コマンド ウィンドウの **[他のウィンドウ&#124;** 表示] コマンド&#124;使用すると、コマンド ウィンドウが表示されます。 コマンド ウィンドウを操作するには、"edit"と入力し、コマンド名の補完と引数 120 を指定すると、次のような結果になります。

```csharp
> Edit.AddColumnGuide 120
>
```

この動作を有効にするサンプルの一部は *、.vsct*ファイルの宣言、`ColumnGuideCommands`コマンド ハンドラーをフックするときのクラス コンストラクター、およびイベント引数をチェックするコマンド ハンドラーの実装です。

コマンドが`<CommandFlag>CommandWellOnly</CommandFlag>`**[編集**] メニューの UI に表示されていない場合でも *、.vsct*ファイルに "" と **[編集**] メイン メニューの配置が表示されています。 メインの **[編集]** メニューにそれらの名前を表示すると **、編集.AddColumnGuide**のような名前が付けられます。 4 つのコマンドを保持するコマンド グループ宣言は **、グループを直接 [編集]** メニューに配置します。

```xml
<Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"
             priority="0xB801">
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />
      </Group>

```

ボタンセクションは後でメインメニュー`CommandWellOnly`で非表示に保つためのコマンドを宣言し、 で`AllowParams`宣言しました:

```xml
<Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"
        priority="0x0100" type="Button">
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />
  <Icon guid="guidImages" id="bmpPicAddGuide" />
  <CommandFlag>CommandWellOnly</CommandFlag>
  <CommandFlag>AllowParams</CommandFlag>

```

クラスコンストラクタでコードをフックするコマンドハンドラが`ColumnGuideCommands`、許可されたパラメータの説明を提供しているのを見ました。

```csharp
_addGuidelineCommand.ParametersDescription = "<column>";

```

現在の列`GetApplicableColumn`のエディター`OleMenuCmdEventArgs`のビューをチェックする前に、関数が値をチェックするのを見ました:

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

## <a name="try-your-extension"></a>拡張機能を試す
**F5**キーを押して、列ガイドの拡張機能を実行できるようになりました。 テキスト ファイルを開き、エディタのコンテキスト メニューを使用して、ガイド線を追加したり、削除したり、色を変更したりします。 行の末尾を通過した空白文字ではないテキストをクリックして列ガイドを追加するか、エディタによって行の最後の列に追加します。 コマンド ウィンドウを使用して引数を指定してコマンドを呼び出す場合は、任意の場所に列ガイドを追加できます。

異なるコマンドの配置、名前の変更、アイコンの変更などを試してみて、メニューの最新のコードを表示する Visual Studio で問題が発生する場合は、デバッグ中の実験用ハイブをリセットできます。 **Windowsのスタートメニュー**を起動し、「リセット」と入力します。 [次の**Visual Studio 実験用インスタンスのリセット]** コマンドを探して実行します。 このコマンドは、すべての拡張コンポーネントの実験用レジストリ ハイブをクリーンアップします。 コンポーネントから設定が消去されないため、Visual Studio の実験用ハイブをシャットダウンしたときに用意していたガイドは、コードが次回の起動時に設定ストアを読み取るときにも表示されます。

## <a name="finished-code-project"></a>完成したコード プロジェクト
まもなく Visual Studio の機能拡張サンプルの GitHub プロジェクトが作成され、完成したプロジェクトが完成します。 この記事は、それが発生したときにそこにポイントするように更新されます。 完成したサンプル プロジェクトは、異なる guid を持つ可能性があり、コマンド アイコン用に異なるビットマップ ストリップがあります。

この Visual Studio ギャラリー[拡張機能](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines)を使用して、列ガイドのバージョンの機能を試すことができます。

## <a name="see-also"></a>関連項目
- [エディタ内](../extensibility/inside-the-editor.md)
- [エディタと言語サービスを拡張する](../extensibility/extending-the-editor-and-language-services.md)
- [言語サービスとエディターの拡張ポイント](../extensibility/language-service-and-editor-extension-points.md)
- [メニューとコマンドの拡張](../extensibility/extending-menus-and-commands.md)
- [メニューにサブメニューを追加する](../extensibility/adding-a-submenu-to-a-menu.md)
- [エディター項目テンプレートを使用して拡張機能を作成する](../extensibility/creating-an-extension-with-an-editor-item-template.md)
