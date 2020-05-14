---
title: '方法 : マネージ コードで複数のスレッドを管理する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 59730063-cc29-4dae-baff-2234ad8d0c8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ceaa0af4f57fe374cf9cf4b2dd8b4f40af74a852
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80702778"
---
# <a name="how-to-manage-multiple-threads-in-managed-code"></a>方法 : マネージ コードで複数のスレッドを管理する
非同期メソッドを呼び出すマネージ VSPackage 拡張機能、または Visual Studio UI スレッド以外のスレッドで実行される操作がある場合は、次のガイドラインに従う必要があります。 別のスレッドでの作業が完了するのを待つ必要がないため、UI スレッドの応答性を維持できます。 スタック領域を使用する余分なスレッドがないため、コードの効率を高めることができます。

 一般に、UI スレッドから別のスレッドに切り替えたり、その逆に切り替えたりできます。 メソッドが返されるときに、現在のスレッドは、そのスレッドが最初に呼び出されたスレッドです。

> [!IMPORTANT]
> 次のガイドラインでは、<xref:Microsoft.VisualStudio.Threading>名前空間の API を使用<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>しています。 この名前空間の API は、[!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)]で新しく追加されました。 のインスタンスは<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory><xref:Microsoft.VisualStudio.Shell.ThreadHelper>プロパティ`ThreadHelper.JoinableTaskFactory`から取得できます。

## <a name="switch-from-the-ui-thread-to-a-background-thread"></a>UI スレッドからバックグラウンド スレッドに切り替える

1. UI スレッドを使用していて、バックグラウンド スレッドで非同期処理を行う場合は、次`Task.Run()`のコマンドを使用します。

    ```csharp
    await Task.Run(async delegate{
        // Now you're on a separate thread.
    });
    // Now you're back on the UI thread.

    ```

2. UI スレッドを使用していて、バックグラウンド スレッドでの作業を実行している間に同期的にブロックする場合は、 <xref:System.Threading.Tasks.TaskScheduler> `TaskScheduler.Default`で<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A>プロパティを使用します。

    ```csharp
    // using Microsoft.VisualStudio.Threading;
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        await TaskScheduler.Default;
        // You're now on a separate thread.
        DoSomethingSynchronous();
        await OrSomethingAsynchronous();
    });
    ```

## <a name="switch-from-a-background-thread-to-the-ui-thread"></a>バックグラウンド スレッドから UI スレッドに切り替える

1. バックグラウンド スレッドを使用していて、UI スレッドで何かをしたい場合は、次の方法<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>を使用します。

    ```csharp
    // Switch to main thread
    await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
    ```

     このメソッドを<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>使用して、UI スレッドに切り替えることができます。 このメソッドは、現在の非同期メソッドの継続を伴うメッセージを UI スレッドにポストし、スレッド フレームワークの残りの部分と通信して、適切な優先順位を設定し、デッドロックを回避します。

     バックグラウンド スレッド メソッドが非同期で、非同期にできない場合でも、次の例のように、次の例`await`のように、この構文を使用して、作業<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.Run%2A>をラップして UI スレッドに切り替えることができます。

    ```csharp
    ThreadHelper.JoinableTaskFactory.Run(async delegate {
        // Switch to main thread
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        // Do your work on the main thread here.
    });
    ```
