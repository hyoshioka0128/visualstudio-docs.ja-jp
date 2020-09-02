---
title: Visual Studio の UX Essentials |Microsoft Docs
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6c329eda477d77ab73be2ad913ac18d67ff3c08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698339"
---
# <a name="ux-essentials-for-visual-studio"></a>UX Essentials for Visual Studio

## <a name="best-practices"></a>ベスト プラクティス

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. Visual Studio 環境内で一貫している。

- シェル内の既存の [相互作用パターン](interaction-patterns-for-visual-studio.md) に従います。

- シェルのビジュアル言語と [職人気質の要件](evaluation-tools-for-visual-studio.md)に合わせて機能を設計します。

- 共有コマンドとコントロールが存在する場合は、それらを使用します。

- Visual Studio の階層と、それによってコンテキストがどのように確立され、UI が駆動されるかを理解します。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. フォントおよび色に対して環境サービスを使用します。

- UI では、[オプション] ダイアログボックスの [フォントおよび色] ページでカスタマイズのために公開されていない限り、現在の [環境のフォント](fonts-and-formatting-for-visual-studio.md) 設定を考慮する必要があります。

- UI 要素は、共有環境トークンまたは機能固有のトークンを使用して、 [Vscolor サービス](colors-and-styling-for-visual-studio.md)を使用する必要があります。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. すべての画像が新しい VS スタイルと一致するようにします。

- アイコン、グリフ、およびその他のグラフィックスについては、Visual Studio のデザイン原則に従ってください。

- テキストをグラフィック要素に配置しないでください。

### <a name="4-design-from-a-user-centric-perspective"></a>4. ユーザー中心の観点からデザインします。

- タスクフローは、その中の個々の機能の前に作成します。

- ユーザーについて理解し、仕様でその知識を明示的に設定してください。

- UI を確認するときは、完全なエクスペリエンスと詳細を評価します。

- ロケールや言語に関係なく機能し、魅力的な状態になるように UI を設計します。

## <a name="screen-resolution"></a>画面解像度

### <a name="minimum-resolution"></a>最小解像度

- Visual Studio 2015 の最小解像度は **1280 0x720**です。 これは、この解像度で Visual Studio を *使用できること* を意味しますが、ユーザーエクスペリエンスが最適ではない可能性があります。 すべての側面が 1280 0x720 より低い解像度で使用できるという保証はありません。

- Visual Studio のターゲットの解像度は **1366x768**です。 これは、 *優れ* たユーザーエクスペリエンスを保証する最も低い解決策です。

- 初期ダイアログの高さは **700 ピクセル未満**にする必要があるため、IDE フレームの最小解像度 (96 dpi) 内に収まるようにしてください。

### <a name="high-density-displays"></a>高密度ディスプレイ
 Visual Studio の UI は、Windows が既定でサポートしているすべての DPI スケールファクター (150%、200%、250%) で適切に動作する必要があります。

## <a name="anti-patterns"></a>アンチパターン
 Visual Studio には、ガイドラインとベストプラクティスに従う UI の例が多数含まれています。 一貫性を保つために、開発者は多くの場合、ビルドしているものと同様の製品 UI デザインパターンを借用します。 これはユーザーの操作や視覚設計の一貫性を向上させるのに役立ちますが、スケジュールの制約や欠陥の優先順位付けのためのガイドラインに合わない詳細情報を含む機能を提供します。 このような場合、チームはこれらの "アンチパターン" のいずれかをコピーしないようにする必要があります。これは、Visual Studio 環境内の不適切な UI または一貫性のない UI が急増するためです。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>既定でエラー状態に表示される必須フィールド/設定

#### <a name="feature-team-goals"></a>機能チームの目標

- 構成する必要がある要素が追加されたことをユーザーに警告します。

- 入力が必要な領域にユーザーの注意を促します。

#### <a name="anti-pattern-solution"></a>アンチパターンソリューション
 ユーザーが操作を開始してタスクを完了する前に、直ちに、構成が必要な領域の横に重大な停止アイコンを配置します。

