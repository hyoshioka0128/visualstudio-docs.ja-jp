---
title: Visual Studio の通知と進行状況 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f0ef65e9-0f1f-45f4-9f25-6e2398691168
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f6a7ddd5d1a5a7257617b03098722e1341017b6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699884"
---
# <a name="notifications-and-progress-for-visual-studio"></a>Visual Studio の通知と進行状況
## <a name="notification-systems"></a><a name="BKMK_NotificationSystems"></a> 通知システム

### <a name="overview"></a>概要
 Visual Studio でのソフトウェア開発タスクに関して何が起こっているかをユーザーに通知するには、いくつかの方法があります。

 任意の種類の通知を実装する場合:

- **通知の数は、有効な最小数まで保持して** ください。 通知メッセージは、Visual Studio の大半のユーザー、または特定の機能または機能領域のユーザーに適用する必要があります。 通知を過剰に使用すると、ユーザーが追跡しやすくなり、システムの使いやすさが低下する可能性があります。

- より複雑な選択肢を作成し、さらにアクションを実行するために、ユーザーが適切なコンテキストを呼び出すために使用できる **、明確で実用的なメッセージを提示していることを確認**します。

- **同期メッセージと非同期メッセージを適切に表示します。** 同期通知は、web サービスがクラッシュした場合やコードの例外がスローされた場合など、早急に対処する必要があることを示します。 ユーザーは、モーダルダイアログボックスなどの入力を必要とする方法で、これらの状況をすぐに通知する必要があります。 非同期通知とは、ユーザーが認識しておく必要があるが、ビルド操作が完了したときや web サイトの配置が終了したときなど、すぐに実行する必要がないことを指します。 これらのメッセージは、ユーザーのタスクフローを中断するのではなく、よりアンビエントである必要があります。

- モーダルダイアログを使用するのは、ユーザーがメッセージを受信確認する前に、またはダイアログで決定を行う前に **、さらにアクションを実行できないようにするためだけです**。

- **アンビエント通知が無効になったときに削除します。** 通知された問題に対処するアクションが既に実行されている場合は、ユーザーに通知を閉じるように要求しないでください。

- **通知によって、誤った相関関係が発生する可能性があることに注意してください。** 実際には、1つまたは複数のアクションによって通知がトリガーされたと考えられる可能性があります。これは、実際には因果関係がなかったことです。 通知のコンテキスト、トリガー、および送信元に関する通知メッセージを明確にします。

### <a name="choosing-the-right-method"></a>適切メソッドの選択
 この表を使用すると、メッセージをユーザーに通知する適切な方法を選択できます。

|Method|用途|使用しない|
|------------|---------|----------------|
|[モーダルエラーメッセージダイアログ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ModalErrorMessageDialogs)|続行する前にユーザーの応答が必要な場合は、を使用します。|ユーザーをブロックしてフローを中断する必要がない場合は、を使用しないでください。 メッセージを別の非侵入的な方法で表示できる場合は、モーダルダイアログを使用しないようにします。|
|[IDE のステータスバー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_IDEStatusBar)|プロセスの状態に関するアンビエントテキスト情報がある場合は、を使用します。|単独で使用しないでください。 別のフィードバックメカニズムと組み合わせて使用することをお勧めします。|
|[埋め込まれた情報バー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedInfobar)|ツールウィンドウまたはドキュメントウィンドウで、を使用して進行状況、エラー状態、結果、または実行可能な情報を通知します。|情報が情報バーが配置されている場所に関連していない場合は、を使用しないでください。<br /><br /> ドキュメント/ツールウィンドウの外部では使用しないでください。|
|[マウスカーソルの変更](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_MouseCursorChanges)|は、プロセスが進行中であることを通知するために使用できます。 また、マウスの状態が変化していることを通知するためにも使用されます。たとえば、ドラッグアンドドロップが進行中の場合や、マウスカーソルが特定のモード (描画モードなど) にある場合などです。|短い進行状況を変更する場合や、カーソルの揺れるの可能性が高い場合 (たとえば、プロセス全体ではなく、実行時間の長いプロセスの一部に関連付けられている場合など) は、を使用しないでください。|
|[進行状況インジケーター](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotSysProgressIndicators)|進行状況を報告する必要がある場合は、を使用します (確定的または不確定)。 さまざまな進行状況インジケーターの種類と、それぞれに固有の使用法があります。 「 [進行状況インジケーター](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators)」を参照してください。||
|[Visual Studio の通知ウィンドウ](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_VSNotificationsToolWindow)|[通知] ウィンドウは、パブリックに拡張できません。 ただし、Visual Studio に関するメッセージの範囲を伝えるために使用されます。これには、ライセンスに関する重要な問題や、Visual Studio またはパッケージの更新に関する情報通知が含まれます。|他の種類の通知には使用しないでください。|
|[エラー一覧](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ErrorList)|問題が現在開いているソリューションに直接関連して問題が発生している場合 (エラー/警告/情報)、コードの操作を実行することが必要になる場合があります。<br /><br /> たとえば、次のようになります。<br /><br /> -コンパイラメッセージ (エラー/警告/情報)<br /><br /> -コードに関するコードアナライザー/診断メッセージ<br /><br /> -ビルドメッセージ<br /><br /> は、プロジェクトファイルまたはソリューションファイルに関連する問題に適している場合がありますが、最初にソリューションエクスプローラーを示すことを検討してください。|ユーザーのオープンソリューションコードとの関係がない項目には使用しないでください。|
|エディターの通知: 電球|開いているファイルに存在する問題を解決できる修正プログラムがある場合は、を使用します。<br /><br /> 電球は、リファクタリングなど、ユーザーのコードに対して実行されるクイックアクションをホストするためにも使用する必要がありますが、その場合は "通知スタイル" と表示されないことに注意してください。|開いているファイルとの関係がない項目には使用しないでください。|
|エディターの通知: 波線|を使用すると、開いているコードの特定の範囲に関する問題 (たとえば、エラーの赤い波線) についてユーザーに通知できます。|開いているコードの特定の範囲に関連しない項目には、を使用しないでください。|
|[埋め込みステータスバー](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_EmbeddedStatusBars)|特定のツールウィンドウ、ドキュメントウィンドウ、またはダイアログウィンドウのコンテキスト内でコンテンツまたはプロセスに関連する状態を提供するために使用します。|一般的な製品通知、プロセス、または特定のウィンドウ内のコンテンツに関係のない項目には使用しないでください。|
|[Windows トレイの通知](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_WindowsTray)|を使用すると、アウトプロセスプロセスやコンパニオンアプリケーションの通知を画面に出力できます。|IDE に関連する通知には使用しないでください。|
|[通知のバブル](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_NotificationBubbles)|を使用すると、リモートプロセスを通知したり、IDE の **外部** で変更したりできます。|IDE **内** のプロセスをユーザーに通知するための手段としてを使用しないでください。|

