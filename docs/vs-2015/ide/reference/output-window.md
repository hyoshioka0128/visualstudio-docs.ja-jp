---
title: '[出力] ウィンドウ | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.build.output
- vs.debug.output
- vs.output
helpviewer_keywords:
- Output window, about Output window
- Output window
- Toolbox, removing controls
ms.assetid: d8931d88-250e-4db4-963f-2c5b3e99b45f
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f17b91cc462b6f628100ffbf370fcdec2eb9888d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662198"
---
# <a name="output-window"></a>[出力] ウィンドウ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**[出力]** ウィンドウには、統合開発環境 (IDE: Integrated Development Environment) のさまざまな機能のステータス メッセージが表示されます。 **[出力]** ウィンドウを開くには、メニュー バーで、 **[表示]、[出力]** の順にクリックします (または、Ctrl キーと Alt キーを押しながら O キーを押します)。

> [!WARNING]
> [出力] ウィンドウは、Visual Studio Express エディションの [表示] メニューに表示されません。 このメニューを表示するには、ホット キーの Ctrl + Alt + O を使用します。

## <a name="toolbar"></a>ToolBar
 **出力元の表示**表示する1つ以上の出力ペインを表示します。 IDE のどのツールが **[出力]** ウィンドウを使用してユーザーにメッセージを配布するかに応じて、複数の情報ペインを使用できる場合があります。

 **コード内のメッセージの検索**コードエディター内のカーソル位置を、選択したビルドエラーを含む行に移動します。

 **前のメッセージにジャンプ** **出力**ウィンドウ内のフォーカスを前のビルドエラーに変更し、コードエディター内のカーソル位置をそのビルドエラーが含まれている行に移動します。

 **次のメッセージに進む** **出力**ウィンドウ内のフォーカスを次のビルドエラーに変更し、コードエディター内のカーソル位置をそのビルドエラーが含まれている行に移動します。

 **すべてクリア** **出力**ペインからすべてのテキストを削除します。

 **折り返しの切り替え** **出力**ウィンドウで [右端で折り返す] 機能をオンまたはオフにします。 ワード ラップ機能が有効になっていると、表示エリアより長いテキストは次の行に折り返されて表示されます。

## <a name="output-pane"></a>出力ペイン
 **[出力元の表示]** の一覧で選択された**出力**ペインは、このボックスで選択された項目の出力結果を表示します。

## <a name="routing-messages-to-the-output-window"></a>[出力] ウィンドウにメッセージを出力する
 プロジェクトをビルドしたときに必ず **[出力]** ウィンドウが表示されるようにするには、 **[全般]** \(オプション ダイアログ ボックス - プロジェクトおよびソリューション) で **[ビルド開始時に出力ウィンドウを表示]** をオンにします。 次に、編集のためにコード ファイルを開けた状態で、 **[出力]** ペインのエントリを選択するために **[出力]** ウィンドウのツール バーの **[次のメッセージに移動]** および **[前のメッセージに移動]** をクリックします。 この動作を続けると、コード エディターのカーソル位置が、選択した問題が発生したコード行へ移動します。

 [コマンド ウィンドウ](../../ide/reference/command-window.md)で実行できる一部の IDE 機能およびコマンドでは、 **[出力]** ウィンドウへ出力結果が送られます。 .bat ファイルや .com ファイルなどの外部ツールからの出力は、通常コマンド プロンプト ウィンドウで表示されますが、「[Visual Studio の外部ツール](../../ide/managing-external-tools.md)」の **[出力ウィンドウを使用]** オプションをオンにすると **[出力]** ペインに送られます。 他の種類のメッセージの多くも **[出力]** ペインで表示できます。 たとえば、ストアド プロシージャの Transact-SQL 構文を対象のデータベースに対してチェックすると、その結果が **[出力]** ウィンドウに表示されます。

 また、実行時に診断メッセージを **[出力]** ペインに書き出すことのできる、独自のアプリケーションをプログラムすることも可能です。 これを行うには、<xref:System.Diagnostics.Debug> クラスのメンバーまたは .NET Framework クラス ライブラリの <xref:System.Diagnostics.Trace> 名前空間にある <xref:System.Diagnostics> クラスを使用します。 <xref:System.Diagnostics.Debug> クラスのメンバーは、ソリューションまたはプロジェクトのデバッグ構成をビルドするときの出力結果を表示します。<xref:System.Diagnostics.Trace> クラスのメンバーは、デバッグ構成またはリリース構成のどちらかをビルドするときの出力結果を表示します。 詳細については、「[出力ウィンドウの診断メッセージ](../../debugger/diagnostic-messages-in-the-output-window.md)」を参照してください。

 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] では、警告とエラー メッセージ、およびその合計数を**出力**ペインで表示できる、カスタム ビルド ステップおよびビルド イベントを作成できます。 出力結果の任意の行で F1 キーを押すと、適切なヘルプ トピックが表示されます。 詳細については、「[カスタム ビルド ステップまたはビルド イベントの出力の書式設定](https://msdn.microsoft.com/library/92ad3e38-24d7-4b89-90e6-5a16f5f998da)」を参照してください。

## <a name="scrolling-behavior"></a>スクロール動作
 [出力] ウィンドウで自動スクロールを使用していて、マウスや方向キーを使用して移動すると、自動スクロールが停止します。 自動スクロールを再開するには、Ctrl キーを押しながら End キーを押します。

## <a name="see-also"></a>参照
 [出力ウィンドウの診断メッセージ](../../debugger/diagnostic-messages-in-the-output-window.md)[方法:](https://msdn.microsoft.com/library/91aebd15-8854-4a7a-9f7d-57376fb4e858) [コンパイルと](../../ide/compiling-and-building-in-visual-studio.md)ビルド出力ウィンドウの制御[ビルド構成](../../ide/understanding-build-configurations.md)の[概要クラスライブラリの概要](https://msdn.microsoft.com/library/7e4c5921-955d-4b06-8709-101873acf157)
