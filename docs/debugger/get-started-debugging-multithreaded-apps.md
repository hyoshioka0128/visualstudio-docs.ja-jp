---
title: マルチスレッド アプリケーションのデバッグについて学習する
description: Visual Studio の [並列スタック] ウィンドウと [並列ウォッチ] ウィンドウを使用してデバッグします
ms.custom: ''
ms.date: 02/14/2020
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- multithreaded debugging, tutorial
- tutorials, multithreaded debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 30fd29357ab8b42ea6a8baa6412f9ccf7eafed28
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85350512"
---
# <a name="get-started-debugging-multithreaded-applications-c-visual-basic-c"></a>マルチスレッド アプリケーションのデバッグを始める (C#、Visual Basic、C++)

Visual Studio には、マルチスレッド アプリケーションのデバッグに役立つツールとユーザー インターフェイス要素がいくつか用意されています。 このチュートリアルでは、スレッド マーカー、 **[並列スタック]** ウィンドウ、 **[並列ウォッチ]** ウィンドウ、条件付きブレークポイントの使用方法と、ブレークポイントのフィルター方法について説明します。 このチュートリアルを完了すると、マルチスレッド アプリケーションをデバッグするための Visual Studio の機能を理解できます。

次の 2 つのトピックでは、他のマルチスレッド デバッグ ツールの使用に関する追加情報が提供されています。

- **[デバッグの場所]** ツール バーと **[スレッド]** ウィンドウの使用方法については、[チュートリアル: マルチスレッド アプリケーションのデバッグ](../debugger/how-to-use-the-threads-window.md)に関するページを参照してください。

- <xref:System.Threading.Tasks.Task> (マネージド コード) と同時実行ランタイム (C++) を使用するサンプルについては、[チュートリアル: 並行アプリケーションのデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)に関するページを参照してください。 ほとんどのマルチスレッド アプリケーションの種類に適用される一般的なデバッグのヒントについては、そのトピックとこのトピックの両方を参照してください。

まず、マルチスレッド アプリケーション プロジェクトが必要です。 以下に例を示します。

## <a name="create-a-multithreaded-app-project"></a>マルチスレッド アプリ プロジェクトを作成する

1. Visual Studio を起動し、新しいプロジェクトを作成します。

   ::: moniker range=">=vs-2019"

   スタート ウィンドウが開いていない場合は、 **[ファイル]** 、 **[スタート ウィンドウ]** の順に選択します。

   スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*コンソール*」と入力またはタイプします。 次に、[言語] の一覧から **[C#]** 、 **[C++]** 、または **[Visual Basic]** を選択し、[プラットフォーム] の一覧から **[Windows]** を選択します。 

   言語とプラットフォームのフィルターを適用した後、 **[コンソール アプリ (.NET Core)]** テンプレートまたは **[コンソール アプリ]** テンプレート (C++ の場合) を選択して、 **[次へ]** を選択します。

   > [!NOTE]
   > 正しいテンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得...]** に移動して、Visual Studio インストーラーを開きます。 **[.NET デスクトップ開発]** ワークロードまたは **[C++ によるデスクトップ開発]** ワークロードを選択し、 **[変更]** を選択します。

   **[新しいプロジェクトの構成]** ウィンドウの **[プロジェクト名]** ボックスに「*MyThreadWalkthroughApp*」と入力します。 次に、 **[作成]** を選択します。

   ::: moniker-end
   ::: moniker range="vs-2017"
   上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左ペインで、以下を選択します。

   - C# アプリの場合は、 **[Visual C#]** で **[Windows デスクトップ]** を選択し、中央のペインで **[コンソール アプリ (.NET Framework)]** を選択します。
   - Visual Basic アプリの場合は、 **[Visual Basic]** で **[Windows デスクトップ]** を選択し、中央のペインで **[コンソール アプリ (.NET Framework)]** を選択します。
   - C++ アプリの場合は、 **[Visual C++]** で **[Windows デスクトップ]** を選択し、 **[Windows コンソール アプリケーション]** を選択します。

   **[コンソール アプリ (.NET Core)]** または **[コンソール アプリ]** (C++ の場合) プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動して、Visual Studio インストーラーを開きます。 **[.NET デスクトップ開発]** ワークロードまたは **[C++ によるデスクトップ開発]** ワークロードを選択し、 **[変更]** を選択します。

   次に、「*MyThreadWalkthroughApp*」のような名前を入力し、 **[OK]** をクリックします。

   **[OK]** を選択します。
   ::: moniker-end

   新しいコンソール プロジェクトが表示されます。 プロジェクトが作成されると、ソース ファイルが表示されます。 選択した言語に応じて、ソース ファイルの名前は *Program.cs*、*MyThreadWalkthroughApp.cpp*、*Module1.vb* などとなります。

