---
title: 'チュートリアル: JavaScript を使用した SDK の作成 |Microsoft Docs'
description: このチュートリアルを使用して、JavaScript を使用して、Visual Studio 拡張機能として簡単な数値演算 SDK を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3b9a3d9e84731fe0c2526b69f60cdda1b1487583
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080386"
---
# <a name="walkthrough-create-an-sdk-using-javascript"></a>チュートリアル: JavaScript を使用した SDK の作成
このチュートリアルでは、JavaScript を使用して、Visual Studio 拡張機能 (VSIX) として簡単な数値演算 SDK を作成する方法について説明します。  このチュートリアルは、次の部分に分かれています。

- [Simplem、Vsix 拡張機能 SDK プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)

- [SDK を使用するサンプルアプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)

  JavaScript の場合、クラスライブラリプロジェクトの種類はありません。 このチュートリアルでは、サンプルの *arithmetic.js* ファイルを VSIX プロジェクトに直接作成します。 実際には、最初に、VSIX プロジェクトに配置する前に、JavaScript と CSS ファイルを Windows ストアアプリとして作成し、テストすることをお勧めします。たとえば、 **空のアプリケーション** テンプレートを使用します。

## <a name="prerequisites"></a>前提条件
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="to-create-the-simplemathvsix-extension-sdk-project"></a><a name="createSimpleMathVSIX"></a> Simplem、Vsix 拡張機能 SDK プロジェクトを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートカテゴリの一覧で、[ **Visual C#**] の下の [ **機能拡張**] を選択し、[ **VSIX プロジェクト** ] テンプレートを選択します。

3. [ **名前** ] テキストボックスで、を指定し、[ `SimpleMathVSIX` **OK** ] をクリックします。

4. **Visual Studio パッケージウィザード** が表示されたら、[**ようこそ**] ページの [**次へ**] をクリックします。次に、 **7 ページ目** の [**完了**] ボタンをクリックします。

     **マニフェストデザイナー** が開きますが、マニフェストファイルを直接変更することで、このチュートリアルを簡単に行うことができます。

5. **ソリューションエクスプローラー** で、 **source.extension.vsixmanifest** ファイルのショートカットメニューを開き、[**コードの表示**] を選択します。 このコードを使用して、ファイル内の既存のコンテンツを置き換えます。

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

6. **ソリューションエクスプローラー** で、 **simplemの vsix** プロジェクトのショートカットメニューを開き、[新しい項目の **追加**] を選択し  >  ます。

7. [ **データ** ] カテゴリで [ **XML ファイル**] を選択し、ファイルに名前 `SDKManifest.xml` を指定して、[ **追加** ] ボタンをクリックします。

8. **ソリューションエクスプローラー** で、 **SDKManifest.xml** ファイルのショートカットメニューを開き、[**開く**] をクリックして、 **XML エディター** でファイルを表示します。

9. 次のコードを **SDKManifest.xml** ファイルに追加します。

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

10. **ソリューションエクスプローラー** の **SDKManifest.xml** ファイルのショートカットメニューで、[**プロパティ**] を選択します。

11. [ **プロパティ** ] ウィンドウで、[ **VSIX に含める** ] プロパティを [ **True**] に設定します。

12. **ソリューションエクスプローラー** で、 **simplemの vsix** プロジェクトのショートカットメニューで、[新しいフォルダーの **追加**] を選択し、  >  フォルダーに名前を指定し `Redist` ます。

13. [Redist] の下にサブフォルダーを追加して、このフォルダー構造を作成します。

     *\Redist\CommonConfiguration\Neutral\SimpleMath\js\\*

14. [ **\\ Js** ] フォルダーのショートカットメニューで、[   >  **新しい項目** の追加] を選択します。

15. [ **Visual C# アイテム**] で、[ **Web** ] カテゴリを選択し、[ **JavaScript ファイル** ] 項目を選択します。 ファイルに名前を指定し、 `arithmetic.js` [ **追加** ] ボタンをクリックします。

16. *arithmetic.js* に次のコードを挿入します。

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

17. **ソリューションエクスプローラー** の **arithmetic.js** ファイルのショートカットメニューで、[**プロパティ**] を選択します。 次のプロパティを変更します。

    - [ **VSIX に含める (VSIX に含める** ) プロパティを **True** に設定します。

    - [ **出力ディレクトリにコピーする** "プロパティ" を " **常にコピー** する" に設定します。

18. **ソリューションエクスプローラー** で、 **Simplemの vsix** プロジェクトのショートカットメニューで、[**ビルド**] を選択します。

19. ビルドが正常に完了したら、プロジェクトのショートカットメニューで、[ **エクスプローラーでフォルダーを開く**] を選択します。 [ **\Bin\debug \\**] に移動し、を実行し `SimpleMathVSIX.vsix` てインストールします。

20. [ **インストール** ] をクリックし、インストールを完了します。

21. Visual Studio を再起動します。

## <a name="to-create-a-sample-app-that-uses-the-sdk"></a><a name="createSampleApp"></a> SDK を使用するサンプルアプリを作成するには

1. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

2. テンプレートカテゴリの一覧で、[ **JavaScript**] の下にある [ **Windows ストア**] を選択し、[ **空のアプリケーション** ] テンプレートを選択します。

3. [ **名前** ] ボックスに、を指定し `ArithmeticUI` ます。 **[OK]** を選択します。

4. **ソリューションエクスプローラー** で、 **ArithmeticUI** プロジェクトのショートカットメニューを開き、[参照の **追加**] を選択し  >  ます。

5. [ **Windows**] の下で [ **拡張機能**] を選択し、 **単純な数値演算** が表示されることを確認します。

6. [ **単純な数値演算** ] チェックボックスをオンにし、[ **OK** ] をクリックします。

7. **ソリューションエクスプローラー** の [**参照**] で、**単純な数値演算** 参照が表示されていることに注意してください。 これを展開して、 **arithmetic.js** を含む **\ \\ js** フォルダーがあることを確認します。 **arithmetic.js** を開いて、ソースコードがインストールされていることを確認できます。

8. 次のコードを使用して、 *default.htm* の内容を置き換えます。

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

9. 次のコードを使用して、 *\js\default.js* の内容を置き換えます。

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

10. *\Css\default.css* の内容を次のコードに置き換えます。

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

11. F5 キーを **押し** て、アプリをビルドして実行します。

12. アプリ UI で、任意の2つの数値を入力し、操作を選択して、ボタンをクリックし **=** ます。 正しい結果が表示されます。

## <a name="see-also"></a>こちらもご覧ください
- [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