#### <a name="example-manifest-designer-declarations"></a>例: マニフェストデザイナーの宣言
 リストに宣言を追加すると、直ちにエラー状態になります。これは、ユーザーが必要なプロパティを設定するまで保持されます。

 この場合、アラートに使用されるアイコンに "" アイコンが含まれているため、追加の問題が発生し &times; ます。そのため、共通の [削除] アイコンを横に使用することはできません。 その結果、UI では、[削除] ボタンを使用して、さらに clunky な制御を行うことができます。

 ![既定で UI をエラー状態にすることは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti-パターン")<br />既定で UI をエラー状態にすることは、Visual Studio のアンチパターンです。

#### <a name="alternatives"></a>代替

この問題を解決するには、次の方法が適しています。

- ユーザーが警告なしで宣言を追加し、すぐに項目のプロパティを設定できるようにします。

- リストに別の宣言を追加したり、デザイナー内のタブを変更したりするなど、項目からフォーカスが移動したときに警告アイコン (金色の三角形) を追加します。

- 宣言のプロパティを設定する前にユーザーがタブを変更しようとすると、警告が解決されるまで、アプリケーションがビルドされない (または影響がある) ことを示すダイアログが表示されます。 ユーザーがダイアログを閉じてタブを変更した場合は、必要に応じてアイコン (重大または警告) が [宣言] タブに追加されます。

### <a name="multiple-clicks-to-dismiss-ui"></a>UI を閉じるための複数のクリック

#### <a name="feature-team-goals"></a>機能チームの目標
 ユーザーは、最初に説明テキストを表示せずに UI を閉じることを許可しないでください。

#### <a name="anti-pattern"></a>アンチパターン
 VS UI 内のさまざまな場所にビデオリンクを挿入するチームは、 &times; UX によって指定された "" 閉じるボタンとツールヒントの説明 "の一般的なパターンと、代わりにドロップダウンと" 今後表示しない "リンクを実装しました。

#### <a name="example-video-links-in-team-explorer"></a>例: チームエクスプローラーのビデオリンク
UI を閉じる前に、ユーザーが説明テキストを強制的に読み取ることは、Visual Studio 内のアンチパターンです。 適切に設計されたビデオリンクには、ホバー時の追加情報を示すツールヒントが表示されます。また、"" をクリックすると、 &times; 詳細な操作を必要とせずにメッセージを閉じる必要があります。

 ![説明テキストのアンチ&#45;パターン &#45; 正しくありません](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />ビデオリンクパターンが正しくありません

ユーザーは、単純な [閉じる] ボタン (ワンクリック) ではなく、2回のクリックを使用して、ビデオリンクが表示されるすべての場所で UI を閉じるだけです。

この状況に適した設計は、Internet Explorer、Office、および Visual Studio の一般的なパターンに従うことです。ホバー時には、ユーザーがツールヒントの説明を表示し、ワンクリックで UI を非表示にすることができます。

 ![説明テキストアンチ&#45;パターン &#45; 正しい](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-正しい")<br />正しいビデオリンクパターン

### <a name="using-command-bars-for-settings"></a>設定用のコマンドバーの使用

**図 A** は、このアンチパターンを表します。コマンドだけではなく、コマンドボタンの下に設定を配置します。 このスケッチでは、[デバッグの開始] 以外のコマンド (ブラウザーでの表示、[デバッグなしで開始]、[ステップイン] など) が選択されています。これは選択した設定に従います。

![図 A: コマンドバーのアンチパターン](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-FigureA")<br />図 A: コマンドバーのアンチパターン

少し良くなりますが、それでも望ましくありませんが、 **図 B**に示すように、ツールバーにこの種類の設定を配置します。分割ボタンでは領域が小さくなりますが、ドロップダウンに対する改善点がありますが、どちらのデザインでも、実際にはコマンドではないものを昇格するツールバーが使用されています。

![図 B: 高度なコマンドバーのアンチパターン](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-FigureB")<br />図 B: 高度なコマンドバーのアンチパターン

**図 C**に示されている正しい方法では、設定は一連のコマンドに関連付けられています。 グローバル設定が設定されておらず、4つのコマンドのみを切り替えています。 これは、ツールバーのコマンドが許容される唯一の状況です。

![図 C: Visual Studio のコマンドバーパターンの適切な使用](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-FigureC")<br />図 C: Visual Studio のコマンドバーパターンの適切な使用

### <a name="control-anti-patterns"></a>アンチパターンの制御
 アンチパターンには、単にコントロールまたはコントロールのグループの不適切な使用やプレゼンテーションがあります。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>ハイパーリンクではなくグループラベルとして使用される下線
 下線テキストはハイパーリンクに対してのみ使用してください。

 **不良**\
 ![ハイパーリンク以外の下線付きテキストは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />ハイパーリンク以外の下線付きテキストは、Visual Studio のアンチパターンです。

 **よし：**\
 ![正しく表示されていないハイパーリンク以外のテキストは、環境のフォントで非修飾表示されます。](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />正しく表示されていないハイパーリンク以外のテキストは、環境のフォントで非修飾表示されます。

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>チェックボックスをクリックすると、ポップアップダイアログが表示される
 [Windows Azure アプリケーションの発行] ウィザードで [すべてのロールのリモートデスクトップを有効にする] チェックボックスをオンにすると、すぐにポップアップダイアログが表示され、Visual Studio のアンチパターンが表示されます。 また、チェックボックスのフィールドは、選択された後のチェックボックス、もう1つの相互作用アンチパターンには含まれません。

 ![チェックボックスをクリックした後にダイアログを表示することは、Visual Studio のアンチパターンです。](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />チェックボックスをクリックした後にダイアログを表示することは、Visual Studio のアンチパターンです。

### <a name="hyperlink-anti-patterns"></a>ハイパーリンクのアンチ パターン
 次の例には、2つのアンチパターンが含まれています。

1. ホバー時の前景色が赤の場合は、フォントサービスからの正しい共有色が使用されていないことを意味します。

2. 概念的なトピックへのリンクについては、「詳細情報」を参照してください。 ユーザーの目標は、さらに学習することではなく、選択した場合の影響を理解することです。

   ![Color サービスを無視し、ハイパーリンクの [詳細情報] を使用すると、Visual Studio のアンチパターンになります。](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />Color サービスを無視し、ハイパーリンクの [詳細情報] を使用すると、Visual Studio のアンチパターンになります。

**より優れたソリューション:** リンクをクリックして、ユーザーが質問する質問をします。 次に例を示します。

- Windows Azure サービスのしくみ

- Windows Azure Mobile Services プロジェクトはどのような場合に必要ですか。

#### <a name="using-click-here-for-links"></a>リンクに対して "ここをクリック" を使用する
 ハイパーリンクは自己記述型である必要があります。 "ここをクリック" または同様のバリエーションを使用するアンチパターンです。

 **無効:** "新しいプロジェクトを作成する手順については、ここをクリックしてください。"

 **いいですね。** "新しいプロジェクトを作成操作方法ますか?"