1. ソース ファイルに表示されているコードを削除し、以下の適切なコード例に置き換えます。

    ```csharp
    using System;
    using System.Threading;

    public class ServerClass
    {

        static int count = 0;
        // The method that will be called when the thread is started.
        public void InstanceMethod()
        {
            Console.WriteLine(
                "ServerClass.InstanceMethod is running on another thread.");

            int data = count++;
            // Pause for a moment to provide a delay to make
            // threads more apparent.
            Thread.Sleep(3000);
            Console.WriteLine(
                "The instance method called by the worker thread has ended. " + data);
        }
    }

    public class Simple
    {
        public static void Main()
        {
            for (int i = 0; i < 10; i++)
            {
                CreateThreads();
            }
        }
        public static void CreateThreads()
        {
            ServerClass serverObject = new ServerClass();

            Thread InstanceCaller = new Thread(new ThreadStart(serverObject.InstanceMethod));
            // Start the thread.
            InstanceCaller.Start();

            Console.WriteLine("The Main() thread calls this after "
                + "starting the new InstanceCaller thread.");

        }
    }
    ```

    ```C++
    // #include "pch.h" // Use with pre-compiled header
    #include <thread>
    #include <iostream>
    #include <vector>
    #include <string>

    int count = 0;

    void doSomeWork() {

        std::cout << "The doSomeWork function is running on another thread." << std::endl;
        int data = count++;
        // Pause for a moment to provide a delay to make
        // threads more apparent.
        std::this_thread::sleep_for(std::chrono::seconds(3));
        std::string str = std::to_string(data);
        std::cout << "The function called by the worker thread has ended. " + str<< std::endl;
    }

    int main() {
        std::vector<std::thread> threads;

        for (int i = 0; i < 10; ++i) {

            threads.push_back(std::thread(doSomeWork));
            std::cout << "The Main() thread calls this after starting the new thread" << std::endl;
    }

    for (auto& thread : threads) {
        thread.join();
    }

    return 0;
    }
    ```

    ```VB
    Imports System.Threading

    Public Class ServerClass
        ' The method that will be called when the thread is started.
        Public count = 0
        Public Sub InstanceMethod()
            Console.WriteLine(
                    "ServerClass.InstanceMethod is running on another thread.")

            Dim data = count + 1
            ' Pause for a moment to provide a delay to make
            ' threads more apparent.
            Thread.Sleep(3000)
            Console.WriteLine(
                    "The instance method called by the worker thread has ended. " + data)
        End Sub

    End Class

    Public Class Simple

        Public Shared Sub Main()

            Dim ts As New ThreadStarter
            For index = 1 To 10
                ts.CreateThreads()
            Next

        End Sub

    End Class
    Public Class ThreadStarter
        Public Sub CreateThreads()
            Dim serverObject As New ServerClass()

            ' Create the thread object, passing in the
            ' serverObject.InstanceMethod method using a
            ' ThreadStart delegate.
            Dim InstanceCaller As New Thread(AddressOf serverObject.InstanceMethod)

            ' Start the thread.
            InstanceCaller.Start()

            Console.WriteLine("The Main() thread calls this after " _
                        + "starting the new InstanceCaller thread.")

        End Sub
    End Class
    ```

