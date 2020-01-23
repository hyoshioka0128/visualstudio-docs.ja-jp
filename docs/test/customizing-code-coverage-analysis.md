---
title: コード カバレッジ分析のカスタマイズ
ms.date: 08/21/2019
ms.topic: conceptual
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: bce7a6b9369f33e6fa5248821f58d9903172415c
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918646"
---
# <a name="customize-code-coverage-analysis"></a>コード カバレッジ分析のカスタマイズ

既定では、コード カバレッジは、単体テスト中に読み込まれるすべてのソリューション アセンブリを分析します。 多くの場合は、この設定が効果的なので、この既定のビヘイビアーを使用することをお勧めします。 詳細については、「[コード カバレッジを使用した、テストされるコード割合の確認](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)」を参照してください。

テスト コードをコード カバレッジの結果から除外して、アプリケーション コードのみを含めるには、<xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute> 属性をテスト クラスに追加します。

ソリューションの一部ではないアセンブリを含めるには、これらのアセンブリの *.pdb* ファイルを取得し、アセンブリ *.dll* ファイルと同じフォルダーにコピーします。

## <a name="run-settings-file"></a>実行設定ファイル

[実行設定ファイル](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)は、単体テスト ツールによって使用される構成ファイルです。 詳細なコード カバレッジの設定は、 *.runsettings* ファイルで指定されます。

コード カバレッジをカスタマイズするには、次の手順を行います。

1. 実行設定ファイルをソリューションに追加します。 **ソリューション エクスプローラー**でソリューションのショートカット メニューを開き、 **[追加]**  >  **[新しい項目]** 、 **[XML ファイル]** の順に選択します。 *CodeCoverage.runsettings* などの名前でファイルを保存します。

2. この記事の最後にあるサンプル ファイルの内容を追加し、後続の各セクションの説明に従って、ニーズに合わせてカスタマイズします。

::: moniker range="vs-2017"