### <a name="notification-methods"></a>通知方法

#### <a name="modal-error-message-dialogs"></a><a name="BKMK_ModalErrorMessageDialogs"></a> モーダルエラーメッセージダイアログ
 モーダルエラーメッセージダイアログを使用して、ユーザーの確認または操作を必要とするエラーメッセージを表示します。

 ![モーダル エラー メッセージ](../../extensibility/ux-guidelines/media/0901-01_modalerrormessage.png "0901-01_ModalErrorMessage")

 **データベースへの無効な接続文字列のユーザーを警告するモーダルエラーメッセージダイアログ**

#### <a name="ide-status-bar"></a><a name="BKMK_IDEStatusBar"></a> IDE のステータスバー
 ユーザーがステータスバーのテキストに通知する可能性は、Windows プラットフォームのすべての周囲のコンピューターエクスペリエンスと特定のエクスペリエンスに関連しています。 Visual Studio の顧客ベースは両方の分野で経験する傾向がありますが、知識のある Windows ユーザーがステータスバーの変更を見逃してしまう可能性があります。 そのため、ステータスバーは、情報のために使用するか、別の場所に表示される情報の冗長なキューとして使用することをお勧めします。 ユーザーがすぐに解決する必要がある重要な情報は、ダイアログまたは [通知] ツールウィンドウに表示されます。

 Visual Studio のステータスバーは、複数の種類の情報を表示できるように設計されています。 フィードバック、デザイナー、進行状況バー、アニメーション、およびクライアントのリージョンに分割されます。

 フィードバック領域とデザイナー領域は常に表示されます。 進行状況バーとアニメーション領域は常に動的で、ユーザーコンテキストに基づいています。 デザイナー領域の幅は、テキストメッセージに付随するリソースから取得された文字列の長さによって決まります。 これにより、コードを変更しなくても、幅のサイズをローカライズできます。 英語の場合、この文字列の幅は約220ピクセルです。 デザイナー領域は正常に動作し、フィードバック領域は残りの領域を吸収します。

 また、IDE がデバッグモードである場合など、さまざまな IDE の状態の変更を伝達することによって、ビジュアルの関心と機能の値を追加するために、ステータスバーも色分けされています。

 ![IDE ステータス バーの色の変更](../../extensibility/ux-guidelines/media/0901-02_idestatusbar.png "0901-02_IDEStatusBar")

 **IDE のステータスバーの色**

#### <a name="embedded-infobar"></a><a name="BKMK_EmbeddedInfobar"></a> 埋め込まれた情報バー
 ドキュメントウィンドウまたはツールウィンドウの上部にある情報バーを使用して、状態または条件をユーザーに通知することができます。 また、コマンドを提供することで、ユーザーが簡単にアクションを実行できるようにすることもできます。 情報バーは標準のシェルコントロールです。 独自のを作成するのは避けてください。独自の機能は、IDE 内の他のユーザーと矛盾していて表示されます。 実装の詳細と使用方法のガイダンスについては、「 [Infobob」](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars) を参照してください。

 ![埋め込まれた情報バー](../../extensibility/ux-guidelines/media/0901-03_embeddedinfobar.png "0901-03_EmbeddedInfobar")

 **ドキュメントウィンドウに埋め込まれた情報バー。 IDE がデバッグ履歴モードであることをユーザーに警告します。エディターは、標準デバッグモードの場合と同じように応答しません。**

