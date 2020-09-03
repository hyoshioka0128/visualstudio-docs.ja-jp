---
title: 'チュートリアル: JavaScript を使用した SDK の作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3e953d9051b9bc7e95dc29e02eb580c4d93fca26
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148832"
---
# <a name="walkthrough-creating-an-sdk-using-javascript"></a>チュートリアル: JavaScript を使用して SDK を作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、JavaScript を使用して、Visual Studio 拡張機能 (VSIX) として簡単な数値演算 SDK を作成する方法について説明します。  このチュートリアルは、次の部分に分かれています。  
  
- [Simplem、Vsix 拡張機能 SDK プロジェクトを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)  
  
- [SDK を使用するサンプルアプリを作成するには](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)  
  
  JavaScript の場合、クラスライブラリプロジェクトの種類はありません。 このチュートリアルでは、サンプルの arithmetic.js ファイルを VSIX プロジェクトに直接作成します。 実際には、最初に、VSIX プロジェクトに配置する前に、JavaScript と CSS ファイルを Windows ストアアプリとして作成し、テストすることをお勧めします。たとえば、 **空のアプリケーション** テンプレートを使用します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="to-create-the-simplemathvsix-extension-sdk-project"></a><a name="createSimpleMathVSIX"></a> Simplem、Vsix 拡張機能 SDK プロジェクトを作成するには  
  
1. メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  
  
2. テンプレートカテゴリの一覧で、[ **Visual C#**] の下の [ **機能拡張**] を選択し、[ **VSIX プロジェクト** ] テンプレートを選択します。  
  
3. [ **名前** ] テキストボックスで、を指定し、[ `SimpleMathVSIX` **OK** ] をクリックします。  
  
4. **Visual Studio パッケージウィザード**が表示されたら、[**ようこそ**] ページの [**次へ**] をクリックします。次に、 **7 ページ目**の [**完了**] ボタンをクリックします。  
  
     **マニフェストデザイナー**が開きますが、マニフェストファイルを直接変更することで、このチュートリアルを簡単に行うことができます。  
  
5. **ソリューションエクスプローラー**で、source.extension.vsixmanifest ファイルのショートカットメニューを開き、[**コードの表示**] を選択します。 このコードを使用して、ファイル内の既存のコンテンツを置き換えます。  
  
    ```  
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
  
6. **ソリューションエクスプローラー**で、Simplemの vsix プロジェクトのショートカットメニューを開き、[**追加**]、[**新しい項目**] の順に選択します。  
  
7. [ **データ** ] カテゴリで [ **XML ファイル**] を選択し、ファイルに名前 `SDKManifest.xml` を指定して、[ **追加** ] ボタンをクリックします。  
  
8. **ソリューションエクスプローラー**で、SDKManifest.xml ファイルのショートカットメニューを開き、[**開く**] をクリックして、 **XML エディター**でファイルを表示します。  
  
9. 次のコードを SDKManifest.xml ファイルに追加します。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <FileList  
      DisplayName="Simple Math"  
      MinVSVersion="14.0"  
      AppliesTo="JavaScript+WindowsAppContainer"  
      SupportsMultipleVersions="Error"  
      MoreInfo="http://www.msdn.microsoft.com/">  
  
      <!-- JS -->  
      <File Content="js\arithmetic.js" />  
    </FileList>  
  
    ```  
  
10. **ソリューションエクスプローラー**の SDKManifest.xml ファイルのショートカットメニューで、[**プロパティ**] を選択します。  
  
11. [ **プロパティ** ] ウィンドウで、[ **VSIX に含める** ] プロパティを [ **True**] に設定します。  
  
12. **ソリューションエクスプローラー**で、Simplemの vsix プロジェクトのショートカットメニューで、[**追加**]、[**新しいフォルダー**] の順に選択し、フォルダーに名前を指定し `Redist` ます。  
  
13. [Redist] の下にサブフォルダーを追加して、このフォルダー構造を作成します。  
  
     \Redist\CommonConfiguration\Neutral\SimpleMath\js\  
  
14. \Js\ フォルダーのショートカットメニューで、[ **追加**]、[ **新しい項目**] の順に選択します。  
  
15. [ **Visual C# アイテム**] で、[ **Web** ] カテゴリを選択し、[ **JavaScript ファイル** ] 項目を選択します。 ファイルに名前を指定し、 `arithmetic.js` [ **追加** ] ボタンをクリックします。  
  
16. arithmetic.js に次のコードを挿入します。  
  
    ```  
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
  
17. **ソリューションエクスプローラー**の arithmetic.js ファイルのショートカットメニューで、[**プロパティ**] を選択します。 次のプロパティを変更します。  
  
    - [ **VSIX に含める (VSIX に含める** ) プロパティを **True**に設定します。  
  
    - [ **出力ディレクトリにコピーする** "プロパティ" を " **常にコピー**する" に設定します。  
  
18. **ソリューションエクスプローラー**で、Simplemの vsix プロジェクトのショートカットメニューで、[**ビルド**] を選択します。  
  
19. ビルドが正常に完了したら、プロジェクトのショートカットメニューで、[ **エクスプローラーでフォルダーを開く**] を選択します。 [\Bin\debug] に移動し、を \\ 実行し `SimpleMathVSIX.vsix` てインストールします。  
  
20. [ **インストール** ] をクリックし、インストールを完了します。  
  
21. Visual Studio を再起動します。  
  
## <a name="to-create-a-sample-app-that-uses-the-sdk"></a><a name="createSampleApp"></a> SDK を使用するサンプルアプリを作成するには  
  
1. メニュー バーで、 **[ファイル]** 、 **[新規作成]** 、 **[プロジェクト]** の順にクリックします。  
  
2. テンプレートカテゴリの一覧で、[ **JavaScript**] の下にある [ **Windows ストア**] を選択し、[ **空のアプリケーション** ] テンプレートを選択します。  
  
3. [ **名前** ] ボックスに、を指定し `ArithmeticUI` ます。 **[OK]** を選択します。  
  
4. **ソリューションエクスプローラー**で、ArithmeticUI プロジェクトのショートカットメニューを開き、[**追加**]、[**参照**] の順に選択します。  
  
5. [ **Windows**] の下で [ **拡張機能**] を選択し、 **単純な数値演算** が表示されることを確認します。  
  
6. [ **単純な数値演算** ] チェックボックスをオンにし、[ **OK** ] をクリックします。  
  
7. **ソリューションエクスプローラー**の [**参照**] で、**単純な数値演算**参照が表示されていることに注意してください。 それを展開し、arithmetic.js を含む \js\ フォルダーがあることを確認します。 arithmetic.js を開いて、ソースコードがインストールされていることを確認できます。  
  
8. 次のコードを使用して、default.htm の内容を置き換えます。  
  
    ```  
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
  
9. 次のコードを使用して、\js\default.js の内容を置き換えます。  
  
    ```  
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
  
10. \Css\default.css の内容を次のコードに置き換えます。  
  
    ```  
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
  
11. F5 キーを押して、アプリをビルドして実行します。  
  
12. アプリ UI で、任意の2つの数値を入力し、操作を選択して、ボタンをクリックし **=** ます。 正しい結果が表示されます。  
  
## <a name="see-also"></a>参照  
 [ソフトウェア開発キットを作成する](../extensibility/creating-a-software-development-kit.md)
