---
title: 'チュートリアル: シンプルな C# コンソール アプリを拡張する'
description: Visual Studio で C# コンソール アプリを開発する方法について、ステップ バイ ステップで説明します。
ms.custom: get-started
ms.date: 07/09/2020
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: aae83c43a106fd68b03a83124ad2ddcea4652c8d
ms.sourcegitcommit: c620d59578db1b89f80e64ae04b4898bc4ab292d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87375934"
---
# <a name="tutorial-extend-a-simple-c-console-app"></a>チュートリアル: シンプルな C# コンソール アプリを拡張する

このチュートリアルでは、最初のパートで作成したコンソール アプリを、Visual Studio を使用して拡張する方法について説明します。 詳細エディター機能の使い方やデバッグなど、開発者が生産性を高めるのに役立つ Visual Studio の機能の一部について説明します。

このシリーズの[最初のパート](tutorial-console.md)を完了している場合は、電卓コンソール アプリは既に用意できています。  パート 1 をスキップするには、GitHub リポジトリからプロジェクトを開くところから始めます。 C# 電卓アプリは、[vs-tutorial-samples リポジトリ](https://github.com/MicrosoftDocs/vs-tutorial-samples)にあるので、「[チュートリアル: リポジトリからプロジェクトを開く](../tutorial-open-project-from-repo.md)」に記載されている手順に従うと開始することができます。

## <a name="add-a-new-project"></a>新しいプロジェクトの追加

実際のコードでは、1 つのソリューション内で多くのプロジェクトを連携させる必要があります。 ここで、電卓アプリに別のプロジェクトを追加してみましょう。 これは、一部の電卓関数を備えたクラス ライブラリとなります。

1. Visual Studio では、トップレベルのメニュー コマンド **[ファイル]**  >  **[追加]**  >  **[新しいプロジェクト]** を使用して新しいプロジェクトを追加することができますが、既存のプロジェクト名 ("プロジェクト ノード" と呼ばれます) を右クリックし、プロジェクトのショートカット メニュー (またはコンテキスト メニュー) を開くこともできます。 このショートカット メニューでは、さまざまな方法でご自分のプロジェクトに機能を追加することができます。 そのため、**ソリューション エクスプローラー**でご自分のプロジェクト ノードを右クリックし、 **[追加]**  >  **[新しいプロジェクト]** の順に選択します。

1. C# プロジェクト テンプレート **[クラス ライブラリ (.NET Standard)]** を選択します。

   ![[クラス ライブラリ] プロジェクト テンプレートの選択のスクリーンショット](media/vs-2019/calculator2-add-project-dark.png)

1. [プロジェクト名] として「**CalculatorLibrary**」と入力し、 **[作成]** を選択します。 Visual Studio によって、新しいプロジェクトが作成され、ソリューションに追加されます。

   ![CalculatorLibrary クラス ライブラリ プロジェクトが追加されているソリューション エクスプローラーのスクリーンショット。](media/vs-2019/calculator2-solution-explorer-with-class-library-dark2.png)

1. *Class1.cs* を使用するのでなく、ファイルの名前を **CalculatorLibrary.cs** に変更します。 **ソリューション エクスプローラー**内で該当する名前をクリックして名前を変更するか、右クリックして **[名前変更]** を選択するか、または **F2** キーを押します。

   ファイル内の `Class1` への参照名を変更するかどうかを確認するメッセージが表示される場合があります。 後の手順でコードを置き換えるので、どのように答えてもかまいません。

1. ここで、新しいクラス ライブラリによって公開される API を最初のプロジェクトが使用できるように、プロジェクト参照を追加する必要があります。  最初のプロジェクト内の **[参照]** ノードを右クリックし、 **[プロジェクト参照の追加]** を選択します。

   ![[プロジェクト参照の追加] 項目のスクリーンショット](media/vs-2019/calculator2-add-project-reference-dark.png)

   **[参照マネージャー]** ダイアログ ボックスが表示されます。 このダイアログ ボックスを使用すると、ご自分のプロジェクトに必要なアセンブリと COM DLL に加えて、他のプロジェクトへの参照を追加できます。

   ![[参照マネージャー] ダイアログ ボックスのスクリーンショット](media/vs-2019/calculator2-ref-manager-dark.png)