3. 実行設定ファイルを選択するには、 **[テスト]** メニューで **[テストの設定]**  >  **[テスト設定ファイルの選択]** の順に選択します。 コマンドラインからテストの実行で使用する実行設定ファイルを指定するには、[単体テストの構成](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md#command-line)に関する説明を参照してください。

::: moniker-end

::: moniker range=">=vs-2019"

3. 実行設定ファイルを選択するには、 **[テスト]** メニューで **[設定ファイルの選択]** を選択します。 コマンドラインからテストの実行で使用する実行設定ファイルを指定するには、[単体テストの構成](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md#command-line)に関する説明を参照してください。

::: moniker-end

   **[コード カバレッジの分析]** を選択すると、実行設定ファイルから構成情報が読み取られます。

   > [!TIP]
   > 前のコード カバレッジの結果とコードの色分けは、テストを実行したりコードを更新したりしても、自動的に非表示にはなりません。

::: moniker range="vs-2017"

カスタム設定のオンとオフを切り替えるには、 **[テスト]** > **[テストの設定]** メニューでファイルを選択したり選択解除したりします。

![Visual Studio 2017 でのカスタム設定ファイルがある設定メニュー](../test/media/codecoverage-settingsfile.png)

::: moniker-end

::: moniker range=">=vs-2019"

カスタム設定のオンとオフを切り替えるには、 **[テスト]** メニューで、ファイルを選択したり選択解除したりします。

::: moniker-end

## <a name="symbol-search-paths"></a>シンボルの検索パス

コード カバレッジには、アセンブリのシンボル ファイル ( *.pdb* ファイル) が必要です。 ソリューションによってビルドされたアセンブリには、通常、バイナリ ファイルと共にシンボル ファイルも存在しており、コード カバレッジは自動的に動作します。 場合によっては、参照されるアセンブリをコード カバレッジ分析に追加したいこともあります。 そのような場合、 *.pdb* ファイルがバイナリと同じ場所にないこともありますが、シンボル検索パスを *.runsettings* ファイルで指定できます。

```xml
<SymbolSearchPaths>
      <Path>\\mybuildshare\builds\ProjectX</Path>
      <!--More paths if required-->
</SymbolSearchPaths>
```

> [!NOTE]
> シンボルの解決には、特に多数のアセンブリでリモートのファイルの場所を使用している場合、時間がかかることがあります。 そのため、 *.pdb* ファイルをバイナリ ( *.dll* または *.exe*) ファイルと同じローカルの場所にコピーすることを検討してください。

## <a name="include-or-exclude-assemblies-and-members"></a>アセンブリやメンバーを含めるか除外する

アセンブリまたは特定の型とメンバーをコード カバレッジ分析に含めたり、コード カバレッジ分析から除外したりできます。 **[含める]** セクションが空か省略されている場合、読み込まれ、PDB ファイルが関連付けられているアセンブリがすべて含まれます。 アセンブリまたはメンバーが **[除外する]** セクションの句に一致する場合、それはコード カバレッジから除外されます。 **[除外する]** セクションは **[含める]** セクションに優先します。あるアセンブリが **[含める]** と **[除外する]** の両方に記載されている場合、コード カバレッジには含まれません。

たとえば、次の XML では、その名前を指定することで 1 つのアセンブリが除外されます。

```xml
<ModulePaths>
  <Exclude>
   <ModulePath>Fabrikam.Math.UnitTest.dll</ModulePath>
   <!-- Add more ModulePath nodes here. -->
  </Exclude>
</ModulePaths>
```

次の例では、アセンブリを 1 つだけコード カバレッジに含めると指定されます。

```xml
<ModulePaths>
  <Include>
   <ModulePath>Fabrikam.Math.dll</ModulePath>
   <!-- Add more ModulePath nodes here. -->
  </Include>
</ModulePaths>
```

次の表では、コード カバレッジに含めるか、コード カバレッジから除外する目的でアセンブリやメンバーを照合するさまざまな方法をまとめています。

| XML 要素 | 一致対象 |
| - | - |
| ModulePath | アセンブリ名またはファイル パスで指定されたアセンブリと一致します。 |
| CompanyName | **Company** 属性でアセンブリと一致します。 |
| PublicKeyToken | 公開キー トークンで署名付きアセンブリと一致します。 |
| ソース | 要素が定義されているソース ファイルのパス名で要素と一致します。 |
| 属性 | 指定された属性を持つ要素と一致します。 `<Attribute>^System\.Diagnostics\.DebuggerHiddenAttribute$</Attribute>` など、属性の完全な名前を指定します。<br/><br/><xref:System.Runtime.CompilerServices.CompilerGeneratedAttribute> 属性を除外すると、`async`、`await`、`yield return` などの言語機能を使用するコードと、自動実装プロパティがコード カバレッジ分析から除外されます。 真に生成されたコードを除外するには、<xref:System.CodeDom.Compiler.GeneratedCodeAttribute> 属性のみを除外します。 |
| 関数 | パラメーター リストなど、完全修飾名でプロシージャ、関数、またはメソッドと一致します。 [正規表現](#regular-expressions)を利用し、名前の一部を照合することもできます。<br/><br/>次に例を示します。<br/><br/>`Fabrikam.Math.LocalMath.SquareRoot(double);` (C#)<br/><br/>`Fabrikam::Math::LocalMath::SquareRoot(double)` (C++) |

### <a name="regular-expressions"></a>正規表現

Include ノードと Exclude ノードでは、ワイルドカードとは異なる正規表現が使用されます。 すべての一致で、大文字と小文字が区別されます。 次に、例を示します。

- **.\*** は任意の文字の文字列と一致します

- **\\.** はピリオド "." と一致します

- **\\(   \\)** は "(  )" と一致します

- **\\\\** はファイル パス区切り記号 "\\" と一致します

- **^** は文字列の先頭と一致します

- **$** は文字列の末尾と一致します

次の XML では、正規表現を利用し、特定のアセンブリを含める方法と除外する方法を確認できます。

```xml
<ModulePaths>
  <Include>
    <!-- Include all loaded .dll assemblies (but not .exe assemblies): -->
    <ModulePath>.*\.dll$</ModulePath>
  </Include>
  <Exclude>
    <!-- But exclude some assemblies: -->
    <ModulePath>.*\\Fabrikam\.MyTests1\.dll$</ModulePath>
    <!-- Exclude all file paths that contain "Temp": -->
    <ModulePath>.*Temp.*</ModulePath>
  </Exclude>
</ModulePaths>
```

次の XML では、正規表現を利用し、特定の関数を含める方法と除外する方法を確認できます。

```xml
<Functions>
  <Include>
    <!-- Include methods in the Fabrikam namespace: -->
    <Function>^Fabrikam\..*</Function>
    <!-- Include all methods named EqualTo: -->
    <Function>.*\.EqualTo\(.*</Function>
  </Include>
  <Exclude>
    <!-- Exclude methods in a class or namespace named UnitTest: -->
    <Function>.*\.UnitTest\..*</Function>
  </Exclude>
</Functions>
```

> [!WARNING]
> 正規表現にエラー (エスケープされていない、または一致しないかっこなど) がある場合、コード カバレッジ分析は実行されません。

正規表現の詳細については、「[Visual Studio での正規表現の使用](../ide/using-regular-expressions-in-visual-studio.md)」を参照してください。

## <a name="sample-runsettings-file"></a>サンプル .runsettings ファイル

このコードをコピーし、自分のニーズに合わせて編集します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- File name extension must be .runsettings -->
<RunSettings>
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
        <Configuration>
          <CodeCoverage>
<!--
Additional paths to search for .pdb (symbol) files. Symbols must be found for modules to be instrumented.
If .pdb files are in the same folder as the .dll or .exe files, they are automatically found. Otherwise, specify them here.
Note that searching for symbols increases code coverage runtime. So keep this small and local.
-->
<!--
            <SymbolSearchPaths>
                   <Path>C:\Users\User\Documents\Visual Studio 2012\Projects\ProjectX\bin\Debug</Path>
                   <Path>\\mybuildshare\builds\ProjectX</Path>
            </SymbolSearchPaths>
-->

<!--
About include/exclude lists:
Empty "Include" clauses imply all; empty "Exclude" clauses imply none.
Each element in the list is a regular expression (ECMAScript syntax). See /visualstudio/ide/using-regular-expressions-in-visual-studio.
An item must first match at least one entry in the include list to be included.
Included items must then not match any entries in the exclude list to remain included.
-->

            <!-- Match assembly file paths: -->
            <ModulePaths>
              <Include>
                <ModulePath>.*\.dll$</ModulePath>
                <ModulePath>.*\.exe$</ModulePath>
              </Include>
              <Exclude>
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
              </Exclude>
            </ModulePaths>

            <!-- Match fully qualified names of functions: -->
            <!-- (Use "\." to delimit namespaces in C# or Visual Basic, "::" in C++.)  -->
            <Functions>
              <Exclude>
                <Function>^Fabrikam\.UnitTest\..*</Function>
                <Function>^std::.*</Function>
                <Function>^ATL::.*</Function>
                <Function>.*::__GetTestMethodInfo.*</Function>
                <Function>^Microsoft::VisualStudio::CppCodeCoverageFramework::.*</Function>
                <Function>^Microsoft::VisualStudio::CppUnitTestFramework::.*</Function>
              </Exclude>
            </Functions>

            <!-- Match attributes on any code element: -->
            <Attributes>
              <Exclude>
                <!-- Don't forget "Attribute" at the end of the name -->
                <Attribute>^System\.Diagnostics\.DebuggerHiddenAttribute$</Attribute>
                <Attribute>^System\.Diagnostics\.DebuggerNonUserCodeAttribute$</Attribute>
                <Attribute>^System\.CodeDom\.Compiler\.GeneratedCodeAttribute$</Attribute>
                <Attribute>^System\.Diagnostics\.CodeAnalysis\.ExcludeFromCodeCoverageAttribute$</Attribute>
              </Exclude>
            </Attributes>

            <!-- Match the path of the source files in which each method is defined: -->
            <Sources>
              <Exclude>
                <Source>.*\\atlmfc\\.*</Source>
                <Source>.*\\vctools\\.*</Source>
                <Source>.*\\public\\sdk\\.*</Source>
                <Source>.*\\microsoft sdks\\.*</Source>
                <Source>.*\\vc\\include\\.*</Source>
              </Exclude>
            </Sources>

            <!-- Match the company name property in the assembly: -->
            <CompanyNames>
              <Exclude>
                <CompanyName>.*microsoft.*</CompanyName>
              </Exclude>
            </CompanyNames>

            <!-- Match the public key token of a signed assembly: -->
            <PublicKeyTokens>
              <!-- Exclude Visual Studio extensions: -->
              <Exclude>
                <PublicKeyToken>^B77A5C561934E089$</PublicKeyToken>
                <PublicKeyToken>^B03F5F7F11D50A3A$</PublicKeyToken>
                <PublicKeyToken>^31BF3856AD364E35$</PublicKeyToken>
                <PublicKeyToken>^89845DCD8080CC91$</PublicKeyToken>
                <PublicKeyToken>^71E9BCE111E9429C$</PublicKeyToken>
                <PublicKeyToken>^8F50407C4E9E73B6$</PublicKeyToken>
                <PublicKeyToken>^E361AF139669C375$</PublicKeyToken>
              </Exclude>
            </PublicKeyTokens>

            <!-- We recommend you do not change the following values: -->

            <!-- Set this to True to collect coverage information for functions marked with the "SecuritySafeCritical" attribute. Instead of writing directly into a memory location from such functions, code coverage inserts a probe that redirects to another function, which in turns writes into memory. -->
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
            <!-- When set to True, collects coverage information from child processes that are launched with low-level ACLs, for example, UWP apps. -->
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
            <!-- When set to True, collects coverage information from child processes that are launched by test or production code. -->
            <CollectFromChildProcesses>True</CollectFromChildProcesses>
            <!-- When set to True, restarts the IIS process and collects coverage information from it. -->
            <CollectAspDotNet>False</CollectAspDotNet>

          </CodeCoverage>
        </Configuration>
      </DataCollector>
    </DataCollectors>
  </DataCollectionRunSettings>
</RunSettings>
```

## <a name="see-also"></a>関連項目

- [.runsettings ファイルを使用して単体テストを構成する](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [コード カバレッジを使用した、テストされるコード割合の確認](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)
- [コードの単体テスト](../test/unit-test-your-code.md)
