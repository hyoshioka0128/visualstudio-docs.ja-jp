---
title: アクティブ スクリプトのデバッグの概要 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Active Script Debugging overview
ms.assetid: ce4ec768-d017-4dfa-a7e3-cced3a29e679
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0181ee305c99a1d0af1d3e1e965c6ac8fe16f375
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835668"
---
# <a name="active-script-debugging-overview"></a>アクティブ スクリプトのデバッグの概要
アクティブ スクリプト デバッグ インターフェイスを使うと、言語やホストに依存しない (ニュートラルな) デバッグを行うことができ、さまざまな開発環境がサポートされます。  
  
 ![スクリプト ホスト プロセス](../winscript/media/scp56activdbgarchgif.gif "Scp56ActivDbgArchgif")  
図 1  
  
 言語に依存しないデバッグ環境は、任意のプログラミング言語またはプログラミング言語の組み合わせをサポートでき、どの言語についても固有の知識を持つ必要はありません。 また、デバッグ環境は異なる言語間のステップ実行およびブレークポイントもサポートします  (この概要では、VBScript や [!INCLUDE[javascript](../javascript/includes/javascript-md.md)] などのスクリプト言語のサポートに主に注目します)。  
  
 ホストに依存しないデバッガーは、Internet Explorer やカスタム ホストなどの任意のアクティブ スクリプト ホストで自動的に使うことができます。 ホストは、ドキュメント ツリーの構造からデバッグ ドキュメントの内容や構文の色分けまで、ユーザーに対するデバッガーの表示を制御します。 これにより、ホスト ドキュメントのコンテキストでデバッグ対象のソース コードを表示できます。 たとえば、Internet Explorer は HTML ページでスクリプトを表示できます。  
  
 以下では、アクティブ デバッグの各主要コンポーネントとそれに関連するインターフェイスについて説明します。 ただし、先に進む前に、アクティブ デバッグのいくつかの重要な概念を定義しておく必要があります。  
  
 **ホスト アプリケーション**  
 スクリプト エンジンをホストし、スクリプト可能なオブジェクトのセット ("オブジェクト モデル") を提供するアプリケーションです。  
  
 **言語エンジン**  
 特定の言語の解析、実行、デバッグの抽象化を提供するコンポーネントです。  
  
 **デバッガー IDE**  
 ホスト アプリケーションおよび言語エンジンと通信することによってデバッグ UI を提供するアプリケーションです。  
  
 **マシン デバッグ マネージャー**デバッグできるアプリケーション プロセスのレジストリを維持するコンポーネントです。  
  
 **プロセスデバッグマネージャー**  
 特定のアプリケーションのデバッグできるドキュメントのツリーの保持、実行中のスレッドの追跡などを行うコンポーネントです。  
  
 **ドキュメントのコンテキスト**  
 ホスト ドキュメントのソース コードで特定の範囲を表す抽象化です。  
  
 **コードコンテキスト**  
 言語エンジンの実行中コードで特定の場所を表します ("仮想命令ポインター")。  
  
 **式コンテキスト**  
 言語エンジンが式を評価できる特定のコンテキスト (たとえば、スタック フレーム) です。  
  
 **オブジェクト参照**  
 "ウォッチ ウィンドウ" UI の実装に適した、オブジェクトの名前、型、値、サブオブジェクトの構造化された言語に依存しない表現です。  
  
 以下は、アクティブ デバッグの各主要コンポーネントとそれらに対応する関連インターフェイスの概要です。インターフェイスの詳細はその後で説明します。  
  
## <a name="language-engine"></a>言語エンジン  
 言語エンジンは以下の機能を提供します。  
  
- 言語の解析と実行。  
  
- デバッグのサポート (ブレークポイントなど)。  
  
- 式の評価。  
  
- 構文の色分け表示。  
  
- オブジェクト参照。  
  
