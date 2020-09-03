---
title: プログラムの起動 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738483"
---
# <a name="launch-a-program"></a>プログラムを起動する
プログラムをデバッグするユーザーは、 **F5** キーを押して、IDE からデバッガーを実行できます。 これにより、次のように、最終的に IDE がデバッグエンジン (DE) に接続されるか、またはアタッチされてからプログラムに接続されるようになる一連のイベントが開始されます。

1. IDE では、最初にプロジェクトパッケージを呼び出して、ソリューションのアクティブなプロジェクトデバッグ設定を取得します。 設定には、開始ディレクトリ、環境変数、プログラムが実行されるポート、およびプログラムの作成に使用する DE (指定されている場合) が含まれます。 これらの設定は、デバッグパッケージに渡されます。

2. DE が指定されている場合、DE はオペレーティングシステムを呼び出してプログラムを起動します。 プログラムを起動した結果として、プログラムの実行時環境が読み込まれます。 たとえば、プログラムが MSIL で記述されている場合、プログラムを実行するために共通言語ランタイムが呼び出されます。

    - または -

    DE が指定されていない場合、ポートはオペレーティングシステムを呼び出してプログラムを起動します。これにより、プログラムの実行時環境が読み込まれます。

   > [!NOTE]
   > DE を使用してプログラムを起動する場合、同じ DE がプログラムにアタッチされる可能性があります。

3. De またはポートがプログラムを起動したかどうかによって、DE またはランタイム環境によってプログラムの説明またはノードが作成され、プログラムが実行されていることがポートに通知されます。

   > [!NOTE]
   > 実行時環境では、プログラムノードを作成することをお勧めします。これは、プログラムノードは、デバッグ可能なプログラムの簡易表現であるためです。 プログラムノードを作成および登録するためだけに、DE 全体を読み込む必要はありません。 DE が IDE のプロセスで実行されるように設計されていても、実際には IDE が実行されていない場合は、プログラムノードをポートに追加できるコンポーネントが必要です。

   新しく作成されたプログラムは、同じ IDE から起動した、または関連付けられていない他のプログラムと共に、デバッグセッションを作成します。

   プログラムによって、ユーザーが最初に **F5 キー**を押したときに、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] のデバッグパッケージがメソッドを使用してプロジェクトパッケージ (起動されているプログラムの種類に関連付けられている) を呼び出します。その後 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> 、 <xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2> ソリューションのアクティブなプロジェクトデバッグ設定を使用して構造体が入力されます。 この構造体は、メソッドの呼び出しによってデバッグパッケージに戻され <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A> ます。 デバッグパッケージは、セッションデバッグマネージャー (SDM) をインスタンス化します。これにより、デバッグ中のプログラムと、関連付けられているデバッグエンジンが起動されます。

   SDM に渡される引数の1つに、プログラムを起動するために使用される DE の GUID があります。

   DE の GUID がでない場合 `GUID_NULL` 、SDM は de を共存させ、その [launchsuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) メソッドを呼び出してプログラムを起動します。 たとえば、プログラムがネイティブコードで記述されている場合、 `IDebugEngineLaunch2::LaunchSuspended` は `CreateProcess` 、 `ResumeThread` プログラムを実行するためにと (Win32 関数) を呼び出すことがあります。

   プログラムを起動した結果として、プログラムの実行時環境が読み込まれます。 その後、DE または実行時の環境では、プログラムを記述する [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスを作成し、このインターフェイスを [addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) に渡して、プログラムが実行されていることをポートに通知します。

   `GUID_NULL`が渡されると、ポートはプログラムを起動します。 プログラムが実行されると、実行時環境によって、 `IDebugProgramNode2` プログラムを記述してに渡すインターフェイスが作成され `IDebugPortNotify2::AddProgramNode` ます。 これにより、プログラムが実行されていることがポートに通知されます。 次に、SDM は、実行中のプログラムにデバッグエンジンをアタッチします。

## <a name="in-this-section"></a>このセクションの内容
 [ポートへの通知](../../extensibility/debugger/notifying-the-port.md) プログラムが起動し、ポートに通知された後の動作について説明します。

 [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md) デバッグセッションがプログラムに DE をアタッチする準備ができたときにドキュメントを追加します。

## <a name="related-sections"></a>関連項目
 [デバッグタスク](../../extensibility/debugger/debugging-tasks.md) プログラムの起動や式の評価など、さまざまなデバッグタスクへのリンクが含まれています。