1. **[参照マネージャー]** ダイアログ ボックスで、 **[CalculatorLibrary]** プロジェクトのチェックボックスをオンにして、 **[OK]** を選択します。  プロジェクト参照は、**ソリューション エクスプローラー**で **[プロジェクト]** ノードの下に表示されます。

   ![プロジェクト参照が表示されているソリューション エクスプローラーのスクリーンショット](media/vs-2019/calculator2-solution-explorer-with-project-reference-dark2.png)

1. *Program.cs* 内で、`Calculator` クラスとそのコード全体を選択し、**CTRL + X** キーを押して Program.cs からそれを切り取ります。 次に、**CalculatorLibrary** にある *CalculatorLibrary.cs* の `CalculatorLibrary` 名前空間にコードを貼り付けます。 次に、Calculator クラスを `public` にして、ライブラリの外部に公開します。 *CalculatorLibrary.cs* 内のコードは、次のコードのようになります。

   ```csharp
   using System;

    namespace CalculatorLibrary
    {
        public class Calculator
        {
            public static double DoOperation(double num1, double num2, string op)
            {
                double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

                // Use a switch statement to do the math.
                switch (op)
                {
                    case "a":
                        result = num1 + num2;
                        break;
                    case "s":
                        result = num1 - num2;
                        break;
                    case "m":
                        result = num1 * num2;
                        break;
                    case "d":
                        // Ask the user to enter a non-zero divisor.
                        if (num2 != 0)
                        {
                            result = num1 / num2;
                        }
                        break;
                    // Return text for an incorrect option entry.
                    default:
                        break;
                }
                return result;
            }
        }
    }
   ```

1. 最初のプロジェクトには参照がありますが、Calculator.DoOperation 呼び出しが解決されないというエラーが表示されます。 これは、CalculatorLibrary が異なる名前空間にあるためです。したがって、完全修飾参照のためには `CalculatorLibrary` 名前空間を追加します。

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   代わりに、using ディレクティブをファイルの先頭に追加してみてください。

   ```csharp
   using CalculatorLibrary;
   ```

   この変更を行えば、呼び出しサイトから CalculatorLibrary 名前空間を削除できるようになりますが、今度はあいまいさが生じます。 `Calculator` は CalculatorLibrary 内のクラスでしょうか、それとも Calculator は名前空間でしょうか?  あいまいさを解決するには、名前空間 `CalculatorProgram` の名前を変更します。

   ```csharp
   namespace CalculatorProgram
   ```

## <a name="reference-net-libraries-write-to-a-log"></a>.NET ライブラリを参照する: ログに書き込む

1. ここで、すべての操作に関するログを追加し、それをテキスト ファイルに書き込むとします。 .NET `Trace` クラスによって、この機能が提供されます (これは基本的な出力デバッグ手法にも役立ちます)。Trace クラスは System.Diagnostics に含まれているので、まず using ディレクティブを追加します。

   ```csharp
   using System.Diagnostics;
   ```

1. Trace クラスがどのように使用されているのかを確認するには、filestream に関連付けられているクラスの参照を維持する必要があります。 つまり、電卓の場合はオブジェクトとしてより適切に機能するので、コンストラクターを追加してみましょう。

   ```csharp
   public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

    public double DoOperation(double num1, double num2, string op)
        {
   ```

1. さらに、静的な `DoOperation` メソッドをメンバー メソッドに変更する必要があります。  また、ログ用に各計算に出力を追加します。結果、DoOperation のコードは次のようになります。

   ```csharp
   public double DoOperation(double num1, double num2, string op)
   {
        double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

        // Use a switch statement to do the math.
        switch (op)
        {
            case "a":
                result = num1 + num2;
                Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                break;
            case "s":
                result = num1 - num2;
                Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                break;
            case "m":
                result = num1 * num2;
                Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                break;
            case "d":
                // Ask the user to enter a non-zero divisor.
                if (num2 != 0)
                {
                    result = num1 / num2;
                    Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                }
                    break;
            // Return text for an incorrect option entry.
            default:
                break;
        }
        return result;
    }
   ```

