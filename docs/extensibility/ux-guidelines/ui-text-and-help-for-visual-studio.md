---
title: Visual Studio の UI テキストとヘルプMicrosoft Docs
description: Visual Studio のヘルプ情報で使用される UI テキストと用語について説明します。
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0b0da682f8403890e57118384b7d979f8760d62f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926148"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Visual Studio の UI テキストとヘルプ
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a> UI のテキストと用語
 わかりやすくテキストは、効果的な UI にとって重要です。 ソフトウェアユーザーは、最初にラベルを読む傾向があります。 静的テキストは、頻度が低い状態で読み取られます。 ユーザーに対して、ウィンドウ全体のクイックスキャンを使用して作業セッションを開始するように計画し、次にこのおおよその順序で UI を読み取ります。

1. 中央の対話型コントロール

2. コミットボタン

3. 他の場所で見つかった対話型コントロール

4. 主要な手順

5. 補足説明

6. ウィンドウのタイトル

7. メイン本文内の他の静的テキスト

### <a name="usage-patterns-for-ui-text"></a>UI テキストの使用パターン

#### <a name="title-bar-text"></a>タイトル バーの文字列
 タイトルバーのテキストは、UI を生成したコマンドと一致している必要があります。

#### <a name="instructional-text-helper-text"></a>指示テキスト (ヘルパーテキスト)
 ダイアログによっては、ウィンドウまたはページで何を行うかを説明するための主要な手順を提供すると便利です。 これは、"ヘルパーテキスト" と呼ばれることもあります。

##### <a name="writing-style-rules-for-helper-text"></a>ヘルパーテキストのスタイルルールの記述

- 明確な説明はありません。 絶対に必要な場合を除き、指示テキストは含めないでください。

- 指示テキストは常にダイアログの上部に配置され、実行されているタスクを参照する必要があります。

- ユーザーに必要な操作を正確に説明します。 過剰な通信と冗長性を回避します。

- 各ウィンドウを確認し、重複する単語とステートメントを削除します。

- 指示テキストを短くします。 特定のユーザーまたはシナリオに関する詳細情報が必要な場合は、詳細な概念的なオンライントピックへのリンクを提供します。

- すべての単語がウエイトを保持し、必要とされるように、テキストを記述します。

- [ユーザーインターフェイスのテキスト](/windows/desktop/uxguide/text-ui)と[スタイルとトーン](/windows/desktop/uxguide/text-style-tone)については、既存の Microsoft ガイダンスに従ってください。

