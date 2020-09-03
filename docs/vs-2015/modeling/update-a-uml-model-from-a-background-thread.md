---
title: バックグラウンドスレッドから UML モデルを更新する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 42c06b0b-b681-4e19-b5f3-6116dd2a4072
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9e6626faa09f1e38506c2d205d13caa9a3707fc0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659465"
---
# <a name="update-a-uml-model-from-a-background-thread"></a>バックグラウンド スレッドから UML モデルを更新する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

バックグラウンド スレッドでモデルに変更を加えると便利な場合があります。 たとえば、低速な外部リソースから情報を読み込む場合は、バックグラウンド スレッドを使用して更新を管理できます。 これにより、ユーザーは、実行された更新をすぐに確認できます。

 ただし、UML ストアがスレッド セーフでないことに注意してください。 重要な注意点を次に示します。

- モデルまたは図に対するすべての更新は、ユーザー インターフェイス (UI) スレッドで行う必要があります。 バックグラウンド スレッドでは、<xref:System.Windows.Forms.Control.Invoke%2A> または `Dispatcher.`<xref:System.Windows.Threading.Dispatcher.Invoke%2A> を使用して、UI スレッドで実際の更新を行う必要があります。

- 一連の変更を単一のトランザクションにグループ化する場合は、トランザクションの実行中にユーザーがモデルを編集できないようにすることをお勧めします。 そうしないと、ユーザーが行った編集が同じトランザクションに含まれます。 モーダル ダイアログ ボックスを表示して、ユーザーが変更を行うことができないようにすることができます。 必要に応じて、ダイアログ ボックスにキャンセル ボタンを追加できます。 ユーザーは、実行された変更を確認することができます。

## <a name="example"></a>例
 この例では、バックグラウンド スレッドを使用してモデルにいくつかの変更を加えます。 スレッドの実行中にユーザーを除外するためにダイアログ ボックスが使用されます。 この簡単な例では、ダイアログ ボックスにキャンセル ボタンは用意されていません。 ただし、ボタンは簡単に追加できます。

#### <a name="to-run-the-example"></a>例を実行するには

1. 「 [モデリング図のメニューコマンドの定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)」の説明に従って、C# プロジェクトでコマンドハンドラーを作成します。

2. 次のアセンブリへの参照がプロジェクトに含まれていることを確認します。

   - Microsoft.VisualStudio.ArchitectureTools.Extensibility

   - Microsoft.VisualStudio.Modeling.Sdk.[バージョン]

   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[バージョン]

   - Microsoft.VisualStudio.Uml.Interfaces

   - System.ComponentModel.Composition

   - System.Windows.Forms

3. プロジェクトに、" **進行形式**" という名前の Windows フォームを追加します。 このフォームには、更新が実行中であることを示すメッセージが表示されます。 他のコントロールを追加する必要はありません。

4. 手順 7. の後に記載されているコードを格納している C# ファイルを追加します。

5. プロジェクトをビルドして実行します。

    [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の新しいインスタンスが実験モードで起動されます。

6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用のインスタンスで UML クラス図を作成するか、または開きます。

7. UML クラス図の任意の場所を右クリックし、[ **いくつかの Uml クラスの追加**] をクリックします。

   複数の新しいクラス ボックスが 0.5 秒間隔で図に順次表示されます。

```csharp
using System;
using System.ComponentModel;
using System.ComponentModel.Composition;
using System.Threading;
using System.Windows.Forms;

using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
using Microsoft.VisualStudio.Uml.Classes;

namespace BackgroundThreadProgressUI // CHANGE TO YOUR NAMESPACE
{
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  class UmlClassAdderCommand : ICommandExtension
  {

    [Import]
    IDiagramContext context { get; set; }

    [Import]
    ILinkedUndoContext linkedUndoContext { get; set; }

    // Called when the user runs the command.
    public void Execute(IMenuCommand command)
    {
      // The form that will exclude the user.
      ProgressForm form = new ProgressForm();

      // System.ComponentModel.BackgroundWorker is a
      // convenient way to run a background thread.
      BackgroundWorker worker = new BackgroundWorker();
      worker.WorkerSupportsCancellation = true;

      worker.DoWork += delegate(object sender, DoWorkEventArgs args)
      {
        // This block will be executed in a background thread.

        IClassDiagram diagram = context.CurrentDiagram as IClassDiagram;
        IModelStore store = diagram.ModelStore;
        const int CLASSES_TO_CREATE = 15;

        // Group all the changes together.
        using (ILinkedUndoTransaction transaction = linkedUndoContext.BeginTransaction("Background Updates"))
        {
          for (int i = 1; i < CLASSES_TO_CREATE; i++)
          {
            if (worker.CancellationPending)
               return; // No commit - undo all.

            // Create model elements using the UI thread by using
            // the Invoke method on the progress form. Always
            // modify the model and diagrams from a UI thread.
            form.Invoke((MethodInvoker)(delegate
            {
              IClass newClass = store.Root.CreateClass();
              newClass.Name = string.Format("NewClass{0}", i);
              diagram.Display(newClass);
            }));

            // Sleep briefly so that we can watch the updates.
            Thread.Sleep(500);
          }

          // Commit the transaction or it will be rolled back.
          transaction.Commit();
        }
      };

      // Close the form when the thread completes.
      worker.RunWorkerCompleted += delegate(object sender, RunWorkerCompletedEventArgs args)
      {
        form.Close();
      };

      // Start the thread before showing the modal progress dialog.
      worker.RunWorkerAsync();

      // Show the form modally, parented on VS.
      // Prevents the user from making changes while in progress.
      form.ShowDialog();
    }

    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled = command.Visible = true;
    }

    public string Text
    {
      get { return "Add several classes"; }
    }
  }
}
```

#### <a name="to-allow-the-user-to-cancel-the-thread-in-the-example"></a>上記の例でユーザーにスレッドの取り消しを許可するには

1. プログレス ダイアログ ボックスにキャンセル ボタンを追加します。

2. プログレス ダイアログ ボックスに次のコードを追加します。

     `public event MethodInvoker Cancel;`

     `private void CancelButton_Click(object sender, EventArgs e)`

     `{`

     `Cancel();`

     `}`

3. Execute() メソッドのフォームの構造の後に次の行を挿入します。

     `form.Cancel += delegate() { worker.CancelAsync(); };`

### <a name="other-methods-of-accessing-the-ui-thread"></a>UI スレッドにアクセスするためのその他のメソッド
 ダイアログ ボックスを作成しない場合は、次のコードを使用して、図を表示するコントロールにアクセスできます。

 `DiagramView uiThreadHolder = context.CurrentDiagram.GetObject<Diagram>().ActiveDiagramView;`

 `uiThreadHolder.Invoke()` を使用すると、UI スレッドで操作を実行できます。

## <a name="see-also"></a>参照
 [モデリング図にメニューコマンドを定義](../modeling/define-a-menu-command-on-a-modeling-diagram.md)する[モデリング図にジェスチャハンドラーを定義](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)する
