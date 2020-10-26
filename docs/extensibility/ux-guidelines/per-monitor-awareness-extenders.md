---
title: Visual Studio extender のモニターごとの認識のサポート
titleSuffix: ''
description: Visual Studio 2019 で利用できる新しい extender のサポートについて説明します。
ms.date: 04/10/2019
helpviewer_keywords:
- Visual Studio, PMA, per-monitor-awareness, extenders, Windows Forms
- Per-Monitor Awareness support for extenders
author: rub8n
ms.author: rurios
manager: anthc
monikerRange: vs-2019
ms.topic: conceptual
dev_langs:
- CSharp
- CPP
ms.openlocfilehash: 09ec5d82251fa4598096fca8a59c9a1fd29e3f27
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "69585376"
---
# <a name="per-monitor-awareness-support-for-visual-studio-extenders"></a>Visual Studio extender のモニターごとの認識のサポート

Visual Studio 2019 より前のバージョンでは、DPI 認識コンテキストがモニターごとの DPI 対応 (PMA) ではなく、システムに対応するように設定されていました。 システム認識を使用して実行すると、Visual Studio がさまざまなスケールファクターを持つモニター間でレンダリングする必要がある場合や、異なるディスプレイ構成 (異なる Windows スケーリングなど) でコンピューターにリモートで表示する必要がある場合に、視覚効果が低下します (たとえば、フォントやアイコンがぼやけています)。

Visual Studio 2019 の DPI 認識コンテキストは、環境でサポートされている場合は PMA として設定されます。これにより、Visual Studio は、1つのシステム定義の構成ではなく、ホストされているディスプレイの構成に従ってレンダリングできます。 最終的には、PMA モードをサポートするセキュリティで常に明瞭な UI に変換されます。

このドキュメントで取り上げられている用語と全体的なシナリオの詳細については、 [Windows ドキュメントの「高 DPI デスクトップアプリケーション開発](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows) 」を参照してください。

## <a name="quickstart"></a>クイック スタート

- Visual Studio が PMA モードで実行されていることを確認します (「 **PMA の有効化**」を参照してください)

- 一連の一般的なシナリオで拡張機能が正しく機能することを検証する (「 **PMA の問題の拡張機能のテスト」を**参照)

- 問題が見つかった場合は、このドキュメントで説明されている戦略と推奨事項を使用して、これらの問題を診断して修正することができます。 また、必要な Api にアクセスするには、新しい [VisualStudio](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) NuGet パッケージをプロジェクトに追加する必要があります。

## <a name="enable-pma"></a>PMA を有効にする

Visual Studio で PMA を有効にするには、次の要件を満たす必要があります。

- Windows 10 April 2018 Update (v1803、RS4) 以降
- .NET Framework 4.8 RTM 以上
- [[ピクセル密度が異なる画面に対して表示を最適化](../../ide/reference/general-environment-options-dialog-box.md)する] オプションが有効になっている Visual Studio 2019

これらの要件が満たされると、Visual Studio によってプロセス全体の PMA モードが自動的に有効になります。

> [!NOTE]
> Visual studio の Windows フォームコンテンツ (プロパティブラウザーなど) は、Visual Studio 2019 バージョン16.1 以降がインストールされている場合にのみ PMA をサポートします。

## <a name="test-your-extensions-for-pma-issues"></a>PMA に関する問題の拡張機能をテストする

Visual Studio は、WPF、Windows フォーム、Win32、および HTML/JS の UI フレームワークを正式にサポートしています。 Visual Studio を PMA モードにすると、各 UI スタックの動作が異なります。 したがって、UI フレームワークに関係なく、すべての UI が PMA モードに準拠していることを確認するためにテストパスを実行することをお勧めします。

次の一般的なシナリオを検証することをお勧めします。

- アプリケーションの実行中に単一の監視環境のスケールファクターを変更する。

  このシナリオは、UI が動的な Windows DPI 変更に応答していることをテストするのに役立ちます。

- 接続されたモニターがプライマリに設定されているラップトップのドッキング/ドッキング解除。接続されているモニターは、アプリケーションの実行中にノート pc とは異なるスケールファクターを持ちます。

  このシナリオでは、UI がディスプレイ DPI の変更に応答していること、および、動的に追加または削除されているディスプレイを処理することをテストできます。

- 異なるスケールファクターを持つ複数のモニターを使用し、それらの間でアプリケーションを移動します。

  このシナリオでは、UI がディスプレイ DPI の変更に応答していることをテストできます。
    