#### <a name="supplemental-instructions"></a>補足手順
 補足指示では、ユーザーがコントロールまたはコントロールのグループ化を理解するのに役立つ追加情報を提供します。 これには、入力コントロールで想定される形式を理解するために必要なヒントテキストを含めることもできます。 補足指示は控えめに使用してください。 ユーザーが行っている選択の影響を完全に理解できない可能性がある場合に備えて予約します。

 ![オプションの設定を変更した場合の影響について説明している Internet Explorer の [オプション] ボタンの下に表示されるスクリーンショット。](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Visual Studio での補足のテキスト**

 ![Visual Studio の [ソース管理の選択] ダイアログのスクリーンショット。ソース管理システムの各オプションについて説明する補足テキストが表示されます。](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Visual Studio での補足のテキスト**

#### <a name="infotips"></a>ヒント
 多くの場合、指示テキストは、UI 内での配置に時間がかかりすぎる場合や、新しいユーザーにのみ役立つ場合があります。経験豊富なユーザーにとっては煩雑です。 この場合、説明と情報のテキストはヒントの下にツールヒントとして配置する必要があります。

 インフォヒントは、関連付けられているコントロールの近くに配置する必要があります。また、わかりやすいヒントアイコンを使用する必要があります。

 ![Visual Studio でのヒント](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Visual Studio のヒントの例**

##### <a name="writing-style-rules-for-infotips"></a>インフォヒントのスタイルルールの記述

- ヒントを完成文として記述します。 これには、特定の動詞、文の大文字と末尾の区切り記号が必要です。

- インフォヒントを使用して、主要な命令や情報を補完します。 異なる単語を使用してメインの概念を確認するだけの場合は、ヒントは必要ありません。

- ヒントを簡潔にしておくことができます。 ユーザーをサポートし、推奨する、小さな単語と、日常の言語を使用します。

- [ユーザーインターフェイスのテキスト](/windows/desktop/uxguide/text-ui)と[スタイルとトーン](/windows/desktop/uxguide/text-style-tone)については、既存の Microsoft ガイダンスに従ってください。

#### <a name="control-labels"></a>コントロールラベル
 コントロールラベルは、簡潔で簡潔なものにする必要があります。また、 [コントロールについては、Windows デスクトップのガイダンス](/windows/desktop/uxguide/controls)に従ってください。

 コントロールラベルの形式と UI 内の配置の詳細については、「 [Visual Studio のレイアウト](../../extensibility/ux-guidelines/layout-for-visual-studio.md)」を参照してください。

#### <a name="help-links"></a>[ヘルプ] リンク
 ヘルプリンクは、指示テキスト内に配置することも、UI の本文内に配置することもできます。 これらのリンクは、内部ダイアログをヘルプまたは起動するためのリンクにすることができます。

##### <a name="visual-style-rules-for-help-links"></a>ヘルプリンクの視覚スタイルの規則

- ハイパーリンクに適切な環境の色を使用します。 正しいスタイルのハイパーリンクをクリックしても、赤色の点滅は行われません。 これが表示される場合は、環境の色が使用されていないことを示しています。

- 下線は、ホバー時またはリンクが段落に埋め込まれている場合にのみ使用してください。

- ハイパーリンクのビジュアルと対話スタイルの詳細については、「ボタンとハイパーリンク」を参照してください。

##### <a name="writing-style-rules-for-help-links"></a>ヘルプリンクのスタイルルールの記述

- ダイアログを起動するときは、省略記号の標準を維持します。ナビゲーションには省略記号がありません。タスクに追加の UI が必要な場合は省略記号。

     ![Visual Studio でのヘルプ リンク](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **ヘルプリンク内の省略記号 (...) は、タスクに追加の UI が必要であることを示します。**

- ユーザーが意図したものではないため、リンクは "学習" で始めることはできません。 ユーザーは、一般的な教育を受けずに特定の質問に回答することを希望しています。

- 語句のヘルプリンクを使用すると、トピックが回答する質問に答えることができます。

     誤り: "Windows Azure Mobile Services の価格についての詳細情報"

     修正: 「Windows Azure Mobile Services で使用できる価格オプション

- リンクテキストには [.. *.]* を使用しないでください。

- "ここに" のみリンクしないでください。 スクリーンリーダーによっては、ハイパーリンクされた単語だけが読み上げられることがあります。

     誤り: "Windows Azure Mobile Services に関する情報を **ここ** に入力してください"

     修正: 「Windows Azure Mobile Services で使用できる価格オプション

- ヘルプリンクの正しい書き込みスタイルの詳細については、 [Windows デスクトップのガイダンス](/windows/desktop/uxguide/winenv-help)を参照してください。

#### <a name="hint-text"></a>ヒントテキスト
 ヒントテキストは、コントロール内またはコントロールの下にウォーターマークとして表示されます。 正しい書式設定は、適切な VSColors トークンを使用して適用され `Environment.GrayText` ます。

 さまざまな形式で表示できます。

- コントロールラベルの代わりに次のようにします。

     !["Search ソリューションエクスプローラー (Ctrl +;)" を読み取るコントロールラベルの代わりにヒントテキストが表示されたドロップダウンコントロールのスクリーンショット。](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- 動詞を使用する場合は、次の手順に従います。

     ![[名前を入力してください] というヒントテキストがコントロール内に表示されているテキストボックスのスクリーンショット。](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- 必須のエントリを示すテキストを含む:

     !["Required" を読み取るコントロール内のヒントテキストを含むテキストボックスのスクリーンショット \< \> 。](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>透かしテキスト
 空のデザインサーフェイスでは、必要に応じて、他の関連ウィンドウを開くためのリンクを提供すると共に、何を行うかを示すテキストが表示されます。

 ![Visual Studio でのウォーターマーク テキスト](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **Visual Studio での透かしテキストの例**

### <a name="common-terminology"></a>一般的な用語

|用語|説明|解説|
|----------|-----------------|-------------|
|サインイン/サインアウト|動詞は、web プロパティに認証を表すために、web で同義語とに使用されていました。 クライアント内では、これを1回使用して、IDE ユーザー接続にサインインおよびサインアウトするための最上位レベルの概念として使用します。これは、他のすべての接続で使用できないローミングやライセンスなどの上位レベルの機能を提供する最上位レベルの id を表します。|IDE ユーザーは、トップレベルの IDE ユーザーを表すため、サインイン/サインアウト動詞を表す唯一の機能です。|
|接続/切断|機能がオンラインサービスへの単一の接続を保持する場所で使用します。|サーバーエクスプローラーには、一度に1つのアクティブな Azure 接続のみを使用できます。接続/切断の例を次に示します。|
|追加/削除|非破壊的。 リストの内容を追加または削除するときに使用します。|[TFS 接続マネージャーサーバーの一覧] ダイアログは、追加/削除の一例です。|
|削除|破壊的. 削除する要素がディスクから完全に破棄または削除される場合にのみ、を使用します。|通常、"削除" では、結果がディスクからファイルを削除する場合は、プロンプトが表示されます。|

## <a name="error-messages"></a>エラー メッセージ

### <a name="overview"></a>概要
 エラーが発生します。 あればエラーメッセージを防止するための最初の手順として、ユーザーが実行できる操作の制限を設定します。 ただし、エラーが発生した場合は、問題を緩和するために、適切に記述されたエラーメッセージが表示されることがあります。 エラーメッセージは、同期的であり、解決する必要がある問題を示すため、ユーザーに表示される最も重要な通知の1つです。 エラーメッセージが正しく記述されていない場合は、ユーザーが独自のエラーを発生させて、エラーの原因と考えられる解決策を判断します。

 ユーザーは、過剰なエラーメッセージまたは混乱を招く可能性のあるエラーメッセージについては、ユーザーエクスペリエンスに値を追加する必要なメッセージだけを書き込むことができます。 メッセージが単なる通知の場合は、別のプレゼンテーションを使用します。

### <a name="rules-for-creating-an-error-message"></a>エラーメッセージを作成するための規則

- エラーメッセージを構築する場合は、対象ユーザーに対して適切なエラーレベルを選択します。 必要に応じて、ユーザーが実行できるアクションを提供する簡単な概要を作成します。 ユーザーが認識している必要のないものは何も表示しません。

- 建設的な支援を提供します。 命令を含むエラーメッセージの読み取りと操作が簡単になります。

- 二重ネガは使用しないでください。

- 作成したエラーメッセージに対して、自動と手動の文法、およびスペルチェックの両方を実行します。

- 複雑なエラーメッセージについては、順次通信を避けてください。 エラーメッセージに F1 フックを使用しないでください。 メッセージ自体が十分である必要があります。

- 適切なアイコンを使用します。

- "削除" や "キャンセル" など、明確な選択肢があるボタンを簡単に理解して使用することができます。

- 警告の場合は、続行の結果がどのようになるかを明確にします。 ボタンは結果を示します。

- エラーの場合は、問題を解決するためにユーザーが実行できる操作を記述します。 ボタンは、アクションとして、または "閉じる" とする必要があります。 エラーメッセージには [OK] ボタンを使用しないでください。

- エラーメッセージを作成する際には、次の点を確認してください。

  - このエラーだけで問題を解決する方法をユーザーが判断することはできますか。

  - ユーザーはこのエラーと同じ語彙を使用しますか。

  - このエラーは複数の状況であいまいですまたは共有されていますか。 その場合、ユーザーが必要なソリューションをどのようにガイドするのでしょうか。

#### <a name="build-errors"></a>ビルド エラー
 Visual Studio はソフトウェア開発ツールであるため、そのコンポーネントの多くには、開発者の作業をバイナリ形式に変換するためのコンパイル、変換、またはエンコードの手順が用意されています。 これらの変換によって、コンパイラが正しく作成されていないファイルを処理できない場合、またはコンパイラオプションが正しく設定されなかった場合に、エラーが発生する

 Visual Studio ユーザーは、ビルドエラーを解決するために膨大な数の開発時間を費やすことができます。 この解決時間は、エラーの依存関係がある場合や、エラーメッセージの書き込みが不十分な場合に発生します。これにより、エラーの原因を特定するのが困難になります。

 最適なビルドエラーは、最初の場所では発生しないものであり、Visual Studio でオートコンプリートと IntelliSense の波線が提供されるためです。 スキーマ検証コントロールと同様のツールでは、同じ種類のフィードバックが提供されます。 これらのメカニズムは、ビルドエラーの可能性を軽減、整形式のコードを作成するためのユーザーを事前にガイドします。

 Visual Studio には、ユーザーがドキュメントウィンドウで発生したエラーを読み取って移動できるツールウィンドウが用意されています。 ユーザーが大量のコードをすばやく移動し、問題の場所に直接移動できるように、キーボードショートカットが用意されています。 また、Visual Studio では、各ビルドエラーを特定のヘルプキーワード/コンテキスト ID に関連付けることができます。これにより、エラーに関する詳細な情報を提供するヘルプトピックにユーザーが直接アクセスできるようになります。

 明確で簡潔なビルドエラーを記述します。

- ほとんどまたはまったくコンパイラの専門用語で問題を説明する **プレーン言語を使用** します。 ビルドエラーのテキストは、あまり技術的ではないはずです。

- **考えられる原因の概要を示します。** たとえば、"(プロパティ): (値) ' 宣言のプロパティと値の間にコロンがありません。" というようになります。

- 潜在的な修正についての詳細を提供します。 十分な領域がない場合は、対応するヘルプトピックに追加の詳細情報が格納されている可能性があります。

### <a name="components-of-a-well-written-error-message"></a>適切に記述されたエラーメッセージのコンポーネント

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>エラーメッセージには、シェルダイアログサービスを使用します。
 Shell dialog service を使用すると、個々の要素に大きな変更を加えずに、メッセージの外観、特にフォントの外観を制御できます。 **IErrorInfo** メカニズムを使用して、 **IVsUIShell:: SetErrorInfo/ReportErrorInfo** を使用してレポートします。

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>効果的で適切な通知プレゼンテーションを選択します。
 データの損失を回避するために直ちに対処する必要がある場合は、重大な警告があるモーダルダイアログを使用します (同期通知)。 重要なアイコンは、メッセージを読み取らずに閉じると、悪影響が生じる可能性があります。 データの損失は、アラームレベルの応答を必要とする重大な状況です。 重要なアイコンを desensitizes して、ユーザーの重要度を超えています。 エラーメッセージに情報が含まれている場合は、モーダルダイアログ (非同期通知) の代替手段を検討してください。

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>技術的な説明ではなく、問題が発生した理由の簡潔で簡潔な説明を提供します。
 過負荷の説明に技術的な詳細が含まれているユーザーは、エラーメッセージを無視する可能性が高くなります。 優れたメッセージングの例を次に示します。

- "要求されたファイルを開けません。"

- "インターネットに接続できません。"

#### <a name="provide-information-about-how-to-fix-the-problem"></a>問題の解決方法に関する情報を提供します。
 問題の解決方法をユーザーに提案します。 提案がない場合は、ユーザーに正直にしてください。 テクニカルサポートやコミュニティサポートなど、代替のオンラインソースへの直接リンクを提供します。 問題に関連する特定のオンライン情報をユーザーにポイントしてみてください。 エラー ID については、その特定のエラーに関するディスカッションスレッドにユーザーをリンクすることを検討してください。 優れたメッセージングの例を次に示します。

- "インターネットに接続していることを確認してから、操作をやり直してください。"

- "ファイルが存在し、それを開くためのアクセス許可があることを確認してください。"

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>短いメッセージとポイントを作成します。
 エラーメッセージは、ソリューションの通知、説明、および提供を行うことができますが、非常に多くの場合には無視されます。 1つの解決策は、詳細ボタンを使用してプログレッシブ開示を使用することです。 たとえば、簡単な説明とソリューションを指定し、詳細ボタンの下に詳細を入力します。 このエラーの詳細については、ユーザーがその他の情報を参照してください。

 メッセージの言語は次のようになります。

- **ドメイン-適切。** ユーザーが理解できる言語を使用します。 お客様は開発者であっても、多くの場合、お客様が持っているコンテキストと用語を持っていません。

- **のみ.** あいまいな表現を避け、特定の名前とオブジェクトの場所を指定します。 たとえば、"character is invalid" などのエラーメッセージは役に立ちません。 どの文字でしょうか。 "ファイルが見つかりません。" ファイルを指定してください。

- **こと.** ユーザーをばかげしたり、感じたりすることは避けてください。 悪意のあるまたは不快な言語 (kill、execute、terminate、fatal、無効) を避けます。 大文字を使用しないでください。大文字のテキストは叫んとして認識され、読み取り可能ではありません。 ユーモアは使用しないでください。

- **正解です。** 正しいスペルと文法を使用します (アルファでも)。 入力ミスは不自然見えると他人です。

- **文脈に適しています。** 適切なボタンテキストを使用します。 [OK] ボタンを使用せずに、代わりに "Continue" または "Yes/No" を使用します。

### <a name="error-message-examples"></a>エラーメッセージの例

|良い|不良|
|----------|---------|
|"ダイヤルした番号はサービスに含まれていません。 電話番号を確認し、もう一度ダイヤルするか、オペレーターの電話番号をダイヤルしてください。 "|-"エラー (449): 数値が正しくありません"<br />-"このハンドルされない例外エラーは、操作が正常に完了したことを示します。"<br /><br /> ![Visual Studio での不適切なエラー メッセージ](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "0602-a_ErrorDialog")|

## <a name="accessing-help"></a>ヘルプへのアクセス

### <a name="overview"></a>概要
 MSDN のドキュメントに加えて、Visual Studio ユーザーには UI でユーザーを支援するためのアクセスポイントがいくつかあります。 これらのアクセスポイントを常に使用できるようにするために、機能チームは環境によって提供されるヘルプシステムを利用する必要があります。 これらのアクセスポイントは次のとおりです。

- **ダイアログの指示と補足テキスト。** UI 画面上またはヒントアイコンの上にマウスポインターを置いたときに、方向または説明を提供する静的テキスト。

- **F1 ヘルプ** (エディターのみ)。 Visual Studio エディターでは、ユーザーはいつでもこのを信頼できます。 F1 キーを押すと、現在の選択項目に固有のヘルプトピックが表示されます。 F1 に関連するトピックが適切であり、有益であることを確認します。

- **ヘルプトピックへのハイパーリンク。** ダイアログ、ツールウィンドウ、またはデザイン画面内のハイパーリンク。トピックを起動して、テクノロジ、機能、またはタスクの実行方法に関する情報をユーザーが理解できるようにします。

- **スマートタグやダイアログの作成などのヘルパー UI 機構。** これらのメカニズムは、ユーザーが UI 要素を理解したり、スマートタグやビルダーダイアログなどのタスクを容易にしたりするのに役立ちます。

- **UI のヘルプボタン** (非推奨)。 関連する F1 ヘルプトピックへのアクセスを提供する、タイトルバーに表示されるインジケーター。

### <a name="text"></a>Text

#### <a name="instructional-and-supplemental-text-in-dialogs"></a>ダイアログの指示と補足テキスト
 複雑なタスクをサポートするダイアログでは、UI 内に指示テキストを付ける必要がある場合があります。これは、多くの場合、ダイアログまたはほぼ複雑なコントロールの上部にあります。 書き方の詳細については [、「UI text and 用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) 」を参照してください。

#### <a name="infotips"></a>ヒント
 多くの場合、指示テキストは UI 内での配置には時間がかかりすぎる場合があります。また、経験豊富なユーザーにとっては煩雑であるように、新しいユーザーにのみ役立ちます。 この場合、説明と情報のテキストはヒントの下にツールヒントとして配置する必要があります。

 インフォヒントは、関連付けられているコントロールの近くに配置する必要があります。また、わかりやすいヒントアイコンを使用する必要があります。

 ![Visual Studio でのヒント](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Visual Studio のヒントの例**

### <a name="interactive-help-mechanisms"></a>対話形式のヘルプ機構

#### <a name="f1-help"></a>F1 ヘルプ
 F1 ヘルプは、エディターまたはデザインサーフェイス内で必要ですが、Visual Studio 環境内の他の場所には必要ありません。

#### <a name="hyperlinks-to-help-topics"></a>ヘルプトピックへのハイパーリンク
 ハイパーリンクを使用すると、アクションの実行、IDE 内での移動、またはブラウザーでのヘルプの起動を行うことができます。 詳細については、「 [UI のテキストと用語](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) 」を参照してください。

#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>ダイアログタイトルバーのヘルプ [?] ボタン (非推奨)
 ほとんどの場合、ダイアログボックスのタイトルバーにあるヘルプボタン ([?]) は非推奨とされます。 UI トピックはドキュメントモデルの一部ではなくなったため、リンクする関連トピックがない可能性があります。 基本的に、タイトルバーボタンは F1 ヘルプと同じものであり、ダイアログでは不要になりました。 場合によっては、これは使用可能な概念または手順の情報があることを示すインジケーターとして使用できます。ただし、ハイパーリンクは新しい UI でよく使用されます。

##### <a name="dialogs-created-through-the-environment"></a>環境を使用して作成されたダイアログ
 多くのシェルダイアログは、 **vb、Boxparam** 関数を使用して作成されます。 この共有関数は、ダイアログボックスからに [ **ヘルプ** ] ボタンを移動するのに役立つように更新されました **。** ボタンをクリックして、下位互換性と拡張が可能なアーキテクチャを維持します。

 具体的には、 **Vbdialogboxparam** 関数は、ID が **idhelp** (9) またはラベルが **ヘルプ** または **&ヘルプ** であるボタンのダイアログテンプレートを参照します。 [ヘルプ] ボタンが見つかった場合は非表示になり、ダイアログに **WS_EX_CONTEXTHELP** スタイルが追加され **ます。** ] ボタンをクリックします。

 ダイアログが作成されると、ダイアログプロシージャがスタックにプッシュされ、ダイアログが呼び出され **ます。この** ダイアログボックスには、[プロパティ] ダイアログボックスが開きます。 **?** ボタンがクリックされると、 **SC_CONTEXTHELP** の **WM_SYSCOMMAND** がダイアログに送信されます。 このコマンド **は、このコマンドをキャプチャし** て **WM_HELP** メッセージに変更し、元のダイアログプロシージャに渡されます。

 ほとんどの環境で作成されたダイアログには、ダイアログの [ヘルプ] ボタンがあります。 ダイアログが表示されると、[ヘルプ] ボタンは自動的に非表示になり **ます。** ボタンが動作します。 **?** Windows では、ボタンが削除または変更されています。このソリューションを使用すると、元のヘルプボタンにすばやく戻ることができます。

 このソリューションでは、次の4つの前提がバグの原因になります。

- ダイアログの [ヘルプ] ボタンは **Idhelp** (9) です。

- [ヘルプ] ボタンが非表示になると、ダイアログが正しく表示されます。

- このダイアログは、winproc の代わりになりません。

- ダイアログが別のダイアログの内部に埋め込まれていません。

  ダイアログが msenv 内に存在し、 **Vb/Boxparam** を使用していない場合は、独自のハンドラーを実装する前に、 **Vbの boxboxparam** を活用することを検討してください。

##### <a name="dialogs-created-through-other-packages"></a>他のパッケージを使用して作成されたダイアログ
 Msenv の外部にあるダイアログに対して独自のソリューションを実装できます。 VSPackage の共有ダイアログクラスの場合は、ボタンをタイトルバーに移動するか、各ダイアログにハンドラーを実装することを検討してください。 次のコードは、作業を開始するのに役立つ実装のスケルトンです。

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

##### <a name="help-buttons-in-managed-code"></a>マネージコードのヘルプボタン
 ウィンドウタイトルバーの既定の動作は、マネージコードでは簡単にオーバーライドできます。 この動作を示す完全なデモアプリケーションを以下に示します。 基本的には、フォームの **WndProc** メソッドをオーバーライドし、 **SC_CONTEXTHELP** メッセージが傍受されたときに F1 ヘルプ要求を起動する必要があります。

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
