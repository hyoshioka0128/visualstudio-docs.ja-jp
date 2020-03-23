---
title: ビジュアル スタジオの UI テキストとヘルプ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c0477a0e1994e9c3b94df13ace4c1f3b4df51039
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301537"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Visual Studio の UI テキストとヘルプ
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a>UI テキストと用語
 理解しやすいテキストは、効果的な UI にとって重要です。 ソフトウェアユーザーは、最初にラベルを読む傾向があります, すなわち、手元のタスクを完了するために最も関連性の高いもの. 静的テキストは、より少ない頻度で読み取られます。 ユーザーがウィンドウ全体をすばやくスキャンして作業セッションを開始し、次のおおよその順序で UI を読み取るように計画します。

1. 中央のインタラクティブコントロール

2. コミットボタン

3. 他の場所で見つかったインタラクティブコントロール

4. 主な説明書

5. 補足説明

6. ウィンドウのタイトル

7. 本文内のその他の静的テキスト

### <a name="usage-patterns-for-ui-text"></a>UI テキストの使用パターン

#### <a name="title-bar-text"></a>タイトル バーの文字列
 タイトル バーのテキストは、UI を生成したコマンドと一致する必要があります。

#### <a name="instructional-text-helper-text"></a>説明テキスト (ヘルパー テキスト)
 ダイアログボックスによっては、ウィンドウまたはページで何をすべきかを説明する主要な指示を提供すると便利です。 これは"ヘルパー テキスト" と呼ばれることもあります。

##### <a name="writing-style-rules-for-helper-text"></a>ヘルパー テキストのスタイル ルールを記述する

- 明白な説明をしないでください。 絶対に必要でない限り、説明文を含まないでください。

- 説明テキストは、常にダイアログの上部に配置され、実行されるタスクを参照する必要があります。

- ユーザーに対して、何をする必要があるかを正確に説明します。 過度の通信と冗長性を避けます。

- 各ウィンドウを確認し、重複する単語や文を削除します。

- 説明テキストを短くします。 特定のユーザーまたはシナリオに関して詳細な情報が必要な場合は、詳細な概念オンライン トピックへのリンクを提供します。

- すべての単語が重みを保持し、必要なように、あなたのテキストを書きます。

- [ユーザー インターフェイス テキスト](/windows/desktop/uxguide/text-ui)と[スタイルとトーン](/windows/desktop/uxguide/text-style-tone)に関する既存の Microsoft ガイダンスに従ってください。

