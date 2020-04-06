---
title: プログラムの起動 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- programs, launching
ms.assetid: 6857e9c6-e44a-468a-afa4-f7c4a0b77844
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf638e0c96c7df1de2650260427a972a07efce23
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738483"
---
# <a name="launch-a-program"></a>プログラムを起動する
プログラムをデバッグするユーザーは **、F5**キーを押して IDE からデバッガーを実行できます。 これにより、最終的に IDE がデバッグ エンジン (DE) に接続される一連のイベントが開始され、次のようにプログラムに接続またはアタッチされます。

1. IDE は、まずプロジェクト パッケージを呼び出して、ソリューションのアクティブなプロジェクトデバッグ設定を取得します。 設定には、開始ディレクトリ、環境変数、プログラムを実行するポート、プログラムの作成に使用する DE (指定されている場合) が含まれます。 これらの設定はデバッグ パッケージに渡されます。

2. DE が指定されている場合、DE はオペレーティング・システムを呼び出してプログラムを起動します。 プログラムを起動した結果、プログラムのランタイム環境が読み込まれます。 たとえば、プログラムが MSIL で記述されている場合、共通言語ランタイムが呼び出され、プログラムが実行されます。

    \- または -

    DE が指定されていない場合、ポートはオペレーティング システムを呼び出してプログラムを起動します。

   > [!NOTE]
   > DE を使用してプログラムを起動する場合、同じ DE がプログラムにアタッチされる可能性があります。

3. DE またはポートがプログラムを起動したかどうかに応じて、DE またはランタイム環境は、プログラムの説明またはノードを作成し、プログラムが実行されていることをポートに通知します。

   > [!NOTE]
   > プログラム ノードはデバッグ可能なプログラムの軽量表現であるため、ランタイム環境でプログラム ノードを作成することをお勧めします。 プログラムノードを作成して登録するためだけに、DE全体をロードする必要はありません。 DE が IDE のプロセスで実行されるように設計されているが、実際に実行されている IDE がない場合は、ポートにプログラムノードを追加できるコンポーネントが必要です。

   新しく作成されたプログラムは、関連または無関係の他のプログラムと共に、同じ IDE から起動またはアタッチされて、デバッグセッションを構成します。

   プログラムを使用すると、ユーザーが**F5**[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]キーを押すと、デバッグ パッケージは<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A>メソッドを通じてプロジェクト パッケージ (起動中のプログラムの種類に関連付けられている) を<xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2>呼び出し、ソリューションのアクティブなプロジェクト デバッグ設定を構造体に入力します。 この構造体は、<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A>メソッドの呼び出しを通じてデバッグ パッケージに返されます。 デバッグ パッケージは、セッション デバッグ マネージャー (SDM) をインスタンス化し、デバッグ中のプログラムと関連付けられたデバッグ エンジンを起動します。

   SDM に渡される引数の 1 つは、プログラムの起動に使用される DE の GUID です。

   DE GUID が`GUID_NULL`でない場合、SDM は DE を共同作成し、[その LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)メソッドを呼び出してプログラムを起動します。 たとえば、プログラムがネイティブ コードで記述されている場合、`IDebugEngineLaunch2::LaunchSuspended`プログラムを実行`CreateProcess`するために`ResumeThread`、プログラムを呼び出して (Win32 関数を) 呼び出す可能性があります。

   プログラムを起動した結果、プログラムのランタイム環境がロードされます。 次に、DE またはランタイム環境は、プログラムを記述する[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスを作成し、プログラムが実行されていることをポートに通知するためにこのインターフェイスを[AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)に渡します。

   渡`GUID_NULL`された場合、ポートはプログラムを起動します。 プログラムが実行されると、ランタイム環境は、プログラムを`IDebugProgramNode2`記述するインターフェイスを作成し、それを に渡します`IDebugPortNotify2::AddProgramNode`。 これにより、プログラムが実行されていることをポートに通知します。 次に、SDM は実行中のプログラムにデバッグ エンジンをアタッチします。

## <a name="in-this-section"></a>このセクションの内容
 [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)プログラムが起動され、ポートに通知された後に発生する処理について説明します。

 [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md)デバッグ セッションがプログラムに DE をアタッチする準備ができたときに文書化されます。

## <a name="related-sections"></a>関連項目
 [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)プログラムの起動や式の評価など、さまざまなデバッグ タスクへのリンクが含まれています。