- スタックの列挙と解析。  
  
  以下は、デバッグ、式の評価、およびオブジェクト参照を提供するためにスクリプト エンジンがサポートする必要のあるインターフェイスです。 これらのインターフェイスを使って、ホスト アプリケーションはそのドキュメント コンテキストとエンジンのコード コンテキストの間をマップし、デバッガー UI は式の評価、スタックの列挙、オブジェクト参照を行います。  
  
  [IActiveScriptDebug インターフェイス](../winscript/reference/iactivescriptdebug-interface.md)  
  構文の色分けと、コード コンテキストの列挙を提供します。  
  
  [IActiveScriptErrorDebug インターフェイス](../winscript/reference/iactivescripterrordebug-interface.md)  
  エラーに対するドキュメント コンテキストとスタック フレームを返します。  
  
  [IActiveScriptSiteDebug インターフェイス](../winscript/reference/iactivescriptsitedebug-interface.md)  
  ホストが提供するスクリプト エンジンからデバッガーへのリンクです。  
  
  [IDebugCodeContext インターフェイス](../winscript/reference/idebugcodecontext-interface.md)  
  スレッド内の仮想 "命令ポインター" を提供します。  
  
  [IEnumDebugCodeContexts インターフェイス](../winscript/reference/ienumdebugcodecontexts-interface.md)  
  ドキュメント コンテキストに対応するコード コンテキストを列挙します。  
  
  [IDebugStackFrame インターフェイス](../winscript/reference/idebugstackframe-interface.md)  
  スレッド スタック上の論理スタック フレームを表します。  
  
  [IDebugExpressionContext インターフェイス](../winscript/reference/idebugexpressioncontext-interface.md)  
  式を評価できるコンテキストを提供します。  
  
  [IDebugStackFrameSniffer インターフェイス](../winscript/reference/idebugstackframesniffer-interface.md)  
  論理スタック フレームを列挙する手段を提供します。  
  
  [IDebugExpression インターフェイス](../winscript/reference/idebugexpression-interface.md)  
  非同期に評価される式を表します。  
  
  [IDebugSyncOperation インターフェイス](../winscript/reference/idebugsyncoperation-interface.md)  
  特定のブロックされたスレッドに入れ子になっているときに実行する必要のある操作を、スクリプト エンジンが抽象化できるようにします。  
  
  [IDebugAsyncOperation インターフェイス](../winscript/reference/idebugasyncoperation-interface.md)  
  同期デバッグ操作への非同期アクセスを提供します。  
  
  [IDebugAsyncOperationCallBack インターフェイス](../winscript/reference/idebugasyncoperationcallback-interface.md)  
  `IDebugAsyncOperation` インターフェイスの評価の進行状況に関連する状態イベントを提供します。  
  
  [IEnumDebugExpressionContexts インターフェイス](../winscript/reference/ienumdebugexpressioncontexts-interface.md)  
  `IDebugExpressionContexts` オブジェクトのコレクションを列挙します。  
  
  [IProvideExpressionContexts インターフェイス](../winscript/reference/iprovideexpressioncontexts-interface.md)  
  特定のコンポーネントによって認識されている式コンテキストを列挙する手段を提供します。  
  
  [IDebugFormatter インターフェイス](../winscript/reference/idebugformatter-interface.md)  
  VARIANT 値または VARTYPE 型と文字列の間の変換を、言語または IDE がカスタマイズできるようにします。  
  
  [IDebugStackFrameSnifferEx インターフェイス](../winscript/reference/idebugstackframesnifferex-interface.md)  
  PDM の論理スタック フレームを列挙します。  
  
## <a name="hosts"></a>Hosts  
 ホストには次の機能があります。  
  
- 言語エンジンをホストします。  
  
- オブジェクト モデル (スクリプト化できるオブジェクトのセット) を提供します。  
  
- デバッグ可能なドキュメントのツリーとドキュメントの内容を定義します。  
  
- スクリプトを仮想アプリケーションに編成します。  
  
  2 種類のホストがあります。  
  
- ダム ホストは、基本的なアクティブ スクリプト インターフェイスだけをサポートします。 ドキュメントの構造や編成を制御することはできません。これは、言語エンジンに提供されるスクリプトによって完全に決定されます。  
  
- スマート ホストは、ドキュメント ツリー、ドキュメントの内容、構文の色分けを定義できる多くのインターフェイスのセットをサポートします。 次のサブセクションで説明するような一連のヘルパー インターフェイスがあり、ホストをより簡単にスマート ホストにできます。  
  