#### <a name="mouse-cursor-changes"></a><a name="BKMK_MouseCursorChanges"></a> マウスカーソルの変更
 マウスカーソルを変更する場合は、VSColor サービスに関連付けられていて、既にカーソルに関連付けられている色を使用します。 カーソルの変更は、実行中の操作を示すために使用できます。また、ドラッグ、ドロップ、またはオブジェクトの選択に使用できるターゲットの上にユーザーがカーソルを置いたときのヒットゾーンも示します。

 使用可能なすべての CPU 時間が操作のために予約されている必要がある場合にのみ、ビジー/待機マウスカーソルを使用します。これにより、ユーザーはそれ以上の入力を表現できなくなります。 ほとんどの場合、マルチスレッドを使用しているアプリケーションを使用すると、ユーザーが他の操作を実行できない時間はめったに発生しません。

 カーソルの変更は、他の場所に表示される情報の冗長なキューとして有効であることに注意してください。 特にユーザーが対処する必要がある重要な情報を伝達しようとする場合は、カーソルの変更に依存しないようにしてください。

#### <a name="progress-indicators"></a><a name="BKMK_NotSysProgressIndicators"></a> 進行状況インジケーター
 進行状況インジケーターは、完了までに数秒以上かかるプロセス中にユーザーフィードバックを提供するために重要です。 進行状況インジケーターは、埋め込みステータスバー、モーダルダイアログボックス、または Visual Studio ステータスバーで、インプレースで (進行中のアクションの開始ポイントの近くに) 表示できます。 使用と実装については、 [進行状況インジケーター](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_ProgressIndicators) のガイダンスに従ってください。

#### <a name="visual-studio-notifications-window"></a><a name="BKMK_VSNotificationsToolWindow"></a> Visual Studio の通知ウィンドウ
 Visual Studio の [通知] ウィンドウでは、ライセンス、環境 (Visual Studio)、拡張機能、および更新プログラムについて開発者に通知します。 ユーザーは、個々の通知を無視したり、特定の種類の通知を無視することができます。 無視される通知の一覧は、[ **ツール > オプション** ] ページで管理されます。

 [通知] ウィンドウは現在拡張できません。

 ![Visual Studio の通知ウィンドウ](../../extensibility/ux-guidelines/media/0901-06_vsnotificationswindow.png "0901-06_VSNotificationsWindow")

 **Visual Studio 通知ツールウィンドウ**

#### <a name="error-list"></a><a name="BKMK_ErrorList"></a> エラー一覧
 エラー一覧内の通知は、コンパイル時またはビルド処理中に発生したエラーと警告を示し、ユーザーがコード内でその特定のコードエラーに移動できるようにします。

 ![エラー一覧](../../extensibility/ux-guidelines/media/0901-08_errorlist.png "0901-08_ErrorList")

 **Visual Studio のエラー一覧**

#### <a name="embedded-status-bars"></a><a name="BKMK_EmbeddedStatusBars"></a> 埋め込みステータスバー
 IDE のステータスバーは動的であり、クライアント領域のコンテキストがアクティブなドキュメントウィンドウに、ユーザーのコンテキストやシステムの応答に関する情報が更新されているため、情報を継続的に表示したり、長期間の非同期プロセスに状態を与えたりすることは困難です。 たとえば、IDE のステータスバーは、複数の実行や、すぐに実行可能な項目選択に対するテストの実行結果の通知には適していません。 このような状態情報は、ユーザーが選択を行ったりプロセスを開始したりするドキュメントまたはツールウィンドウのコンテキストで保持することが重要です。

 ![埋め込まれたステータス バー](../../extensibility/ux-guidelines/media/0901-09_embeddedstatusbar.png "0901-09_EmbeddedStatusBar")

 **Visual Studio の埋め込まれたステータスバー**

#### <a name="windows-tray-notifications"></a><a name="BKMK_WindowsTray"></a> Windows トレイの通知
 Windows の通知領域は、Windows タスクバーのシステムクロックの横にあります。 多くのユーティリティおよびソフトウェアコンポーネントにはこの領域のアイコンが用意されているため、ユーザーは画面の解像度の変更やソフトウェア更新プログラムの取得など、システム全体のタスクのコンテキストメニューを取得できます。

 環境レベルの通知は、Windows 通知領域ではなく、Visual Studio 通知ハブに表示されます。

