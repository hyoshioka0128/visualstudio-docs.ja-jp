---
title: 'How to: Invoke the Workflow Debugger | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
ms.assetid: 34c592af-f4f6-4d02-99f6-63a94698e48b
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 13fd54eeebf0323fcb9b8cad6a8cd8b75ae11fb3
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74292889"
---
# <a name="how-to-invoke-the-workflow-debugger"></a>ワークフロー デバッガーを呼び出す方法
ほとんどの場合、他の Visual Studio プログラミング言語で書かれたプログラムをデバッグするときと同じようにして、ワークフローをデバッグすることができます。 ワークフロー デバッガーは、次の方法で開始できます。

- Select **Attach to Process** on the **Debug** menu to select the running host process for your workflow instance. この手順は、マネージド コードのホスト プロセスへのアタッチと同じです。

- Press **F5** to start running an instance of the workflow, or to continue to run after a breakpoint has been hit.

- リモート デバッグを使用します。 For information on using remote debugging, see [How to: Enable Remote Debugging](https://go.microsoft.com/fwlink/?LinkId=196257).

    > [!NOTE]
    > If the workflow application targets the x86 architecture and is hosted on a machine running a 64 bit operating system, then remote debugging will not work unless [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] is installed on the remote machine or the target for the workflow application is changed to **Any CPU**.

### <a name="stepping-through-code"></a>コードのステップ実行

- **Step In**: You can step into an activity using **F11**. デバッガーは、任意の定義済みハンドラーにステップ インします。 ハンドラーが定義されていない場合は、アクティビティをステップ オーバーするか、(他のアクティビティを含む) 複合アクティビティの場合には、実行される最初のアクティビティにステップ インします。

- **Step Out:** You can step out of an activity using **Shift-F11**. アクティビティからステップ アウトすると、現在のアクティビティとすべての兄弟アクティビティは最後まで実行されます。 その後、デバッガーは現在のアクティビティの親で停止します。 コード ハンドラーからステップ アウトするとき、デバッガーはハンドラーに関連付けられたアクティビティで停止します。

- **Step Over**: You can step over an activity using **F10**. 複合アクティビティをステップ オーバーするときは、デバッガーが、複合アクティビティの最初の実行可能な子で停止します。 複合ではないアクティビティ (<xref:System.Activities.Statements.Assign> アクティビティなど) をステップ オーバーするときは、デバッガーが、そのアクティビティおよび関連するハンドラーを実行して、次のアクティビティで停止します。 実行されるアクティビティが複合アクティビティの最後の子アクティビティである場合、デバッガーは、それを実行した後に親アクティビティで停止します。

### <a name="debugging-with-f5"></a>F5 キーを使ったデバッグ

- If you are building a Workflow Console Application project, simply press **F5** to begin debugging into your application and workflow. アクティビティ ライブラリを単独で構築する場合は、実行可能なホスト アプリケーションをスタートアップ プロジェクトとして用意する必要があります。 To set a startup project in **Solution Explorer**, right-click the project name of the host and select **Set as StartUp Project**.

## <a name="see-also"></a>参照
 [How to: Set Breakpoints in Workflows](../workflow-designer/how-to-set-breakpoints-in-workflows.md) [Debugging Workflows with the Workflow Designer](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)