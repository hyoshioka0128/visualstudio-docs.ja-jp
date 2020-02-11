---
title: マルチスレッドアプリケーションのデバッグについて学習する
description: Visual Studio の [並列スタック] ウィンドウと [並列ウォッチ] ウィンドウを使用したデバッグ
ms.custom: ''
ms.date: 11/16/2018
ms.topic: conceptual
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
ms.openlocfilehash: 6e21d5174c9a909e9ad8031dfb7585abc52a7e78
ms.sourcegitcommit: 00ba14d9c20224319a5e93dfc1e0d48d643a5fcd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2020
ms.locfileid: "77091796"
---
# <a name="get-started-debugging-multithreaded-applications-c-visual-basic-c"></a>マルチスレッドアプリケーションのデバッグをC#開始する ( C++、Visual Basic、)

Visual Studio には、マルチスレッドアプリケーションのデバッグに役立つ、いくつかのツールとユーザーインターフェイス要素が用意されています。 このチュートリアルでは、スレッドマーカー、**並列スタック**ウィンドウ、**並列ウォッチ**ウィンドウ、条件付きブレークポイント、フィルターブレークポイントの使用方法について説明します。 このチュートリアルを完了すると、マルチスレッドアプリケーションをデバッグするための Visual Studio の機能に慣れることができます。

次の2つのトピックでは、その他のマルチスレッドデバッグツールの使用に関する追加情報を提供します。

- デバッグの **[場所]** ツールバーと **[スレッド]** ウィンドウを使用するには、「[チュートリアル: マルチスレッドアプリケーションのデバッグ](../debugger/how-to-use-the-threads-window.md)」を参照してください。

- 使用するサンプルの<xref:System.Threading.Tasks.Task>(マネージ コード) を参照してください (C++)、同時実行ランタイムと[チュートリアル: 並行アプリケーションをデバッグ](../debugger/walkthrough-debugging-a-parallel-application.md)します。 ほとんどのマルチスレッドアプリケーションの種類に適用される一般的なデバッグのヒントについては、そのトピックとこのトピックの両方を参照してください。

まず、マルチスレッドアプリケーションプロジェクトが必要です。 以下に例を示します。

## <a name="create-a-multithreaded-app-project"></a>マルチスレッドアプリプロジェクトを作成する

1. Visual Studio を起動し、新しいプロジェクトを作成します。

   ::: moniker range=">=vs-2019"

   スタート ウィンドウが開いていない場合は、 **[ファイル]** 、>[スタート ウィンドウ]** の順に選択します。

   スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。

   **[新しいプロジェクトの作成]** ウィンドウで、検索ボックスに「*コンソール*」と入力またはタイプします。 次に、 **C#** **C++** 言語 ボックスの一覧で、、、または**Visual Basic**を選択し、プラットフォーム ボックスの一覧から  **Windows** を選択します。 

   言語とプラットフォームのフィルターを適用したら、**コンソールアプリ (.net Core)** を選択するかC++、**コンソールアプリ**テンプレートを選択し、 **[次へ]** を選択します。

   > [!NOTE]
   > 正しいテンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能の取得]** に移動して、Visual Studio インストーラーを開きます。 **[.NET デスクトップ開発]** ワークロードまたは **[C++ によるデスクトップ開発]** ワークロードを選択し、 **[変更]** を選択します。

   **[新しいプロジェクトの構成]** ウィンドウで、 **[プロジェクト名]** ボックスに「 *mythread」* と入力するか、「」と入力します。 次に、 **[作成]** を選択します。

   ::: moniker-end
   ::: moniker range="vs-2017"
   上部のメニュー バーで、 **[ファイル]** 、 > [新規作成] **、** [プロジェクト] >  の順に選択します。 **[新しいプロジェクト]** ダイアログボックスの左ペインで、次のように選択します。

   - C#アプリの場合、 **[ビジュアルC# ]** の下で **[Windows デスクトップ]** を選択し、中央のウィンドウで **[コンソールアプリ (.NET Framework)]** を選択します。
   - Visual Basic アプリの場合は、 **[Visual Basic]** の下で **[Windows デスクトップ]** を選択し、中央のウィンドウで **[コンソールアプリ (.NET Framework)]** を選択します。
   - アプリの場合、 **[ビジュアルC++ ]** で **[windows デスクトップ]** 、、 **[windows コンソールアプリケーション]** の順に選択します。 C++

   **コンソールアプリ (.Net Core)** が表示されない場合、またC++は**コンソールアプリケーション**プロジェクトテンプレートの場合は、 **[ツール]**  >  **[ツールと機能の取得]** に移動し、Visual Studio インストーラーを開きます。 **[.NET デスクトップ開発]** ワークロードまたは **[C++ によるデスクトップ開発]** ワークロードを選択し、 **[変更]** を選択します。

   次に、 *Mythreadの*ような名前を入力し、[ **OK]** をクリックします。

   **[OK]** を選択します。
   ::: moniker-end

   新しいコンソール プロジェクトが表示されます。 プロジェクトが作成されると、ソースファイルが表示されます。 選択した言語に応じて、ソースファイルは*Program.cs、* *mythread*、または module1.vb と呼ばれる場合が*あります。*