- ローカルコンピューターとリモートコンピューターがプライマリモニターに対して異なるスケールファクターを持つ場合のコンピューターへのリモート処理。

  このシナリオは、UI が動的な Windows DPI 変更に応答していることをテストするのに役立ちます。

UI に問題があるかどうかを確認するには、コードが *VisualStudio*、 *VisualStudio*、 *組み込み vsui:: cdpihelper* の各クラスを使用しているかどうかを確認することをお勧めします。 これらの古い DpiHelper クラスでは、システム DPI 認識のみがサポートされ、プロセスが PMA の場合は常に正しく機能しません。

これらの DpiHelpers の一般的な使用法は次のようになります。

```cs
Point screenTopRight = logicalBounds.TopRight.LogicalToDeviceUnits();

POINT screenIntTopRight = new POINT
{
    x = (int)screenTopRIght.X,
    y = (int)screenTopRIght.Y
}

// Declared via P/Invoke
IntPtr monitor = MonitorFromPoint(screenIntTopRight, MONITOR_DEFAULTTONEARST);
```

前の例では、ウィンドウの論理境界を表す四角形がデバイス単位に変換され、正確なモニターポインターを返すためにデバイス座標を想定しているネイティブメソッド MonitorFromPoint に渡すことができるようになりました。

### <a name="classes-of-issues"></a>問題のクラス
Visual Studio で PMA モードが有効になっている場合、UI ではいくつかの一般的な方法で問題をレプリケートできます。 これらの問題のほとんどは、Visual Studio のサポートされているすべての UI フレームワークで発生する可能性があります。 また、これらの問題は、UI の一部が混合モードの DPI スケーリングシナリオでホストされている場合にも発生することがあります (詳細については、Windows の [ドキュメント](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows) を参照してください)。 

#### <a name="win32-window-creation"></a>Win32 ウィンドウの作成
CreateWindow () または CreateWindowEx () を使用して windows を作成する場合、一般的なパターンは、座標 (0, 0) (プライマリディスプレイの左上隅) にウィンドウを作成してから、最終的な位置に移動することです。 ただし、これを行うと、ウィンドウが DPI 変更メッセージまたはイベントをトリガーする可能性があります。これにより、他の UI メッセージやイベントを再トリガー、最終的には望ましくない動作やレンダリングにつながる可能性があります。

#### <a name="wpf-element-placement"></a>WPF 要素の配置
以前の VisualStudio を使用して WPF 要素を移動する場合、要素が非プライマリ DPI 上にあるときは、左上の座標が正しく計算されないことがあります。

#### <a name="serialization-of-ui-element-sizes-or-positions"></a>UI 要素のサイズまたは位置のシリアル化
UI のサイズまたは位置 (デバイスユニットとして保存されている場合) が、に格納されているものとは異なる DPI コンテキストで復元されると、配置され、サイズが正しく設定されません。 これは、デバイスユニットに固有の DPI 関係があるために発生します。

#### <a name="incorrect-scaling"></a>不適切なスケーリング
プライマリ DPI で作成された UI 要素は正しくスケーリングされますが、別の DPI を使用してディスプレイに移動した場合は、サイズ変更が行われず、コンテンツが大きくなったり小さすぎたりすることはありません。

#### <a name="incorrect-bounding"></a>境界が正しくありません
スケーリングの問題と同様に、UI 要素はプライマリ DPI コンテキスト上で適切に境界を計算しますが、非プライマリ DPI に移行しても、新しい境界は正しく計算されません。 そのため、コンテンツウィンドウが小さすぎるか、ホストしている UI と比較して大きすぎるため、空白またはクリッピングが発生します。

#### <a name="drag--drop"></a>ドラッグ & ドロップ
混合モードの DPI シナリオでは (たとえば、異なる DPI 認識モードでレンダリングする UI 要素が異なる場合)、ドラッグアンドドロップ座標は miscalculated になる可能性があるため、最終的なドロップ位置が正しくなくなります。

#### <a name="out-of-process-ui"></a>アウトプロセス UI
一部の UI はアウトプロセスで作成されます。外部プロセスの作成が Visual Studio とは異なる DPI 認識モードになっている場合は、以前のレンダリングの問題が発生する可能性があります。

