---
title: デバッグの技術とツール
description: Visual Studio を使用して例外を修正し、エラーを修正して、コードを改善することで、バグが少ないコードをより適切に記述します
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89311392"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>より優れたコードを記述するためのデバッグ手法とツール

コード内のバグとエラーの修正は、時間がかかり、場合によっては面倒な作業になることがあります。 効率的なデバッグ方法について学習するには時間がかかりますが、Visual Studio のような強力な IDE を使用すると、仕事がはるかに簡単になります。 IDE を使用すると、エラーの修正やコードのデバッグをより迅速に行うことができます。それだけでなく、より適切なコードを記述してバグを減らすこともできます。 この記事の目的は、"バグ修正" プロセスの全体像を示すことであり、コード アナライザーを使用するタイミング、デバッガーを使用するタイミング、例外を修正する方法、意図したようにコーディングする方法を知ることができます。 デバッガーを使用する必要があることが既にわかっている場合は、「[デバッガーでのはじめに](../debugger/debugger-feature-tour.md)」を参照してください。

この記事では、IDE を利用してコーディング セッションの生産性を高める方法について説明します。 ここでは、次のようないくつかのタスクについて説明します。

* IDE のコード アナライザーを利用して、デバッグ用にコードを準備する

* 例外を修正する方法 (実行時エラー)

* 意図したコーディングでバグを最小化する方法 (アサートの使用)

* どのようなときにデバッガーを使用するか

これらのタスクをデモンストレーションするために、アプリをデバッグするときに発生する最も一般的な種類のエラーとバグをいくつか示します。 サンプル コードは C# ですが、概念情報は一般に、C++、Visual Basic、JavaScript、Visual Studio でサポートされているその他の言語にも適用されます (特別な記載のない限り)。 スクリーン ショットは C# になっています。

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>バグやエラーが含まれるサンプル アプリを作成する

次のコードには、Visual Studio IDE を使用して修正できるいくつかのバグがあります。 ここでのアプリは、ある操作からの JSON データの取得、データのオブジェクトへの逆シリアル化、新しいデータでの簡単なリストの更新をシミュレートするシンプルなアプリです。

アプリを作成するには:

1. Visual Studio をインストールし、作成するアプリの種類に応じて、 **.NET Core クロスプラットフォームの開発**ワークロードまたは **.NET デスクトップ開発**ワークロードをインストールする必要があります。

    Visual Studio をまだインストールしていない場合は、 [Visual Studio のダウンロード](https://visualstudio.microsoft.com/downloads/)  ページに移動し、無料試用版をインストールしてください。

    Visual Studio は既にインストールされていて、ワークロードだけをインストールする必要がある場合は、 **[ツール]**  >  **[ツールと機能を取得]** の順にクリックします。 Visual Studio インストーラーが起動します。 **[.NET Core クロスプラットフォームの開発]** または **[.NET デスクトップ開発]** ワークロードを選択し、 **[変更]** を選択します。

1. Visual Studio を開きます。

    ::: moniker range=">=vs-2019"
    スタート ウィンドウで、 **[新しいプロジェクトの作成]** を選択します。 検索ボックスに「**コンソール**」と入力し、 **[コンソール アプリ (.NET Core)]** または **[コンソール アプリ (.NET Framework)]** のいずれかを選択します。 **[次へ]** をクリックします。 **Console_Parse_JSON** のようなプロジェクト名を入力して、 **[作成]** をクリックします。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで、 **[Visual C#]** の下にある **[コンソール アプリ]** を選択し、次に真ん中のウィンドウで **[コンソール アプリ (.NET Core)]** または **[コンソール アプリ (.NET Framework)]** のいずれかを選択します。 **Console_Parse_JSON** のような名前を入力して、 **[OK]** をクリックします。
    ::: moniker-end

    **[コンソール アプリ (.NET Core)]** または **[コンソール アプリ (.NET Framework)]** プロジェクト テンプレートが表示されない場合は、 **[ツール]**  >  **[ツールと機能を取得]** に移動して、Visual Studio インストーラーを開きます。 **[.NET Core クロスプラットフォームの開発]** ワークロードまたは **[.NET デスクトップ開発]** ワークロードのいずれかを選択して、 **[変更]** を選択します。

    Visual Studio によってコンソール プロジェクトが作成され、ソリューション エクスプローラーの右側のウィンドウに表示されます。

1. プロジェクトの *Program.cs* ファイルの既定のコードを、次のサンプル コードに置き換えます。

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

## <a name="find-the-red-and-green-squiggles"></a>赤と緑の波線を探します。

サンプル アプリを起動してデバッガーを実行する前に、コード エディターのコードで赤と緑の波線を確認します。 これらは、IDE のコード アナライザーによって識別されたエラーと警告を表します。 赤い波線はコンパイル時エラーであり、コードを実行する前に修正する必要があります。 緑の波線は警告です。 多くの場合、警告を修正せずにアプリを実行できますが、バグの原因となる場合があり、多くの場合、警告を調査することによって時間を節約し問題を減らすことができます。 リスト ビューの方がよければ、これらの警告とエラーは **[エラー一覧]** ウィンドウにも表示されます。

サンプル アプリでは、修正が必要ないくつかの赤い波線と、1 つの緑の波線が表示されます。 1 つ目のエラーは次のとおりです。

![赤い波線で示されるエラー](../debugger/media/write-better-code-red-squiggle.png)

このエラーを修正するには、電球アイコンによって表される IDE の別の機能を使用します。

## <a name="check-the-light-bulb"></a>電球を確認する

最初の赤い波線は、コンパイル時のエラーを表します。 それをポイントすると、```The name `Encoding` does not exist in the current context``` というメッセージが表示されます。

このエラーの左下に電球アイコンが表示されることに注意してください。 ドライバー アイコン ![ドライバーアイコン](../ide/media/screwdriver-icon.png) と共に、電球アイコン ![電球アイコン](../ide/media/light-bulb-icon.png) は、コードをインラインで修正またはリファクタリングするのに役立つクイック アクションを表します。 電球は、修正する "*必要がある*" 問題を表します。 ドライバーは、修正することができる問題を示します。 左側の **using System.Text** をクリックし、最初の修正候補を使用してこのエラーを解決します。

![電球を使用してコードを修正する](../debugger/media/write-better-code-missing-include.png)

この項目をクリックすると、Visual Studio によって `using System.Text` ステートメントが *Program.cs* ファイルの先頭に追加され、赤い波線が表示されなくなります。 (修正候補の効果がわからない場合は、修正を適用する前に、右側の **[変更のプレビュー]** リンクを選択します)。

前述のエラーは、コードに新しい `using` ステートメントを追加することによって通常は修正される、一般的なエラーです。 このエラーには、共通の類似するエラーがいくつかあります (```The type or namespace `Name` cannot be found.``` など)。この種のエラーでは、アセンブリ参照が存在しないこと (プロジェクトを右クリックして **[追加]**  >  **[参照]** を選択)、名前のスペルミス、または追加する必要のある足りないライブラリ (C# の場合は、プロジェクトを右クリックして **[NuGet パッケージの管理]** を選択) が示されている場合があります。

## <a name="fix-the-remaining-errors-and-warnings"></a>残りのエラーと警告を修正する

このコードには、調べる必要のある波線がさらにいくつかあります。 ここでは、一般的な型変換エラーを見ます。 波線をポイントすると、コードで string から int への変換が試みられていることがわかります。これは、変換を行う明示的なコードを追加しない限り、サポートされていません。

![型変換エラー](../debugger/media/write-better-code-conversion-error.png)

コード アナライザーでは意図を推測できないため、今度は役に立つ電球は表示されません。 このエラーを修正するには、コードの意図を理解する必要があります。 この例では、`totalpoints` に `points` を追加しようとしているため、`points` が数値 (整数) でなければならないことは簡単にわかります。

このエラーを修正するには、`User` クラスの `points` メンバーを変更します。変更前は次のようになっています。

```csharp
[DataMember]
internal string points;
```

変更後は次のようになります。

```csharp
[DataMember]
internal int points;
```

コード エディターの赤い波線が消えます。

次に、`points` データ メンバーの宣言で緑色の波線をポイントします。 コード アナライザーで、変数に値が割り当てられていないことが示されます。

![割り当てられない変数に関する警告メッセージ](../debugger/media/write-better-code-warning-message.png)

通常、これは修正する必要がある問題を表します。 ただし、サンプル アプリでは、逆シリアル化プロセスの間に `points` 変数にデータを格納し、その値を `totalpoints` データ メンバーに追加しています。 この例では、コードの意図がわかっていて、警告を無視しても問題ありません。 ただし、警告を除去したい場合は、次のコードを置き換えることができます。

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

すべての赤い波線を修正し、すべての緑の波線を解決するか、少なくとも調査したら、デバッガーを起動してアプリを実行できる状態になります。

**F5** キーを押すか ( **[デバッグ] > [デバッグの開始]** )、デバッグ ツール バーの **[デバッグの開始]** ボタン ![デバッグの開始](../debugger/media/dbg-tour-start-debugging.png "デバッグの開始") を選択します。

この時点で、サンプル アプリからは `SerializationException` 例外 (実行時エラー) がスローされます。 つまり、アプリは、シリアル化しようとしているデータで止まっています。 デバッグ モード (デバッガーがアタッチされた状態) でアプリを起動したため、デバッガーの例外ヘルパーにより、例外をスローしたコードに直接移動し、役に立つエラー メッセージが表示されます。

![SerializationException が発生している](../debugger/media/write-better-code-serialization-exception.png)

このエラー メッセージでは、値 `4o` を整数として解析できないことが示されています。 したがって、この例では、データが不適切であることがわかります。`4o` を `40` にする必要があります。 ただし、実際のシナリオでデータを制御できない場合 (web サービスから取得する場合など) は、どうすればよいでしょうか。 これをどのように解決すればよいでしょう。

例外が発生した場合は、いくつかの質問に答える必要があります。

* この例外は、修正できる単なるバグか。 または

* この例外は、ユーザーが遭遇する可能性があるものか。

前者の場合は、バグを修正します。 (サンプル アプリでは、不適切なデータを修正することを意味します)。後者の場合は、`try/catch` ブロックを使用して、コードで例外を処理することが必要になる場合があります (次のセクションでは、他の可能な戦略について説明します)。 サンプル アプリでは、次のコードを置き換えます。

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

`try/catch` ブロックにはパフォーマンス コストがあるため、どうしても必要なときにのみ使用します。つまり、(a) アプリのリリース バージョンで発生する可能性があり、(b) メソッドのドキュメントで例外をチェックする必要があることが示されている場合です (ドキュメントが完全であるものとして)。 多くの場合は、例外を適切に処理することができ、ユーザーはそのことを知る必要はありません。

例外処理のいくつかの重要なヒントを次に示します。

* `catch (Exception) {}` のような空の catch ブロックは使わないようにします。エラーを公開または処理するための適切なアクションが実行されません。 空または情報のない catch ブロックを使用すると、例外が隠され、コードのデバッグが容易になるのではなく、困難になる可能性があります。

* 例外をスローする特定の関数 (サンプル アプリでは `ReadObject`) に対して `try/catch` ブロックを使用します。 コードの大きなチャンクに対して使用すると、エラーの場所がわからなくなります。 たとえば、次に示すような、親関数 `ReadToObject` の呼び出しに対して `try/catch` ブロックを使用しないでください。使用すると、例外が発生した場所を正確に把握できなくなります。

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

* アプリによく知らない関数が含まれる場合は (特に、Web 要求など、外部データと対話するもの)、ドキュメントを調べて、関数でスローされる可能性がある例外を確認します。 これは、適切なエラー処理とアプリのデバッグのために不可欠な情報です。

サンプル アプリの場合、`4o` を `40` に変更することで、`GetJsonData` メソッドの `SerializationException` を修正します。

## <a name="clarify-your-code-intent-by-using-assert"></a>アサートを使用してコードの意図を明確にする

[デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5** キー)。 これにより、アプリがより少い手順で再起動されます。 コンソール ウィンドウに次の出力が表示されます。

![出力に null 値がある](../debugger/media/write-better-code-using-assert-null-output.png)

この出力には何か問題があることがわかります。 3 番目のレコードの **name** と **lastname** が空白です。

これは、関数内で `assert` ステートメントを使用するという、あまり利用されていない、役に立つコーディング手法について説明するよい機会です。 次のコードを追加することで、`firstname` と `lastname` が `null` ではないことを確認する実行時チェックを組み込みます。 `UpdateRecords` メソッドの次のコードを置き換えます。

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

開発プロセス中にこのような `assert` ステートメントを関数に追加することで、コードの意図を指定することができます。 前の例では、次のことを指定しています。

* 名には有効な文字列が必要です
* 姓には有効な文字列が必要です

この方法で意図を指定することにより、要件を適用します。 これは、開発中にバグを明らかにするために使用できる簡単で便利な方法です。 (`assert` ステートメントは、単体テストのメイン要素としても使用されます)。

[デバッグ] ツール バーの **[再起動]** ![アプリの再起動](../debugger/media/dbg-tour-restart.png "RestartApp") ボタンをクリックします (**Ctrl** + **Shift** + **F5** キー)。

> [!NOTE]
> `assert` コードは、デバッグ ビルドでのみアクティブになります。

再起動すると、式 `users[i].firstname != null` が `true` ではなく `false` と評価されるため、デバッガーは `assert` ステートメントで一時停止します。

![アサートが false に解決される](../debugger/media/write-better-code-using-assert.png)

`assert` エラーは、調べる必要がある問題があることを示しています。 `assert` を使用すると、必ずしも例外が表示されない多くのシナリオに対応できます。 この例では、ユーザーには例外が表示されず、レコードの一覧に `firstname` として `null` 値が追加されます。 これにより、後で (コンソール出力に表示されるような) 問題が発生し、デバッグが困難になる場合があります。

> [!NOTE]
> `null` 値に対してメソッドを呼び出すと、結果は `NullReferenceException` になります。 通常は、一般的な例外 (特定のライブラリ関数に関連付けられていない例外) には、`try/catch` ブロックを使用しません。 任意のオブジェクトで `NullReferenceException` がスローされる可能性があります。 不明な場合は、ライブラリ関数のドキュメントを確認してください。

デバッグ プロセスの間は、実際のコード修正に置き換える必要があることがわかるまで、特定の `assert` ステートメントを残しておくのがよい方法です。 たとえば、アプリのリリース ビルドでユーザーに対して例外が発生する可能性があることがわかったとします。 その場合は、アプリで致命的な例外がスローされたり、他のエラーが発生したりしないように、コードをリファクターする必要があります。 このコードを修正するには、次のコードを置き換えます。

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

このコードを使用すると、コードの要件を満たしながら、`firstname` または `lastname` の値が `null` であるレコードがデータに追加されないようにすることができます。

この例では、2 つの `assert` ステートメントをループ内に追加しました。 通常、`assert` を使用するときは、関数またはメソッドのエントリ ポイント (先頭) に `assert` ステートメントを追加することをお勧めします。 現在、サンプル アプリの `UpdateRecords` メソッドを見ています。 このメソッドでは、メソッドのいずれかの引数が `null` の場合に問題が発生することがわかっているため、関数のエントリ ポイントで `assert` ステートメントを使用して両方を確認します。

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

上記のステートメントの意図は、何かを更新する前に、既存のデータ (`db`) を読み込み、新しいデータ (`users`) を取得することです。

`assert` は、`true` または `false` として解決される任意の種類の式で使用できます。 たとえば、次のような `assert` ステートメントを追加できます。

```csharp
Debug.Assert(users[0].points > 0);
```

上記のコードは、ユーザーのレコードを更新するにはゼロ (0) より大きい新しいポイント値が必要である、という意図を指定する場合に便利です。

## <a name="inspect-your-code-in-the-debugger"></a>デバッガーでコードを検査する

サンプル アプリの重要な問題をすべて修正したので、他の重要な事柄に移ることができます。

デバッガーの例外ヘルパーを紹介しましたが、デバッガーははるかに強力なツールであり、コードのステップ実行や変数の検査など、他の操作も実行できます。 これらの強力な機能は、特に次のような多くのシナリオで役立ちます。

* コード内の実行時のバグを究明しようとしていますが、これまでに説明された手法とツールを使用したのでは実行できません。

* コードを検証する必要があります。つまり、実行中にコードを監視して、期待どおりに動作し、意図したことが行われていることを確認します。

    実行しながらコードを監視することをお勧めします。 このようにするとコードに関する詳細がわかり、明らかな症状を示す前にバグを識別できることがよくあります。

デバッガーの重要な機能を使用する方法については、「[入門者向けのデバッグ](../debugger/debugging-absolute-beginners.md)」を参照してください。

## <a name="fix-performance-issues"></a>パフォーマンスの問題を修正

別の種類のバグには、アプリの実行速度の低下や、メモリの過剰使用の原因になる、非効率的なコードが含まれます。 一般に、パフォーマンスの最適化は、アプリ開発の最後の方で行います。 ただし、早い段階でもパフォーマンスの問題が発生する可能性があり (たとえば、アプリの一部分の実行が遅いことがわかった場合など)、早期にプロファイリング ツールでアプリをテストすることが必要になる場合があります。 CPU 使用率ツールやメモリ アナライザーなどのプロファイリング ツールの詳細については、[プロファイリング ツールの概要](../profiling/profiling-feature-tour.md)に関する記事を参照してください。

## <a name="next-steps"></a>次の手順

この記事では、コード内の多くの一般的なバグを回避して修正する方法と、デバッガーを使用する状況について説明しました。 次に、Visual Studio のデバッガーを使用してバグを修正する方法の詳細について説明します。

> [!div class="nextstepaction"]
> [入門者向けのデバッグ](../debugger/debugging-absolute-beginners.md)