1. ソースファイルに表示されているコードを削除し、以下の適切なコード例に置き換えます。

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

1. (Visual Basic のみ)ソリューションエクスプローラー (右側のウィンドウ) で、プロジェクトノードを右クリックし、 **[プロパティ]** を選択します。 **[アプリケーション]** タブで、**スタートアップオブジェクト**を**Simple**に変更します。

## <a name="debug-the-multithreaded-app"></a>マルチスレッドアプリをデバッグする

1. ソースコードエディターで、次のいずれかのコードスニペットを探します。

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

    余白では、赤い円は、ブレークポイントがこの場所に設定されていることを示します。

2. **[デバッグ]** メニューの **[デバッグの開始]** をクリックします (**F5 キー**)。

    Visual Studio によってソリューションがビルドされ、デバッガーがアタッチされた状態でアプリが実行を開始し、ブレークポイントでアプリが停止します。

3. ソースコードエディターで、ブレークポイントが含まれている行を見つけます。

### <a name="ShowThreadsInSource"></a>スレッドマーカーの検出  

1. デバッグ ツールバーで、 **[ソースのスレッドを表示]** ボタンをクリックし、![ソースにスレッドを表示する](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker") を選択します。

2. **F11**キーを1回押して、デバッガーを1行のコードに進めます。

3. ウィンドウ左端の余白に注目します。 この行には、2つのツイストスレッドに似た*スレッドマーカー*アイコン![スレッドマーカー](../debugger/media/dbg-thread-marker.png "ThreadMarker")が表示されます。 スレッド マーカーは、スレッドが停止している位置を示します。

    スレッドマーカーは、ブレークポイントによって部分的に非表示にされる場合があります。

4. スレッド マーカーの上にポインターを置きます。 各停止したスレッドの名前とスレッド ID 番号を示す DataTip が表示されます。 この場合、名前は `<noname>`のようになります。

5. スレッドマーカーを選択すると、ショートカットメニューの使用可能なオプションが表示されます。

### <a name="ParallelStacks"></a>スレッドの場所を表示する

**[並列スタック]** ウィンドウでは、スレッドビューと (タスクベースのプログラミングの) タスクビューを切り替えることができます。また、各スレッドの呼び出し履歴情報を表示できます。 このアプリでは、スレッドビューを使用できます。

1. [**デバッグ** > **Windows** > **並列スタック**] を選択して、 **[並列スタック]** ウィンドウを開きます。 次のような内容が表示されます。 正確な情報は、各スレッドの現在の場所、ハードウェア、およびプログラミング言語によって異なります。

    ![並列スタックウィンドウ](../debugger/media/dbg-multithreaded-parallel-stacks.png "ParallelStacksWindow")

    この例では、左から右に、マネージコードに関する次の情報が表示されます。

    - メインスレッド (左側) が `Thread.Start`で停止しました。ここで、停止ポイントはスレッドマーカーアイコン![スレッドマーカー](../debugger/media/dbg-thread-marker.png "ThreadMarker")によって示されます。
    - 2つのスレッドが `ServerClass.InstanceMethod`に入りました。1つは現在のスレッド (黄色の矢印) で、もう一方のスレッドは `Thread.Sleep`で停止されています。
    - 新しいスレッド (右側) も開始されていますが、`ThreadHelper.ThreadStart`で停止しています。

2. **[並列スタック]** ウィンドウのエントリを右クリックすると、ショートカットメニューの使用可能なオプションが表示されます。

    これらの右クリックメニューからさまざまな操作を実行できますが、このチュートリアルでは、 **[並列ウォッチ]** ウィンドウ (次のセクション) でこれらの詳細について説明します。

    > [!NOTE]
    > 各スレッドに関する情報を含むリストビューを表示するには、代わりに **[スレッド]** ウィンドウを使用します。 「[チュートリアル: マルチスレッドアプリケーションのデバッグ」を](../debugger/how-to-use-the-threads-window.md)参照してください。

### <a name="set-a-watch-on-a-variable"></a>変数にウォッチを設定する

1. [**デバッグ** > **Windows** > **並列**ウォッチ > **並列ウォッチ 1**] を選択して **[並列ウォッチ]** ウィンドウを開きます。

2. `<Add Watch>` テキスト (または4番目の列の空のヘッダーセル) が表示されているセルを選択し、「`data`」と入力します。

    各スレッドのデータ変数の値がウィンドウに表示されます。

3. `<Add Watch>` テキストが表示されているセル (または5番目の列の空のヘッダーセル) を選択し、「`count`」と入力します。

    各スレッドの `count` 変数の値がウィンドウに表示されます。 この情報がまだ表示されていない場合は、 **F11**キーを数回押して、デバッガーでスレッドの実行を進めるようにしてください。

    ![並列ウォッチウィンドウ](../debugger/media/dbg-multithreaded-parallel-watch.png "ParallelWatchWindow")

4. ウィンドウ内のいずれかの行を右クリックすると、使用可能なオプションが表示されます。

### <a name="flag-and-unflag-threads"></a>スレッドに対するフラグの設定と設定解除を行う
スレッドにフラグを付けることで、重要なスレッドを追跡し、他のスレッドを無視することができます。

1. **[並列ウォッチ]** ウィンドウで、 **shift**キーを押しながら複数の行を選択します。

2. 右クリックして **[フラグ]** を選択します。

    選択されたすべてのスレッドにフラグが設定されます。 これで、フィルター処理して、フラグが設定されたスレッドのみを表示できるようになりました。

3. **[並列ウォッチ]** ウィンドウで、フラグが設定された **[スレッドのみを表示]** ボタンを選択すると、![フラグ付きのスレッドが表示](../debugger/media/dbg-threads-show-flagged.png "ThreadMarker")されます。

    フラグが設定されたスレッドのみが一覧に表示されます。

    > [!TIP]
    > 一部のスレッドにフラグを設定したら、コードエディターでコード行を右クリックし、[フラグが設定された**スレッドをカーソルに実行**] を選択します。 すべてのフラグが設定されたスレッドがリーチするコードを選択してください。 Visual Studio は、選択したコード行のスレッドを一時停止します。これにより、[スレッドの凍結と凍結](#bkmk_freeze)解除によって実行の順序を制御しやすくなります。

4. フラグが設定された **[スレッドのみを表示]** ボタンをもう一度クリックして、 **[すべてのスレッドの表示]** モードに戻します。

5. スレッドのフラグを解除するには、 **[並列ウォッチ]** ウィンドウで1つ以上のフラグが設定されたスレッドを右クリックし、 **[フラグ]** の解除 を選択します。

### <a name="bkmk_freeze"></a>スレッド実行の凍結と凍結解除

> [!TIP]
> スレッドの凍結と凍結解除 (中断と再開) を行って、スレッドが作業を実行する順序を制御できます。 これは、デッドロックや競合状態などの同時実行の問題を解決するのに役立ちます。

1. **[並列ウォッチ]** ウィンドウで、すべての行を選択した状態で右クリックし、 **[フリーズ]** を選択します。

    2番目の列には、行ごとに一時停止アイコンが表示されます。 [一時停止] アイコンは、スレッドが固定されていることを示します。

2. 1行だけを選択して、他のすべての行の選択を解除します。

3. 行を右クリックし、[**凍結**解除] を選択します。

    この行の [一時停止] アイコンが消え、スレッドが凍結されなくなったことが示されます。

4. コードエディターに切り替えて、 **F11**キーを押します。 凍結されていないスレッドだけが実行されます。

    アプリでは、いくつかの新しいスレッドをインスタンス化することもできます。 新しいスレッドはすべてフラグがなしで、固定されていません。

### <a name="bkmk_follow_a_thread"></a>条件付きブレークポイントを使用して1つのスレッドに従う

デバッガーで1つのスレッドを実行すると便利な場合があります。 これを行う1つの方法として、関心のないスレッドを凍結する方法があります。 場合によっては、特定のバグを再現するなど、他のスレッドをフリーズせずに1つのスレッドに従う必要があります。 他のスレッドを凍結せずにスレッドに従うには、関心のあるスレッド以外のコードの中断を避ける必要があります。 これを行うには、[条件付きブレークポイント](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)を設定します。

スレッド名やスレッド ID など、さまざまな条件にブレークポイントを設定できます。 各スレッドに対して一意であることがわかっているデータの条件を設定すると便利な場合があります。 これは、特定のスレッドよりも特定のデータ値に関心がある一般的なデバッグシナリオです。

1. 以前に作成したブレークポイントを右クリックし、 **[条件]** を選択します。

2. **[ブレークポイントの設定]** ウィンドウで、条件式の `data == 5` を入力します。

    ![条件付きブレークポイント](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint ポイント")

    > [!TIP]
    > 特定のスレッドに関心がある場合は、その条件にスレッド名またはスレッド ID を使用します。 **[ブレークポイントの設定]** ウィンドウでこれを行うには、[**条件式**の代わりに**フィルター** ] を選択し、フィルターのヒントに従います。 デバッガーを再起動すると、スレッド Id が変化するため、アプリコードでスレッドに名前を付けることができます。

3. **[ブレークポイントの設定]** ウィンドウを閉じます。

4. [再起動![アプリ](../debugger/media/dbg-tour-restart.png "RestartApp")の再起動] ボタンを選択して、デバッグセッションを再開します。

    データ変数の値が5であるスレッドでコードを分割します。 **[並列ウォッチ]** ウィンドウで、現在のデバッガーコンテキストを示す黄色の矢印を探します。

5. これで、コードをステップオーバー (**F10**) してコードにステップイン (**F11**) し、1つのスレッドの実行に従うことができます。

    ブレークポイントの条件がスレッドに対して一意であり、デバッガーが他のスレッドの他のブレークポイントにヒットしていない場合 (無効にする必要がある場合もあります)、他のスレッドに切り替えずにコードをステップオーバーしてコードにステップインできます。

    > [!NOTE]
    > デバッガーを進めると、すべてのスレッドが実行されます。 ただし、他のスレッドの1つがブレークポイントにヒットしない限り、デバッガーは他のスレッドでコードを中断しません。

## <a name="see-also"></a>参照

- [マルチスレッド アプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [方法 : デバッグ中に別のスレッドに切り替える](../debugger/how-to-switch-to-another-thread-while-debugging.md)
- [方法: [並列スタック] ウィンドウを使用する](../debugger/using-the-parallel-stacks-window.md)
- [方法: [並列ウォッチ] ウィンドウを使用する](../debugger/how-to-use-the-parallel-watch-window.md)