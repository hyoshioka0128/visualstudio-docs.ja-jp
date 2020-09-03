---
title: Windows Workflow Foundation に対するデバッガーの呼び出し (レガシ) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- stepping
- Step Over command
- stepping, commands
- debugging, using workflow debugger
- workflows, debugger
- workflow debugger, starting
- Step In command
- debugger, workflow
- Step Out command
- debugging workflows, starting the debugger
ms.assetid: d6f58e35-5cce-4ff2-9afc-b2d9d0f819cf
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: bcceca362f3c2a891d36f8f4e8071d0e35c8f164
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658979"
---
# <a name="invoking-the-visual-studio-debugger-for-windows-workflow-foundation-legacy"></a>Visual Studio Debugger for Windows Workflow Foundation の起動 (レガシ)
このトピックでは、従来の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]で [!INCLUDE[wf](../includes/wf-md.md)] アプリケーションをデバッグするための [!INCLUDE[wfd1](../includes/wfd1-md.md)] デバッガーの使用方法について説明します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 ほとんどの場合、他の Visual Studio プログラミング言語で書かれたプログラムをデバッグするときと同じようにして、従来のワークフローをデバッグすることができます。 [!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] Debugger for Windows Workflow Foundation を起動するには、次の方法に従います。

- [**デバッグ**] メニューの [**プロセスにアタッチ**] をクリックして、実行中のワークフローインスタンスを [使用可能なプロセス] から選択します。

- **F5**キーを押して、ワークフローのインスタンスの実行を開始します。または、ブレークポイントにヒットした後も実行を継続します。

## <a name="stepping-through-code"></a>コードのステップ実行
 このデバッガは、最も一般的なデバッグ手順の 1 つであるステップ実行 (コードを 1 行ずつ段階的に実行していくこと) をサポートします。 コードをステップ実行するコマンドには、次の 3 つがあります。

- **ステップイン**: **F11**キーを使用してアクティビティにステップインできます。 デバッガーは、任意の定義済みハンドラーにステップ インします。 ハンドラーが定義されていない場合は、アクティビティをステップ オーバーするか、(他のアクティビティを含む) 複合アクティビティの場合には、実行される最初のアクティビティにステップ インします。 デザイナーからコードハンドラーへのステップインは、 **IfElseActivity、** **、** **conditionedactivitygroup**、または **replicatoractivity**ではサポートされていません。 これらのアクティビティに関連したハンドラをデバッグするには、明示的なブレークポイントをコード内に配置する必要があります。

- **ステップアウト**: **Shift + F11 キー**を使用して、アクティビティからステップアウトできます。 アクティビティからステップ アウトすると、現在のアクティビティとすべての兄弟アクティビティは最後まで実行されます。 その後、デバッガーは現在のアクティビティの親で停止します。 コード ハンドラーからステップ アウトするとき、デバッガーはハンドラーに関連付けられたアクティビティで停止します。

- **ステップオーバー**: **F10**キーを使用してアクティビティをステップオーバーできます。 複合アクティビティをステップ オーバーすると、 デバッガーは複合アクティビティの最初の実行可能な子で停止します。 **CodeActivity**アクティビティなどの非複合をステップオーバーすると、デバッガーはアクティビティとそれに関連付けられたハンドラーを実行し、次のアクティビティで中断します。 実行されるアクティビティが複合アクティビティの最後の子アクティビティである場合には、デバッガはそれを実行した後、親アクティビティで停止します。

## <a name="attaching-to-a-process"></a>プロセスへのアタッチ
 プロセスにアタッチしてワークフローをデバッグするには、[**プロセスにアタッチ**] ダイアログボックスの [選択**可能な**プロセス] ボックスの一覧から、使用可能なプロセスを選択します。 [ **自動: ワークフローコード** ] が [ **アタッチ先** ] テキストボックスに表示されていない場合は、[ **選択**] をクリックします。 [ **コードの種類の選択** ] ダイアログボックスで、[次のコードの種類を **デバッグ** ] をクリックし、[ **ワークフロー**] を選択します。 [ **OK]** をクリックし、[ **アタッチ**] をクリックします。

## <a name="debugging-with-f5"></a>F5 キーを使ったデバッグ
 ワークフローのホストアプリケーションとワークフロー DLL が別の Visual Studio プロジェクトに配置されている場合 (たとえば、ワークフローアクティビティライブラリを使用している場合)、 **F5 キー**を使用してワークフローをデバッグするために、ワークフロー dll プロジェクトを visual studio ソリューションのスタートアッププロジェクトとして設定する必要があります。 また、ワークフロー DLL プロジェクトの **Start external program** プロパティでホストアプリケーションのパスを設定する必要があります。

 ソリューションエクスプローラーでスタートアッププロジェクトを設定するには、プロジェクト名を右クリックし、[ **スタートアッププロジェクトに設定**] を選択します。 [ **外部プログラムの開始** ] プロパティでホストのパスを設定するには、ソリューションエクスプローラーでワークフロープロジェクトの [ **プロパティ** ] ノードをダブルクリックし、[ **デバッグ** ] タブを選択します。[ **開始アクション**] で、[ **外部プログラムの開始** ] を選択し、デバッグするワークフローをホストしている .exe ファイルへのパスを入力します。

 ホスト アプリケーションがスタートアップ プロジェクトとして設定されている場合は、Visual Studio デバッガだけがデバッグ用に起動されます。[!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] Debugger for Windows Workflow Foundation は起動されません。 Visual Studio デバッガを使用する場合、C# または Visual Basic コード ブレークポイントだけがヒットします。ワークフロー デザイナで設定されたブレークポイントはヒットしません。 たとえば、デザイナで <xref:System.Workflow.Activities.ParallelActivity> アクティビティに対して設定したブレークポイントは、[!INCLUDE[vs_current_long](../includes/vs-current-long-md.md)] Debugger for Windows Workflow Foundation が使用される場合にヒットしますが、Visual Studio デバッガが使用される場合はヒットしません。

## <a name="see-also"></a>参照
 [方法: ワークフローにブレークポイントを設定する (レガシ)](../workflow-designer/how-to-set-breakpoints-in-workflows-legacy.md) [従来のワークフローのデバッグ](../workflow-designer/debugging-legacy-workflows.md)