#### <a name="notification-bubbles"></a><a name="BKMK_NotificationBubbles"></a> 通知のバブル
 通知バブルは、エディターまたはデザイナー内または Windows 通知領域の一部として、情報として表示できます。 ユーザーは、これらのバブルを後で解決できる問題として認識します。これは、重要でない通知の利点です。 バブルは、ユーザーがすぐに解決する必要がある重要な情報には適していません。 Visual Studio で通知バブルを使用する場合は、 [通知バブルの Windows デスクトップガイダンス](/windows/desktop/uxguide/mess-notif)に従ってください。

 ![通知バブル](../../extensibility/ux-guidelines/media/0901-07_notificationbubbles.png "0901-07_NotificationBubbles")

 **Visual Studio で使用される Windows 通知領域の通知バブル**

## <a name="progress-indicators"></a><a name="BKMK_ProgressIndicators"></a> 進行状況インジケーター

### <a name="overview"></a>概要
 進行状況インジケーターは、ユーザーからのフィードバックを提供するための通知システムの重要な部分です。 プロセスと操作が完了したことをユーザーに通知します。 使い慣れたインジケーターの種類には、進行状況バー、スピンカーソル、およびアニメーションアイコンが含まれます。 進行状況インジケーターの種類と配置は、報告されている内容や、プロセスまたは操作が完了するまでにかかる時間など、コンテキストによって異なります。

#### <a name="factors"></a>考慮すべき要素
 どのインジケーターの種類が適切であるかを判断するには、次の要素を決定する必要があります。

1. **タイミング:** 操作にかかる時間の長さ

2. **モダリティ:** 操作が環境に対してモーダル (プロセスが完了するまで UI をロックする) かどうかを指定します。

3. **Persistent/Transient:** 進行状況の最終的な結果を報告したり、後で表示したりする必要があるかどうか

4. **確定/不確定:** 操作終了時刻と進行状況を計算できるかどうか

5. **グラフィック/テキストの場所:** 進行状況またはプロセスをインラインでキャプチャするか、メッセージの本文に含めるか、またはツリーコントロールなどの特定のコントロールをキャプチャするかを指定します。

6. **近接:** 進行状況を、関連付けられている UI の近くに配置するかどうかを指定します。 (たとえば、ステータスバーには、遠く離れている場合もあれば、プロセスを起動したボタンの近くにある必要がある場合もあります)。

#### <a name="determinate-progress"></a>確定した進行状況

|進行状況の種類|使用するタイミングと方法|Notes|
|-------------------|-------------------------|-----------|
|進行状況バー (確定)|>5 秒の予想される期間。<br /><br /> プロセスの詳細の説明テキストを含めることができます。|テキストをアニメーションに埋め込ま**ない**でください。|
|情報バー|コンテキスト UI に関連付けられたメッセージング。 「 [Infobob」](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)を参照してください。<br /><br /> プロセスの詳細の説明テキストを含めることができます。|複数のプロセスを示す必要がある場合は、複数の infobobを使用**しない**でください。 代わりに、積み上げられた進行状況バーを使用してください。|
|[出力ウィンドウ]|一時的な通知: ユーザーが完了後にの詳細を **確認** するアプリレベルのプロセス。|ユーザーが後でデータを参照する必要がある場合は、を使用**しない**でください。|
|ログ ファイル|完了後に詳細を **保存** することが重要な場合に、intransient 通知と組み合わせて使用します。||
|ステータス バー|一時的な通知: ユーザーが完了後にの詳細を必要とし **ない** アプリレベルのプロセス。<br /><br /> 埋め込まれた進行状況バーを含みます。<br /><br /> プロセスの詳細の説明テキストを含めることができます。||

#### <a name="indeterminate-progress"></a>不確定の進行状況

|進行状況の種類|使用するタイミングと方法|Notes|
|-------------------|-------------------------|-----------|
|進行状況バー (不確定)|>5 秒の予想される期間。<br /><br /> プロセスの詳細の説明テキストを含めることができます。|テキストをアニメーションに埋め込ま**ない**でください。|
|アリ (水平方向のドット)|サーバーへのラウンドトリップ。<br /><br /> 親コンテナーの最上位に配置されます。|コンテナー全体で親を持たない場合は使用**しない**でください。|
|スピンボタン (進行状況のリング)|コンテキスト UI に関連付けられたプロセス、または領域が考慮される場所。<br /><br /> プロセスの詳細の説明テキストを含めることができます。||
|情報バー|コンテキスト UI に関連付けられたメッセージング。 「 [Infobob」](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)を参照してください。|複数のプロセスを示す必要がある場合は、複数の infobobを使用**しない**でください。 代わりに、積み上げられた進行状況バーを使用してください。|
|[出力ウィンドウ]|一時的な通知: ユーザーが完了後にの詳細を **確認** するアプリレベルのプロセス。|セッション間で永続化する必要がある情報には、を使用**しない**でください。|
|ログ ファイル|完了後に詳細を **保存** することが重要な場合に、intransient 通知と組み合わせて使用します。||
|ステータス バー|一時的な通知: ユーザーが完了後にの詳細を必要とし **ない** アプリレベルのプロセス。<br /><br /> 埋め込まれた進行状況バーを含みます。<br /><br /> プロセスの詳細の説明テキストを含めることができます。||

### <a name="progress-indicator-types"></a>進行状況インジケーターの種類

