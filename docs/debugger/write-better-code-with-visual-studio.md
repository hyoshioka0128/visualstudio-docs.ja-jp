---
title: デバッグの技術とツール
description: Visual Studio を使用して例外を修正し、エラーを修正し、コードを改善することで、バグの少ない優れたコードを記述する
ms.custom:
- debug-experiment
- seodec18
ms.date: 02/14/2020
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2ac595098d793e44d65312a09fc8857225f150ef
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301021"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>より良いコードを作成するためのデバッグ手法とツール

コード内のバグやエラーを修正するには、時間がかかり、時にはイライラするタスクになります。 効果的なデバッグ方法を学ぶには時間がかかりますが、Visual Studio のような強力な IDE を使用すると、作業が非常に簡単になります。 IDE はエラーを修正し、コードをより迅速にデバッグするのに役立ちますが、バグが少ないコードを作成するのにも役立ちます。 この記事の目的は、コード アナライザーを使用するタイミング、デバッガーを使用するタイミング、例外を修正する方法、および意図をコーディングする方法を知るために、"バグ修正" プロセスの全体的なビューを提供することです。 デバッガーを使用する必要がある場合は、「[最初にデバッガーを見る](../debugger/debugger-feature-tour.md)」を参照してください。

この記事では、IDE を活用してコーディング セッションの生産性を向上させる方法について説明します。 次のようないくつかのタスクについて説明します。

* IDE のコード アナライザーを活用して、デバッグ用のコードを準備する

* 例外を修正する方法 (ランタイム エラー)

* 意図をコーディングしてバグを最小限に抑える方法 (assert を使用)

* デバッガーを使用する場合

これらのタスクを示すために、アプリをデバッグするときに発生する最も一般的な種類のエラーやバグをいくつか示します。 サンプル コードは C# ですが、概念的な情報は、通常、C++ 、Visual Basic、JavaScript、および Visual Studio でサポートされているその他の言語 (特に記載がある場合を除く) に適用されます。 スクリーン ショットは C# になっています。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>バグやエラーが含まれるサンプル アプリを作成する

次のコードには、Visual Studio IDE を使用して修正できるいくつかのバグがあります。 このアプリは、JSON データを何らかの操作から取得し、オブジェクトにデータを逆シリアル化し、新しいデータで単純なリストを更新する、シミュレートする単純なアプリです。

アプリを作成するには:

1. 作成するアプリの種類に応じて、Visual Studio をインストールし **、.NET Core クロス プラットフォーム開発**または **.NET デスクトップ開発**ワークロードのいずれかがインストールされている必要があります。

    まだ Visual Studio をインストールしていない場合は [、Visual Studio](https://visualstudio.microsoft.com/downloads/) のダウンロード ページにアクセスして無料でインストールします。

    ワークロードをインストールする必要があるが、既に Visual Studio**Tools** > がある場合は、[**ツールの取得ツールと機能**] をクリックします。 Visual Studio インストーラーが起動します。 NET **Core クロス プラットフォーム開発**または **.NET デスクトップ開発**ワークロードを選択し、[**変更**] を選択します。

1. Visual Studio を開きます。

    ::: moniker range=">=vs-2019"
    スタート ウィンドウで、[**新しいプロジェクトの作成**] を選択します。 検索ボックスに **「コンソール**」と入力し、[**コンソール アプリケーション] (.NET Core)** または **[コンソール アプリケーション] (.NET Framework)** を選択します。 **[次へ]** を選択します。 **Console_Parse_JSON**のようなプロジェクト名を入力し、[**作成**] をクリックします。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーで、[**ファイル] メニュー** > **の [新しい** > **プロジェクト**] をクリックします。 [**新しいプロジェクト**] ダイアログ ボックスの左側のウィンドウで **、[Visual C#]** の下の [**コンソール アプリ**] を選択し、中央のウィンドウで [**コンソール アプリ ] (.NET Core)** または **[コンソール アプリケーション] (.NET Framework)** を選択します。 **Console_Parse_JSON**などの名前を入力し **、[OK]** をクリックします。
    ::: moniker-end

    **コンソール アプリケーション (.NET Core) またはコンソール アプリケーション (.NET** **Framework)** プロジェクト テンプレートが表示されない場合は、**ツール** > の**取得ツールと機能**に移動して Visual Studio インストーラーを開きます。 **NET Core クロス プラットフォーム開発または .NET** **デスクトップ開発**ワークロードを選択し、[**変更**] を選択します。

    Visual Studio によってコンソール プロジェクトが作成され、ソリューション エクスプローラーの右側のウィンドウに表示されます。

1. プロジェクトの*Program.cs*ファイルの既定のコードを、次のサンプル コードに置き換えます。

```csharp
using System;
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
using System.Runtime.Serialization;
using System.IO;

namespace Console_Parse_JSON
{
    class Program
    {
        static void Main(string[] args)
        {
            var localDB = LoadRecords();
            string data = GetJsonData();

            User[] users = ReadToObject(data);

            UpdateRecords(localDB, users);

            for (int i = 0; i < users.Length; i++)
            {
                List<User> result = localDB.FindAll(delegate (User u) {
                    return u.lastname == users[i].lastname;
                    });
                foreach (var item in result)
                {
                    Console.WriteLine($"Matching Record, got name={item.firstname}, lastname={item.lastname}, age={item.totalpoints}");
                }
            }

            Console.ReadKey();
        }

        // Deserialize a JSON stream to a User object.
        public static User[] ReadToObject(string json)
        {
            User deserializedUser = new User();
            User[] users = { };
            MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(json));
            DataContractJsonSerializer ser = new DataContractJsonSerializer(users.GetType());

            users = ser.ReadObject(ms) as User[];

            ms.Close();
            return users;
        }

        // Simulated operation that returns JSON data.
        public static string GetJsonData()
        {
            string str = "[{ \"points\":4o,\"firstname\":\"Fred\",\"lastname\":\"Smith\"},{\"lastName\":\"Jackson\"}]";
            return str;
        }

        public static List<User> LoadRecords()
        {
            var db = new List<User> { };
            User user1 = new User();
            user1.firstname = "Joe";
            user1.lastname = "Smith";
            user1.totalpoints = 41;

            db.Add(user1);

            User user2 = new User();
            user2.firstname = "Pete";
            user2.lastname = "Peterson";
            user2.totalpoints = 30;

            db.Add(user2);

            return db;
        }
        public static void UpdateRecords(List<User> db, User[] users)
        {
            bool existingUser = false;

            for (int i = 0; i < users.Length; i++)
            {
                foreach (var item in db)
                {
                    if (item.lastname == users[i].lastname && item.firstname == users[i].firstname)
                    {
                        existingUser = true;
                        item.totalpoints += users[i].points;

                    }
                }
                if (existingUser == false)
                {
                    User user = new User();
                    user.firstname = users[i].firstname;
                    user.lastname = users[i].lastname;
                    user.totalpoints = users[i].points;

                    db.Add(user);
                }
            }
        }
    }

    [DataContract]
    internal class User
    {
        [DataMember]
        internal string firstname;

        [DataMember]
        internal string lastname;

        [DataMember]
        // internal double points;
        internal string points;

        [DataMember]
        internal int totalpoints;
    }
}
```

## <a name="find-the-red-and-green-squiggles"></a>赤と緑の波線を見つけよう!

サンプル アプリを起動してデバッガーを実行する前に、コード エディターでコードに赤と緑の波線が表示されるかどうかを確認します。 これらは、IDE のコード アナライザによって識別されるエラーと警告を表します。 赤い波線はコンパイル時のエラーであり、コードを実行する前に修正する必要があります。 緑色の波線は警告です。 警告を修正せずにアプリを実行することはよくありますが、バグの原因になる可能性があり、調査することで時間と手間を省くことがよくあります。 これらの警告とエラーは、リストビューを希望する場合は、[**エラー一覧**] ウィンドウにも表示されます。

サンプル アプリでは、修正する必要がある赤い波線と、見る緑色の波線が 1 つずつ表示されます。 最初のエラーはここにあります。

![赤い波線として表示中にエラーが発生しました](../debugger/media/write-better-code-red-squiggle.png)

このエラーを修正するには、電球アイコンで表される IDE の別の機能を確認します。

## <a name="check-the-light-bulb"></a>電球をチェック!

最初の赤い波線はコンパイル時のエラーを表します。 その上にカーソルを置くと、```The name `Encoding` does not exist in the current context```メッセージが表示されます。

このエラーは左下に電球アイコンを示しています。 ![ドライバー アイコン のドライバー](../ide/media/screwdriver-icon.png)アイコンと共に、電球アイコン![電球アイコン](../ide/media/light-bulb-icon.png)は、コードをインラインで修正またはリファクタリングするのに役立つクイック アクションを表します。 電球*は、修正*すべき問題を表します。 ドライバーは、修正を選択する可能性がある問題です。 最初に提案された修正プログラムを使用して、左側の**System.Text を使用して**クリックしてこのエラーを解決します。

![電球を使用してコードを修正する](../debugger/media/write-better-code-missing-include.png)

この項目をクリックすると、ステートメントが`using System.Text`*Program.cs*ファイルの先頭に追加され、赤い波線が消えます。 (推奨される修正プログラムが何を行うかわからない場合は、修正プログラムを適用する前に右側の **[変更のプレビュー** ] リンクを選択します)。

上記のエラーは、通常、コードに新しい`using`ステートメントを追加することで修正される一般的なエラーです。 このようなエラーは```The type or namespace `Name` cannot be found.```、アセンブリ参照が見つからない (プロジェクトを右クリックして**参照**の**追加** > を選択する)、名前のスペルが間違っているか、追加する必要があるライブラリが見つからない (C# の場合はプロジェクトを右クリックし **、[NuGet パッケージの管理**] を選択するなど) 、このような一般的なエラーがいくつか存在します。

## <a name="fix-the-remaining-errors-and-warnings"></a>残りのエラーと警告を修正する

このコードで見る波線がもう少しあります。 ここでは、一般的な型変換エラーが表示されます。 波線にカーソルを合わせると、コードが文字列を int に変換しようとしていることがわかります。

![型変換エラー](../debugger/media/write-better-code-conversion-error.png)

コード アナライザは意図を推測できないため、今回は電球を使用できません。 このエラーを修正するには、コードの意図を知る必要があります。 この例では、に追加`points``points`しようとしているので、数値 (整数) の値を確認するのは難しいことではありません。 `totalpoints`

このエラーを修正するには、次`points`のコードから`User`クラスのメンバーを変更します。

```csharp
[DataMember]
internal string points;
```

これを、次のように変更します。

```csharp
[DataMember]
internal int points;
```

コード エディターの赤い波線が消えます。

次に、データ メンバーの宣言で緑色の波線の上`points`にカーソルを合わせます。 コードアナライザは、変数に値が割り当てられないことを示します。

![未割り当ての変数に関する警告メッセージ](../debugger/media/write-better-code-warning-message.png)

通常、これは修正する必要がある問題を表します。 ただし、サンプル アプリでは、実際には逆シリアル化プロセス中`points`に変数にデータを格納し、その値をデータ メンバー`totalpoints`に追加します。 この例では、コードの意図がわかっており、警告を無視しても問題ありません。 ただし、警告を解消する場合は、次のコードを置き換えることができます。

```csharp
item.totalpoints = users[i].points;
```

以下に置き換えます。

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

緑色の波線が消えます。

## <a name="fix-an-exception"></a>例外を修正する

すべての赤い波線を修正し、解決した (または少なくとも調査済み) すべての緑色の波線を修正したら、デバッガーを起動してアプリを実行する準備が整いました。

**F5**キー (**デバッグ > デバッグ開始**)を押すか、[デバッグ] ツールバーの [**デバッグ**開始]![ボタンを](../debugger/media/dbg-tour-start-debugging.png "[デバッグ]")クリックします。

この時点で、サンプル アプリは`SerializationException`例外 (ランタイム エラー) をスローします。 つまり、アプリはシリアル化しようとしているデータをチョークします。 デバッグ モード (デバッガーがアタッチ) でアプリを起動したため、デバッガーの例外ヘルパーは、例外をスローしたコードに右を移動し、役に立つエラー メッセージを表示します。

![シリアル化例外が発生します。](../debugger/media/write-better-code-serialization-exception.png)

エラー メッセージは、値`4o`を整数として解析できないことを示します。 したがって、この例では、データが悪いことがわかります。 `4o` `40` しかし、実際のシナリオでデータを制御できない場合 (Web サービスから取得していると言う場合)、そのデータについてどうしますか。 これをどのように解決すればよいでしょう。

例外が発生した場合は、次の質問をする (および回答する) 必要があります。

* この例外は、あなたが修正できるバグだけですか? または、

* この例外は、ユーザーが直面する可能性のあるものですか?

前者の場合は、バグを修正します。 (サンプル アプリでは、不良データを修正することを意味します。後者の場合は、ブロックを使用してコード内の例外を`try/catch`処理する必要があります (次のセクションでは他の可能な戦略を見てください)。 サンプル アプリで、次のコードを置き換えます。

```csharp
users = ser.ReadObject(ms) as User[];
```

次のコードに置き換えます。

```csharp
try
{
    users = ser.ReadObject(ms) as User[];
}
catch (SerializationException)
{
    Console.WriteLine("Give user some info or instructions, if necessary");
    // Take appropriate action for your app
}
```

ブロック`try/catch`にはパフォーマンスコストがいくらかあるため、実際に必要な場合、つまり(a) アプリのリリースバージョンで発生する可能性があり、(b) メソッドのドキュメントでは例外を確認する必要があることを示します (ドキュメントが完了すると仮定します)。 多くの場合、例外を適切に処理でき、ユーザーはその例外を知る必要はありません。

例外処理の重要なヒントを次に示します。

* などの`catch (Exception) {}`空の catch ブロックを使用しないでください。 空または情報に関する catch ブロックを使用すると、例外が隠れてしまい、コードのデバッグが簡単になるのではなく、より困難になる可能性があります。

* 例外を`try/catch`スローする特定の関数 (`ReadObject`サンプル アプリ) の周囲でブロックを使用します。 大きなコードのチャンクの周囲で使用すると、エラーの場所が隠れてしまいます。 たとえば、ここに示す`try/catch`親関数`ReadToObject`の呼び出しの前後にブロックを使用しない場合や、例外が発生した場所が正確にわからない場合などです。

    ```csharp
    // Don't do this
    try
    {
        User[] users = ReadToObject(data);
    }
    catch (SerializationException)
    {
    }
    ```

* アプリに含まれているなじみのない関数、特に外部データとやり取りする関数 (Web 要求など) については、ドキュメントを参照して、関数がスローする可能性のある例外を確認してください。 これは、適切なエラー処理やアプリのデバッグに不可欠な情報です。

サンプル アプリの 場合は`SerializationException`、`GetJsonData`に変更`4o`してメソッド`40`内の を修正します。

## <a name="clarify-your-code-intent-by-using-assert"></a>アサートを使用してコードの意図を明確にする

[デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5** キー)。 これにより、少ない手順でアプリが再起動されます。 コンソール ウィンドウに次の出力が表示されます。

![出力の NULL 値](../debugger/media/write-better-code-using-assert-null-output.png)

この出力では、正しくないものを見ることができます。 **3**番目のレコードの**名前と姓**は空白です。

これは、関数でステートメントを使用`assert`する、多くの場合、十分に活用されていない、役に立つコーディングのプラクティスについて話す良い時期です。 次のコードを追加すると、ランタイム チェックを含め、`firstname``lastname`そのチェックが行`null`われているかどうかが確認されます。 メソッドの次のコードを`UpdateRecords`置き換えます。

```csharp
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

以下に置き換えます。

```csharp
// Also, add a using statement for System.Diagnostics at the start of the file.
Debug.Assert(users[i].firstname != null);
Debug.Assert(users[i].lastname != null);
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

開発プロセス`assert`中にこのようなステートメントを関数に追加すると、コードの意図を指定しやすくなります。 前の例では、次のように指定します。

* 名には有効な文字列が必要です
* 姓には有効な文字列が必要です

この方法でインテントを指定することで、要件を適用します。 これは、開発中にバグを表面化するために使用できる、シンプルで便利な方法です。 (`assert`ステートメントは単体テストのメイン要素としても使用されます ) 。

[デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5** キー)。

> [!NOTE]
> コード`assert`はデバッグ ビルドでのみアクティブです。

デバッガーを再起動`assert`すると、式`users[i].firstname != null`が`false``true`の代わりに評価されるため、ステートメントでデバッガーが一時停止します。

![アサートは false に解決します。](../debugger/media/write-better-code-using-assert.png)

この`assert`エラーは、調査が必要な問題があることを示します。 `assert`例外が発生する必要がない多くのシナリオをカバーできます。 この例では、ユーザーに例外が表示されず、レコードの`null`一覧に示すように`firstname`値が追加されます。 この結果、後で問題が発生する (コンソール出力に表示されるなど) ため、デバッグが困難になる場合があります。

> [!NOTE]
> 値のメソッドを呼び出す`null`シナリオでは、結果。 `NullReferenceException` 通常、一般的な例外、つまり`try/catch`特定のライブラリ関数に関連付けられていない例外に対してブロックを使用しないようにします。 任意のオブジェクトが`NullReferenceException`スローできます。 不明な場合は、ライブラリ関数のドキュメントを確認してください。

デバッグプロセス中は、実際のコード修正で置き換`assert`える必要がある場合に、特定のステートメントを保持することをお勧めします。 アプリのリリース ビルドで、ユーザーが例外を検出する可能性があるとします。 その場合は、アプリが致命的な例外をスローしたり、他のエラーが発生しないようにコードをリファクタリングする必要があります。 したがって、このコードを修正するには、次のコードを置き換えます。

```csharp
if (existingUser == false)
{
    User user = new User();
```

次のコードに置き換えます。

```csharp
if (existingUser == false && users[i].firstname != null && users[i].lastname != null)
{
    User user = new User();
```

このコードを使用すると、コード要件を満たし、`firstname`または`lastname`の値を持つレコード`null`がデータに追加されないようにします。

この例では、ループ内に`assert`2 つのステートメントを追加しました。 通常、 を`assert`使用する場合は、関数または`assert`メソッドのエントリ ポイント (先頭) にステートメントを追加することをお勧めします。 現在、サンプル アプリで`UpdateRecords`メソッドを確認しています。 このメソッドでは、メソッド引数のいずれかが`null`で問題になっている場合に問題が発生していることを知っているので、関数のエントリ ポイント`assert`にあるステートメントを使用して両方をチェックします。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

上記のステートメントの目的は、既存のデータ (`db`) を読み込み、`users`何かを更新する前に新しいデータ ( ) を取得することです。

または に`assert`解決される任意の種類の式で`true`使用できます`false`。 たとえば、このようなステートメントを`assert`追加できます。

```csharp
Debug.Assert(users[0].points > 0);
```

上記のコードは、ユーザーのレコードを更新するためにゼロ (0) より大きい新しいポイント値が必要であるという、次の意図を指定する場合に便利です。

## <a name="inspect-your-code-in-the-debugger"></a>デバッガーでコードを検査する

さて、あなたはサンプルアプリで間違っている重要なすべてを修正したので、あなたは他の重要なものに移動することができます!

デバッガーの例外ヘルパーを示しましたが、デバッガーは、コードのステップ実行や変数の検査など、他の処理も実行できる、はるかに強力なツールです。 これらの強力な機能は、多くのシナリオ、特に次のシナリオで役立ちます。

* コード内のランタイム バグを特定しようとしていますが、前に説明したメソッドやツールを使用して、それを行うことはできません。

* コードを検証する、つまり、コードが実行されている間に見て、コードが期待どおりの動作をして、必要な動作を行っていることを確認する必要があります。

    実行中にコードを監視する場合は、有益です。 コードの詳細については、この方法で学習し、明らかな現象を明らかにする前にバグを識別できます。

デバッガーの基本機能の使用方法については、「[絶対初級者のデバッグ](../debugger/debugging-absolute-beginners.md)」を参照してください。

## <a name="fix-performance-issues"></a>パフォーマンスの問題を修正

別の種類のバグには、アプリの実行速度が遅くなったり、メモリを使いすぎたりする非効率的なコードが含まれます。 一般的に、パフォーマンスの最適化は、後でアプリ開発で行うものです。 ただし、パフォーマンスの問題は早くから発生する可能性があり (たとえば、アプリの一部の実行速度が遅くなるなど)、プロファイリング ツールを使用してアプリをテストする必要がある場合があります。 CPU 使用率ツールやメモリ アナライザーなどのプロファイリング ツールの詳細については、「[最初にプロファイリング ツールを参照](../profiling/profiling-feature-tour.md)してください」 を参照してください。

## <a name="next-steps"></a>次のステップ

この記事では、コードの多くの一般的なバグを回避および修正する方法と、デバッガーを使用するタイミングについて説明しました。 次に、Visual Studio デバッガーを使用してバグを修正する方法について説明します。

> [!div class="nextstepaction"]
> [入門者向けのデバッグ](../debugger/debugging-absolute-beginners.md)
