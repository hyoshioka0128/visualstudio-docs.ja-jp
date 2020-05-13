---
title: Visual Studio の通知と進行状況 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f6a7ddd5d1a5a7257617b03098722e1341017b6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699884"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Visual Studio の通知と進行状況
## <a name="notification-systems"></a><a name="BKMK_NotificationSystems"></a>通知システム

### <a name="overview"></a>概要
 ソフトウェア開発タスクに関して Visual Studio で発生している内容をユーザーに通知する方法はいくつかあります。

 あらゆる種類の通知を実装する場合:

- **通知の数を最小有効数に抑えます**。 通知メッセージは、大多数の Visual Studio ユーザー、または特定の機能領域のユーザーに適用する必要があります。 通知を過度に使用すると、ユーザーを横取りしたり、システムの使いやすさが低下したりする可能性があります。

- ユーザーが、より複雑な選択を行い、さらにアクションを実行するために適切なコンテキストを呼び出すために使用できる **、明確で実行可能なメッセージを提示していることを確認**します。

- **同期メッセージと非同期メッセージを適切に表示する。** 同期通知は、Web サービスがクラッシュしたり、コード例外がスローされたりした場合など、即時の注意が必要であることを示します。 モーダル ダイアログなどで、入力が必要な方法で、これらの状況をすぐにユーザーに通知する必要があります。 非同期通知は、ビルド操作の完了や Web サイトの配置の完了など、ユーザーが直ちに通知する必要があるが、すぐに実行する必要がない通知です。 これらのメッセージは、よりアンビエントであり、ユーザーのタスク フローを中断しないようにする必要があります。

- モーダル ダイアログは、メッセージを受信したり、ダイアログで提示された決定を下す前に**ユーザーがそれ以上のアクションを実行できないようにするために必要な場合にのみ使用**します。

- **アンビエント通知が無効になった場合は、アンビエント通知を削除します。** 通知された問題に対処するためのアクションを既に実行している場合は、通知を終了する必要はありません。

- **通知は誤った相関関係につながる可能性があることに注意してください。** ユーザーは、実際に因果関係がない場合に、1 つ以上のアクションが通知をトリガーしたと考えるかもしれません。 通知メッセージでは、コンテキスト、トリガー、および通知のソースを明確にします。

### <a name="choosing-the-right-method"></a>正しい方法を選択する
 この表を使用して、メッセージをユーザーに通知する適切な方法を選択します。