#### <a name="progress-bars"></a>進行状況バー

##### <a name="indeterminate"></a>Indeterminate
 ![進行状況不定バー](../../extensibility/ux-guidelines/media/0901-04_indeterminate.png "0901-04_Indeterminate")

 **進行状況不定バー**

 "不確定" は、操作またはプロセスの全体的な進行状況を判断できないことを意味します。 無制限の時間を必要とする操作や、不明な数のオブジェクトにアクセスする操作には、不確定な進行状況バーを使用します。 説明テキストを使用して、何が起こっているかを説明します。 タイムアウトを使用して、時間ベースの操作の範囲を指定します。 不確定な進行状況バーは、進行状況を示すためにアニメーションを使用しますが、その他の情報は提供しません。 精度が不十分な場合にのみ、不確定な進行状況バーを選択しないでください。

##### <a name="determinate"></a>Determinate
 ![確定した進行状況バー](../../extensibility/ux-guidelines/media/0901-05_determinate.png "0901-05_Determinate")

 **確定した進行状況バー**

 "確定" とは、その時間を正確に予測できない場合でも、操作またはプロセスに一定の時間がかかることを意味します。 完了を明確に示します。 操作が完了していない場合は、進行状況バーを100% にすることはできません。 確定した進行状況バーのアニメーションは、0 ~ 100% の左から右に移動します。

 操作中は、進行状況インジケーターを逆に移動しないでください。 操作が開始され、終了時に100% に到達すると、バーは徐々に進む必要があります。 進行状況バーのポイントは、関係しているステップの数に関係なく、操作全体の所要時間をユーザーに示すためのものです。

##### <a name="concurrent-reporting-stacked-progress-bars"></a>同時実行レポート (積み上げ進行状況バー)
 操作の実行に時間がかかる場合 (通常は数分)、2つの進行状況バーが使用されます。1つは操作の全体的な進行状況、もう1つは現在のステップの進行状況を示します。 たとえば、セットアッププログラムによって多数のファイルがコピーされている場合、1秒間に実行されている現在のファイルまたはディレクトリのパーセンテージを示すことができます。 スタックされた進行状況バーを使用して、同時に5つ以上の操作またはプロセスを報告しないでください。 レポート対象の同時実行またはプロセスが5つを超える場合は、[キャンセル] ボタンのあるモーダルダイアログボックスを使用して、進行状況の詳細を出力ウィンドウに報告します。

##### <a name="textual-descriptions"></a>説明テキスト
 説明文を使用して、発生している内容と完了までの推定所要時間を記述します。 操作の所要時間を判断できない場合は、フィードバックを提供するためのより良い選択肢が、進行状況バーではなく、アニメーション化されたアイコンである可能性があります。

 Visual Studio には、Visual Studio に統合されている任意の製品で使用できる標準の進行状況バーがステータスバーに用意されています。 プログレスバーがアニメーション化されている間に起こっていることについての説明テキストを表示するには、ステータスバーのテキストを更新します。

#### <a name="other-progress-indicators"></a>その他の進行状況インジケーター

##### <a name="ants-animated-horizontal-dots"></a>アリ (水平方向のドット)
 ![進行状況 Ant](../../extensibility/ux-guidelines/media/0903-01_ants.png "0903-01_Ants")

 "楕円" は、アニメーション化した水平ドットで、不確定ラウンドトリップサーバープロセスの視覚的な参照を提供します。

##### <a name="spinner-progress-ring"></a>スピンボタン (進行状況のリング)
 ![進行状況スピナー](../../extensibility/ux-guidelines/media/0903-02_spinner.png "0903-02_Spinner")

 スピンボタン ("進行状況のリング" とも呼ばれます) は、主にコンテキスト UI に関連して使用される不確定な進行状況インジケーターです。 テキストカテゴリのヘッダー、メッセージング、コントロールなど、関連するコンテンツに近接したスピンボタンを表示します。

##### <a name="cursor-feedback"></a>カーソルのフィードバック
 2-7 秒間にかかる操作の場合は、カーソルフィードバックを提供します。 通常、これはオペレーティングシステムによって提供される待機カーソルを使用することを意味します。 ガイダンスについては、MSDN の記事「cursor [. Wait プロパティ](/dotnet/api/system.windows.input.cursors.wait)」を参照してください。

#### <a name="progress-indicator-locations"></a>進行状況インジケーターの場所

##### <a name="status-bar"></a>ステータス バー
 ステータスバーでは、ユーザーの作業を中断することなく、ユーザーにメッセージや有用な情報を表示するための場所をアプリケーションに提供します。 通常、ウィンドウの下部に表示されます。進行状況の状態は、プログレスバーインジケーターとの組み合わせでの進行状況の測定に関するメッセージを含むツールヒントペインです。

 ![進行状況バー付きのステータス バー](../../extensibility/ux-guidelines/media/0903-03_statusbarprogressbar.png "0903-03_StatusBarProgressBar")

 **進行状況バー付きのステータス バー**

 ![メッセージング付きのステータス バー](../../extensibility/ux-guidelines/media/0903-04_statusbarmessage.png "0903-04_StatusBarMessage")

 **テキストの説明が表示されるステータスバー**