### <a name="smart-host-helper-interfaces"></a>スマート ホスト ヘルパー インターフェイス  
 `IDebugDocumentHelper` のメソッドが提供する大幅に簡略化された一連のインターフェイスを使うことで、ホストは、完全なホスト インターフェイスの複雑さ (と能力) をすべて処理しなくても、スマート ホストのメリットを利用できます。  
  
 もちろん、ホストはこれらのインターフェイスを使わなくてもかまいません。 ただし、これらのインターフェイスを使うと、多くのさらに複雑なインターフェイスを実装したり使ったりする必要がなくなります。  
  
 [IDebugDocumentHelper インターフェイス](../winscript/reference/idebugdocumenthelper-interface.md)  
 PDM によって実装され、スマート ホストに必要な多くのインターフェイスの実装を提供します。  
  
 [IDebugDocumentHost インターフェイス](../winscript/reference/idebugdocumenthost-interface.md)  
 ホストによって実装され (省略可能)、構文の色分けなどのホスト固有の機能をデバッガーに公開します。  
  
 詳しくは、「[スマート ホスト ヘルパー インターフェイスの実装](../winscript/implementing-smart-host-helper-interfaces.md)」をご覧ください。  
  
### <a name="full-smart-host-interfaces"></a>完全なスマート ホスト インターフェイス  
 次に示すのは、スマート ホストがヘルパー インターフェイスを使わない場合に実装または使用する必要があるインターフェイスの完全なセットです。  
  
 ホストによって実装されるインターフェイス:  
  
 [IDebugDocumentInfo インターフェイス](../winscript/reference/idebugdocumentinfo-interface.md)  
 ドキュメントの情報を提供します。インスタンス化することも、しないこともできます。  
  
 [IDebugDocumentProvider インターフェイス](../winscript/reference/idebugdocumentprovider-interface.md)  
 必要に応じてドキュメントをインスタンス化するための手段を提供します。  
  
 [IDebugDocument インターフェイス](../winscript/reference/idebugdocument-interface.md)  
 すべてのデバッグ ドキュメントの基底インターフェイスです。  
  
 [IDebugDocumentText インターフェイス](../winscript/reference/idebugdocumenttext-interface.md)  
 デバッグ ドキュメントのテキストのみのバージョンへのアクセスを提供します。  
  
 [IDebugDocumentTextAuthor インターフェイス](../winscript/reference/idebugdocumenttextauthor-interface.md)  
 デバッグ ドキュメントのテキストのみのバージョンを編集できるようにします。  
  
 [IDebugDocumentContext インターフェイス](../winscript/reference/idebugdocumentcontext-interface.md)  
 デバッグ中のドキュメントの一部分の抽象表現を提供します。  
  
 ホストに代わって PDM によって実装されるインターフェイス:  
  
 [IDebugApplicationNode インターフェイス](../winscript/reference/idebugapplicationnode-interface.md)  
 プロジェクト ツリー内のコンテキストを提供することにより、`IDebugDocumentProvider` インターフェイスの機能を拡張します。  
  
## <a name="debugger-ide"></a>デバッガー IDE  
 IDE は、言語に依存しないデバッグ UI です。 共有サービスには次のものが含まれています。  
  
- ドキュメント ビューアー/エディター。  
  
- ブレークポイントの管理。  
  
- 式の評価とウォッチ ウィンドウ。  
  
- スタック フレームの参照。  
  
- オブジェクト/クラスの参照。  
  
- 仮想アプリケーションの構造の参照。  
  
  デバッガーによって実装されるインターフェイス:  
  
  [IApplicationDebugger インターフェイス](../winscript/reference/iapplicationdebugger-interface.md)  
  デバッガー IDE セッションによって公開される主インターフェイスです。  
  
  [IApplicationDebuggerUI インターフェイス](../winscript/reference/iapplicationdebuggerui-interface.md)  
  外部コンポーネントが制御できるデバッガーのユーザー インターフェイス (UI) の範囲を拡大します。  
  
  [IDebugExpressionCallBack インターフェイス](../winscript/reference/idebugexpressioncallback-interface.md)  
  `IDebugExpression` による評価の進行状況についての状態イベントを提供します。  
  
  [IDebugDocumentTextEvents インターフェイス](../winscript/reference/idebugdocumenttextevents-interface.md)  
  関連付けられているテキスト ドキュメントへの変更を示すイベントを提供します。  
  
  [IDebugApplicationNodeEvents インターフェイス](../winscript/reference/idebugapplicationnodeevents-interface.md)  
  `IDebugApplicationNode` インターフェイスに対するイベント インターフェイスを提供します。  
  
