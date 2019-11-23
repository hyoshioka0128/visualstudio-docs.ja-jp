---
title: デバッグの技術とツール
description: Visual Studio を使用して例外を修正し、エラーを修正して、コードを改善することで、バグが少ないコードをより適切に記述します
ms.custom:
- debug-experiment
- seodec18
ms.date: 01/24/2019
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1fe0a9bb1e966bd1451bb5d816eaab814071fb5
ms.sourcegitcommit: 7825d4163e52d724e59f6c0da209af5fbef673f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72000168"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>より優れたコードを記述するためのデバッグ手法とツール

コード内のバグとエラーを修正すると、時間がかかり、場合によっては面倒な作業になることがあります。 効率的にデバッグする方法については時間がかかりますが、Visual Studio のような強力な IDE では、仕事がはるかに簡単になります。 IDE を使用すると、エラーの修正やコードのデバッグをより迅速に行うことができます。それだけでなく、より適切なコードを記述してバグを減らすこともできます。 この記事の目的は、"バグ修正" プロセスの全体像を示すことです。そのため、コードアナライザーを使用するタイミング、デバッガーを使用するタイミング、例外を修正する方法、インテントをコーディングする方法を知ることができます。 デバッガーを使用する必要があることが既にわかっている場合は、「[デバッガーの概要](../debugger/debugger-feature-tour.md)」を参照してください。

この記事では、IDE を利用してコーディングセッションの生産性を高める方法について説明します。 ここでは、次のようないくつかのタスクについて説明します。

* IDE のコードアナライザーを利用し、デバッグ用のコードを準備する

* 例外を修正する方法 (実行時エラー)

* 意図したコーディングでバグを最小化する方法 (assert を使用)

* デバッガーを使用する場合

これらのタスクをデモンストレーションするために、アプリをデバッグするときに発生する最も一般的な種類のエラーとバグをいくつか示します。 このサンプルコードはですC#が、概念情報は、、Visual Basic C++、JavaScript、および Visual Studio でサポートされているその他の言語 (特に記載されている場合を除く) に対して一般的に適用されます。 スクリーン ショットは C# になっています。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>いくつかのバグとエラーを含むサンプルアプリを作成する

次のコードには、Visual Studio IDE を使用して修正できるいくつかのバグがあります。 ここでのアプリは、ある操作からの JSON データの取得、オブジェクトへのデータの逆シリアル化、および新しいデータを使用した単純なリストの更新をシミュレートする単純なアプリです。

アプリを作成するには:

1. Visual Studio を開き、[**ファイル** > **新しい** > **プロジェクト**] を選択します。 **[ビジュアルC# ]** で、 **[Windows デスクトップ]** または **[.net Core]** を選択し、中央のウィンドウで**コンソールアプリ**を選択します。

    > [!NOTE]
    > **[コンソール アプリケーション]** プロジェクト テンプレートが表示されない場合は、 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウにある **[Visual Studio インストーラーを開く]** リンクをクリックします。 Visual Studio インストーラーが起動します。 **[.NET デスクトップ開発]** または **[.NET Core クロスプラットフォームの開発]** ワークロードを選択し、 **[変更]** を選択します。

2. **[名前]** フィールドに「 **Console_Parse_JSON** 」と入力し、[ **OK]** をクリックします。 Visual Studio によってプロジェクトが作成されます。

3. プロジェクトの*Program.cs*ファイルの既定のコードを、次のサンプルコードに置き換えます。

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

## <a name="find-the-red-and-green-squiggles"></a>赤と緑の波線を検索します。

サンプルアプリを起動してデバッガーを実行する前に、コードエディターのコードで赤と緑の波線を確認してください。 これらは、IDE のコードアナライザーによって識別されるエラーと警告を表します。 赤い波線はコンパイル時のエラーであり、コードを実行する前に修正する必要があります。 緑の波線は警告です。 多くの場合、警告を修正せずにアプリを実行できますが、バグの原因となる場合があります。また、多くの場合、バグを調査することによって時間と問題を節約できます。 これらの警告とエラーは、リストビューを使用する場合に**エラー一覧**ウィンドウにも表示されます。

サンプルアプリでは、修正が必要ないくつかの赤い波線と、1つの緑色の波線が表示されます。 最初のエラーを次に示します。

![赤い波線で表示されるエラー](../debugger/media/write-better-code-red-squiggle.png)

このエラーを解決するには、電球アイコンによって表される IDE の別の機能を確認します。

## <a name="check-the-light-bulb"></a>電球をチェックします。

最初の赤い波線は、コンパイル時のエラーを表します。 その上にマウスポインターを合わせると、```The name `Encoding` does not exist in the current context```というメッセージが表示されます。

このエラーは、左下に電球アイコンが表示されていることに注意してください。 ドライバーアイコン ![ドライバーアイコン](../ide/media/screwdriver-icon.png)、電球アイコン ![電球アイコン](../ide/media/light-bulb-icon.png) は、コードインラインの修正またはリファクタリングに役立つクイックアクションを表します。 電球は、修正する*必要*がある問題を表します。 ドライバーは、修正が必要な問題を対象としています。 左側にある [system.string]**を**クリックして、このエラーを解決するには、最初の修正候補を使用します。

![電球を使用してコードを修正する](../debugger/media/write-better-code-missing-include.png)

この項目をクリックすると、Visual Studio によって*Program.cs*ファイルの先頭に `using System.Text` ステートメントが追加され、赤い波線が表示されなくなります。 (推奨される修正方法がわからない場合は、修正プログラムを適用する前に、右側にある **[変更のプレビュー]** リンクを選択してください)。

前述のエラーは、コードに新しい `using` ステートメントを追加することによって通常修正される一般的なエラーです。 このようなエラーには、いくつかの一般的なエラーがあります。たとえば、アセンブリ参照が存在しないこと (プロジェクトを右クリックして [**参照**の > **追加**] を選択)、スペルミスの名前、または追加C#する必要のあるライブラリ (の場合は、プロジェクトを右クリックして **[NuGet パッケージの管理]** ) を ```The type or namespace `Name` cannot be found.``` ます。

## <a name="fix-the-remaining-errors-and-warnings"></a>残りのエラーと警告を修正する

このコードでは、さらにいくつかの波線が表示されます。 ここでは、一般的な型変換エラーが表示できます。 波線の上にマウスポインターを置くと、コードが文字列を int に変換しようとしていることがわかります。これは、変換を行う明示的なコードを追加しない限り、サポートされていません。

![型変換エラー](../debugger/media/write-better-code-conversion-error.png)

コードアナライザーは意図を推測できないため、この時間を短縮するための電球はありません。 このエラーを修正するには、コードの意図を理解している必要があります。 この例では、`totalpoints`に `points` を追加しようとしているため、`points` が数値 (整数) 値である必要はありません。

このエラーを修正するには、`User` クラスの `points` メンバーを次のように変更します。

```csharp
[DataMember]
internal string points;
```

変更後は次のようになります。

```csharp
[DataMember]
internal int points;
```

コードエディターの赤い波線が消えます。

次に、`points` データメンバーの宣言で緑色の波線の上にマウスポインターを置きます。 コードアナライザーからは、変数に値が割り当てられていないことがわかります。

![未割り当て変数に関する警告メッセージ](../debugger/media/write-better-code-warning-message.png)

通常、これは修正する必要がある問題を表します。 ただし、このサンプルアプリでは、逆シリアル化プロセス中に `points` 変数にデータを格納し、その値を `totalpoints` データメンバーに追加しています。 この例では、コードの意図がわかっていて、警告を無視しても問題ありません。 ただし、警告を除去する場合は、次のコードを置き換えることができます。

```csharp
item.totalpoints = users[i].points;
```

以下に置き換えます。

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

緑の波線が消えます。

## <a name="fix-an-exception"></a>例外を修正する

すべての赤の波線を修正し、少なくとも調査している場合は、すべての緑の波線が表示されたら、デバッガーを起動してアプリを実行する準備ができています。

**F5** キー ( **[デバッグ] > [デバッグの開始]** ) を押すか、またはデバッグ ツールバーの **[デバッグの開始]** ボタン ![デバッグの開始](../debugger/media/dbg-tour-start-debugging.png "デバッグの開始") を選択します。

この時点で、サンプルアプリは `SerializationException` 例外 (ランタイムエラー) をスローします。 つまり、アプリでは、シリアル化しようとしているデータに対してチョークが発生します。 デバッグモード (デバッガーにアタッチされている) でアプリを起動したため、デバッガーの例外ヘルパーは例外をスローしたコードに直接アクセスし、役に立つエラーメッセージを表示します。

![SerializationException が発生します](../debugger/media/write-better-code-serialization-exception.png)

このエラーメッセージは、`4o` 値を整数として解析できないことを指示します。 この例では、データが不適切であることがわかっています。 `4o` `40`する必要があります。 ただし、実際のシナリオでデータを制御していない場合 (web サービスから取得する場合など) は、どうすればよいでしょうか。 これをどのように解決すればよいでしょう。

例外が発生した場合は、次のいくつかの質問に答える必要があります。

* この例外は、修正できるバグだけですか。 または

* この例外は、ユーザーが遭遇する可能性があるものですか。

前者の場合は、バグを修正します。 (サンプルアプリでは、これは不適切なデータを修正することを意味します)。後者の場合は、`try/catch` ブロックを使用して、コードで例外を処理する必要がある場合があります (次のセクションでは、他の方法についても説明します)。 サンプルアプリで、次のコードを置き換えます。

```csharp
users = ser.ReadObject(ms) as User[];
```

を、次のコードで置換します。

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

`try/catch` ブロックにはパフォーマンスコストがあるため、実際に必要なときにのみ使用します。つまり、アプリのリリースバージョンではどこ (a) が発生するか、および (b) メソッドのドキュメントは、(ドキュメントが完成したと仮定して) 例外を確認する必要があることを示します。 多くの場合、例外を適切に処理することができ、ユーザーはそれを知る必要はありません。

例外処理のいくつかの重要なヒントを次に示します。

* `catch (Exception) {}`のような空の catch ブロックは使用しないでください。これにより、エラーを公開または処理するための適切なアクションは実行されません。 空または情報のない catch ブロックによって例外が隠され、コードをより簡単にデバッグできるようになります。

* 例外をスローする特定の関数 (`ReadObject`サンプルアプリでは、`try/catch` ブロック) を使用します。 より大きなコードのチャンクを使用すると、エラーの場所が隠蔽されます。 たとえば、ここに示すように、親 `ReadToObject`関数の呼び出しの周囲に `try/catch` ブロックを使用しないでください。または、例外が発生した場所を正確に把握できません。

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

* アプリに含まれる不明な関数 (特に、web 要求などの外部データとの対話) については、ドキュメントを参照して、関数がスローする可能性のある例外を確認してください。 これは、適切なエラー処理とアプリのデバッグに関する重要な情報です。

サンプルアプリの場合、`4o` を `40`に変更して、`GetJsonData` メソッドの `SerializationException` を修正します。

## <a name="clarify-your-code-intent-by-using-assert"></a>Assert を使用してコードインテントを明確にする

デバッグ ツールバーにある **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5**)。 これにより、アプリがより少数の手順で再起動されます。 コンソールウィンドウに次の出力が表示されます。