##### <a name="infobar"></a>情報バー
 ステータスバーと同様に、情報バーはコンテキストの通知とメッセージングを提供します。これは、進行状況バーやスピンボタンなどの不確定な進行状況インジケーターと組み合わせて使用することもできます。 詳細レベルの進捗状況や確定した進行状況を示す情報バーは使用できません。 「 [Infobob」](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md#BKMK_Infobars)を参照してください。

 ![進行状況バーとメッセージング付きの情報バー](../../extensibility/ux-guidelines/media/0903-05_infobar.png "0903-05_InfoBar")

 **進行状況バーとテキストの説明が表示された情報バー**

 ![ウィンドウ内の情報バー](../../extensibility/ux-guidelines/media/0903-06_infobarinwindow.png "0903-06_InfoBarInWindow")

##### <a name="inline"></a>インライン
 インラインの進行状況は、進行状況のローダーの種類によって表すことができます。 通常、進行状況インジケーターはメッセージングとペアになっていますが、これは必須ではありません。

 ![インラインの進行状況スピナー](../../extensibility/ux-guidelines/media/0903-07_inlinespinner.png "0903-07_InlineSpinner")

 **スピンボタンとテキストの説明の組み合わせ**

 ![インラインの積み上げ進行状況バー](../../extensibility/ux-guidelines/media/0903-08_inlinestackedprogress.png "0903-08_InlineStackedProgress")

 **確定した進行状況バー**

 ![インラインの進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-09_inlinetext.png "0903-09_InlineText")

 **インラインテキストのサーバーエクスプローラー: 更新しています...**

##### <a name="tool-windows"></a>ツール ウィンドウ
 グローバルな進行状況は、ツールバーのすぐ下に配置されている不確定な進行状況バーで表されます。

 ![グローバルで不確定な進行状況バー](../../extensibility/ux-guidelines/media/0903-23_globalindeterminate.png "0903-23_GlobalIndeterminate")

 **チームエクスプローラーグローバルで不確定な進行状況バー**

##### <a name="dialogs"></a>ダイアログ
 ダイアログには、進行状況のローダーの種類を含めることができます。 進行状況インジケーターは、メッセージングと組み合わせて使用することもできます。また、詳細な進行状況を示す複数レベルの進行状況を組み合わせて、詳細なサブプロセスを表現することもできます。

 ![複数の種類の進行状況インジケーターがあるダイアログ](../../extensibility/ux-guidelines/media/0903-11_dialog.png "0903-11_Dialog")

 **同時実行プロセスと複数の進行状況インジケーターの種類が表示された Visual Studio ダイアログ**

 ![進行状況ローダーとメッセージングを含むダイアログ](../../extensibility/ux-guidelines/media/0903-12_dialog2.png "0903-12_Dialog2")

 **進行状況ローダーとメッセージングインラインコマンド実行のある Visual Studio ダイアログ**

##### <a name="document-well"></a>ドキュメントウェル
 ドキュメントウェルでは、複数の進行状況ローダーの種類をコントロールと組み合わせて表示できます。

 ![ドキュメント ウェル内の進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-13_documentwell.png "0903-13_DocumentWell")

 **ツールバーの下の不確定の進行状況バー**

##### <a name="output-window"></a>[出力ウィンドウ]
 [出力] ウィンドウは、インラインテキストメッセージングによるプロセスの進行状況と進行中の進行状況の処理に適しています。 ステータスバーは、出力ウィンドウの進行状況レポートと共に使用する必要があります。

 ![出力ウィンドウ内の進行状況メッセージング](../../extensibility/ux-guidelines/media/0903-14_outputwindow.png "0903-14_OutputWindow")

 **進行中のプロセスの状態と待機メッセージを含む出力ウィンドウ**

## <a name="infobars"></a><a name="BKMK_Infobars"></a> 情報バー

### <a name="overview"></a>概要
 ユーザーは、注目するポイントの近くにインジケーターを提供し、共有された情報バーコントロールを使用して、視覚的な外観と対話性の一貫性を確保します。

 ![情報バー](../../extensibility/ux-guidelines/media/0904-01_infobar.png "0904-01_Infobar")

 **Visual Studio での infobobi**

#### <a name="appropriate-uses-for-an-infobar"></a>情報バーの適切な使用方法

- 現在のコンテキストに関連する、非ブロッキングの重要なメッセージをユーザーに付与するには

- UI が特定の状態または状態にあり、デバッグ履歴など、何らかの相互作用に影響を与えることを示すには

- 拡張機能によってパフォーマンスの問題が発生しているなど、システムによって問題が検出されたことをユーザーに通知するには

- ファイルにタブとスペースが混在していることがエディターによって検出された場合などに、ユーザーが簡単にアクションを実行できるようにするには

##### <a name="do"></a>次の処理が必要です。

- 情報バーのメッセージテキストを短く、そのポイントまで保持します。

- リンクとボタンにテキストを簡潔に保存します。

- ユーザーに対して指定する "アクション" オプションが最小限であることを確認し、必要なアクションのみを表示します。

##### <a name="dont"></a>できません：

- ツールバーに配置する必要がある標準コマンドを提供するには、情報バーを使用します。

- モーダルダイアログボックスの代わりに情報バーを使用します。

- ウィンドウ外にフローティングメッセージを作成します。

- 同じウィンドウ内の複数の場所で複数の情報バー使用します。

#### <a name="can-multiple-infobars-show-at-the-same-time"></a>複数の配信を同時に表示できますか。
 はい。複数の infobobを同時に表示できます。 これらの情報は、最初に表示される順に表示されます。最初の情報バーには、上部に表示される情報と、以下に示す追加の情報が表示されます。

 ユーザーには、一度に最大3つの情報が表示されます。その後、より多くの情報バー使用可能な場合は、情報バーの領域がスクロール可能になります。

### <a name="creating-an-infobar"></a>情報バーの作成
 情報バーには、左から右に4つのセクションがあります。

- **アイコン:** ここで、情報バーに表示するアイコン (警告アイコンなど) を追加します。

- **テキスト:** 必要に応じて、テキスト内のリンクと共に、ユーザーのシナリオや状況を説明するテキストを追加できます。 テキストは簡潔に保つようにしてください。

- **アクション:** このセクションには、ユーザーが情報バーで実行できるアクションのリンクとボタンが含まれている必要があります。

- **閉じるボタン:** 右側の最後のセクションには、[閉じる] ボタンを含めることができます。

#### <a name="creating-a-standard-infobar-in-managed-code"></a>マネージコードでの標準の情報バーの作成
 InfoBarModel クラスを使用すると、情報バーのデータソースを作成できます。 次の4つのコンストラクターのいずれかを使用します。

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

 次に示すのは、ハイパーリンク、アクションボタン、およびアイコンを含むテキストを使用して InfoBarModel を作成する例です。

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

#### <a name="creating-a-standard-infobar-in-native-code"></a>ネイティブコードでの標準の情報バーの作成
 ネイティブコードから情報バーを提供するために、IVsInfoBar バーインターフェイスを実装します。

```
public interface IVsInfoBar
{
    IVsInfoBarActionItemCollection ActionItems { get; }
    ImageMoniker Image { get; }
    bool IsCloseButtonVisible { get; }
    IVsInfoBarTextSpanCollection TextSpans { get; }
}

```

#### <a name="getting-an-infobar-uielement-from-an-infobar"></a>情報バーから情報バーを取得する
 InfoBarModel または IVsInfoBar の実装は、UI に表示するために UIElement に切り替える必要があるデータモデルです。 UIElement は、SVsInfoBarUIFactory/IVsInfoBarUIFactory サービスを使用して取得できます。

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
 Infobars、次の1つまたは複数の場所に表示できます。

- ツール ウィンドウ

- ドキュメントタブ内

> [!IMPORTANT]
> 情報バーを配置して、グローバルコンテキストに関するメッセージを表示することができます。 これは、ツールバーとドキュメントウェルの間に表示されます。 IDE の "jump and jerk" に関する問題が発生するため、この方法は推奨されません。絶対に必要かつ適切でない限り、回避する必要があります。

#### <a name="placing-an-infobar-in-a-toolwindowpane"></a>Createtoolwindow は toolwindowpane に情報バーを配置する
 Createtoolwindow は toolwindowpane (IVsInfoBar バー) メソッドを使用して、ツールウィンドウに情報バーを追加できます。 この API では、IVsInfoBar (InfoBarModel が既定の実装である)、または Ivsuielement 的を追加できます。

#### <a name="placing-an-infobar-in-a-document-or-non-toolwindowpane"></a>ドキュメントまたは非 Createtoolwindow は toolwindowpane に情報バーを配置する
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

#### <a name="placing-an-infobar-in-the-main-window"></a>メインウィンドウに情報バーを配置する
 メインウィンドウに情報バーを配置するには、IVsShell サービスの VSSPROPID_MainWindowInfoBarHost を使用してメインウィンドウの IVsInfoBarHost を取得し、そこに情報バーを追加します。

### <a name="will-i-know-when-the-user-takes-action-in-my-infobar"></a>ユーザーが自分の情報バーでアクションを実行したことがわかりますか。
 はい、すべてのイベントアクションを情報バーの作成者に返します。 次に、情報バーのユーザー選択に基づいて IDE でアクションを実行するための情報バーの作成者になります。 [閉じる] ボタンがクリックされたホストからは、[Ok] が自動的に削除されますが、終了後に他の infを削除する必要がある場合は、追加の作業が必要になります。 また、テレメトリは各情報バーによって個別にログに記録される必要があります。

#### <a name="receiving-infobar-events-in-a-toolwindowpane"></a>Createtoolwindow は toolwindowpane での情報バーイベントの受信
 Createtoolwindow は toolwindowpane には、2つのイベントがあります。 Createtoolwindow は toolwindowpane の情報バーが閉じたときに、InfoBarClosed イベントが発生します。 InfoBarActionItemClicked イベントは、情報バー内のハイパーリンクまたはボタンがクリックされたときに発生します。

#### <a name="receiving-infobar-events-directly-from-the-uielement"></a>UIElement からの情報バーイベントの直接受信
 IVsInfoBarUIElement. Advise を使用すると、情報バーの UIElement から直接イベントをサブスクライブできます。 IVsInfoBarUIEvents を実装すると、作成者は close イベントと click イベントを受け取ることができます。

```
public interface IVsInfoBarUIEvents
{
    void OnActionItemClicked(IVsInfoBarUIElement infoBarUIElement, IVsInfoBarActionItem actionItem);
    void OnClosed(IVsInfoBarUIElement infoBarUIElement);
}

```

## <a name="error-validation"></a><a name="BKMK_ErrorValidation"></a> エラーの検証
 必須フィールドがスキップされた場合や、データが不適切な形式で入力された場合など、ユーザーが受け入れられない情報を入力する場合は、コントロールの検証またはフィードバックを、ブロックポップアップエラーダイアログを使用するのではなく、コントロールの近くに使用することをお勧めします。

### <a name="field-validation"></a>Field validation
 フォームとフィールドの検証は、コントロール、アイコン、およびツールヒントの3つのコンポーネントで構成されています。 いくつかの種類のコントロールでこれを使用できますが、テキストボックスが例として使用されます。

 ![空白の&#41;&#40;フィールドの検証 ](../../extensibility/ux-guidelines/media/0905-01_fieldvalidation.png "0905-01_FieldValidation")

 フィールドが必須の場合は、ウォーターマークテキストが表示され、 **\<Required>** フィールドの背景が薄い黄色 (VSColor:) であり、 `Environment.ControlEditRequiredBackground` 前景が灰色 (vscolor:) である必要があり `Environment.ControlEditRequiredHintText` ます。

 !["必須" のラベルを持つフィールドの検証](../../extensibility/ux-guidelines/media/0905-02_fieldvalidationrequired.png "0905-02_FieldValidationRequired")

 プログラムは、フォーカスが別のコントロールに移動したとき、またはユーザーが [OK] コミットボタンをクリックしたとき、またはユーザーがドキュメントまたはフォームを保存したときに、コントロールが *無効なコンテンツ* として入力された状態であることを確認できます。

 無効なコンテンツの状態が決定されると、コントロール内またはその横にアイコンが表示されます。 アイコンまたはコントロールのいずれかにマウスポインターを置くと、エラーを説明するヒントが表示されます。 また、無効な状態を作成しているコントロールの周囲に1ピクセルの枠線が表示されます。

 ![フィールドの検証のレイアウトの仕様](../../extensibility/ux-guidelines/media/0905-03_layoutspecs.png "0905-03_LayoutSpecs")

 **フィールド検証のレイアウトの指定**

#### <a name="acceptable-variations-for-icon-location"></a>アイコンの場所に許容されるバリエーション
 検証エラーについてユーザーに通知する必要がある一意のケースがあります。 UI のコントロールの種類と構成を考慮して、状況に適したアイコンの配置を選択します。

 ![アイコンの場所の適切な場所](../../extensibility/ux-guidelines/media/0905-04_iconlocation.png "0905-04_IconLocation")

 **フィールド検証アイコンの場所で許容されるバリエーション**

#### <a name="validation-requiring-a-round-trip-to-a-server-or-network-connection"></a>サーバーまたはネットワーク接続へのラウンドトリップを必要とする検証
 場合によっては、サーバーへのラウンドトリップがコンテンツを確認する必要があります。また、ユーザーの進捗状況、検証済み、エラーの状態を表示することが重要になります。 次の図は、このケースと推奨される UI の例を示しています。

 ![サーバーへのラウンド トリップに関連する検証](../../extensibility/ux-guidelines/media/0905-05_roundtrip.png "0905-05_RoundTrip")

 **サーバーへのラウンド トリップに関連する検証**

 "検証しています..." を格納するためには、コントロールの右側に十分な空き領域を用意する必要があることに注意してください。「Retry」というテキストを入力します。

#### <a name="in-place-warning-text"></a>インプレース警告テキスト
 エラーメッセージをコントロールの近くに配置するための空き領域がある場合は、ツールヒントだけを使用することをお勧めします。

 ![&#45;位置の警告](../../extensibility/ux-guidelines/media/0905-06_inplacewarning.png "0905-06_InPlaceWarning")

 **インプレース警告テキスト**

#### <a name="watermarks"></a>透かし
 コントロールまたはウィンドウ全体がエラー状態になることがあります。 このような場合は、ウォーターマークを使用してエラーを示します。

 ![ウォーターマーク](../../extensibility/ux-guidelines/media/0905-07_watermark.png "0905-07_Watermark")

 **透かしフィールドの検証**
