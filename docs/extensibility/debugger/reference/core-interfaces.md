---
description: 次のインターフェイスは、VS SDK を使用してデバッガーを拡張するためのコアインターフェイスです。
title: コアインターフェイス |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Debugging SDK], core interfaces
ms.assetid: 666b9116-8550-4bdd-bc15-55fc57de87df
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f24dd16656144fa155d0473d7f722487c0edd03
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170758"
---
# <a name="core-interfaces"></a>コア インターフェイス
次のインターフェイスは、を使用してデバッガーを拡張するためのコアインターフェイスです [!INCLUDE[vsipsdk](../../../extensibility/includes/vsipsdk_md.md)] 。

## <a name="discussion"></a>ディスカッション
 これらのインターフェイスは、主にデバッグエンジン (DE) を作成するために使用されます。 カテゴリ別に分類されています。

- [ブレークポイント](#Breakpoints)

- [コンテキスト](#Contexts)

- [コアサーバー](#CoreServer)

- [デバッグエンジン](#DebugEngines)

- [ドキュメント](#Documents)

- [イベント](#Events)

- [式](#Expressions)

- [メモリ](#Memory)

- [モジュール](#Modules)

- [ポート](#Ports)

- [処理](#Processes)

- [Programs](#Programs)

- [Properties](#Properties)

- [スタック フレーム](#StackFrames)

- [スレッド](#Threads)

- [型ビジュアライザー](#TypeVisualizers)

  インターフェイスを実装できるエンティティは次のとおりです。

- デバッグエンジン (DE)

- ポート供給業者 (PS)

- 式エバリュエーター (EE)

- Visual Studio (VS)

## <a name="breakpoints"></a><a name="Breakpoints"></a> 区切り
 これらのインターフェイスは、ブレークポイントの実装と追跡に関連しています。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)|DE|メモリ位置にバインドされたブレークポイントを表します。|
|[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)|DE|ブレークポイントがメモリ位置にバインドされたときに、DE によって送信されます。|
|[IDebugBreakpointChecksumRequest2](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2.md)|VS|ブレークポイント要求のドキュメントチェックサムを表します。|
|[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)|DE|ブレークポイントがメモリ位置にバインドされない場合に、DE によって送信されます。|
|[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)|DE|ブレークポイントに到達したときに、DE によって送信されます。|
|[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)|VS|ブレークポイントの要求を表します。保留中のブレークポイントの作成に使用されます。|
|[IDebugBreakpointRequest3](../../../extensibility/debugger/reference/idebugbreakpointrequest3.md)|VS|ブレークポイントの要求を表します。保留中のブレークポイントの作成に使用されます。|
|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|DE|ブレークポイントをバインドするために使用する情報を表します。|
|[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)|DE|ブレークポイントがメモリ位置からバインド解除されたときに、DE によって送信されます。|
|[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)|DE|無効なブレークポイント (によって返される) を表し `IDebugBreakpointErrorEvent2` ます。|
|[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)|DE|無効なブレークポイントに関する解決情報を表します。|
|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|DE|ブレークポイントが設定されている関数内の位置を表します。|
|[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)|DE|バインドされるブレークポイントを表します。バインドされたブレークポイントを作成するときに使用します。|
|[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)|DE|バインドされたブレークポイントのセットに対する列挙体を表します。|
|[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)|DE|メモリ位置にバインドできなかったブレークポイントのセットに対する列挙体を表します。|

## <a name="contexts"></a><a name="Contexts"></a> 状況
 これらのインターフェイスは、デバッグ中のプログラム内のさまざまな種類のコンテキストを表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|DE|コード命令の開始位置を表します。|
|[IDebugCodeContext3](../../../extensibility/debugger/reference/idebugcodecontext3.md)|DE|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)インターフェイスを拡張して、モジュールインターフェイスとプロセスインターフェイスを取得できるようにします。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS、DE|ドキュメント内の位置を表します。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|式を評価するコンテキストを表します。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|バイトのコレクションのメモリ内での開始位置を表します。|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|ブレークポイントまたは例外のスタックフレームコンテキストを表します。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|ブレークポイントまたは例外のスタックフレームコンテキストを表します。|
|[IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)|DE|コードコンテキストのセットに対する列挙体を表します。|

## <a name="core-server"></a><a name="CoreServer"></a> コアサーバー
 これらのインターフェイスは、プログラムがデバッグされているコンピューターを表します。 これらはによって実装され [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ますが、デバッグエンジンによって呼び出すことができます。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)|VS|コンピューターに関する情報だけでなく、ポートとポートの供給元へのアクセスを提供します。|
|[IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)|VS|リモートデバッグをサポートする [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md) を表します。|

## <a name="debug-engines"></a><a name="DebugEngines"></a> デバッグエンジン
 これらのインターフェイスは、デバッグエンジンとそれに関連付けられたイベントを表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)|DE|カスタムデバッグエンジンを表します。|
|[IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)|DE|シンボル、Mycode、および例外の読み込みをサポートするカスタムデバッグエンジンを表します。|
|[IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)|DE|デバッグタスクを処理する準備ができていることを示すために、DE の新しい各インスタンスによって送信されます。|
|[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)|DE|プログラムの起動をサポートするカスタムデバッグエンジンを表します。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE、PS|複数のデバッグエンジンを処理するプログラムノードを表します。|
|[IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)|DE|SDM がスレッド、プログラム、またはスタックフレームからデバッグエンジンへのインターフェイスを取得する方法を提供します。|

## <a name="documents"></a><a name="Documents"></a> ドキュメント
 これらのインターフェイスは、ドキュメント (ソースファイル) とそれに関連付けられている要素を表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md)|DE|ドキュメントを開くように要求するために、DE によって送信されます。|
|[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)|DE|ドキュメントからの逆アセンブル命令のストリームを表します。|
|[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)|VS、DE|名前とクラス ID (CLSID) を指定して、DE によって提供されるドキュメントを表します。|
|[IDebugDocumentChecksum2](../../../extensibility/debugger/reference/idebugdocumentchecksum2.md)|DE、EE|デバッグドキュメントのチェックサムを表し、コンポーネント間でチェックサムを渡すことができるようにします。|
|[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)|VS、DE|ドキュメントコンテキスト (特定のステートメントおよびコードコンテキストに対応するドキュメント内の位置) を表します。|
|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|VS、DE|ドキュメント内の一般的な位置を表します。|
|[IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)|VS|ソースファイル内の文字オフセットとしての位置を表します。|
|[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)|VS、DE|( [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)から派生した) DE によって提供されるテキストドキュメントを表し、実際のテキストを提供します。|
|[IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)|DE|DE によって送信され、メモリ内のソースファイルに対する変更を指定します。|

## <a name="events"></a><a name="Events"></a> 記録
 これらのインターフェイスは、DE とセッションデバッグマネージャー (SDM) の間で送信されるすべてのイベントを表します。

| Interface | 実装 | 説明 |
| - |----------------| - |
| [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) | DE | ドキュメントを開くように要求するために、DE によって送信されます。 |
| [IDebugBeforeSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugbeforesymbolsearchevent2.md) | DE | デバッグエンジン (DE) は、シンボルの読み込み中にステータスバーメッセージを設定するために、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。 |
| [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) | DE | プログラムの中断が完了したときに、DE によって送信されます。 |
| [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) | DE | ブレークポイントがバインドされたときに、DE によって送信されます。 |
| [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md) | DE | ブレークポイントのバインドに失敗したときに、DE によって送信されます。 |
| [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) | DE | ブレークポイントに到達したときに、DE によって送信されます。 |
| [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md) | DE | ブレークポイントがバインド解除されるときに、DE によって送信されます。 |
| [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md) | DE | DE が特定の場所で停止する必要があるかどうかを判断するために送信されます。 |
| [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) | DE | DE によって送信され、メモリ内のソースファイルに対する変更を指定します。 |
| [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) | DE | デバッグタスクを処理する準備ができていることを示すために、DE の新しい各インスタンスによって送信されます。 |
| [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) | DE | デバッグ中のプログラムが最初の命令を実行する準備ができていることを示すために、DE によって送信されます。 |
| [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md) | DE | ユーザーが判読できるエラーメッセージを提供するためにエラーを返す可能性がある、他のイベントインターフェイスによって使用されるインターフェイス。 |
| [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md) | DE、PS | 他のすべてのイベントインターフェイスの派生元となる基本インターフェイス。 |
| [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) | VS | イベント (特定のイベントインターフェイスを実装するオブジェクトとして表される) が送信される SDM によって実装されるインターフェイスを表します。 |
| [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md) | DE | デバッグ中のプログラムで例外が発生したときに、DE によって送信されます。 |
| [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) | DE | 非同期式の評価が完了したときに、DE によって送信されます。 |
| IDebugFindSymbolEvent2 | | 互換性のために残されています。 使用しないでください。 |
| [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) | DE | インターセプトされた例外の処理が完了したときに、DE によって送信されました。 |
| [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md) | DE | プログラムの読み込みが完了したときに、DE によって送信されます。 |
| [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md) | DE | ユーザーに情報メッセージを表示するために、DE によって送信されます。 |
| [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md) | DE | モジュールが読み込まれたとき、またはアンロードされたときに、DE によって送信されます。 |
| [IDebugNoSymbolsEvent2](../../../extensibility/debugger/reference/idebugnosymbolsevent2.md) | DE | [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]起動された実行可能ファイルのシンボルが見つからなかったことをユーザーに警告するように、デバッガーの UI に通知します。 |
| [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md) | DE | IDE で任意の文字列を表示するために、DE によって送信されます。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | VS、DE | ポートイベントを任意のリスナーに伝達するために、ポートによって送信されます。 |
| [IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md) | DE、PS | プロセスが作成されたときに、DE またはポートによって送信されます。 |
| [IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) | DE、PS | プロセスが破棄されたときに、DE またはポートによって送信されます。 |
| [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) | DE、PS | プログラムが作成されたときに、DE またはポートによって送信されます。 |
| [IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) | DE、PS | プログラムが破棄されたときに、DE またはポートによって送信されます。 |
| [IDebugProgramDestroyEventFlags2](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2.md) | DE | デバッグセッションを終了するときに、デバッグエンジンが UI の既定の動作をオーバーライドできるようにし [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ます。 |
| [IDebugProgramNameChangedEvent2](../../../extensibility/debugger/reference/idebugprogramnamechangedevent2.md) | DE | プログラムの名前が変更されたときに、デバッグエンジン (DE) からセッションデバッグマネージャー (SDM) に送信されます。 |
| [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) | DE | (インターフェイスによって表される) 新しいプロパティが作成されたときに、DE によって送信され `IDebugProperty2` ます。 |
| [IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md) | DE | プロパティが破棄されたときに、DE によって送信されます。 |
| [IDebugReturnValueEvent2](../../../extensibility/debugger/reference/idebugreturnvalueevent2.md) | DE | 関数のステップアウト時に DE によって送信されます。これにより、戻り値が正しく表示されるようになります。 |
| [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md) | VS | デバッグエンジンがメトリック設定をリモートで読み取ることができるようにします。 |
| [IDebugStepCompleteEvent2](../../../extensibility/debugger/reference/idebugstepcompleteevent2.md) | DE | 命令のステップイン、ステップオーバー、またはステップアウトが完了したときに、DE によって送信されます。 |
| [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) | DE | モジュールのシンボルの読み込みが成功したか失敗したかを示すために、DE によって送信されます。 |
| [IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md) | DE | スレッドが作成されたときに、DE によって送信されます。 |
| [IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md) | DE | スレッドが破棄されたときに、DE によって送信されます。 |
| [IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md) | DE | スレッドの名前が変更されたときに、DE によって送信されます。 |

## <a name="expressions"></a><a name="Expressions"></a> 式
 これらのインターフェイスは、特定のコンテキストで評価される式を表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)|DE|評価される式を表します。 [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)インターフェイスから取得されます。|
|[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)|DE|式が評価されるコンテキストを表します。 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)インターフェイスから取得されます。|
|[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)|DE|非同期式の評価が完了したときに、DE によって送信されます。|

## <a name="memory"></a><a name="Memory"></a> 量
 これらのインターフェイスは、メモリ内のバイトシーケンスを表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)|DE|読み取りまたは書き込みが可能なメモリ内のバイトシーケンスを表します。|
|[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)|DE|バイトシーケンスのメモリ内の場所を表します。|

## <a name="modules"></a><a name="Modules"></a> モジュール
 これらのインターフェイスは、実行可能ファイルまたはに対応するモジュールを表します。DLL ファイル。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)|DE|1つの実行可能ファイルまたは DLL を表します。|
|[IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)|DE|シンボルをサポートする [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) を表します。|
|[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)|DE|モジュールが読み込まれたとき、またはアンロードされたときに、DE によって送信されます。|
|[IDebugSourceServerModule](../../../extensibility/debugger/reference/idebugsourceservermodule.md)|DE|PDB ファイルに格納されているソースサーバー情報を表します。|
|[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)|DE|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)によって認識されるモジュールのセットに対する列挙体を表します。|

## <a name="ports"></a><a name="Ports"></a> シリアル
 これらのインターフェイスは、ポートとポートサプライヤーを表します。

| Interface | 実装 | 説明 |
| - |----------------| - |
| [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md) | VS、PS | ローカルコンピューターの既定のポートを表します。 |
| [IDebugFirewallConfigurationCallback2](../../../extensibility/debugger/reference/idebugfirewallconfigurationcallback2.md) | VS | DCOM を使用して、 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] ファイアウォールがリモートデバッグをブロックしないように UI に要求するデバッグエンジンを有効にします。 |
| [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) | VS、PS | ポートを表します。 |
| [IDebugPortEvents2](../../../extensibility/debugger/reference/idebugportevents2.md) | PS | ポートイベントを任意のリスナーに伝達するために、ポートによって送信されます。 |
| [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md) | PS | プロセスを起動および終了できるポートを表します。 |
| [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) | PS | ポートを使用してプログラムを登録および登録解除するために使用されます。現在デバッグ中のプログラムをポートが追跡できるようにします。 |
| [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md) | PS | ポートを選択するためのカスタマイズされた UI を表します。 |
| [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) | VS | 新しいポートが作成または配置されるポートの要求を表します。 |
| [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) | PS | ポートの供給業者を表します。 |
| [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md) | PS | 作成したポートに関する情報を永続化 (ディスクに保存) できるポートの供給業者を表します。 |
| [IDebugPortSupplierDescription2](../../../extensibility/debugger/reference/idebugportsupplierdescription2.md) | PS | [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)][**プロセスにアタッチ**] ダイアログボックスの [**トランスポート情報**] セクション内のテキストを UI で表示できるようにします。 |
| [IDebugWindowsComputerPort2](../../../extensibility/debugger/reference/idebugwindowscomputerport2.md) | VS | 対象のコンピュータに関する情報のクエリを実行できるようにします。 |
| [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md) | VS、PS | 一連のポートに対する列挙体を表します。 |
| [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) | VS | ポートサプライヤーのセットに対する列挙体を表します。 |

## <a name="processes"></a><a name="Processes"></a> プロセス
 これらのインターフェイスは、1つまたは複数のプログラムを含む1つの実行可能ファイルであるプロセスを表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)|PS、DE|コンピューター上で実行されているプロセスを表します。|
|[IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)|PS、DE|デバッグをアクティブにサポートするプロセスを表します (ステップの置換、続行、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスのメソッドの実行に使用されます)。|
|[IDebugProcessCreateEvent2](../../../extensibility/debugger/reference/idebugprocesscreateevent2.md)|DE、PS|プロセスが作成されたときに、DE またはポートによって送信されます。|
|[IDebugProcessDestroyEvent2](../../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)|DE、PS|プロセスが破棄されたときに、DE またはポートによって送信されます。|
|[IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)|PS|アタッチされているセッションを追跡する必要があるプロセスを表します。|
|[IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)|PS|ポート上の一連のプロセスの列挙体を表します。|

## <a name="programs"></a><a name="Programs"></a> プログラム
 これらのインターフェイスは、物理的な実行可能ファイルまたはモジュールに対応しているとは限りません。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)|DE|同時にデバッグされている他のプログラムと連携して作業する必要がある [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) を表します。|
|[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)|DE、PS|実行の論理単位を表します。|
|[IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)|DE、PS|プログラムが作成されたときに、DE またはポートによって送信されます。|
|[IDebugProgramDestroyEvent2](../../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)|DE、PS|プログラムが破棄されたときに、DE またはポートによって送信されます。|
|[IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)|DE、PS|複数のデバッグエンジンによって処理できる [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を表します。|
|[IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)|PS|アタッチされているセッションを追跡できる必要がある [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) を表します。|
|[IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)|DE、PS|実行中のプロセスに関する情報を返すことができる [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) を表します。|
|[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)|DE、PS|デバッグできるプログラムを表します。|
|[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)|DE、PS|関連付けられているプログラムにアタッチしようとしたことをプログラムノードに通知します。|
|[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)|DE|SDM が、その DE によって制御されるプログラムに関する DE を照会する方法を提供します。|
|[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)|VS|プログラムを SDM に登録して、プログラムがデバッグ中であることを示すために、DEs によって使用されます。|
|[IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)|DE、PS|スレッドまたはプロセスの境界を越えてインターフェイスをマーシャリングできる [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) を表します。|
|[IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)|DE、PS|一連のプログラムの列挙体を表します。|

## <a name="properties"></a><a name="Properties"></a> プロパティ
 これらのインターフェイスは、特定のコンテキストに関連付けられた値 (通常は式の評価の結果) を表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugCustomViewer](../../../extensibility/debugger/reference/idebugcustomviewer.md)|EE|カスタムの方法で値を表示できる [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を表します。|
|[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)|DE|スタックフレーム、ドキュメント、または式の評価結果の値を表します。|
|[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)|DE|任意の長い文字列をサポートする [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) を表します。|
|[IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)|DE|( [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) インターフェイスによって表される) 新しいプロパティが作成されたときに、DE によって送信されます。|
|[IDebugPropertyDestroyEvent2](../../../extensibility/debugger/reference/idebugpropertydestroyevent2.md)|DE|プロパティが破棄されたときに、DE によって送信されます。|
|[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)|DE|特定のスタックフレームの外に存在する可能性があるプロパティへの参照を表します。|
|[IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)|DE|変数、レジスタ、パラメーター、および式を記述する一連の [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 構造体に対する列挙体を表します。|
|[IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)|DE|一連の [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体に対する列挙体を表します。|

## <a name="stack-frames"></a><a name="StackFrames"></a> スタックフレーム
 これらのインターフェイスは、ブレークポイントまたは例外が発生したコンテキストであるスタックフレームを表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)|DE|ブレークポイントまたは例外が発生したコンテキストを表します。|
|[IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)|DE|インターセプトした例外を処理できる [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) を表します。|
|[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)|DE|特定のスタックフレームに到達するために使用される関数呼び出しシーケンスを指定する [CODE_PATH](../../../extensibility/debugger/reference/code-path.md) 構造体のセットに対する列挙体を表します。|
|[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)|DE|スタックフレームを記述する一連の [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体に対する列挙体を表します。|

## <a name="threads"></a><a name="Threads"></a>スレッド
 これらのインターフェイスは、スレッドとそれに関連付けられたイベントを表します。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|DE|実行のスレッドを表します。|
|[IDebugThreadCreateEvent2](../../../extensibility/debugger/reference/idebugthreadcreateevent2.md)|DE|スレッドが作成されたときに、DE によって送信されます。|
|[IDebugThreadDestroyEvent2](../../../extensibility/debugger/reference/idebugthreaddestroyevent2.md)|DE|スレッドが破棄されたときに、DE によって送信されます。|
|[IDebugThreadNameChangedEvent2](../../../extensibility/debugger/reference/idebugthreadnamechangedevent2.md)|DE|スレッドの名前が変更されたときに、DE によって送信されます。|
|[IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)|DE|一連のスレッドに対する列挙体を表します。|

## <a name="type-visualizers"></a><a name="TypeVisualizers"></a> 型ビジュアライザー
 これらのインターフェイスは、型ビジュアライザーのサポートを提供します。 これらのインターフェイスは、通常、式エバリュエーターによって実装されます。

|Interface|実装|説明|
|---------------|--------------------|-----------------|
|[IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)|EE|型ビジュアライザーに提示されるバイト配列を表します。|
|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)|EE|型ビジュアライザーに渡されるデータへのアクセスを取得するためのメソッドを提供します。|
|[IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)|EE|[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)実装へのアクセスを提供するプロパティを表します。|

## <a name="see-also"></a>関連項目
- [API リファレンス](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [カスタム デバッグ エンジンの作成](../../../extensibility/debugger/creating-a-custom-debug-engine.md)