1. ここで Program.cs に戻ると、静的な呼び出しに赤い波線のフラグが付けられています。 これを修正するには、while ループの直前に次の行を追加して、`calculator` 変数を作成します。

   ```csharp
   Calculator calculator = new Calculator();
   ```

   そして、`DoOperation` の呼び出しサイトを次のように変更します。

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

1. プログラムをもう一度実行します。完了したら、プロジェクト ノードを右クリックし、 **[エクスプローラーでフォルダーを開く]** を選択して、エクスプローラーを下方の出力フォルダーまで移動します。 それは *bin/Debug/netcoreapp3.1* である可能性があります。*calculator.log* ファイルを開きます。

    ```output
    Starting Calculator Log
    Started 7/9/2020 1:58:19 PM
    1 + 2 = 3
    3 * 3 = 9
    ```

## <a name="add-a-nuget-package-write-to-a-json-file"></a>NuGet パッケージを追加する: JSON ファイルに書き込む

1. ここで、操作を JSON 形式で出力するとします。これは、オブジェクト データを格納するための一般的で移植可能な形式です。 その機能を実装するには、NuGet パッケージ Newtonsoft.Json を参照する必要があります。 NuGet パッケージは、.NET クラス ライブラリを配布するための主要な手段です。 **ソリューション エクスプローラー**で、CalculatorLibrary プロジェクトの **[参照]** ノードを右クリックし、 **[NuGet パッケージの管理]** を選択します。

   ![ショートカット メニューの [NuGet パッケージの管理] のスクリーンショット](media/vs-2019/calculator2-manage-nuget-packages-dark2.png)

   NuGet パッケージ マネージャーが開きます。

   ![NuGet パッケージ マネージャーのスクリーンショット](media/vs-2019/calculator2-nuget-package-manager-dark.png)

1. Newtonsoft.Json パッケージを検索し、 **[インストール]** を選択します。

   ![Newtonsoft NuGet パッケージ情報のスクリーンショット](media/vs-2019/calculator2-nuget-newtonsoft-json-dark2.png)

   そのパッケージがダウンロードされ、ご自分のプロジェクトに追加されます。**ソリューション エクスプローラー**内の [参照] ノードに新しいエントリが表示されます。

1. *CalculatorLibrary.cs* の先頭に Newtonsoft.Json パッケージ用の using ディレクティブを追加します。

   ```csharp
   using Newtonsoft.Json;
   ```

1. ここで、電卓のコンストラクターを次のコードに置き換え、JsonWriter メンバー オブジェクトを作成します。

   ```csharp
        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }
   ```

1. `DoOperation` メソッドを変更して、JSON ライター コードを追加します。

   ```csharp
        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }
   ```

1. ユーザーが操作データの入力を完了したら、JSON 構文を完了するためのメソッドを追加する必要があります。

   ```csharp
    public void Finish()
    {
        writer.WriteEndArray();
        writer.WriteEndObject();
        writer.Close();
    }
   ```

1. さらに、*Program.cs* 内で、最後に Finish への呼び出しを追加します。

   ```csharp
            // And call to close the JSON writer before return
            calculator.Finish();
            return;
        }
   ```

1. アプリをビルドして実行します。いくつかの操作を入力したら、'n' コマンドを使用してアプリを適切に閉じます。  ここで、consolelog.json ファイルを開くと、次のような内容が表示されます。

   ```json
   {
    "Operations": [
        {
        "Operand1": 2.0,
        "Operand2": 3.0,
        "Operation": "Add",
        "Result": 5.0
        },
        {
        "Operand1": 3.0,
        "Operand2": 4.0,
        "Operation": "Multiply",
        "Result": 12.0
        }
    ]
   }
   ```

## <a name="next-steps"></a>次の手順

これでこのチュートリアルは完了です。 さらに詳しく学習するには、引き続き以下のチュートリアルをご覧ください。

> [!div class="nextstepaction"]
> [さらに C# チュートリアルを続ける](/dotnet/csharp/tutorials/)

> [!div class="nextstepaction"]
> [Visual Studio IDE の続行の概要](/../visual-studio-ide.md)

## <a name="see-also"></a>関連項目

* [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
* [Visual Studio での C# コードのデバッグについて理解する](tutorial-debugger.md)
