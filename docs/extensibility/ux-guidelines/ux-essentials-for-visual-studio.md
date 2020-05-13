---
title: ビジュアルスタジオのUXの必需品 |マイクロソフトドキュメント
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6c329eda477d77ab73be2ad913ac18d67ff3c08
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80698339"
---
# <a name="ux-essentials-for-visual-studio"></a>UX Essentials for Visual Studio

## <a name="best-practices"></a>ベスト プラクティス

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. Visual Studio 環境内で一貫性を保つ。

- シェル内の既存の[相互作用パターン](interaction-patterns-for-visual-studio.md)に従います。

- シェルのビジュアル言語と職人技の要件に合わせて設計[機能](evaluation-tools-for-visual-studio.md)。

- 共有コマンドと共有コントロールが存在する場合は、そのコマンドとコントロールを使用します。

- Visual Studio の階層と、コンテキストを確立して UI を駆動する方法について理解する。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. フォントと色に環境サービスを使用します。

- UI は、[オプション] ダイアログの [フォントと色] ページでカスタマイズ用に公開されていない限り、現在の[環境](fonts-and-formatting-for-visual-studio.md)フォント設定を尊重する必要があります。

- UI 要素は、共有環境トークンまたは機能固有のトークンを使用して[VSColor サービス](colors-and-styling-for-visual-studio.md)を使用する必要があります。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. すべての画像を新しい VS スタイルと一致させます。

- アイコン、グリフ、その他のグラフィックスに関する Visual Studio のデザインの原則に従います。

- グラフィック要素にテキストを配置しないでください。

### <a name="4-design-from-a-user-centric-perspective"></a>4. ユーザー中心の視点から設計する。

- タスク フローは、その中の個々の機能の前に作成します。

- ユーザーに精通し、その知識を仕様に明示してください。

- UI を確認する際は、完全なエクスペリエンスと詳細を評価します。

- ロケールや言語に関係なく、UI が機能し、魅力的な状態に保たるように UI を設計します。

## <a name="screen-resolution"></a>画面解像度

### <a name="minimum-resolution"></a>最小解像度

- Visual Studio 2015 の最小解像度は**1280x720**です。 つまり、この解像度では Visual Studio を使用*できますが*、最適なユーザー エクスペリエンスではない可能性があります。 1280x720 より低い解像度ですべての側面が使用できる保証はありません。

- Visual Studio のターゲット解像度は**1366x768**です。 これは、*優*れたユーザー エクスペリエンスを約束する最低の解像度です。

- ダイアログの最初の高さは**700 ピクセルより小さく**する必要があります。

### <a name="high-density-displays"></a>高密度ディスプレイ
 Visual Studio の UI は、Windows がサポートするすべての DPI スケール ファクターで適切に動作する必要があります: 150%、200%、および 250% です。

## <a name="anti-patterns"></a>反パターン
 Visual Studio には、ガイドラインとベスト プラクティスに従う UI の例が多数用意されています。 開発者は、一貫性を保つために、構築しているものと同様の製品 UI 設計パターンを利用することがよくあります。 これはユーザー操作とビジュアル デザインの一貫性を促進するのに役立つ優れたアプローチですが、スケジュールの制約や欠陥の優先順位付けのためにガイドラインを満たしていないいくつかの詳細を含む、いくつかの詳細を含む場合があります。 このような場合、チームは Visual Studio 環境内で不適切な UI または一貫性のない UI が増殖するため、これらの "アンチパターン" の 1 つをコピーすることは望ましくありません。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>既定でエラー状態で表示される必須フィールド/設定

#### <a name="feature-team-goals"></a>機能チームの目標

- 構成する必要のある要素が追加されたことをユーザーに警告します。

- 入力が必要な領域にユーザーの注意を引きます。

#### <a name="anti-pattern-solution"></a>アンチパターンソリューション
 ユーザーがアクションを開始し、タスクを完了する前に、直ちに構成が必要な領域の横にクリティカル ストップ アイコンを配置します。

#### <a name="example-manifest-designer-declarations"></a>例: マニフェスト デザイナーの宣言
 宣言をリストに追加すると、すぐにエラー状態になります。

 この場合、アラートに使用されるアイコンには " " アイコン&times;が含まれているため、その横に共通の削除アイコンを使用できないため、さらに懸念があります。 その結果、UI は削除ボタンを使用します。

 ![既定で UI をエラー状態に設定するのは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "マニフェストデザイナー エラー宣言anti-pattern")<br />既定で UI をエラー状態に設定するのは、Visual Studio のアンチパターンです。

#### <a name="alternatives"></a>代替

この問題に対するより良い解決策は、次のとおりです。

- ユーザーが警告なしに宣言を追加し、項目のプロパティを設定するためにすぐに移動できるようにします。

- リストに別の宣言を追加したり、デザイナー内のタブを変更したりするなど、項目からフォーカスが移動したときに警告アイコン (ゴールドの三角形) を追加します。

- 宣言のプロパティを設定する前にユーザーがタブを変更しようとすると、警告が解決されるまでアプリケーションがビルドされないこと (または、その影響を含む) ことを説明するダイアログボックスをポップします。 ユーザーがダイアログを閉じてタブを変更した場合は、アイコン (重要または警告) が [宣言] タブに追加されます。

### <a name="multiple-clicks-to-dismiss-ui"></a>複数のクリックで UI を閉じる

#### <a name="feature-team-goals"></a>機能チームの目標
 説明テキストを最初に表示せずに、ユーザーが UI を閉じるようにしないでください。