![出力に Null 値があります](../debugger/media/write-better-code-using-assert-null-output.png)

この出力には、あまり適切ではないものが表示されます。 3番目のレコードの**名前**と**lastname**は空白です。

これは、関数内で `assert` ステートメントを使用するためのコーディング手法 (多くの場合は過小使用) について説明するのに最適なタイミングです。 次のコードを追加することで、`firstname` と `lastname` が `null`ないことを確認するランタイムチェックを含めます。 `UpdateRecords` メソッド内の次のコードを置き換えます。

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

開発プロセス中にこのようなステートメントを関数に `assert` 追加することにより、コードの意図を指定することができます。 前の例では、次のように指定します。

* 名には有効な文字列が必要です
* 最後の名前には有効な文字列が必要です

この方法でインテントを指定することにより、要件を適用できます。 これは、開発中にバグを表面化させるために使用できる簡単で便利な方法です。 (`assert` ステートメントは、単体テストのメイン要素としても使用されます)。

デバッグ ツールバーにある **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5**)。

> [!NOTE]
> `assert` コードは、デバッグビルドでのみアクティブです。

を再起動すると、デバッガーは `assert` ステートメントで一時停止します。これは、式 `users[i].firstname != null` が `true`ではなく `false` に評価されるためです。

![Assert が false に解決される](../debugger/media/write-better-code-using-assert.png)

`assert` エラーは、調査する必要がある問題があることを示しています。 `assert` は、必ずしも例外が表示されない多くのシナリオに対応できます。 この例では、ユーザーには例外が表示されず、レコードの一覧に `firstname` として `null` 値が追加されます。 これにより、後で (コンソール出力に表示されるように) 問題が発生し、デバッグが困難になる場合があります。

