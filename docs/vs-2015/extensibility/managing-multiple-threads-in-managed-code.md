---
title: マネージコードでの複数のスレッドの管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 296ef23bc512a86917920b3c3d5fbb5ec203a21e
ms.sourcegitcommit: a77158415da04e9bb8b33c332f6cca8f14c08f8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2020
ms.locfileid: "86387019"
---
# <a name="managing-multiple-threads-in-managed-code"></a>マネージド コードの複数のスレッドを管理する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

非同期メソッドを呼び出すマネージ VSPackage 拡張機能がある場合、または Visual Studio UI スレッド以外のスレッドで実行される操作がある場合は、次のガイドラインに従う必要があります。 別のスレッドでの作業が完了するまで待機する必要がないため、UI スレッドの応答性を維持できます。 スタック領域を占有する余分なスレッドがないため、コードの効率を向上させることができます。また、デッドロックと無応答を避けることができるため、信頼性が高く、デバッグが容易になります。  
  
 一般に、UI スレッドから別のスレッドに切り替えることも、その逆の切り替えを行うこともできます。 メソッドから制御が戻ると、現在のスレッドは、最初に呼び出されたスレッドになります。  
  
> [!IMPORTANT]
> 次のガイドラインでは、 <xref:Microsoft.VisualStudio.Threading> 名前空間の api (特にクラス) を使用し <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> ます。 この名前空間の Api は、で新しく追加されたもの [!INCLUDE[vs_dev12](../includes/vs-dev12-md.md)] です。 のインスタンスは、 <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> プロパティから取得でき <xref:Microsoft.VisualStudio.Shell.ThreadHelper> `ThreadHelper.JoinableTaskFactory` ます。  
  
## <a name="switching-from-the-ui-thread-to-a-background-thread"></a>UI スレッドからバックグラウンドスレッドへの切り替え  
  
1. UI スレッドを使用していて、バックグラウンドスレッドで非同期処理を実行する場合は、次のように指定します。  
  
    ```csharp  
    await Task.Run(async delegate{  
        // Now you’re on a separate thread.  
    });  
    // Now you’re back on the UI thread.  
  
    ```  
  
2. UI スレッドを使用していて、バックグラウンドスレッドで作業を実行している間に同期的にブロックする場合は、内のプロパティを使用し <xref:System.Threading.Tasks.TaskScheduler> `TaskScheduler.Default` <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> ます。  
  
    ```csharp  
    // using Microsoft.VisualStudio.Threading;  
    ThreadHelper.JoinableTaskFactory.Run(async delegate {  
        await TaskScheduler.Default;  
        // You're now on a separate thread.  
        DoSomethingSynchronous();  
        await OrSomethingAsynchronous();  
    });  
    ```  
  
## <a name="switching-from-a-background-thread-to-the-ui-thread"></a>バックグラウンドスレッドから UI スレッドへの切り替え  
  
1. バックグラウンドスレッドを使用していて、UI スレッドで何らかの処理を行う場合は、次のように入力し <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ます。  
  
    ```csharp  
    // Switch to main thread  
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
    ```  
  
     メソッドを使用し <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> て、UI スレッドに切り替えることができます。 このメソッドは、現在の非同期メソッドの継続を使用して UI スレッドにメッセージをポストします。また、スレッドフレームワークの残りの部分と通信して、正しい優先順位を設定し、デッドロックを回避します。  
  
     バックグラウンドスレッドメソッドが非同期ではなく、非同期にすることができない場合でも、次の例のように、を使用して `await` 作業をラップすることで、UI スレッドに切り替えることができ <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A> ます。  
  
    ```csharp  
    ThreadHelper.JoinableTaskFactory.Run(async delegate {  
        // Switch to main thread  
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();  
        // Do your work on the main thread here.  
    });  
    ```