#### <a name="windows-forms-controls-images-or-layouts-rendered-incorrectly"></a>正しく表示されないコントロール、画像、またはレイアウトの Windows フォーム
すべての Windows フォームコンテンツが PMA モードをサポートしているわけではありません。 結果として、レイアウトまたはスケーリングが正しくないレンダリングの問題が発生することがあります。 この場合の解決策として、Windows フォームコンテンツを "システム対応" DpiAwarenessContext に明示的に表示することが考えられます (「 [コントロールを特定の DpiAwarenessContext に](#force-a-control-into-a-specific-dpiawarenesscontext)適用する」を参照してください)。

#### <a name="windows-forms-controls-or-windows-not-displaying"></a>Windows フォームコントロールまたはウィンドウが表示されない
この問題の主な原因の1つは、ある DpiAwarenessContext を持つコントロールまたはウィンドウを、別の DpiAwarenessContext を持つウィンドウに親を変更しようとしている開発者です。

次の図は、親ウィンドウでの現在の **既定** の windows オペレーティングシステムの制限を示しています。

![正しい親の動作のスクリーンショット](media/PMA-parenting-behavior.PNG)

> [!Note]
> この動作を変更するには、スレッドのホスト動作を設定します ( [Dpi_Hosting_Behavior 列挙体](/windows/desktop/api/windef/ne-windef-dpi_hosting_behavior)を参照してください)。

その結果、サポートされていないモード間の親子リレーションシップを設定すると、失敗し、コントロールまたはウィンドウが想定どおりにレンダリングされない可能性があります。

### <a name="diagnose-issues"></a>問題の診断

PMA 関連の問題を特定する際には、次のような点を考慮する必要があります。 

- UI または API は論理値またはデバイス値を想定していますか。
    - WPF UI と Api は通常、論理値を使用します (常にではありません)。
    - Win32 UI と Api は通常、デバイスの値を使用します。

- 値はどこから来ていますか。
    - 他の UI または API から値を受け取る場合は、デバイスまたは論理値を渡すことになります。
    - 複数のソースから値を受け取る場合は、同じ種類の値を使用するのか、または変換する必要があるのか、または混在させる必要がありますか。

- UI 定数が使用されているかどうか、どのような形式であるか。

- スレッドが受信している値の正しい DPI コンテキストにあるか。

  混合 DPI ホスティングを有効にするための変更では、通常、適切なコンテキストでコードパスを配置する必要がありますが、メインメッセージループやイベントフローの外部で実行される作業は、間違った DPI コンテキストで実行される可能性があります。

- 値は DPI コンテキストの境界を越えていますか?

  ドラッグ & ドロップは、座標が DPI コンテキストを越える可能性がある一般的な状況です。 ウィンドウは正しい操作を試みますが、場合によっては、ホスト UI が、一致するコンテキスト境界を確保するために変換処理を必要とする場合があります。

### <a name="pma-nuget-package"></a>PMA NuGet パッケージ
新しい DpiAwarness ライブラリは、 [VisualStudio](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) の NuGet パッケージで確認できます。

### <a name="recommended-tools"></a>推奨されるツール
次のツールを使用すると、Visual Studio でサポートされているさまざまな UI スタックで、PMA 関連の問題をデバッグできます。

#### <a name="snoop"></a>捜索
Snoop は、組み込みの Visual Studio XAML ツールにはない追加機能を備えた XAML デバッグツールです。 さらに、Snoop は、Visual Studio をアクティブにデバッグして WPF UI を表示および調整する必要がありません。 Snoop の問題の診断に役立つ2つの主な方法は、論理配置座標またはサイズの境界を検証し、UI に適切な DPI があることを検証することです。
 
#### <a name="visual-studio-xaml-tools"></a>Visual Studio XAML ツール
Snoop と同様に、Visual Studio の XAML ツールは、PMA の問題の診断に役立ちます。 原因が見つかった場合は、ブレークポイントを設定し、[ライブビジュアルツリー] ウィンドウおよびデバッグウィンドウを使用して、UI の境界と現在の DPI を調べることができます。

## <a name="strategies-for-fixing-pma-issues"></a>PMA の問題を修正するための戦略

### <a name="replace-dpihelper-calls"></a>DpiHelper 呼び出しの置換

ほとんどの場合、PMA モードで UI の問題を修正するには、マネージコード内の呼び出しを古い *VisualStudio* クラスと *VisualStudio* クラスに置換し、新しい *VisualStudio* ヘルパークラスの呼び出しを使用するようにすることが一番下になっていることに注意してください。 

```cs
// Remove this kind of use:
Point deviceTopLeft = new Point(window.Left, window.Top).LogicalToDeviceUnits();

// Replace with this use:
Point deviceTopLeft = window.LogicalToDevicePoint(new Point(window.Left, window.Top));
```

ネイティブコードの場合は、古い *組み込み vsui:: CDpiHelper* クラスへの呼び出しを、新しい *組み込み vsui:: cdpihelper* 度クラスの呼び出しに置き換える必要があります。 

```cpp
// Remove this kind of use:
int cx = VsUI::DpiHelper::LogicalToDeviceUnitsX(m_cxS);
int cy = VsUI::DpiHelper::LogicalToDeviceUnitsY(m_cyS);

// Replace with this use:
int cx = m_cxS;
int cy = m_cyS;
VsUI::CDpiAwareness::LogicalToDeviceUnitsX(m_hwnd, &cx);
VsUI::CDpiAwareness::LogicalToDeviceUnitsY(m_hwnd, &cy);
```

新しい DpiAwareness クラスと CDpiAwareness 度クラスは、Dpiawareness クラスと同じ単位変換ヘルパーを提供しますが、追加の入力パラメーターを必要とします。これは、変換操作の参照として使用する UI 要素です。 イメージスケーリングヘルパーは新しい DpiAwareness/CDpiAwareness ヘルパーに存在しないことに注意してください。また、必要な場合は、代わりに [Imageservice](../image-service-and-catalog.md) を使用する必要があります。

マネージ DpiAwareness クラスは、WPF ビジュアル、Windows フォームコントロール、Win32 Hwnd および HMONITORs (両方の形式の IntPtrs) のヘルパーを提供します。一方、ネイティブ CDpiAwareness クラスは、HWND および HMONITORS ヘルパーを提供します。

### <a name="windows-forms-dialogs-windows-or-controls-displayed-in-the-wrong-dpiawarenesscontext"></a>間違った DpiAwarenessContext に表示されるダイアログ、ウィンドウ、またはコントロールの Windows フォーム
異なる DpiAwarenessContexts を使用して (Windows の既定の動作によって) windows の親を正常に設定した後でも、ユーザーには、異なる DpiAwarenessContexts scale の異なるウィンドウとしてスケーリングの問題が表示されることがあります。 その結果、UI でのテキストの配置や画像の問題がユーザーに表示される可能性があります。

この問題を解決するには、アプリケーションのすべてのウィンドウとコントロールに適切な DpiAwarenessContext スコープを設定します。

### <a name="top-level-mixed-mode-tlmm-dialogs"></a>トップレベル混合モード (TLMM) ダイアログ
モーダルダイアログなどの最上位レベルのウィンドウを作成するときは、スレッドが作成されるウィンドウ (およびそのハンドル) の前に、スレッドが正しい状態であることを確認することが重要です。 このスレッドは、ネイティブの CDpiScope ヘルパーまたはマネージドの DpiAwareness を使用して、システム認識にすることができます。 (TLMM は、一般に非 WPF ダイアログ/ウィンドウで使用する必要があります)。

### <a name="child-level-mixed-mode-clmm"></a>子レベル混在モード (CLMM)
既定では、子ウィンドウは、親を指定せずに作成された場合は現在のスレッド DPI 認識コンテキストを受け取り、親を使用して作成された場合は、親の DPI 認識コンテキストを受け取ります。 親とは異なる DPI 認識コンテキストを持つ子を作成するには、そのスレッドを目的の DPI 認識コンテキストに配置できます。 次に、親を使用せずに子を作成し、手動で親ウィンドウに親ことができます。

#### <a name="clmm-issues"></a>CLMM の問題
メインのメッセージングループやイベントチェーンの一部として発生する UI 計算作業のほとんどは、適切な DPI 認識コンテキストで既に実行されている必要があります。 ただし、このようなメインワークフローの外部 (アイドル時間タスク中、UI スレッドの停止時など) に計算が行われた場合は、現在の DPI 認識コンテキストが間違って UI misplacement や誤ったサイズ設定の問題につながる可能性があります。 UI 作業のための適切な状態にスレッドを配置すると、一般的に問題が解決されます。
 
#### <a name="opt-out-of-clmm"></a>CLMM からオプトアウト
WPF 以外のツールウィンドウが PMA を完全にサポートするように移行されている場合は、CLMM からオプトアウトする必要があります。 これを行うには、IVsDpiAware という新しいインターフェイスを実装する必要があります。

```cs
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IVsDpiAware
{
    [ComAliasName("Microsoft.VisualStudio.Shell.Interop.VSDPIMode")]
    uint Mode {get;}
}
```

```cpp
IVsDpiAware : public IUnknown
{
    public:
        HRRESULT STDMETHODCALLTYPE get_Mode(__RCP__out VSDPIMODE *dwMode);
};
```

マネージ言語では、このインターフェイスを実装するための最適な場所は、 *VisualStudio*から派生したクラスと同じクラスです。 C++ の場合、このインターフェイスを実装する最適な場所は、vsshell から *IVsWindowPane* を実装するクラスと同じです。

インターフェイスの Mode プロパティによって返される値は __VSDPIMODE であり、マネージの uint にキャストされます。

```cs
enum __VSDPIMODE
{
    VSDM_Unaware    = 0x01,
    VSDM_System     = 0x02,
    VSDM_PerMonitor = 0x03,
}
```

- 非認識とは、ツールウィンドウが 96 DPI を処理する必要があることを意味します。 Windows は、他のすべてのファイルのスケーリングを処理します。 結果として、コンテンツが少しぼやけて表示されます。
- システムとは、ツールウィンドウがプライマリディスプレイ DPI の DPI を処理する必要があることを意味します。 DPI が一致するすべてのディスプレイは鮮明に見えますが、DPI が異なる場合やセッション中に変更された場合は、Windows によってスケーリングが処理され、若干ぼやけて表示されます。
- PerMonitor は、ツールウィンドウがすべてのディスプレイで、DPI が変更されたときにすべてのを処理する必要があることを意味します。

> [!NOTE]
> Visual Studio では PerMonitorV2 認識のみがサポートされているため、PerMonitor 列挙値は DPI_AWARENESS_CONTEXT_PER_MONITOR_AWARE_V2 の Windows 値に変換されます。

#### <a name="force-a-control-into-a-specific-dpiawarenesscontext"></a>コントロールを特定の DpiAwarenessContext に強制的に適用する

PMA モードをサポートするように更新されていないレガシ UI でも、Visual Studio が PMA モードで実行されている間は、小さな修正が必要になる場合があります。 このような修正の1つは、正しい DpiAwarenessContext で UI が作成されていることを確認することです。 UI を特定の DpiAwarenessContext に強制的に適用するには、次のコードを使用して DPI スコープを入力します。

```cs
using (DpiAwareness.EnterDpiScope(DpiAwarenessContext.SystemAware))
{
    Form form = new MyForm();
    form.ShowDialog();
}
```

```cpp
void MyClass::ShowDialog()
{
    VsUI::CDpiScope dpiScope(DPI_AWARENESS_CONTEXT_SYSTEM_AWARE);
    HWND hwnd = ::CreateWindow(...);
}
```

> [!NOTE]
> DpiAwarenessContext の強制は、WPF 以外の UI および最上位の WPF ダイアログでのみ機能します。 ツールウィンドウまたはデザイナー内でホストされる WPF UI を作成する場合、コンテンツが WPF UI ツリーに挿入されるとすぐに、現在のプロセス DpiAwarenessContext に変換されます。

## <a name="known-issues"></a>既知の問題

### <a name="windows-forms"></a>Windows フォーム

新しい混合モードのシナリオに合わせて最適化するために、Windows フォーム、親が明示的に設定されていないときにコントロールとウィンドウを作成する方法が変更されました。 以前は、明示的な親を持たないコントロールは、作成されるコントロールまたはウィンドウの一時的な親として内部 "駐車ウィンドウ" を使用していました。 

.NET 4.8 より前の場合、ウィンドウの作成時に現在のスレッド DPI 認識コンテキストから DpiAwarenessContext を取得する "パーキングウィンドウ" が1つありました。 コントロールのハンドルが作成されると、親でないコントロールは、そのコントロールのハンドルが作成されたときに駐機ウィンドウと同じ DpiAwarenessContext を継承し、アプリケーション開発者によって最終的な親または予期される親に親されます。 これにより、"パーキングウィンドウ" の DpiAwarenessContext が最終的な親ウィンドウよりも大きい場合に、タイミングに基づくエラーが発生します。

.NET 4.8 の時点で、検出されたすべての DpiAwarenessContext に対して "駐車ウィンドウ" があります。 もう1つの大きな違いは、コントロールに使用される DpiAwarenessContext は、コントロールが作成されるときではなく、コントロールの作成時にキャッシュされることです。 つまり、全体的な終了動作は同じですが、時間ベースの問題として使用されているものを一貫性のある問題に変えることができます。 また、UI コードを記述して適切にスコープを設定するために、アプリケーション開発者により決定的な動作を提供します。