#### <a name="supplemental-instructions"></a>補足説明書
 補足説明書では、ユーザーがコントロールまたはコントロールのグループ化を理解するのに役立つ追加情報を提供します。 入力コントロールがどの形式を想定しているのかを理解するために必要なヒント テキストも含まれます。 補足の指示を控えめに使用してください。 ユーザーが選択の影響を十分に理解していない可能性がある場合に備え、それらを予約します。

 ![Visual Studio での補足のテキスト](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Visual Studio での補足のテキスト**

 ![Visual Studio での補足のテキスト](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Visual Studio での補足のテキスト**

#### <a name="infotips"></a>ヒント
 多くの場合、説明テキストは UI 内のインプレースに配置するには時間がかかりすぎるか、新しいユーザーにのみ役立つ可能性があります。 この場合、説明テキスト/情報テキストはヒントの下にツールチップとして配置する必要があります。

 ヒントは、関連するコントロールの近くに配置する必要があり、目立たないが目立つ特定の情報ヒント アイコンを使用する必要があります。

 ![Visual Studio でのヒント](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **ビジュアル スタジオの情報ヒントの例**

##### <a name="writing-style-rules-for-infotips"></a>ヒントのスタイル ルールの作成

- ヒントを完全な文章として書く。 特定の動詞、文の大文字と小文字、および句読点の終了が必要です。

- ヒントを使用して、主な指示や情報を補足します。 異なる単語を使用してメインのアイデアを書き直すだけの場合は、情報ヒントは必要ありません。

- ヒントを短く、甘く保ちます。 ユーザーをサポートし、奨励する小さな単語と平易な日常の言語を使用します。

- [ユーザー インターフェイス テキスト](/windows/desktop/uxguide/text-ui)と[スタイルとトーン](/windows/desktop/uxguide/text-style-tone)に関する既存の Microsoft ガイダンスに従ってください。

#### <a name="control-labels"></a>コントロールラベル
 コントロール ラベルは短く簡潔にし[、Windows デスクトップのコントロールガイダンスに従う](/windows/desktop/uxguide/controls)必要があります。

 コントロール ラベルの形式と UI 内での配置の詳細については、「 [Visual Studio のレイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md)」を参照してください。

#### <a name="help-links"></a>[ヘルプ] リンク
 ヘルプ リンクは、説明テキスト内または UI の本文に配置できます。 ヘルプへのリンクを使用したり、内部ダイアログを起動したりできます。

##### <a name="visual-style-rules-for-help-links"></a>ヘルプ リンクの表示スタイルルール

- ハイパーリンクに適切な環境色を使用します。 適切なスタイルのハイパーリンクをクリックしても、一時的に赤く点滅しません。 これが表示される場合は、環境の色が使用されていないということを示します。

- 下線は、ホバー時またはリンクが段落に埋め込まれている場合にのみ使用してください。

- ハイパーリンクのビジュアル スタイルと対話スタイルの詳細については、「ボタンとハイパーリンク」を参照してください。

##### <a name="writing-style-rules-for-help-links"></a>ヘルプ リンクのスタイル ルールの作成

- ダイアログを起動する場合は、省略記号の標準を維持します: ナビゲーション用の省略記号なし、タスクに追加の UI が必要な場合は省略記号を使用します。

     ![Visual Studio でのヘルプ リンク](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **ヘルプ リンクの省略記号 (..) は、タスクに追加の UI が必要であることを示します。**

- リンクはユーザーの意図ではないため、"Learn" で始めないようにしてください。 ユーザーは、一般教育を受け取らずに、特定の質問に答えたいと考えています。

- トピックが回答する質問を表示するように、ヘルプ リンクをフレーズにします。

     間違っている: "Windows Azure モバイル サービスの料金の詳細を参照してください。

     正しい: "Windows Azure モバイル サービスで使用できる価格オプションは何ですか?

- リンク テキストに*Click...* を使用しないでください。

- 「ここに」という言葉だけをリンクしないでください。 これは、ハイパーリンクされた単語だけを音声で表示するスクリーン リーダーの中には問題があります。

     間違っている: "Windows Azure モバイル サービスに関する情報**はこちらから検索する**"

     正しい: "Windows Azure モバイル サービスで使用できる価格オプションは何ですか?

- ヘルプ リンクの正しい書き方の詳細については[、Windows デスクトップのヘルプを](/windows/desktop/uxguide/winenv-help)参照してください。

#### <a name="hint-text"></a>ヒントテキスト
 ヒント テキストは、コントロール内またはコントロールの下にウォーターマークとして表示されます。 適切な VSColors トークン`Environment.GrayText`を使用して、正しい書式が適用されます。

 これは、いくつかのフォームで表示できます。

- コントロール ラベルの代わりに:

     ![Visual Studio でのヒント テキスト](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- 動詞で、指示を与える:

     ![Visual Studio でのヒント テキスト](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- 必須エントリを示すテキスト:

     ![Visual Studio でのヒント テキスト](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>透かしテキスト
 空のデザイン サーフェイスでは、テキストは、必要に応じて、他の関連するウィンドウを開くリンクを提供するだけでなく、何をすべきかを示す必要があります。

 ![Visual Studio でのウォーターマーク テキスト](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **ビジュアル スタジオの透かしテキストの例**

### <a name="common-terminology"></a>一般的な用語

|期間|説明|解説|
|----------|-----------------|-------------|
|サインイン/サインアウト|動詞は、Web プロパティへの認証を表す目的で、Web と同義に使用されます。 クライアント内では、この概念を IDE ユーザー接続のサインインとアウトの最上位の概念として使用します。|IDE ユーザーは、最上位レベルの IDE ユーザーを表すため、サインイン/サインアウトの動詞を表す唯一の機能です。|
|接続/切断|機能がオンライン サービスへの単一の接続を維持する場所で使用します。|サーバー エクスプローラーは、一度に 1 つのアクティブな Azure 接続しか持てなさないもので、接続/切断の例です。|
|追加/削除|非破壊的。 リストに対して何かを追加または削除するときに使用します。|TFS 接続マネージャーサーバーの一覧ダイアログは、追加と削除の例です。|
|削除|破壊。 削除する要素がディスクから完全に破棄または削除される場合にのみ使用します。|「削除」は、結果がディスクからファイルを削除する場合、一般にプロンプトを必要とします。|

## <a name="error-messages"></a>エラー メッセージ

### <a name="overview"></a>概要
 エラーが発生します。 ユーザーができることに制限を設定することは、回避可能なエラー メッセージを防ぐための賢明な第一歩です。 ただし、エラーが発生した場合、適切に記述されたエラー メッセージは、問題の軽減に大いに取り組むことができます。 エラー メッセージは、同期的であり、解決する必要がある問題を示すため、ユーザーが見る最も重要な種類の通知の 1 つになることは間違いありません。 不十分に記述されたエラー メッセージは、エラーの原因と考えられる解決策を自分で決定するためにユーザーを残します。

 ユーザーは、過度に使用されたり混乱を招くエラー メッセージに注意を払わなくなったりする可能性があるため、ユーザー エクスペリエンスに価値を追加する必要なメッセージのみを書き込みます。 メッセージが単なる通知である場合は、別のプレゼンテーションを使用します。

### <a name="rules-for-creating-an-error-message"></a>エラー メッセージを作成するための規則

- エラー メッセージを作成する場合は、対象ユーザーに適切なエラー レベルを選択します。 ユーザーが実行できるアクションを提供する簡単な要約を目指します (該当する場合)。 ユーザーが知る必要がないものは何も述べないでください。

- 建設的な支援を提供する。 命令を含むエラー メッセージを読み取り、操作する方が簡単です。

- ダブルネガティブは使用しないでください。

- 作成したエラー メッセージに対して、自動および手動の文章校正とスペル チェックの両方を実行します。

- 複雑なエラー・メッセージの場合は、順次通信を避けてください。 エラー メッセージに F1 フックアップを使用しないでください。 メッセージ自体で十分です。

- 正しいアイコンを使用します。

- 質問を理解しやすくし、「削除」や「キャンセル」などの明確な選択肢があるボタンを使用します。

- 警告については、進行の結果がどうなるかを明確にしてください。 ボタンは結果を示す必要があります。

- エラーについては、問題を解決するためにユーザーが実行できる操作を記述します。 ボタンはアクションまたは「閉じる」と言う必要があります。 エラー メッセージに [OK] ボタンを使用しないでください。

- エラーメッセージを作成する際に、次の点に関する質問を受けてください。

  - ユーザーは、このエラーだけで問題を解決する方法を理解できますか?

  - ユーザーはこのエラーと同じボキャブラリを使用しますか?

  - このエラーは、複数の状況で、あいまいであるか、共有されているか。 その場合、ユーザーが必要とするソリューションをどのように導きますか。

#### <a name="build-errors"></a>ビルド エラー
 Visual Studio はソフトウェア開発ツールであるため、多くのコンポーネントには、開発者の作業をバイナリ形式に変換するためのコンパイル、変換、またはエンコードの手順があります。 これらの変換は、コンパイラが正しく作成されたファイルを処理できない場合や、コンパイラ オプションが正しく設定されていない場合にエラーを引き起こす可能性があります。

 Visual Studio ユーザーは、ビルド エラーの解決に膨大な時間の開発時間を費やすことができます。 この解決時間は、エラーに依存関係がある場合や、エラー メッセージの記述が不十分な場合に長くなり、エラーの原因を明らかにすることが困難になる可能性があります。

 最良のビルド エラーは、最初に発生しないエラーであるため、Visual Studio ではオートコンプリートと IntelliSense 波線が用意されています。 スキーマ検証ツールと同様のツールは、同じ種類のフィードバックを提供します。 これらのメカニズムは、ユーザーが整形式のコードを構築するように積極的に導き、ビルド エラーの可能性を減らします。

 Visual Studio には、ユーザーがドキュメント ウィンドウで発生したエラーを読み取り、移動できるツール ウィンドウが用意されています。 キーボード ショートカットは、ユーザーが大量のコードをすばやくナビゲートし、問題の場所に直接移動できるように用意されています。 Visual Studio では、各ビルド エラーを特定のヘルプ キーワード/コンテキスト ID に関連付けることができるため、ユーザーはエラーに関する詳細な情報を提供するヘルプ トピックに直接移動できます。

 明確で簡潔なビルドエラーを記述します。

- コンパイラの専門用語をほとんどまたはまったく使用しない場合は、問題を説明する**単純な言語を使用**します。 ビルド エラーのテキストは、過度に技術的であってはなりません。

- **考えられる原因の概要を示します。** たとえば、'(プロパティ) : (値)' 宣言のプロパティと値の間にコロンがありません。

- 潜在的な修正に関する詳細を提供します。 十分なスペースがない場合は、対応するヘルプ トピックに追加の詳細情報を追加できます。

### <a name="components-of-a-well-written-error-message"></a>適切に記述されたエラー メッセージのコンポーネント

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>エラー メッセージにはシェル ダイアログ サービスを使用します。
 シェル ダイアログ サービスを使用すると、個々の要素に大きな変更を加えることなく、メッセージ、特にフォントの外観を制御できます。 **IErrorInfo**メカニズムを使用して **、IVsUIShell:::エラーエラー情報**を使用してレポートします。

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>効果的で適切な通知プレゼンテーションを選択します。
 データの損失を避けるために即時のアクションが必要な場合は、重大な警告を伴うモーダル ダイアログを使用します (同期通知)。 重要なアイコンは、メッセージを読まずに閉じると、否定的な結果につながる可能性がある状況のために予約されています。 データの損失は、アラーム レベルの応答を必要とする重大な状況です。 重要なアイコンの過剰使用は、その重要性にユーザーを鈍感にします. エラー メッセージが本来情報提供である場合は、モーダル ダイアログ (非同期通知) の代替手段を検討してください。

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>技術的な説明ではなく、問題が発生した理由を簡潔に説明します。
 説明の技術的な詳細をユーザーに負担をかけると、エラーメッセージを無視する可能性が高くなります。 良いメッセージの例:

- "要求されたファイルを開くことができません。

- 「インターネットに接続できません。

#### <a name="provide-information-about-how-to-fix-the-problem"></a>問題の解決方法に関する情報を提供します。
 問題の解決方法について、ユーザーに提案を提供します。 提案がない場合は、ユーザーに正直にしてください。 テクニカル サポートやコミュニティ サポートなど、代替オンライン ソースへの直接リンクを提供します。 問題に関連する特定のオンライン情報をユーザーに示すよう試みます。 エラー ID の場合は、その特定のエラーに関するディスカッション スレッドにユーザーをリンクすることを検討してください。 良いメッセージの例:

- "インターネットに接続していることを確認してから、この操作をやり直してください。

- "ファイルが存在し、開く権限があることを確認してください。

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>短いメッセージを書き込みます。
 エラー メッセージは、通知、説明、および解決策を提供できますが、それがあまりにも言葉が言い難い場合は無視されます。 1 つの解決策は、詳細ボタンでプログレッシブ開示を使用することです。 たとえば、簡単な説明/ソリューションを入力し、詳細ボタンの下に詳細を配置します。 ユーザーがエラーに関する詳細情報を読むことを選択した場合は、その情報を読むことができます。

 メッセージ内の言語は次のようになります。

- **ドメインに適しています。** ユーザーが理解する言語を使用します。 当社の顧客は開発者ですが、多くの場合、私たちが持っているコンテキストと用語を持っていません。

- **特定。** あいまいな文言を避け、関係するオブジェクトの特定の名前と場所を指定します。 たとえば、「文字が無効です」などのエラー メッセージは役に立ちません。 どのキャラクター? "ファイルが見つかりません。 どのファイルですか?

- **丁寧。** ユーザーを責めたり、愚かな気持ちにしたりしないでください。 敵対的または攻撃的な言葉(殺す、実行する、終了する、致命的な、違法)を避けてください。 大文字のテキストは、叫び声と見なされることが多く、読み取り不可能なテキストは避けてください。 ユーモアを使ってはいけません。

- **そうです。** 正しいスペルと文法を使用します(アルファでも)。 タイプミスは非専門的で恥ずかしいです。

- **文脈的に適切です。** 適切なボタン テキストを使用します。 [OK] ボタンを使用せずに、[続行] または [はい/いいえ] を使用してください。

### <a name="error-message-examples"></a>エラー メッセージの例

|[良い]|不良|
|----------|---------|
|「ダイヤルした番号は、もはや使用されていません。 番号を確認して再度ダイヤルするか、またはオペレータに 0 をダイヤルしてください。|- "エラー (449): 無効な番号"<br />- "この未処理の例外エラーは、操作が正常に完了したことを示します。<br /><br /> ![Visual Studio での不適切なエラー メッセージ](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "0602-a_ErrorDialog")|

## <a name="accessing-help"></a>ヘルプへのアクセス

### <a name="overview"></a>概要
 MSDN のドキュメントに加えて、Visual Studio ユーザーには、UI を使用している間にユーザーを支援するためのいくつかのアクセス ポイントがあります。 これらのアクセス ポイントを常に利用できるようにするには、機能チームが環境で提供するヘルプ システムを利用する必要があります。 これらのアクセス ポイントは次のとおりです。

- **ダイアログ内の説明テキストと補足テキスト。** UI 画面に表示されるか、情報ヒント アイコンの上にカーソルを置いたときに使用可能な方向または説明を示す静的テキスト。

- **F1 ヘルプ**(エディターのみ)。 Visual Studio エディター内では、ユーザーはいつでも、F1 キーを押すと、現在の選択項目に固有のヘルプ トピックが表示されることを信頼できます。 F1 に関連付けられたトピックが適切で有益であることを確認します。

- **ヘルプ トピックへのハイパーリンク** ユーザーがタスクの実行方法に関するテクノロジ、機能、または情報について学習する際に役立つトピックを起動する、ダイアログ、ツール ウィンドウ、またはデザイン サーフェイス内のハイパーリンク。

- **スマート タグやダイアログの作成などのヘルパー UI メカニズム。** これらのメカニズムは、ユーザーが UI 要素を理解したり、スマート タグやビルダー ダイアログなどのタスクを容易にしたりするために役立ちます。

- **UI ヘルプ ボタン**(非推奨)。 関連する F1 ヘルプ トピックにアクセスするための、タイトル バーに表示されているインジケータ。

### <a name="text"></a>Text

#### <a name="instructional-and-supplemental-text-in-dialogs"></a>ダイアログ内の説明テキストと補足テキスト
 複雑なタスクをサポートするダイアログでは、ダイアログの上部または複雑なコントロールの近くで、UI 内で説明テキストを提供する必要がある場合があります。 書き方の詳細については[、UI テキストと用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)を参照してください。

#### <a name="infotips"></a>ヒント
 多くの場合、説明テキストは UI 内で配置するには時間がかかりすぎるか、新しいユーザーにのみ役立つことがあります。 この場合、説明テキスト/情報テキストはヒントの下にツールチップとして配置する必要があります。

 ヒントは、関連するコントロールの近くに配置する必要があり、目立たないが目立つ特定の情報ヒント アイコンを使用する必要があります。

 ![Visual Studio でのヒント](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **ビジュアル スタジオの情報ヒントの例**

### <a name="interactive-help-mechanisms"></a>対話型ヘルプのメカニズム

#### <a name="f1-help"></a>F1 ヘルプ
 F1 ヘルプは、エディターまたはデザイン サーフェイス内で必要ですが、Visual Studio 環境の他の場所では必要ありません。

#### <a name="hyperlinks-to-help-topics"></a>ヘルプ トピックへのハイパーリンク
 ハイパーリンクを使用して、アクションの実行、IDE 内での移動、ブラウザーでのヘルプの起動を行うことができます。 言語の詳細については[UI テキストと用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)、および視覚的およびレイアウトのガイドラインについては、07.10.01 ボタンとハイパーリンクを参照してください。

#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>ダイアログタイトルバーのヘルプ [?] ボタン (非推奨)
 ほとんどの場合、ダイアログのタイトル バーにある [ヘルプ]ボタンは廃止されました。 UI トピックはドキュメント モデルの一部ではなくなったため、関連するトピックがリンクされていない可能性があります。 基本的に、タイトル バーボタンは F1 ヘルプと同じものであり、ダイアログでは不要になりました。 ハイパーリンクは新しい UI でより一般的に使用されますが、場合によっては、より多くの概念的または手順に関する情報が利用可能であることを示す指標として使用できる場合もあります。

##### <a name="dialogs-created-through-the-environment"></a>環境を通じて作成されたダイアログ
 多くのシェル ダイアログは **、VBDialogBoxParam**関数を使用して作成されます。 この共有機能は、ダイアログから [ ] ダイアログ ボックスに **[ヘルプ**] ボタンを移動するために更新されました **。** 下位互換性と拡張可能なアーキテクチャを保持しながらボタン。

 具体的には **、VBDialogBoxParam**関数は、ID が**IDHELP** (9) またはラベルがヘルプまたは**ヘルプ**であるボタンをダイアログ テンプレート **&** 検索します。 [ヘルプ] ボタンが見つかった場合、そのボタンは非表示になり、**ダイアログにWS_EX_CONTEXTHELP**スタイルが追加され、どのボタンが **?** ボタンをクリックすると、ダイアログのタイトル バーに表示されます。

 ダイアログが作成されると、ダイアログ プロシージャがスタックにプッシュされ **、DialogPreProc**という名前の処理前のダイアログ プロシージャを使用してダイアログを呼び出します。 いつ **?** ボタンがクリックされると、WM_SYSCOMMAND**の****SC_CONTEXTHELP**がダイアログに送信されます。 **DialogPreProc**は、このコマンドをキャプチャし、元のダイアログ プロシージャに渡される**WM_HELP**メッセージに変更します。

 環境に作成されたダイアログボックスの多くは、ダイアログに[ヘルプ]ボタンがあります。 ダイアログが表示されると、[ヘルプ] ボタンは自動的に非表示になり **、?** ボタンが動作します。 の場合**は?** ボタンが削除されたり、Windowsで変更された場合、このソリューションを使用すると、すぐに元のヘルプボタンに戻ることができます。

 このソリューションでは、バグの原因となる可能性のある 4 つの前提条件を次に示します。

- ダイアログのヘルプボタンは**IDHELP** (9) です。

- [ヘルプ] ボタンが非表示になっている場合、ダイアログは正しく表示されます。

- ダイアログは、その winproc を置き換えません。

- ダイアログは、別のダイアログの内部に埋め込まれていません。

  ダイアログが msenv 内にあり **、VBDialogBoxParam**を使用していない場合は、独自のハンドラーを実装する前に**VBDialogBoxParam**を活用することを調査します。

##### <a name="dialogs-created-through-other-packages"></a>他のパッケージを使用して作成されたダイアログ
 msenv の外部にあるダイアログに対して独自のソリューションを実装できます。 VSPackage で共有ダイアログ クラスの場合は、ボタンをタイトル バーに移動するか、各ダイアログにハンドラーを実装することを検討してください。 次のコードは、開始に役立つ実装のスケルトンです。

```
struct DLGPROCITEM
{
    FARPROC proc; // The info used to create the dialog.
    DLGPROCITEM* procPrev;
};

DLGPROCITEM* g_dlgProcStack = NULL;

// A dialog starter/wrapper function is used to push the new
// dialog proc to the top of our dialog proc stack.

int SomeDialogStarterFunction(hinst, id, proc, etc)
{
    if (g_dlgProcStack == NULL)
    {
        g_dlgProcStack = new DLGPROCITEM;
        g_dlgProcStack->procPrev = NULL;
    }
    else
    {
        DLGPROCITEM* procItem = new DLGPROCITEM;
        g_dlgProcStack->procPrev = g_dlgProcStack;
        g_dlgProcStack = procItem;
    }
}

// Pop this dialog proc off the dialog proc stack.

DialogBoxIndirectParam...(...)
{
    DLGPROCITEM* procItem = g_dlgProcStack->procPrev;
    delete g_dlgProcStack;
    g_dlgProcStack = procItem;
}

// A wrapper dialog procedure will allow us to capture the
// SC_CONTEXTHELP button on the title bar from Windows and
// forward it as a simple WM_HELP message back to the dialog.

INT_PTR CALLBACK DialogPreProc(HWND hwndDlg, UINT uMsg,
    WPARAM wParam, LPARAM lParam)
{
    if (uMsg == WM_SYSCOMMAND && wParam == SC_CONTEXTHELP)
    {
        uMsg = WM_HELP;
        wParam = 0;
        lParam = 0;
    }
    return CallWindowProc((WNDPROC)g_dlgProcStack->proc,
        hwndDlg, uMsg, wParam, lParam);
}
```

##### <a name="help-buttons-in-managed-code"></a>マネージ コードのヘルプ ボタン
 マネージ コードでは、ウィンドウ タイトル バーの [ヘルプ] ボタンの既定の動作をオーバーライドするのは簡単です。 この動作を示す完全なデモ アプリケーションを次に示します。 基本的に、フォームの**WndProc**メソッドをオーバーライドし **、SC_CONTEXTHELP**メッセージが傍受されたときに F1 ヘルプ要求を起動する必要があります。

```
using System;
using System.Windows.Forms;

public class HelpForm : Form
{
    private const int SC_CONTEXTHELP = 0xF180;
    private const int WM_SYSCOMMAND = 0x0112;

    public HelpForm()
    {
        this.ClientSize = new System.Drawing.Size(300, 250);
        this.HelpButton = true;
        this.MaximizeBox = false;
        this.MinimizeBox = false;
        this.Name = "HelpForm";
        this.Text = "Help Form";
    }

    protected override void WndProc(ref Message m)
    {
        if (m.Msg == WM_SYSCOMMAND && SC_CONTEXTHELP == (int)m.WParam)
            ShowHelp();
        else
            base.WndProc(ref m);
    }

    private void ShowHelp()
    {
        MessageBox.Show("F1 Help goes here.");
    }

     [STAThread]
    static void Main()
    {
        Application.EnableVisualStyles();
        Application.EnableRTLMirroring();
        Application.Run(new HelpForm());
    }
}
```

## <a name="see-also"></a>関連項目
- [Visual Studio のフォントと書式設定](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)
- [Visual Studio のレイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md)
- [Visual Studio の通知と進行状況](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)
