---
title: 'チュートリアル: JavaScript を使用して SDK を作成する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f3a3fa110bd6521443521449898474299dd267d6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697502"
---
# <a name="walkthrough-create-an-sdk-using-javascript"></a>チュートリアル: Java スクリプトを使用して SDK を作成する
このチュートリアルでは、JavaScript を使用して単純な数学 SDK を Visual Studio 拡張機能 (VSIX) として作成する方法について説明します。  このチュートリアルは、次の部分に分かれています。

- [拡張 SDK プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)

- [SDK を使用するサンプル アプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)

  JavaScript の場合、クラス ライブラリ プロジェクトタイプはありません。 このチュートリアルでは、サンプル*の算術.js*ファイルは、VSIX プロジェクトで直接作成されます。 実際には、VSIX プロジェクトに配置する前に、まず、JavaScript ファイルと CSS ファイルを Windows ストア アプリとして (**たとえば、空のアプリ**テンプレートを使用して) ビルドしてテストすることをお勧めします。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-simplemathvsix-extension-sdk-project"></a><a name="createSimpleMathVSIX"></a>拡張 SDK プロジェクトを作成するには

1. メニュー バーで、[**ファイル] を** > クリックして **[新しい** > **プロジェクト**] をクリックします。

2. テンプレート カテゴリの一覧の **[Visual C#]** で [**機能拡張**] を選択し、次に **[VSIX プロジェクト**] テンプレートを選択します。

3. **[名前**] テキスト ボックス`SimpleMathVSIX`で **、[OK] ボタン**を指定して選択します。

4. Visual **Studio パッケージ ウィザード**が表示された場合は、[**ようこそ**] ページの [**次へ**] をクリックし **、[1/7] ページ**で **[完了**] ボタンをクリックします。

     マニフェスト**デザイナー**が開きますが、マニフェスト ファイルを直接変更することで、このチュートリアルは簡単に行われます。

5. **ソリューション エクスプローラー**で **、source.extension.vsixmanifest**ファイルのショートカット メニューを開き、[**コードの表示**] をクリックします。 このコードを使用して、ファイル内の既存のコンテンツを置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
      <Metadata>
        <Identity Id="SimpleMathVSIX" Version="1.0" Language="en-US" Publisher="myname" />
        <DisplayName>Simple Math</DisplayName>
        <Description>Does basic arithmetic calculations.</Description>
      </Metadata>
      <Installation Scope="Global" AllUsers="true">
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="SimpleMath" SdkVersion="1.0" />
      </Installation>
      <Dependencies>
        <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="4.5" />
      </Dependencies>
      <Assets>
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
      </Assets>
    </PackageManifest>
    ```

6. **ソリューション エクスプローラー**で**SimpleMathVSIX**プロジェクトのショートカット メニューを開き、[**Add** > **新しい項目**の追加] をクリックします。

7. [**データ**] カテゴリで **、[XML ファイル**]`SDKManifest.xml`を選択し、ファイルに名前を付け、[**追加**] をクリックします。

8. **ソリューション エクスプローラー**で **、SDKManifest.xml**ファイルのショートカット メニューを開き、[**開く**] を選択して XML**エディター**にファイルを表示します。

9. 次のコードを**SDKManifest.xml**ファイルに追加します。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <FileList
      DisplayName="Simple Math"
      MinVSVersion="14.0"
      AppliesTo="JavaScript+WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">

      <!-- JS -->
      <File Content="js\arithmetic.js" />
    </FileList>

    ```

10. **ソリューション エクスプローラー**の**SDKManifest.xml**ファイルのショートカット メニューで、[**プロパティ**] を選択します。

11. [**プロパティ]** ウィンドウで **、[VSIX に含める**] プロパティを**True**に設定します。

12. **ソリューション エクスプローラー**の**SimpleMathVSIX**プロジェクトのショートカット メニューで、[**Add** > **新しいフォルダー**の追加] をクリック`Redist`し、フォルダーに名前を付けます。

13. Redist の下にサブフォルダを追加して、次のフォルダ構造を作成します。

     *\リディスト\共通構成\ニュートラル\シンプル数学\js\\*

14. **\js\\**フォルダのショートカット メニューで、[**新しい項目**の**追加]** > をクリックします。

15. [Visual **C# アイテム**] で**Web**カテゴリを選択し **、[JavaScript ファイル]** 項目を選択します。 ファイル`arithmetic.js`に名前を付け、[**追加**] をクリックします。

16. 次のコードを*算術.js*に挿入します。

    ```csharp
    (function (global) {
        "use strict";
        global.Arithmetic = {
            add: function (firstNumber, secondNumber) {
                return firstNumber + secondNumber;
            },

            subtract: function (firstNumber, secondNumber) {
                return firstNumber - secondNumber;
            },

            multiply: function (firstNumber, secondNumber) {
                return firstNumber * secondNumber;
            },

            divide: function (firstNumber, secondNumber) {
                return firstNumber / secondNumber;
            }
        };
    })(this);

    ```

17. **ソリューション エクスプローラー**で、**算術ファイル**のショートカット メニューの [**プロパティ**] をクリックします。 次のプロパティを変更します。

    - **[VSIX に含める**] プロパティを**True**に設定します。

    - [**出力ディレクトリにコピー** ] プロパティを **[常にコピー]** に設定します。

18. **ソリューション エクスプローラー**で、 **SimpleMathVSIX**プロジェクトのショートカット メニューの [**ビルド**] をクリックします。

19. ビルドが正常に完了したら、プロジェクトのショートカット メニューで 、[**エクスプローラーでフォルダーを開く]** をクリックします。 **\bin\debug\\**に移動し、`SimpleMathVSIX.vsix`実行してインストールします。

20. [**インストール**] ボタンを選択し、インストールを完了させます。

21. Visual Studio を再起動します。

## <a name="to-create-a-sample-app-that-uses-the-sdk"></a><a name="createSampleApp"></a>SDK を使用するサンプル アプリを作成するには

1. メニュー バーで、[**ファイル] を** > クリックして **[新しい** > **プロジェクト**] をクリックします。

2. テンプレート カテゴリの一覧の **[JavaScript]** で **[Windows ストア**] を選択し、[**空のアプリ]** テンプレートを選択します。

3. [**名前]** ボックスで`ArithmeticUI`、 を指定します。 **[OK]** をクリックします。

4. **ソリューション エクスプローラー**で **、算術 UI**プロジェクトのショートカット メニューを開き、[**参照**の**追加** > ] をクリックします。

5. [**ウィンドウ]** で **[拡張]** を選択し、[**簡易演算**] が表示されていることを確認します。

6. [**単純な計算**] チェック ボックスをオンにし **、[OK] をクリックします**。

7. **ソリューション エクスプローラー**の [**参照 ]** に、**単純な数式**参照が表示されていることを確認します。 それを展開し、**算術.js**を含む**\\\js**フォルダーがあることに注意してください。 この場合、このコードがインストールされていることを確認するために **、arithmetic.js**を開くことができます。

8. 次のコードを使用して*default.htm*の内容を置き換えます。

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <meta charset="utf-8" />
       <title>ArithmeticUI</title>

       <!-- WinJS references -->
       <link href="//Microsoft.WinJS.1.0/css/ui-dark.css" rel="stylesheet" />
       <script src="//Microsoft.WinJS.1.0/js/base.js"></script>
       <script src="//Microsoft.WinJS.1.0/js/ui.js"></script>

       <!-- ArithmeticUI references -->
       <link href="/css/default.css" rel="stylesheet" />
       <script src="/js/default.js"></script>
       <script src="/SimpleMath/js/arithmetic.js"></script>
   </head>
   <body>
       <form>
       <div id="calculator" class="ms-grid">
           <input name="firstNumber" id="firstNumber" type="number" step="any">
           <div id="operators">
               <button class="operator" type="button">+</button>
               <button class="operator" type="button">-</button>
               <button class="operator" type="button">*</button>
               <button class="operator" type="button">/</button>
           </div>
           <input id="secondNumber" type="number">
           <button class="calculate" type="button">=</button>
           <input id="result" type="number" name="result" disabled="" readonly="">
       </div>
       </form>
   </body>
   </html>
   ```

9. 次のコードを使用して *、\js\default.js*の内容を置き換えます。

    ```csharp
    (function () {
        "use strict";

        var app = WinJS.Application;
        var operation = null;

        function calculateResult() {
            var firstNumber = parseFloat(document.querySelector("#firstNumber").value),
                secondNumber = parseFloat(document.querySelector("#secondNumber").value),
                result = 0;

            if (isNaN(firstNumber) || isNaN(secondNumber)) {
                result = 0;
            }
            else {
                switch (operation) {
                    case "+":
                        result = Arithmetic.add(firstNumber, secondNumber);
                        break;
                    case "-":
                        result = Arithmetic.subtract(firstNumber, secondNumber);
                        break;
                    case "*":
                        result = Arithmetic.multiply(firstNumber, secondNumber);
                        break;
                    case "/":
                        result = Arithmetic.divide(firstNumber, secondNumber);
                        break;
                    default:
                }
            }
            document.querySelector("#result").value = result.toString();
        }

        app.onactivated = function (args) {
            document.querySelector("#calculator").addEventListener("click", function (event) {
                if (event.target.tagName.toLowerCase() === "button") {
                    switch (event.target.className) {
                        case "operator":
                            operation = event.target.innerText;
                            break;
                        case "calculate":
                            calculateResult();
                            break;
                        default:
                            break;
                    }
                }
            });
        };

        app.start();
    })();
    ```

10. *\css\default.css*の内容を次のコードに置き換えます。

    ```xml
    form {
        display: -ms-grid;
        -ms-grid-rows: 1fr auto 1fr;
        -ms-grid-columns: 1fr auto 1fr;
        height: 100%;
        width: 100%;
    }

    button, input[type=number] {
        margin-right: 5px;
        -ms-grid-row-align: center;
    }

    #calculator {
        -ms-grid-column: 2;
        -ms-grid-row: 2;
        display: -ms-grid;
        -ms-grid-rows: 1fr;
        -ms-grid-columns: auto min-content auto auto auto;
    }

    .ms-grid input {
        width: 5em;
    }

    #firstNumber {
        -ms-grid-column: 1;
        -ms-grid-row-align: center;
    }

    #operators {
        -ms-grid-column: 2;
        -ms-grid-row-align: center;
    }

        #operators button.operator {
            margin-bottom: 5px;
            height: 40px;
        }

    #secondNumber {
        -ms-grid-column: 3;
    }

    button.calculate {
        -ms-grid-column: 4;
        -ms-grid-row-align: center;
        height: 40px;
    }

    #result {
        -ms-grid-column: 5;
    }

    ```

11. **F5**キーを選択してアプリをビルドして実行します。

12. アプリの UI で、任意の 2 つの数値を入力し、**=** 操作を選択して、ボタンを選択します。 正しい結果が表示されます。

## <a name="see-also"></a>関連項目
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