### <a name="machine-debug-manager"></a>マシン デバッグ マネージャー  
 マシン デバッグ マネージャーは、アクティブな仮想アプリケーションのリストを維持して列挙することにより、仮想アプリケーションとデバッガーの間のフックアップ ポイントを提供します。  
  
 [IDebugSessionProvider インターフェイス](../winscript/reference/idebugsessionprovider-interface.md)  
 実行中のアプリケーションのデバッグ セッションを確立します。  
  
 [IMachineDebugManager インターフェイス](../winscript/reference/imachinedebugmanager-interface.md)  
 マシン デバッグ マネージャーの主インターフェイスです。  
  
 [IMachineDebugManagerCookie インターフェイス](../winscript/reference/imachinedebugmanagercookie-interface.md)  
 `IMachineDebugManager` インターフェイスと似ていますが、このインターフェイスはデバッグ Cookie をサポートします。  
  
 [IMachineDebugManagerEvents インターフェイス](../winscript/reference/imachinedebugmanagerevents-interface.md)  
 マシン デバッグ マネージャーによって管理されている実行中アプリケーションのリストの変更を通知します。  
  
 [IEnumRemoteDebugApplications インターフェイス](../winscript/reference/ienumremotedebugapplications-interface.md)  
 マシンで実行中のアプリケーションを列挙します。  
  
### <a name="process-debug-manager"></a>プロセス デバッグ マネージャー  
 PDM は以下の処理を行います。  
  
- 複数の言語エンジンのデバッグを同期します。  
  
- デバッグできるドキュメントのツリーを保持します。  
  
- スタック フレームをマージします。  
  
- 言語エンジン間でブレークポイントとステップ実行を調整します。  
  
- スレッドを追跡します。  
  
- 非同期処理のためにデバッガー スレッドを保持します。  
  
- マシン デバッグ マネージャーおよびデバッガー IDE と通信します。  
  
  プロセス デバッグ マネージャーによって提供されるインターフェイスを次に示します。  
  
  [IProcessDebugManager インターフェイス](../winscript/reference/iprocessdebugmanager-interface.md)  
  プロセス デバッグ マネージャーの主インターフェイスです。 このインターフェイスは、プロセスの仮想アプリケーションを作成、追加、または削除することができます。  
  
  [IRemoteDebugApplication インターフェイス](../winscript/reference/iremotedebugapplication-interface.md)  
  実行中のアプリケーションを表します。  
  
  [IDebugApplication インターフェイス](../winscript/reference/idebugapplication-interface.md)  
  言語エンジンとホストが使用するためのリモート処理が不可能なデバッグ メソッドを公開します。  
  
  [IRemoteDebugApplicationThread インターフェイス](../winscript/reference/iremotedebugapplicationthread-interface.md)  
  特定のアプリケーション内の実行のスレッドを表します。  
  
  [IDebugApplicationThread インターフェイス](../winscript/reference/idebugapplicationthread-interface.md)  
  言語エンジンとホストが、スレッド同期を提供し、スレッド固有のデバッグ状態情報を維持できるようにします。  
  
  [IEnumRemoteDebugApplicationThreads インターフェイス](../winscript/reference/ienumremotedebugapplicationthreads-interface.md)  
  アプリケーションで実行中のスレッドを列挙します。  
  
  [IDebugThreadCall インターフェイス](../winscript/reference/idebugthreadcall-interface.md)  
  マーシャリングされた呼び出しをディスパッチします。  
  
  [IDebugApplicationNode インターフェイス](../winscript/reference/idebugapplicationnode-interface.md)  
  階層内でのドキュメントの位置を保持します。  
  
  [IEnumDebugApplicationNodes インターフェイス](../winscript/reference/ienumdebugapplicationnodes-interface.md)  
  アプリケーションに関連付けられているノードの子ノードを列挙します。  
  
  [IEnumDebugStackFrames インターフェイス](../winscript/reference/ienumdebugstackframes-interface.md)  
  エンジンからマージされた、スレッドに対応するスタック フレームを列挙します。  
  
  [IDebugCookie インターフェイス](../winscript/reference/idebugcookie-interface.md)  
  スクリプト デバッガーでデバッグ Cookie を設定できるようにします。  
  
  [IDebugHelper インターフェイス](../winscript/reference/idebughelper-interface.md)  
  オブジェクト ブラウザーに対するファクトリおよびスクリプト エンジンに対する単純な接続ポイントとして機能します。  
  
  [ISimpleConnectionPoint インターフェイス](../winscript/reference/isimpleconnectionpoint-interface.md)  
  特定の接続ポイントで発生したイベントを記述および列挙する簡単な方法をスクリプト エンジンに提供します。  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト デバッガー インターフェイス](../winscript/reference/active-script-debugger-interfaces.md)
