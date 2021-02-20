---
title: Vbc タスク | Microsoft Docs
description: MSBuild で、実行可能ファイル、ダイナミックリンク ライブラリ、またはコード モジュールを生成する vbc.exe をラップする Vbc タスクの使用方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 04/12/2018
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Vbc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Vbc task [MSBuild]
- MSBuild, Vbc task
ms.assetid: 595278b1-2782-4577-b1ba-b4b5ab5625a3
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6596dd0893d0ab302a738cb12856fc6758df039
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908868"
---
# <a name="vbc-task"></a>Vbc タスク

実行可能ファイル ( *.exe*)、ダイナミック リンク ライブラリ ( *.dll*)、またはコード モジュール ( *.netmodule*) を生成する *vbc.exe* をラップします。 *vbc.exe* の詳細については、「[Visual Basic のコマンド ライン コンパイラ](/dotnet/visual-basic/reference/command-line-compiler/index)」を参照してください。

## <a name="parameters"></a>パラメーター

 `Vbc` タスクのパラメーターの説明を次の表に示します。

| パラメーター | 説明 |
|------------------------------| - |
| `AdditionalLibPaths` | 省略可能な `String[]` 型のパラメーターです。<br /><br /> 参照属性に指定されているアセンブリを探す追加のフォルダーを指定します。 |
| `AddModules` | 省略可能な `String[]` 型のパラメーターです。<br /><br /> 指定ファイル内のすべての型情報を現在のコンパイル対象のプロジェクトで使用できるようにします。 このパラメーターは、*vbc.exe* コンパイラの [-addmodule](/dotnet/visual-basic/reference/command-line-compiler/addmodule) スイッチに相当します。 |
| `BaseAddress` | 省略可能な `String` 型のパラメーターです。<br /><br /> DLL のベース アドレスを指定します。 このパラメーターは、*vbc.exe* コンパイラの [-baseaddress](/dotnet/visual-basic/reference/command-line-compiler/baseaddress) スイッチに相当します。 |
| `CodePage` | 省略可能な `Int32` 型のパラメーターです。<br /><br /> コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。 このパラメーターは、*vbc.exe* コンパイラの [-codepage](/dotnet/visual-basic/reference/command-line-compiler/codepage) スイッチに相当します。 |
| `DebugType` | 省略可能な `String[]` 型のパラメーターです。<br /><br /> コンパイラにデバッグ情報を生成させます。 このパラメーターには、次の値を指定できます。<br /><br /> -   `full`<br />-   `pdbonly`<br /><br /> 既定値は `full` です。実行中のプログラムにデバッガーをアタッチできます。 値 `pdbonly` を指定すると、プログラムがデバッガーで開始されたとき、ソース コードのデバッグが可能になりますが、実行中のプログラムがデバッガーにアタッチされているときにのみアセンブリ言語コードが表示されます。 詳細については、「[-debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug)」を参照してください。 |
| `DefineConstants` | 省略可能な `String[]` 型のパラメーターです。<br /><br /> 条件付きコンパイル定数を定義します。 次の構文に従い、シンボルと値のペアをセミコロン (;) で区切って指定します。<br /><br /> *symbol1* `=` *value1* `;` *symbol2* `=` *value2*<br /><br /> このパラメーターは、*vbc.exe* コンパイラの [-define](/dotnet/visual-basic/reference/command-line-compiler/define) スイッチに相当します。 |
| `DelaySign` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、公開鍵がアセンブリに配置されます。 `false` の場合、アセンブリに完全署名されます。 既定値は `false` です。`KeyFile` パラメーターまたは `KeyContainer` パラメーターと併用しない限り、このパラメーターは無効です。 このパラメーターは、*vbc.exe* コンパイラの [-delaysign](/dotnet/visual-basic/reference/command-line-compiler/delaysign) スイッチに相当します。 |
| `Deterministic` | 省略可能な `Boolean` 型のパラメーターです。<br/><br/> `true` の場合、バイナリ コンテンツがコンパイル全体で同一のアセンブリをコンパイラに出力させます (入力が同一である場合)。<br/><br/>詳細については、「[-deterministic](/dotnet/visual-basic/reference/command-line-compiler/deterministic)」を参照してください。 |
| `DisabledWarnings` | 省略可能な `String` 型のパラメーターです。<br /><br /> 指定された警告の出力を抑制します。 警告 ID の数値だけを指定します。 複数の警告を指定するときは、セミコロン (;) で区切ります。 このパラメーターは、*vbc.exe* コンパイラの [-nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn) スイッチに相当します。 |
| `DocumentationFile` | 省略可能な `String` 型のパラメーターです。<br /><br /> 指定した XML ファイルにドキュメント コメントを出力します。 このパラメーターは `GenerateDocumentation` 属性をオーバーライドします。 詳細については、「[-doc](/dotnet/visual-basic/reference/command-line-compiler/doc)」を参照してください。 |
| `EmitDebugInformation` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、デバッグ情報が生成され、 *.pdb* ファイルに格納されます。 詳細については、「[-debug (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/debug)」を参照してください。 |
| `ErrorReport` | 省略可能な `String` 型のパラメーターです。<br /><br /> 内部コンパイル エラーの報告方法を指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `prompt`<br />-   `send`<br />-   `none`<br /><br /> `prompt` を指定した場合、内部コンパイラ エラーが発生すると、ユーザーはエラー データを Microsoft に送信するかどうかを選択するように求められます。<br /><br /> `send` を指定した場合、内部コンパイラ エラーが発生すると、エラー データが Microsoft に送信されます。<br /><br /> 既定値は `none` です。テキスト出力のみでエラーが報告されます。<br /><br /> このパラメーターは、*vbc.exe* コンパイラの [-errorreport](/dotnet/visual-basic/reference/command-line-compiler/errorreport) スイッチに相当します。 |
| `FileAlignment` | 省略可能な `Int32` 型のパラメーターです。<br /><br /> 出力ファイルでセクションをアラインするサイズをバイト単位で指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `512`<br />-   `1024`<br />-   `2048`<br />-   `4096`<br />-   `8192`<br /><br /> このパラメーターは、*vbc.exe* コンパイラの [-filealign](/dotnet/visual-basic/reference/command-line-compiler/filealign) スイッチに相当します。 |
| `GenerateDocumentation` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、ドキュメント情報が生成され、タスクが作成する実行可能ファイルまたはライブラリの名前が与えられた XML ファイルに格納されます。 詳細については、「[-doc](/dotnet/visual-basic/reference/command-line-compiler/doc)」を参照してください。 |
| `Imports` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定した項目コレクションから名前空間をインポートします。 このパラメーターは、*vbc.exe* コンパイラの [-imports](/dotnet/visual-basic/reference/command-line-compiler/imports) スイッチに相当します。 |
| `KeyContainer` | 省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キー コンテナーの名前を指定します。 このパラメーターは、*vbc.exe* コンパイラの [-keycontainer](/dotnet/visual-basic/reference/command-line-compiler/keycontainer) スイッチに相当します。 |
| `KeyFile` | 省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キーを格納するファイル名を指定します。 詳細については、「[-keyfile](/dotnet/visual-basic/reference/command-line-compiler/keyfile)」を参照してください。 |
| `LangVersion` | 省略可能な <xref:System.String?displayProperty=fullName> 型のパラメーターです。<br /><br /> [言語バージョン](/dotnet/visual-basic/language-reference/configure-language-version)を指定します ("15.5" など)。 |
| `LinkResources` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 出力ファイル内で .NET Framework リソースへのリンクを作成します。リソース ファイルは出力ファイル内に置かれません。 このパラメーターは、*vbc.exe* コンパイラの [-linkresource](/dotnet/visual-basic/reference/command-line-compiler/linkresource) スイッチに相当します。 |
| `MainEntryPoint` | 省略可能な `String` 型のパラメーターです。<br /><br /> `Sub Main` プロシージャを格納するクラスまたはモジュールを指定します。 このパラメーターは、*vbc.exe* コンパイラの [-main](/dotnet/visual-basic/reference/command-line-compiler/main) スイッチに相当します。 |
| `ModuleAssemblyName` | 省略可能な `String` 型のパラメーターです。<br /><br /> このモジュールが一部となるアセンブリを指定します。 |
| `NoConfig` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> コンパイラで *vbc.rsp* ファイルを使用しないように指定します。 このパラメーターは、*vbc.exe* コンパイラの [-noconfig](/dotnet/visual-basic/reference/command-line-compiler/noconfig) パラメーターに相当します。 |
| `NoLogo` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラの著作権情報が表示されません。 このパラメーターは、*vbc.exe* コンパイラの [-nologo](/dotnet/visual-basic/reference/command-line-compiler/nologo) スイッチに相当します。 |
| `NoStandardLib` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> コンパイラが標準ライブラリを参照しないようにします。 このパラメーターは、*vbc.exe* コンパイラの [-nostdlib](/dotnet/visual-basic/reference/command-line-compiler/nostdlib) スイッチに相当します。 |
| `NoVBRuntimeReference` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> 内部使用のみ。 true の場合、*Microsoft.VisualBasic.dll* の自動参照が禁止されます。 |
| `NoWarnings` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、すべての警告が非表示になります。 詳しくは、「[-nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn)」をご覧ください。 |
| `Optimize` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラ最適化が有効になります。 このパラメーターは、*vbc.exe* コンパイラの [-optimize](/dotnet/visual-basic/reference/command-line-compiler/optimize) スイッチに相当します。 |
| `OptionCompare` | 省略可能な `String` 型のパラメーターです。<br /><br /> 文字列比較の方法を指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `binary`<br />-   `text`<br /><br /> 値 `binary` を指定すると、バイナリ文字列比較が使用されます。 値 `text` を指定すると、テキスト文字列比較が使用されます。 このパラメーターの既定値は、`binary` です。 このパラメーターは、*vbc.exe* コンパイラの [-optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare) スイッチに相当します。 |
| `OptionExplicit` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、変数の明示的宣言が必要になります。 このパラメーターは、*vbc.exe* コンパイラの [-optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit) スイッチに相当します。 |
| `OptionInfer` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、変数の型推論を許可します。 |
| `OptionStrict` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、厳密な型のセマンティックスが強制され、暗黙的な型変換が制限されます。 このパラメーターは、*vbc.exe* コンパイラの [-optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) スイッチに相当します。 |
| `OptionStrictType` | 省略可能な `String` 型のパラメーターです。<br /><br /> 警告を生成する厳密な型のセマンティックスを指定します。 現在のところ、"custom" のみに対応しています。 このパラメーターは、*vbc.exe* コンパイラの [-optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict) スイッチに相当します。 |
| `OutputAssembly` | 省略可能な `String` 型の出力パラメーターです。<br /><br /> 出力ファイルの名前を指定します。 このパラメーターは、*vbc.exe* コンパイラの [-out](/dotnet/visual-basic/reference/command-line-compiler/out) スイッチに相当します。 |
| `Platform` | 省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのターゲットとするプロセッサ プラットフォームを指定します。 このパラメーターの値には、`x86`、`x64` 、`Itanium`、または `anycpu` を指定できます。 既定値は `anycpu` です。 このパラメーターは、*vbc.exe* コンパイラの [-platform](/dotnet/visual-basic/reference/command-line-compiler/platform) スイッチに相当します。 |
| `References` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定したアイテムから現在のプロジェクトにパブリック型の情報をインポートするようにタスクに指示します。 このパラメーターは、*vbc.exe* コンパイラの [-reference](/dotnet/visual-basic/reference/command-line-compiler/reference) スイッチに相当します。 |
| `RemoveIntegerChecks` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、整数オーバーフローのエラー チェックを無効にします。 既定値は `false` です。 このパラメーターは、*vbc.exe* コンパイラの [-removeintchecks](/dotnet/visual-basic/reference/command-line-compiler/removeintchecks) スイッチに相当します。 |
| `Resources` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> .NET Framework のリソースを出力ファイルに埋め込みます。 このパラメーターは、*vbc.exe* コンパイラの [-resource](/dotnet/visual-basic/reference/command-line-compiler/resource) スイッチに相当します。 |
| `ResponseFiles` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> このタスクのコマンドを含む応答ファイルを指定します。 このパラメーターは、*vbc.exe* コンパイラの [@ (Specify Response File)](/dotnet/visual-basic/reference/command-line-compiler/specify-response-file) オプションに相当します。 |
| `RootNamespace` | 省略可能な `String` 型のパラメーターです。<br /><br /> すべての型宣言に対してルート名前空間を指定します。 このパラメーターは、*vbc.exe* コンパイラの [-rootnamespace](/dotnet/visual-basic/reference/command-line-compiler/rootnamespace) スイッチに相当します。 |
| `SdkPath` | 省略可能な `String` 型のパラメーターです。<br /><br /> *mscorlib.dll* および *microsoft.visualbasic.dll* の位置を指定します。 このパラメーターは、*vbc.exe* コンパイラの [-sdkpath](/dotnet/visual-basic/reference/command-line-compiler/sdkpath) スイッチに相当します。 |
| `Sources` | 省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 1 つまたは複数の Visual Basic ソース ファイルを指定します。 |
| `TargetCompactFramework` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、タスクのターゲットは .NET Compact Framework になります。 このスイッチは、*vbc.exe* コンパイラの [-netcf](/dotnet/visual-basic/reference/command-line-compiler/netcf) スイッチに相当します。 |
| `TargetType` | 省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのファイル形式を指定します。 このパラメーターには値として、コード ライブラリを作成する `library`、コンソール アプリケーションを作成する `exe`、モジュールを作成する `module`、Windows プログラムを作成する `winexe` を指定できます。 既定値は `library` です。 このパラメーターは、*vbc.exe* コンパイラの [-target](/dotnet/visual-basic/reference/command-line-compiler/target) スイッチに相当します。 |
| `Timeout` | 省略可能な `Int32` 型のパラメーターです。<br /><br /> タスク実行を終了するまでの時間をミリ秒単位で指定します。 既定値は `Int.MaxValue` であり、タイムアウト期限がないことを示します。 |
| `ToolPath` | 省略可能な `String` 型のパラメーターです。<br /><br /> タスクが基になる実行可能ファイル (*vbc.exe*) を読み込む場所を指定します。 このパラメーターを指定しない場合、タスクでは、MSBuild を実行しているフレームワークのバージョンに対応する SDK インストール パスが使用されます。 |
| `TreatWarningsAsErrors` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、すべての警告がエラーとして処理されます。 詳細については、「[-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)」を参照してください。 |
| `UseHostCompilerIfAvailable` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> 利用できる場合、インプロセス コンパイラ オブジェクトを使用するようにタスクに指示します。 Visual Studio によってのみ使用されます。 |
| `Utf8Output` | 省略可能な `Boolean` 型のパラメーターです。<br /><br /> UTF-8 エンコードを使用してコンパイラ出力をログに記録します。 このパラメーターは、*vbc.exe* コンパイラの [-utf8output](/dotnet/visual-basic/reference/command-line-compiler/utf8output) スイッチに相当します。 |
| `Verbosity` | 省略可能な `String` 型のパラメーターです。<br /><br /> コンパイラ出力の詳細度を指定します。 詳細度は `Quiet`、`Normal` (既定)、または `Verbose` です。 |
| `WarningsAsErrors` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱う警告の一覧を指定します。 詳細については、「[-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)」を参照してください。<br /><br /> このパラメーターは `TreatWarningsAsErrors` パラメーターをオーバーライドします。 |
| `WarningsNotAsErrors` | 省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱わない警告の一覧を指定します。 詳細については、「[-warnaserror (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/warnaserror)」を参照してください。<br /><br /> このパラメーターは、`TreatWarningsAsErrors` パラメーターが `true` に設定されている場合にのみ役に立ちます。 |
| `Win32Icon` | 省略可能な `String` 型のパラメーターです。<br /><br /> **ファイル エクスプローラー** で出力ファイルを適切に表示する *.ico* ファイルをアセンブリに挿入します。 このパラメーターは、*vbc.exe* コンパイラの [-win32icon](/dotnet/visual-basic/reference/command-line-compiler/win32icon) スイッチに相当します。 |
| `Win32Resources` | 省略可能な `String` 型のパラメーターです。<br /><br /> Win32 リソース ( *.res* ファイル) を出力ファイルに挿入します。 このパラメーターは、*vbc.exe* コンパイラの [-win32resource](/dotnet/visual-basic/reference/command-line-compiler/win32resource) スイッチに相当します。 |

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="example"></a>例

 次の例では、Visual Basic プロジェクトがコンパイルされます。

```xml
<VBC
   Sources="@(sources)"
   Resources="strings.resources"
   Optimize="true"
   OutputAssembly="out.exe"/>
```

## <a name="see-also"></a>関連項目

- [Visual Basic のコマンド ライン コンパイラ](/dotnet/visual-basic/reference/command-line-compiler/index)
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