|Method|用途|使用しない|
|------------|---------|----------------|
|[モーダル エラー メッセージ ダイアログ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|続行する前にユーザーの応答が必要な場合に使用します。|ユーザーをブロックしてフローを中断する必要がない場合は使用しないでください。 別の、より侵入の少ない方法でメッセージを表示することができる場合は、モーダルダイアログを使用しないでください。|
|[IDE ステータス バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|プロセスのステータスに関するアンビエント テキスト情報がある場合に使用します。|単独で使用しないでください。 他のフィードバックメカニズムと組み合わせて使用するのが最適です。|
|[埋め込まれた情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|ツール ウィンドウまたはドキュメント ウィンドウで、進行状況、エラー状態、結果、および/または実行可能な情報を通知するために使用します。|情報が情報バーの配置場所に関係ない場合は使用しないでください。<br /><br /> ドキュメント/ツール ウィンドウの外側では使用しないでください。|
|[マウスカーソルの変更](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|プロセスが実行されていることを通知するために使用できます。 また、ドラッグ アンド ドロップが進行中の場合や、マウス カーソルが描画モードなどの特定のモードにある場合など、マウスの状態が変化したことを通知するためにも使用されます。|短い進行状況の変更や、カーソルのフラッターが発生する可能性がある場合 (たとえば、プロセス全体ではなく、長時間実行されているプロセスの一部に関連付けられている場合) には使用しないでください。|
|[進捗インジケータ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|進行状況を報告する必要がある場合 (確定または不確定) に使用します。 進行状況インジケーターの種類と、それぞれの具体的な使用法がさまざまです。 [進行状況インジケータを](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)参照してください。||
|[Visual Studio の通知ウィンドウ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|[通知] ウィンドウは、公開可能な拡張ではありません。 ただし、ライセンスに関する重大な問題や Visual Studio またはパッケージに対する更新の情報通知など、Visual Studio に関するさまざまなメッセージを伝達するために使用されます。|他の種類の通知には使用しないでください。|
|[エラー一覧](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|問題が、問題 (エラー/警告/情報) を持つユーザーの現在開いているソリューションに直接関連する場合、コードに対してアクションを実行する必要があります。<br /><br /> これには、たとえば次のものが含まれます。<br /><br /> - コンパイラメッセージ(エラー/警告/情報)<br /><br /> - コードアナライザ/コードに関する診断メッセージ<br /><br /> - メッセージを作成する<br /><br /> プロジェクトファイルやソリューションファイルに関連する問題には適切ですが、まずソリューションエクスプローラの指示を検討してください。|ユーザーの開いているソリューション コードとの関係がない項目には使用しないでください。|
|編集者通知: 電球|開いているファイルに存在する問題を修正するための修正プログラムがある場合に使用します。<br /><br /> 電球は、リファクタリングなど、ユーザーのコードで実行されるクイック アクションをオンデマンドで行う場合にも使用する必要がありますが、その場合は "通知スタイル" と表示されません。|開いているファイルとの関係がないアイテムには使用しないでください。|
|編集者通知: 波線|開いているコードの特定のスパン (エラーの赤い波線など) に関する問題をユーザーに警告するために使用します。|開いているコードの特定の範囲に関連しない項目には使用しないでください。|
|[埋め込みステータス バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|特定のツール ウィンドウ、ドキュメント ウィンドウ、またはダイアログ ウィンドウのコンテキスト内でコンテンツまたはプロセスに関連するステータスを提供するために使用します。|特定のウィンドウ内のコンテンツに関連しない一般的な製品通知、プロセス、またはアイテムには使用しないでください。|
|[ウィンドウトレイ通知](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|アウト プロセスまたはコンパニオン アプリケーションの通知を表示するために使用します。|IDE に関連する通知には使用しないでください。|
|[通知の泡](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|IDE**の外部**でリモート プロセスまたは変更を通知するために使用します。|IDE**内**のプロセスをユーザーに通知する手段として使用しないでください。|

### <a name="notification-methods"></a>通知方法

#### <a name="modal-error-message-dialogs"></a><a name="BKMK_ModalErrorMessageDialogs"></a>モーダル エラー メッセージ ダイアログ
 モーダル エラー メッセージ ダイアログボックスは、ユーザーの確認またはアクションを必要とするエラー メッセージを表示するために使用されます。

 ![モーダル エラー メッセージ](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901-01_ModalErrorMessage")

 **データベースに対する無効な接続文字列をユーザーに警告するモーダル エラー メッセージ ダイアログ**

#### <a name="ide-status-bar"></a><a name="BKMK_IDEStatusBar"></a>IDE ステータス バー
 ユーザーがステータス バーのテキストに気づく可能性は、すべてのコンピューターエクスペリエンスと Windows プラットフォームでの特定のエクスペリエンスに関連しています。 Visual Studio の顧客基盤は両方の領域で経験する傾向がありますが、知識豊富な Windows ユーザーでもステータス バーの変更を見逃す可能性があります。 したがって、ステータス バーは情報提供の目的や、他の場所で提示される情報の冗長なキューとして使用するのが最適です。 ユーザーが直ちに解決する必要がある重要な情報は、ダイアログまたは通知ツール ウィンドウで提供する必要があります。

 Visual Studio のステータス バーは、さまざまな種類の情報を表示できるように設計されています。 フィードバック、デザイナー、プログレス バー、アニメーション、およびクライアントの領域に分割されます。

 フィードバック領域とデザイナー領域は常に表示されます。 プログレス バーとアニメーション領域は常に動的で、ユーザー コンテキストに基づきます。 デザイナー領域は、テキスト メッセージの付随するリソースから取得される文字列の長さによって決まる静的な幅を持ちます。 これにより、ローカライズでは、コードを変更せずに幅のサイズを変更できます。 英語の場合、この文字列の幅は約 220 ピクセルです。 デザイナー領域は正常に動作し、フィードバック領域は残りの領域を吸収します。

 ステータス バーも色分けされ、IDE がデバッグ モードの場合など、さまざまな IDE 状態の変化を伝えることで、視覚的な関心と機能の価値が追加されます。

 ![IDE ステータス バーの色の変更](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901-02_IDEStatusBar")

 **IDE ステータスバーの色**

#### <a name="embedded-infobar"></a><a name="BKMK_EmbeddedInfobar"></a>埋め込みインフォバー
 情報バーは、ドキュメント ウィンドウまたはツール ウィンドウの上部で、状態や状態をユーザーに通知するために使用できます。 また、ユーザーが簡単にアクションを実行できるようにコマンドを提供することもできます。 情報バーは、標準のシェル コントロールです。 IDE で他のユーザーと一貫性のない動作をする独自のユーザーを作成しないようにします。 実装の詳細と使用方法については、[インフォバー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)を参照してください。

 ![埋め込まれた情報バー](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901-03_EmbeddedInfobar")

 **ドキュメント ウィンドウに埋め込まれた情報バーで、IDE がデバッグ履歴モードであり、エディターが標準のデバッグ モードと同じように応答しないことをユーザーに警告します。**

#### <a name="mouse-cursor-changes"></a><a name="BKMK_MouseCursorChanges"></a>マウスカーソルの変更
 マウス カーソルを変更する場合は、VSColor サービスに関連付けられ、既にカーソルに関連付けられている色を使用します。 カーソルの変更は、進行中の操作を示す場合や、ユーザーがオブジェクトのドラッグ、ドロップ、または選択に使用できるターゲット上にマウスポインターを置くヒットゾーンを示すために使用できます。

 ビジー/待機マウス カーソルは、操作のために使用可能なすべての CPU 時間を予約する必要がある場合にのみ使用し、ユーザーがそれ以上の入力を表現できないようにします。 マルチスレッドを使用するアプリケーションが適切に記述されているほとんどの場合、ユーザーが他の操作を実行できない場合はまれです。

 カーソルの変更は、他の場所で表示される情報の冗長なキューとして役立つことに注意してください。 特にユーザーが対処しなければならない重要なことを伝えようとする場合は、ユーザーとの通信の唯一の方法としてカーソルの変更に依存しないでください。

#### <a name="progress-indicators"></a><a name="BKMK_NotSysProgressIndicators"></a>進捗インジケータ
 進行状況インジケータは、完了するまでに数秒以上かかるプロセス中にユーザーにフィードバックを与えるために重要です。 進行状況インジケーターは、埋め込みステータス バー、モーダル ダイアログ、または Visual Studio ステータス バーに、埋め込みステータス バーに埋め込み (進行中のアクションの開始ポイントの近く)、インプレースで表示できます。 使用と実装に関[する進行状況インジケーターの](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)ガイダンスに従います。

#### <a name="visual-studio-notifications-window"></a><a name="BKMK_VSNotificationsToolWindow"></a>[ビジュアル スタジオの通知] ウィンドウ
 [Visual Studio の通知] ウィンドウでは、ライセンス、環境 (Visual Studio)、拡張機能、および更新プログラムについて開発者に通知します。 ユーザーは個々の通知を破棄することも、特定の種類の通知を無視することもできます。 無視された通知の一覧は **、[ツール] >オプション**ページで管理されます。

 [通知] ウィンドウは現在拡張できません。

 ![Visual Studio の通知ウィンドウ](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901-06_VSNotificationsWindow")

 **[Visual Studio の通知] ツール ウィンドウ**

#### <a name="error-list"></a><a name="BKMK_ErrorList"></a>エラー一覧
 エラー一覧内の通知は、コンパイルまたはビルド処理中に発生したエラーと警告を示し、ユーザーはその特定のコード エラーにコード内を移動できるようにします。

 ![エラー一覧](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901-08_ErrorList")

 **エラーリスト**

#### <a name="embedded-status-bars"></a><a name="BKMK_EmbeddedStatusBars"></a>埋め込みステータス バー
 IDE ステータス バーは動的で、クライアント領域のコンテキストがアクティブドキュメントウィンドウに設定され、ユーザーのコンテキストやシステムの応答に関する情報が更新されるため、情報の継続的な表示を維持したり、長期非同期プロセスの状態を与えたりすることは困難です。 たとえば、IDE ステータス バーは、複数の実行や直ちにアクション可能な項目の選択に対するテストの実行結果の通知には適していません。 このようなステータス情報は、ユーザーが選択したり、プロセスを開始したりするドキュメントまたはツール ウィンドウのコンテキストに保持することが重要です。

 ![埋め込まれたステータス バー](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **Visual Studio の埋め込みステータス バー**

#### <a name="windows-tray-notifications"></a><a name="BKMK_WindowsTray"></a>ウィンドウトレイ通知
 Windows の通知領域は、Windows タスク バーのシステム クロックの横にあります。 多くのユーティリティおよびソフトウェア コンポーネントは、画面解像度の変更やソフトウェアの更新の取得など、システム全体のタスクのコンテキスト メニューをユーザーが取得できるように、この領域にアイコンを提供します。

 環境レベルの通知は、Windows の通知領域ではなく、Visual Studio 通知ハブで表示する必要があります。

#### <a name="notification-bubbles"></a><a name="BKMK_NotificationBubbles"></a>通知の泡
 通知のバブルは、エディターまたはデザイナー内で情報として表示されるか、Windows 通知領域の一部として表示されます。 ユーザーは、これらのバブルを後で解決できる問題と認識し、重要でない通知の利点です。 バブルは、ユーザーがすぐに解決しなければならない重要な情報には不適切です。 Visual Studio で通知バブルを使用する場合は[、Windows デスクトップのガイダンス](/windows/desktop/uxguide/mess-notif)に従って通知バブルを表示します。

 ![通知バブル](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901-07_NotificationBubbles")

 **Visual Studio で使用される Windows の通知領域の通知のバブル**

## <a name="progress-indicators"></a><a name="BKMK_ProgressIndicators"></a>進捗インジケータ

### <a name="overview"></a>概要
 進捗状況インジケータは、ユーザーのフィードバックを与えるために、通知システムの重要な部分です。 プロセスと操作がいつ完了するかをユーザーに伝えます。 使い慣れたインジケーターの種類には、進行状況バー、回転するカーソル、アニメーションアイコンなどがあります。 進行状況インジケーターの種類と配置は、報告対象やプロセスまたは操作の完了にかかる時間など、コンテキストによって異なります。

#### <a name="factors"></a>考慮すべき要素
 どの指標タイプが適切かを判断するには、以下の要因を決定する必要があります。

1. **タイミング:** 操作にかかる時間の長さ

2. **モダリティ:** 操作が環境に対してモーダルであるかどうか (プロセスが完了するまで UI をロックします)

3. **持続/過渡:** 進行状況の最終結果を後で報告および表示可能にするかどうか

4. **確定/不定:** 工程終了時間と進捗を計算できるかどうか

5. **グラフィック/テキストの場所:** 進行状況またはプロセスがインラインでキャプチャされるか、メッセージの本文に含まれているか、Tree コントロールなどの特定のコントロールにキャプチャされるか

6. **近接:** 進行状況が関連する UI に近接する必要があるかどうか。 (たとえば、遠く離れている可能性があるステータス バーに入れるか、プロセスを起動したボタンの近くにある必要がありますか。

#### <a name="determinate-progress"></a>進行状況の確定

|進捗タイプ|使用するタイミングと方法|Notes|
|-------------------|-------------------------|-----------|
|プログレス バー (確定)|予想される>の時間は 5 秒です。<br /><br /> プロセスの詳細に関するテキストの説明を含めることができます。|アニメーションにテキストを埋め込**むのはやめないでください**。|
|情報バー|コンテキスト UI に関連付けられたメッセージング。 [「インフォバー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。<br /><br /> プロセスの詳細に関するテキストの説明を含めることができます。|複数**のプロセスを**示す必要がある場合は、複数の情報バーを使用しないでください。 代わりに、積み上げプログレスバーを使用してください。|
|[出力ウィンドウ]|一時的な通知: ユーザーが完了後の詳細を**確認**する必要があるアプリ レベルのプロセス。|ユーザーが後でデータを参照する必要がある場合は使用**しないでください**。|
|ログ ファイル|完了後に詳細を**保存**することが重要な場合に非一時的な通知と組み合わせられます。||
|ステータス バー|一時的な通知: ユーザーが完了後の詳細を**必要としない**アプリ レベルのプロセス。<br /><br /> 埋め込みプログレスバーが含まれています。<br /><br /> プロセスの詳細に関するテキストの説明を含めることができます。||

#### <a name="indeterminate-progress"></a>不確定な進行状況

|進捗タイプ|使用するタイミングと方法|Notes|
|-------------------|-------------------------|-----------|
|プログレス バー (不確定)|予想される>の時間は 5 秒です。<br /><br /> プロセスの詳細に関するテキストの説明を含めることができます。|アニメーションにテキストを埋め込**むのはやめないでください**。|
|アリ (アニメーション水平ドット)|サーバーへのラウンド トリップ。<br /><br /> 親コンテナーの上端にコンテキストの近くに配置されます。|コンテナ全体で親にされていない場合は使用**しないでください**。|
|スピナー(プログレスリング)|コンテキスト UI に関連付けられたプロセス、またはスペースが考慮される場所。<br /><br /> プロセスの詳細に関するテキストの説明を含めることができます。||
|情報バー|コンテキスト UI に関連付けられたメッセージング。 [「インフォバー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。|複数**のプロセスを**示す必要がある場合は、複数の情報バーを使用しないでください。 代わりに、積み上げプログレスバーを使用してください。|
|[出力ウィンドウ]|一時的な通知: ユーザーが完了後の詳細を**確認**する必要があるアプリ レベルのプロセス。|セッション間で保持する必要がある情報には使用**しないでください**。|
|ログ ファイル|完了後に詳細を**保存**することが重要な場合に非一時的な通知と組み合わせられます。||
|ステータス バー|一時的な通知: ユーザーが完了後の詳細を**必要としない**アプリ レベルのプロセス。<br /><br /> 埋め込みプログレスバーが含まれています。<br /><br /> プロセスの詳細に関するテキストの説明を含めることができます。||

### <a name="progress-indicator-types"></a>進行状況インジケーターの種類

#### <a name="progress-bars"></a>プログレスバー

##### <a name="indeterminate"></a>不確定
 ![進行状況不定バー](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901-04_Indeterminate")

 **進行状況不定バー**

 「不確定」とは、操作またはプロセスの全体的な進行状況を判断できないことを意味します。 無制限の時間を必要とする操作や、未知の数のオブジェクトにアクセスする操作には、不確定な進行状況バーを使用します。 何が起こっているかに付随するテキストの説明を使用します。 タイムアウトを使用して、時間ベースの操作に制限を与えます。 不確定な進行状況バーは、アニメーションを使用して進行状況が作成されていることを示しますが、その他の情報は提供しません。 精度の欠如のみに基づいて不確定な進行状況バーを選択しないでください。

##### <a name="determinate"></a>確定
 ![確定した進行状況バー](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901-05_Determinate")

 **確定した進行状況バー**

 「確定」とは、その時間を正確に予測できない場合でも、工程またはプロセスに限られた時間が必要であることを意味します。 完了を明確に示します。 操作が完了しない限り、進行状況バーを 100% に設定しないでください。 プログレス バーアニメーションの終了は、0 から 100% に左から右へ移動します。

 操作中に進行状況インジケーターを後方に移動しないでください。 バーは、操作が開始されると着実に前進し、終了すると100%に達するはずです。 進行状況バーのポイントは、操作全体にかかる時間を、必要な手順の数に関係なくユーザーに知らせます。

##### <a name="concurrent-reporting-stacked-progress-bars"></a>同時レポート (積み上げ進行状況バー)
 操作に時間がかかる場合 (おそらく数分) は、2 つの進行状況バーを使用できます。 たとえば、セットアップ プログラムが多数のファイルをコピーしている場合、1 つの進行状況バーを使用して、プロセス全体にかかる時間を示すことができます。 スタックされた進行状況バーを使用して、5 つ以上の同時操作またはプロセスを報告しないでください。 レポートする操作またはプロセスが 5 つ以上ある場合は、[キャンセル] ボタンを備えたモーダル ダイアログを使用し、進行状況の詳細を出力ウィンドウに報告します。

##### <a name="textual-descriptions"></a>テキストの説明
 何が起こっているかと完了までの推定時間に付随するテキストの説明を使用します。 操作にかかる時間を判断できない場合は、進行状況バーではなく、アニメーションアイコンを使用することをお望みの選択肢として使用できます。

 Visual Studio には、Visual Studio に統合された任意の製品で使用できるステータス バーに標準の進行状況バーが用意されています。 プログレス バーのアニメーション中に何が起こっているかのテキストの説明の場合、ステータス バーのテキストを更新できます。

#### <a name="other-progress-indicators"></a>その他の進行状況インジケータ

##### <a name="ants-animated-horizontal-dots"></a>アリ (アニメーション水平ドット)
 ![進行状況 Ant](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903-01_Ants")

 「アリ」は、アニメーション化された水平ドットで、不確定な往復サーバープロセスの視覚的な参照を提供します。

##### <a name="spinner-progress-ring"></a>スピナー(プログレスリング)
 ![進行状況スピナー](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903-02_Spinner")

 スピナー (「進行状況リング」とも呼ばれる) は、主にコンテキスト UI に関連して使用される不確定な進行状況インジケーターです。 テキストカテゴリヘッダー、メッセージング、コントロールなど、関連するコンテンツの近くにスピナーを表示します。

##### <a name="cursor-feedback"></a>カーソルフィードバック
 2 ~ 7 秒の間の操作については、カーソルのフィードバックを提供します。 通常、これはオペレーティング システムによって提供される待機カーソルを使用する意味です。 ガイダンスについては、MSDN の記事[Cursors.Wait プロパティを参照してください](/dotnet/api/system.windows.input.cursors.wait)。

#### <a name="progress-indicator-locations"></a>進行状況インジケーターの場所

##### <a name="status-bar"></a>ステータス バー
 ステータス バーを使用すると、アプリケーションはユーザーの作業を中断することなく、メッセージや有益な情報をユーザーに表示できます。 通常、ウィンドウの下部に表示される進行状況は、進行状況バーインジケーターと組み合わせて進行状況の測定に関するメッセージを含むツール ヒント ウィンドウになります。

 ![進行状況バー付きのステータス バー](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903-03_StatusBarProgressBar")

 **進行状況バー付きのステータス バー**

 ![メッセージング付きのステータス バー](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903-04_StatusBarMessage")

 **テキストの説明を含むステータス バー**

##### <a name="infobar"></a>情報バー
 ステータス バーと同様に、情報バーにはコンテキスト通知とメッセージングが表示され、進行状況バーやスピン ボタンなどの不確定な進行状況インジケーターと組み合わせることもできます。 情報バーは、詳細レベルの進行状況や確定進捗の表示を提供すべきではありません。 [「インフォバー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)」を参照してください。

 ![進行状況バーとメッセージング付きの情報バー](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903-05_InfoBar")

 **進行状況バーとテキストの説明を含む情報バー**

 ![ウィンドウ内の情報バー](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903-06_InfoBarInWindow")

##### <a name="inline"></a>インライン
 インライン進行状況の表示は、進行状況ローダーの種類によって表すことができます。 通常、進行状況インジケーターはメッセージングと組み合わせられますが、これは必須ではありません。

 ![インラインの進行状況スピナー](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903-07_InlineSpinner")

 **テキストの説明と組み合わせたスピナー**

 ![インラインの積み上げ進行状況バー](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903-08_InlineStackedProgress")

 **積み上げプログレス バーの確定**

 ![インラインの進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903-09_InlineText")

 **サーバー エクスプローラーのインライン テキスト: 更新します。**

##### <a name="tool-windows"></a>ツール ウィンドウ
 グローバル進捗状況表示は、ツールバーの直下に位置する不確定な進行状況バーで表されます。

 ![グローバルで不確定な進行状況バー](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903-23_GlobalIndeterminate")

 **チーム エクスプローラーのグローバル不確定進行状況バー**

##### <a name="dialogs"></a>ダイアログ
 ダイアログには、進行状況ローダーの種類を含めることができます。 進行状況インジケーターは、メッセージングと組み合わせて、複数レベルの進行状況表示と組み合わせて、細かいプロセスとサブプロセスを表すことができます。

 ![複数の種類の進行状況インジケーターがあるダイアログ](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903-11_Dialog")

 **同時実行プロセスと複数の進行状況インジケーターの種類を持つ Visual Studio ダイアログ**

 ![進行状況ローダーとメッセージングを含むダイアログ](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903-12_Dialog2")

 **プログレス ローダーとメッセージングのインライン コマンドを使用した Visual Studio ダイアログ**

##### <a name="document-well"></a>よく文書化する
 ドキュメントウェルは、コントロールと組み合わせて複数のプログレスローダータイプを表示できます。

 ![ドキュメント ウェル内の進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903-13_DocumentWell")

 **ツールバーの下の不確定進行状況バー**

##### <a name="output-window"></a>[出力ウィンドウ]
 出力ウィンドウは、インライン・テキスト・メッセージングを介してプロセスの進行と進行中の進捗状況を処理するのに適しています。 [ステータス バー] は、出力ウィンドウの進行状況レポートと共に使用する必要があります。

 ![出力ウィンドウ内の進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903-14_OutputWindow")

 **進行中のプロセスステータスと待機メッセージを含む出力ウィンドウ**

## <a name="infobars"></a><a name="BKMK_Infobars"></a>インフォバー

### <a name="overview"></a>概要
 インフォバーは、ユーザーに注意点に近いインジケータを提供し、共有情報バー コントロールを使用すると、外観と操作の一貫性を確保します。

 ![情報バー](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **ビジュアル スタジオの情報バー**

#### <a name="appropriate-uses-for-an-infobar"></a>情報バーの適切な用途

- 現在のコンテキストに関連する非ブロッキングで重要なメッセージをユーザーに与える

- UI が特定の状態または状態で、履歴デバッグなど、相互作用に影響を与えることを示す場合

- 拡張機能がパフォーマンスの問題を引き起こしている場合など、システムが問題を検出したことをユーザーに通知するには

- ファイルにタブとスペースが混在していることをエディタが検出した場合など、ユーザーが簡単に操作を実行できるようにする

##### <a name="do"></a>次の処理が必要です。

- 情報バーのメッセージ テキストを短く、ポイントに保ちます。

- リンクやボタンのテキストを簡潔に保ちます。

- ユーザーに提供する「アクション」オプションが最小限で、必要なアクションのみが表示されるようにします。

##### <a name="dont"></a>できません：

- 情報バーを使用して、ツールバーに配置する必要がある標準コマンドを提供します。

- モーダル ダイアログの代わりに情報バーを使用します。

- ウィンドウの外側にフローティング メッセージを作成します。

- 同じウィンドウ内の複数の場所で複数の情報バーを使用します。

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>複数の情報バーを同時に表示できますか?
 はい、複数の情報バーを同時に表示できます。 これらは先着順で表示され、最初の情報バーが上部に表示され、追加の情報バーが下に表示されます。

 ユーザーには一度に最大 3 つの情報バーが表示され、その後、さらに多くの情報バーが使用可能な場合、情報バー領域はスクロール可能になります。

### <a name="creating-an-infobar"></a>情報バーの作成
 情報バーには、左から右へ 4 つのセクションがあります。

- **アイコン:** このダイアログ ボックスでは、情報バーに表示するアイコン (警告アイコンなど) を追加します。

- **テキスト:** 必要に応じて、ユーザーが入力しているシナリオ/シチュエーションを説明するテキストと、テキスト内のリンクを追加できます。 テキストを簡潔に保つことを忘れないでください。

- **アクション:** このセクションには、ユーザーが情報バーで実行できるアクションのリンクとボタンが含まれている必要があります。

- **閉じるボタン:** 右側の最後のセクションには閉じるボタンがあります。

#### <a name="creating-a-standard-infobar-in-managed-code"></a>マネージ コードでの標準情報バーの作成
 InfoBarModel クラスを使用して、情報バーのデータ ソースを作成できます。 次の 4 つのコンストラクターのいずれかを使用します。

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(IEnumerable<IVsInfoBarTextSpan> textSpans, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);

```

```
public InfoBarModel(string text, IEnumerable<IVsInfoBarActionItem> actionItems, ImageMoniker image = default(ImageMoniker), bool isCloseButtonVisible = true);
```

 ハイパーリンク、アクション ボタン、およびアイコンを持つテキストを含む InfoBarModel を作成する例を次に示します。

 ![ハイパーリンクを含むページ](../../extensibility/ux-guidelines/media/0904-02_infobarhyperlink.png "0904-02_InfobarHyperlink")

```
var infoBar = new InfoBarModel(
    textSpans: new[]
    {
        new InfoBarTextSpan("This is a "),
        new InfoBarHyperlink("hyperlink"),
        new InfoBarTextSpan(" InfoBar.")
    },
    actionItems: new[]
    {
        new InfoBarButton("Click Me")
    },
    image: KnownMonikers.StatusInformation,
    isCloseButtonVisible: true);

```

#### <a name="creating-a-standard-infobar-in-native-code"></a>ネイティブ コードでの標準情報バーの作成
 ネイティブ コードから情報バーを提供するために IVsInfoBar インターフェイスを実装します。

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>情報バーからの情報バー UIElement の取得
 インフォバーモデルまたは IVsInfoBar の実装は、UI に表示されるために UIElement に変換する必要があるデータ モデルです。 サービスを取得できます。

```
private bool TryCreateInfoBarUI(IVsInfoBar infoBar, out IVsInfoBarUIElement uiElement)
{
    IVsInfoBarUIFactory infoBarUIFactory = serviceProvider.GetService(typeof(SVsInfoBarUIFactory)) as IVsInfoBarUIFactory;
    if (infoBarUIFactory == null)
    {
        uiElement = null;
        return false;
    }

    uiElement = infoBarUIFactory.CreateInfoBar(infoBar);
    return uiElement != null;
}
```

### <a name="placement"></a>配置
 インフォバーは、次の 1 つ以上の場所に表示できます。

- ツール ウィンドウ

- ドキュメントタブ内

> [!IMPORTANT]
> グローバル コンテキストに関するメッセージを表示するように情報バーを配置できます。 これは、ツールバーとドキュメントウェルの間に表示されます。 これは、IDE の "ジャンプとジャーク" に問題が発生し、絶対に必要かつ適切でない限り避ける必要があるため、お勧めできません。

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>ツール ウィンドウ ウィンドウに情報バーを配置する
 ツール ウィンドウ ウィンドウに情報バーを追加するのには、ツール ウィンドウウィンドウ.AddInfoBar (IVsInfoBar) メソッドを使用できます。 この API は、IVsInfoBar (情報バーモデルは既定の実装) または IVsUIElement を追加できます。

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>文書または非ツール ウィンドウ ウィンドウに情報バーを配置する
 任意の IVsWindowFrame に情報バーを配置するには、VSFPROPID_InfoBarHost プロパティを使用して、フレームの IVsInfoBarHost を取得し、情報バーの UIElement を追加します。

```
private void AddInfoBar(IVsWindowFrame frame, IVsUIElement uiElement)
{
    IVsInfoBarHost infoBarHost;
    if (TryGetInfoBarHost(frame, out infoBarHost))
    {
        infoBarHost.AddInfoBar(uiElement);
    }
}
private bool TryGetInfoBarHost(IVsWindowFrame frame, out IVsInfoBarHost infoBarHost)
{
    object infoBarHostObj;
    if (ErrorHandler.Failed(frame.GetProperty((int)__VSFPROPID7.VSFPROPID_InfoBarHost, out infoBarHostObj)))
    {
        infoBarHost = null;
        return false;
    }

    infoBarHost = infoBarHostObj as IVsInfoBarHost;
    return infoBarHost != null;
}

```

#### <a name="placing-an-infobar-in-the-main-window"></a>メイン ウィンドウに情報バーを配置する
 メイン ウィンドウに情報バーを配置するには、IVsShell サービスのVSSPROPID_MainWindowInfoBarHostを使用してメイン ウィンドウの IVsInfoBarHost を取得し、その情報バー UIElement を追加します。

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>ユーザーが自分の情報バーでアクションを実行するタイミングを知るでしょうか?
 はい、すべてのイベント アクションを情報バーの作成者に返します。 その後、情報バーのユーザーの選択に基づいて IDE でアクションを実行するのは、情報バーの作成者に対して行います。 情報バーは、閉じるボタンがクリックされたホストから自動的に削除されますが、閉じた後に他の情報バーを削除する必要がある場合は、追加の作業が必要です。 テレメトリは、各情報バーによって個別にログに記録する必要もあります。

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>ツール ウィンドウ ウィンドウでの情報バー イベントの受信
 ツールウィンドウ ペインには、インフォバー用の 2 つのイベントがあります。 InfoBarClosed イベントは、ツール ウィンドウ ウィンドウウィンドウの情報バーが閉じられたときに発生します。 情報バー内のハイパーリンクまたはボタンがクリックされると、イベントが発生します。

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>UIElement から情報バー イベントを直接受信する
 情報バーの UIElement から直接イベントをサブスクライブするために使用できます。 IVsInfoBarUIイベントを実装すると、著者はクローズアンドクリックイベントを受け取ります。

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="error-validation"></a><a name="BKMK_ErrorValidation"></a>エラーの検証
 ユーザーが、必須フィールドがスキップされたり、データが誤った形式で入力されたりした場合など、受け入れられない情報を入力する場合は、ブロックポップアップ エラー ダイアログを使用するのではなく、コントロールの近くでコントロールの検証やフィードバックを使用することをおしいます。

### <a name="field-validation"></a>Field validation
 フォームとフィールドの検証は、コントロール、アイコン、ツールヒントの 3 つのコンポーネントで構成されます。 いくつかの種類のコントロールがこれを使用できますが、テキスト ボックスが例として使用されます。

 ![フィールドの検証&#40;空白の&#41;](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905-01_FieldValidation")

 フィールドが必須の場合は、**\<必要な>** を示す透かしテキストがあり、フィールドの背景は淡い黄色 (VSColor: `Environment.ControlEditRequiredBackground`) で、前景は`Environment.ControlEditRequiredHintText`灰色 (VSColor: ) にする必要があります。

 !["必須" のラベルを持つフィールドの検証](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905-02_FieldValidationRequired")

 プログラムは、フォーカスが別のコントロールに移動したとき、またはユーザーが [OK] のコミット ボタンをクリックしたとき、またはユーザーがドキュメントまたはフォームを保存したときに、コントロールが*無効なコンテンツ*の状態であることを判断できます。

 無効なコンテンツの状態が確認されると、コントロール内または横にアイコンが表示されます。 エラーを説明するツールヒントは、アイコンまたはコントロールのホバー時に表示されます。 さらに、無効な状態を作成しているコントロールの周囲に 1 ピクセルの境界線が表示されます。

 ![フィールドの検証のレイアウトの仕様](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905-03_LayoutSpecs")

 **フィールド検証のレイアウト仕様**

#### <a name="acceptable-variations-for-icon-location"></a>アイコンの場所に対して許容されるバリエーション
 検証エラーについてユーザーに通知する必要がある、数え切れないほどのユニークなケースがあります。 UI のコントロールの種類と構成を考慮して、状況に応じて適切なアイコンの配置を選択します。

 ![アイコンの場所の適切な場所](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905-04_IconLocation")

 **フィールド検証アイコンの場所に対して許容されるバリエーション**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>サーバーまたはネットワーク接続へのラウンド トリップを必要とする検証
 場合によっては、サーバーへのラウンド トリップでコンテンツを確認する必要があり、ユーザーの進行状況、検証済み、およびエラー状態を示す必要があります。 下の図は、このケースと推奨される UI の例を示しています。

 ![サーバーへのラウンド トリップに関連する検証](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905-05_RoundTrip")

 **サーバーへのラウンド トリップに関連する検証**

 コントロールの右側に十分な空き領域を確保する必要があることに注意してください。「再試行」テキストを表示します。

#### <a name="in-place-warning-text"></a>インプレース警告テキスト
 エラー状態のコントロールにエラー メッセージを配置できる余地がある場合は、ツールヒントを単独で使用する方が適しています。

 ![&#45;場所の警告](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905-06_InPlaceWarning")

 **インプレース警告テキスト**

#### <a name="watermarks"></a>透かし
 コントロール全体またはウィンドウ全体がエラー状態である場合があります。 この状況では、エラーを示すウォーターマークを使用します。

 ![透かし](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **透かしフィールドの検証**