> [!NOTE]
> `null` 値に対してメソッドを呼び出す場合、`NullReferenceException` の結果になります。 通常は、一般的な例外 (特定のライブラリ関数に関連付けられていない例外) に `try/catch` ブロックを使用しないようにします。 任意のオブジェクトが `NullReferenceException`をスローできます。 不明な場合は、ライブラリ関数のドキュメントを確認してください。

デバッグプロセスでは、特定の `assert` ステートメントを実際のコード修正に置き換える必要があることを把握しておくことをお勧めします。 たとえば、アプリのリリースビルドでユーザーが例外を発生させる可能性があるとします。 その場合は、アプリが致命的な例外をスローしないように、または他のエラーが発生しないように、コードをリファクターする必要があります。 このため、このコードを修正するには、次のコードを置き換えます。

```csharp
if (existingUser == false)
{
    User user = new User();
```

を、次のコードで置換します。

```csharp
if (existingUser == false && users[i].firstname != null && users[i].lastname != null)
{
    User user = new User();
```

このコードを使用すると、コードの要件を満たし、`null` の `firstname` または `lastname` の値を持つレコードがデータに追加されないようにすることができます。

この例では、2つの `assert` ステートメントをループ内に追加しました。 通常、`assert`を使用する場合は、関数またはメソッドのエントリポイント (先頭) に `assert` ステートメントを追加することをお勧めします。 現在、サンプルアプリの `UpdateRecords` メソッドを見ています。 このメソッドでは、いずれかのメソッド引数が `null`場合、問題が発生していることがわかっています。そのため、関数のエントリポイントで `assert` ステートメントを使用して両方を確認してください。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

上記のステートメントでは、データを更新する前に、既存のデータ (`db`) を読み込み、新しいデータ (`users`) を取得することを目的としています。

`assert` は、`true` または `false`に解決される任意の種類の式と共に使用できます。 たとえば、次のような `assert` ステートメントを追加できます。

```csharp
Debug.Assert(users[0].points > 0);
```

上記のコードは、次の目的を指定する場合に便利です。ユーザーのレコードを更新するには、ゼロ (0) より大きい新しいポイント値が必要です。

## <a name="inspect-your-code-in-the-debugger"></a>デバッガーでのコードの検査

これで、サンプルアプリに問題があることをすべて修正しました。他の重要な項目に移動できます。

デバッガーの例外ヘルパーを紹介しましたが、デバッガーははるかに強力なツールであり、コードのステップ実行や変数の検査など、他の操作も実行できます。 これらの強力な機能は、特に次のような多くのシナリオで役立ちます。

* コード内のランタイムバグを分離しようとしていますが、前に説明したメソッドとツールを使用して実行することはできません。

* コードを検証する必要があります。つまり、実行中にコードを見て、期待どおりに動作するかどうかを確認します。

    実行中にコードを見ることができます。 この方法でコードの詳細を確認し、明らかな症状を示す前にバグを識別することがよくあります。

デバッガーの重要な機能を使用する方法については、「[絶対初心者向けのデバッグ](../debugger/debugging-absolute-beginners.md)」を参照してください。

## <a name="fix-performance-issues"></a>パフォーマンスの問題を修正

別の種類のバグには、アプリの実行速度を低下させたり、メモリを過剰に使用したりする非効率的なコードが含まれます。 一般に、パフォーマンスの最適化は、アプリ開発で後から実行するものです。 ただし、早い段階でパフォーマンスの問題が発生する可能性があります (たとえば、アプリの一部が低速で実行されていることがわかります)。また、プロファイリングツールでアプリを事前にテストしなければならないことがあります。 CPU 使用率ツールやメモリアナライザーなどのプロファイリングツールの詳細については、「[プロファイリングツールの](../profiling/profiling-feature-tour.md)概要」を参照してください。

## <a name="next-steps"></a>次のステップ:

この記事では、コード内の多くの一般的なバグを回避して修正する方法と、デバッガーを使用するタイミングについて説明しました。 次に、Visual Studio デバッガーを使用してバグを修正する方法の詳細について説明します。

> [!div class="nextstepaction"]
> [入門者向けのデバッグ](../debugger/debugging-absolute-beginners.md)