#### <a name="anti-pattern"></a>アンチパターン
 VS UI 内のさまざまな場所にビデオ リンクを挿入するチームは、UX で指定された&times;"閉じるボタンとツールヒントの説明" の一般的なパターンに対して決定し、代わりにドロップダウンと "再表示しない" リンクを実装しました。

#### <a name="example-video-links-in-team-explorer"></a>例: チーム エクスプローラーでのビデオ リンク
UI を閉じる前に説明文を読み取るようにユーザーに強制することは、Visual Studio 内の反パターンです。 正しくデザインされたビデオ リンクには、ホバーに関する追加情報を含むツール&times;ヒントが表示され、"" をクリックすると、それ以上の操作が必要なくメッセージが閉じられます。

 ![説明テキストアンチ&#45;パターン&#45;正しくありません](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "複数クリックの誤用")<br />ビデオ リンク パターンが正しくありません

単純な閉じるボタン (1 回のクリック) の代わりに、ユーザーは 2 回のクリックを使用して、ビデオ リンクが表示される場所ごとに UI を閉じるだけです。

この状況の正しい設計は、Internet Explorer、Office、および Visual Studio に共通するパターンに従う方法です。

 ![説明テキストアンチ&#45;パターン&#45;正しい](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "説明テキストの反パターン正しい")<br />ビデオリンクパターンを修正する

### <a name="using-command-bars-for-settings"></a>設定にコマンド バーを使用する

**図 A は**、コマンド以外のコマンド ボタンの下に設定を置くというアンチパターンを表しています。 このスケッチでは、選択した設定を考慮するコマンド (ブラウザーでの表示、デバッグなしで開始、ステップ インなど) のデバッグの開始以外にもコマンドがあります。

![図 A: コマンド バーのアンチパターン](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "コマンドバランティパターン図A")<br />図 A: コマンド バーのアンチパターン

少し良いが、まだ望ましくない、**図 B**に示すように、ツールバーにこの種類の設定を配置しています。分割ボタンのスペースが少ないため、ドロップダウンを改善できますが、どちらのデザインもツールバーを使用して実際にはコマンドではないものを宣伝しています。

![図B:より良いが、まだコマンドバーのアンチパターン](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "コマンドバランティパターン図B")<br />図B:より良いが、まだコマンドバーのアンチパターン

**図 C**に示す正しい方法では、設定は一連のコマンドに関連付けられています。 グローバル設定が設定されていないので、4 つのコマンドを切り替えるだけです。 これは、ツールバーのコマンドが受け入れられる唯一の状況です。

![図 C: Visual Studio コマンド バー パターンの正しい使用](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "コマンドバランティパターン図C")<br />図 C: Visual Studio コマンド バー パターンの正しい使用

### <a name="control-anti-patterns"></a>アンチパターンの制御
 一部のアンチパターンは、単にコントロールまたはコントロールのグループの不適切な使用方法または表示です。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>ハイパーリンクではなく、グループ ラベルとして使用される下線
 下線付きテキストは、ハイパーリンクにのみ使用してください。

 **悪い：**\
 ![ハイパーリンクではない下線付きのテキストは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />ハイパーリンクではない下線付きのテキストは、Visual Studio のアンチパターンです。

 **よし：**\
 ![正しくスタイルが設定されている場合、ハイパーリンクのないテキストは環境フォントで飾られていない形で表示されます。](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />正しくスタイルが設定されている場合、ハイパーリンクのないテキストは環境フォントで飾られていない形で表示されます。

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>チェック ボックスをクリックするとポップアップ ダイアログが表示されます。
 「Windows Azure アプリケーションの発行」ウィザードの [すべてのロールに対してリモート デスクトップを有効にする] チェック ボックスをオンにすると、すぐにポップアップ ダイアログが表示されます。 さらに、チェック ボックス フィールドは、選択された後にチェック ボックスが塗りつぶされません。別の相互作用アンチパターン。

 ![チェック ボックスをクリックした後でダイアログを表示するのは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />チェック ボックスをクリックした後でダイアログを表示するのは、Visual Studio のアンチパターンです。

### <a name="hyperlink-anti-patterns"></a>ハイパーリンクのアンチ パターン
 次の例には、2 つのアンチパターンが含まれています。

1. フォアグラウンドがホバー時に赤に変わった場合、フォント サービスの正しい共有色が使用されていません。

2. 「詳細」は、概念トピックへのリンクに適したテキストではありません。 ユーザーの目標は、より多くを学ぶことではなく、自分の選択の影響を理解することです。

   ![カラー サービスを無視し、ハイパーリンクに対して "詳細を参照する" を使用する場合は、Visual Studio のアンチパターンが使用されます。](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />カラー サービスを無視し、ハイパーリンクに対して "詳細を参照する" を使用する場合は、Visual Studio のアンチパターンが使用されます。

**より良いソリューション:** ユーザーがリンクをクリックして質問をする。 次に例を示します。

- Windows Azure サービスはどのように機能しますか?

- Windows Azure モバイル サービス プロジェクトが必要な場合

#### <a name="using-click-here-for-links"></a>リンクに「ここをクリック」を使用する
 ハイパーリンクは、自己記述的にする必要があります。 「ここをクリック」または同様のバリエーションを使用するのはアンチパターンです。

 **悪い:**「新しいプロジェクトの作成方法については、ここをクリックしてください。

 **良い:**「新しいプロジェクトを作成する方法は?