1. **[ファイル]** メニューの **[すべてを保存]** をクリックします。

1. (Visual Basic のみ) ソリューション エクスプローラー (右ペイン) でプロジェクト ノードを右クリックし、 **[プロパティ]** を選択します。 **[アプリケーション]** タブで、 **[スタートアップ オブジェクト]** を **[シンプル]** に変更します。

## <a name="debug-the-multithreaded-app"></a>マルチスレッド アプリをデバッグする

1. ソース コード エディターで、次のいずれかのコード スニペットを探します。

    ```csharp
    Thread.Sleep(3000);
    Console.WriteLine();
    ```

    ```C++
    std::this_thread::sleep_for(std::chrono::seconds(3));
    std::cout << "The function called by the worker thread has ended." << std::endl;
    ```

    ```VB
    Thread.Sleep(3000)
    Console.WriteLine()
    ```

1. `Thread.Sleep` または `std::this_thread::sleep_for` ステートメントの左側の余白を左クリックして、新しいブレークポイントを挿入します。

    余白の赤い円は、ブレークポイントがこの場所に設定されていることを示します。

2. **[デバッグ]** メニューの **[デバッグの開始]** (**F5** キー) を選択します。

    Visual Studio によってソリューションがビルドされ、デバッガーがアタッチされた状態でアプリの実行が開始されて、ブレークポイントでアプリが停止します。

3. ソース コード エディターで、ブレークポイントが含まれている行を探します。

### <a name="discover-the-thread-marker"></a><a name="ShowThreadsInSource"></a>スレッド マーカーを見つける  

1. [デバッグ] ツール バーで、 **[ソースのスレッドを表示]** ボタン ![ソースのスレッドを表示](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker") を選択します。

2. もう一度 **F11** キーを押して、デバッガーを 1 コード行進めます。

3. ウィンドウ左端の余白に注目します。 この行には、2 本の撚糸に似た "*スレッド マーカー*" アイコン ![スレッド マーカー](../debugger/media/dbg-thread-marker.png "ThreadMarker") が表示されています。 スレッド マーカーは、スレッドが停止している位置を示します。

    スレッド マーカーは、ブレークポイントによって部分的に隠されている場合があります。

4. スレッド マーカーの上にポインターを置きます。 データヒントには、停止されている各スレッドの名前とスレッド ID 番号が表示されます。 この場合、名前はおそらく `<noname>` になります。

5. スレッド マーカーを選択すると、ショートカット メニューに使用可能なオプションが表示されます。

### <a name="view-the-thread-locations"></a><a name="ParallelStacks"></a>スレッドの場所を表示する

**[並列スタック]** ウィンドウでは、[スレッド] ビューと (タスク ベースのプログラミングの場合) [タスク] ビューを切り替えることができ、各スレッドの呼び出し履歴情報を表示できます。 このアプリでは、[スレッド] ビューを使用できます。

1. **[デバッグ]**  >  **[Windows]**  >  **[並列スタック]** を選択して、 **[並列スタック]** ウィンドウを開きます。 次のような内容が表示されます。 正確な情報は、各スレッドの現在の位置、ハードウェア、プログラミング言語によって異なります。

    ![[並列スタック] ウィンドウ](../debugger/media/dbg-multithreaded-parallel-stacks.png "ParallelStacksWindow")

    この例では、左から右に、マネージド コードに関する次の情報が表示されています。

    - メイン スレッド (左側) は `Thread.Start` で停止しています。ここでは、停止ポイントがスレッド マーカー アイコン ![スレッド マーカー](../debugger/media/dbg-thread-marker.png "ThreadMarker") によって示されます。
    - 2 つのスレッドが `ServerClass.InstanceMethod` に入っています。1 つは現在のスレッド (黄色の矢印) で、もう一方のスレッドは `Thread.Sleep` で停止しています。
    - 新しいスレッド (右側) も開始していますが、`ThreadHelper.ThreadStart` で停止されています。

2. **[並列スタック]** ウィンドウでエントリを右クリックし、ショートカット メニューで使用可能なオプションを表示します。

    これらの右クリック メニューからはさまざまな操作を行うことができますが、このチュートリアルでは、 **[並列ウォッチ]** ウィンドウ (次のセクション) でこれらについて詳しく説明します。

    > [!NOTE]
    > 各スレッドに関する情報のリスト ビューを表示するには、代わりに **[スレッド]** ウィンドウを使用します。 「[チュートリアル:マルチスレッド アプリケーションのデバッグ](../debugger/how-to-use-the-threads-window.md)に関するページを参照してください。

### <a name="set-a-watch-on-a-variable"></a>変数にウォッチを設定する

1. **[デバッグ]**  >  **[Windows]**  >  **[並列ウォッチ]**  >  **[並列ウォッチ 1]** を選択して、 **[並列ウォッチ]** ウィンドウを開きます。

2. `<Add Watch>` というテキストが表示されているセル (または 4 番目の列の空のヘッダー セル) を選択し、「`data`」と入力します。

    各スレッドのデータ変数の値がウィンドウに表示されます。

3. `<Add Watch>` というテキストが表示されているセル (または 5 番目の列の空のヘッダー セル) を選択し、「`count`」と入力します。

    各スレッドの `count` 変数の値がウィンドウに表示されます。 この情報がまだ表示されない場合は、**F11** キーを数回押して、デバッガーでスレッドの実行を進めてください。

    ![[並列ウォッチ] ウィンドウ](../debugger/media/dbg-multithreaded-parallel-watch.png "ParallelWatchWindow")

4. ウィンドウ内のいずれかの行を右クリックし、使用可能なオプションを表示します。

### <a name="flag-and-unflag-threads"></a>スレッドに対するフラグの設定と設定解除を行う
スレッドにフラグを付けることで、重要なスレッドを追跡し、他のスレッドを無視することができます。

1. **[並列ウォッチ]** ウィンドウで、**Shift** キーを押しながら複数の行を選択します。

2. 右クリックして、 **[フラグ]** を選択します。

    選択したすべてのスレッドにフラグが設定されます。 これで、フィルター処理して、フラグが設定されたスレッドのみを表示できるようになります。

3. **[並列ウォッチ]** ウィンドウで、 **[フラグが設定されたスレッドのみを表示]** ボタン ![フラグが設定されたスレッドを表示する](../debugger/media/dbg-threads-show-flagged.png "ThreadMarker") を選択します。

    フラグが設定されたスレッドのみが一覧に表示されます。

    > [!TIP]
    > いくつかのスレッドにフラグを設定したら、コード エディターでコード行を右クリックし、 **[フラグが設定されたスレッドをカーソル行の前まで実行]** を選択できます。 フラグが設定されたすべてのスレッドが到達するコードを選択してください。 Visual Studio により選択したコード行でスレッドが一時停止されるので、[スレッドを凍結および凍結解除](#bkmk_freeze)することにより、実行の順序を簡単に制御できます。

4. **すべてのスレッドを表示**モードに戻すには、 **[フラグが設定されたスレッドのみを表示]** ボタンをもう一度選択します。

5. スレッドのフラグを解除するには、 **[並列ウォッチ]** ウィンドウでフラグが設定されたスレッドを 1 つ以上右クリックして、 **[フラグ解除]** を選択します。

### <a name="freeze-and-thaw-thread-execution"></a><a name="bkmk_freeze"></a>スレッドの実行を凍結および凍結解除する

> [!TIP]
> スレッドを凍結および凍結解除 (一時停止と再開) して、スレッドによる処理の実行順序を制御できます。 これは、デッドロックや競合状態など、同時実行の問題を解決するのに役立ちます。

1. **[並列ウォッチ]** ウィンドウですべての行を選択し、右クリックして、 **[凍結]** を選択します。

    各行の 2 番目の列に、一時停止アイコンが表示されます。 一時停止アイコンは、スレッドが凍結されていることを示します。

2. 1 行だけを選択し、他のすべての行の選択を解除します。

3. 行を右クリックして、 **[凍結解除]** を選択します。

    この行の一時停止アイコンが消え、スレッドが凍結されなくなったことが示されます。

4. コード エディターに切り替えて、**F11** キーを押します。 凍結されていないスレッドだけが実行されます。

    アプリで新しいスレッドがインスタンス化される場合があります。 新しいスレッドはすべて、フラグを設定されておらず、凍結されていません。

### <a name="follow-a-single-thread-with-conditional-breakpoints"></a><a name="bkmk_follow_a_thread"></a> 条件付きブレークポイントを使用して 1 つのスレッドを追跡する

デバッガーで 1 つのスレッドの実行を追跡すると、便利な場合があります。 これを行う 1 つの方法は、関心のないスレッドを凍結することです。 特定のバグを再現する場合など、シナリオによっては、他のスレッドを凍結せずに 1 つのスレッドを追跡することが必要になる場合があります。 他のスレッドを凍結せずにスレッドを追跡するには、関心のあるスレッド以外のコードに割り込まないようにする必要があります。 これを行うには、[条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を設定します。

スレッド名やスレッド ID など、さまざまな条件でブレークポイントを設定できます。 スレッドごとに一意であることがわかっているデータで条件を設定すると、便利な場合があります。 これは、特定のスレッドより特定のデータ値に関心がある場合の、一般的なデバッグ シナリオです。

1. 前に作成したブレークポイントを右クリックし、 **[条件]** を選択します。

2. **[ブレークポイント設定]** ウィンドウで、条件式に「`data == 5`」と入力します。

    ![条件付きブレークポイント](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint")

    > [!TIP]
    > 特定のスレッドの方に関心がある場合は、条件にスレッド名またはスレッド ID を使用します。 これを行うには、 **[ブレークポイント設定]** ウィンドウで、 **[条件式]** ではなく **[フィルター]** を選択し、フィルターのヒントに従います。 スレッド ID はデバッガーを再起動すると変化するため、アプリ コードでスレッドに名前を付けることができます。

3. **[ブレークポイント設定]** ウィンドウを閉じます。

4. [再起動] ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンを選択して、デバッグ セッションを再開します。

    データ変数の値が 5 になったスレッドで、コードに割り込みます。 **[並列ウォッチ]** ウィンドウで、現在のデバッガー コンテキストを示す黄色の矢印を探します。

5. これで、コードをステップオーバー (**F10** キー) およびステップイン (**F11** キー) して、1 つのスレッドの実行を追跡できます。

    ブレークポイントの条件がスレッドに対して一意であり、デバッガーが他のスレッドで他のブレークポイントにヒットしない場合 (無効にすることが必要な場合があります)、他のスレッドに切り替えずに、コードのステップオーバーやステップインを行うことができます。

    > [!NOTE]
    > デバッガーを進めると、すべてのスレッドが実行されます。 ただし、他のスレッドのいずれかがブレークポイントにヒットしない限り、デバッガーが他のスレッドのコードに割り込むことはありません。

## <a name="see-also"></a>関連項目

- [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [方法: デバッグ中に別のスレッドに切り替える](../debugger/how-to-switch-to-another-thread-while-debugging.md)
- [方法: [並列スタック] ウィンドウを使用する](../debugger/using-the-parallel-stacks-window.md)
- [方法: [並列ウォッチ] ウィンドウを使用する](../debugger/how-to-use-the-parallel-watch-window.md)