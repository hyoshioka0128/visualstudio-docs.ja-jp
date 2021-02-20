---
title: "\"マイ コードのみ\" を使用したユーザー コードのデバッグ | Microsoft Docs"
description: "\"マイ コードのみ\" はデバッグ機能であり、非ユーザー コードに呼び出しを自動的にステップ オーバーします。 この機能を有効化、無効化、使用する方法について説明します。"
ms.custom: SEO-VS-2020
ms.date: 02/13/2019
ms.topic: how-to
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9d4ea8bb6a1d03d3b61ab5be51992a7b51f661d1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893257"
---
# <a name="debug-only-user-code-with-just-my-code"></a>"マイ コードのみ" を使用してユーザー コードのみをデバッグする

"*マイ コードのみ*" は Visual Studio のデバッグ機能であり、システム、フレームワーク、およびその他の非ユーザー コードに呼び出しを自動的にステップ オーバーします。 **[呼び出し履歴]** ウィンドウでは、"マイ コードのみ" によってこれらの呼び出しが **[外部コード]** フレームに折りたたまれます。

.NET、C++、および JavaScript のプロジェクトでは、"マイ コードのみ" の動作が異なります。

## <a name="enable-or-disable-just-my-code"></a><a name="BKMK_Enable_or_disable_Just_My_Code"></a>"マイ コードのみ" の有効/無効の切り替え

ほとんどのプログラミング言語では、"マイ コードのみ" は既定で有効になっています。

- Visual Studio で "マイ コードのみ" を有効または無効にするには、 **[ツール]**  >  **[オプション]** (または **[デバッグ]**  >  **[オプション]** ) > **[デバッグ]**  >  **[全般]** で **[マイ コードのみを有効にする]** をオンまたはオフにします。

![[オプション] ダイアログ ボックス内の [マイ コードのみを有効にする]](../debugger/media/dbg_justmycode_options.png "マイ コードのみを有効にする")

> [!NOTE]
> **[マイ コードのみを有効にする]** は、すべての言語のすべての Visual Studio プロジェクトに適用されるグローバル設定です。

## <a name="just-my-code-debugging"></a>マイ コードのみデバッグ

デバッグ セッション中、 **[モジュール]** ウィンドウには、デバッガーがマイ コード (ユーザー コード) として扱っているコード モジュールが、そのシンボルの読み込み状態と共に表示されます。 詳細については、「[アプリにデバッガーをアタッチする方法について理解を深める](../debugger/debugger-tips-and-tricks.md#modules_window)」を参照してください。

![[モジュール] ウィンドウのユーザー コード](../debugger/media/dbg_justmycode_module.png "[モジュール] ウィンドウのユーザー コード")

**[呼び出し履歴]** ウィンドウまたは **[タスク]** ウィンドウでは、"マイ コードのみ" によって非ユーザー コードが `[External Code]` というラベルが付いた、淡色表示の注釈付きコード フレームに折りたたまれます。

![[呼び出し履歴] ウィンドウの外部コード フレーム](../debugger/media/dbg_justmycode_externalcode.png "外部コード フレーム")

>[!TIP]
>**[モジュール]** 、 **[呼び出し履歴]** 、 **[タスク]** 、またはその他のほとんどのデバッグ ウィンドウを開くには、デバッグ セッション中である必要があります。 デバッグ中に、 **[デバッグ]**  >  **[ウィンドウ]** で、開くウィンドウを選択します。

<a name="BKMK_Override_call_stack_filtering"></a> 折りたたまれた **[外部コード]** フレーム内のコードを表示するには、 **[呼び出し履歴]** ウィンドウまたは **[タスク]** ウィンドウ内を右クリックし、コンテキスト メニューから **[外部コードの表示]** を選択します。 **[外部コード]** フレームが展開された外部コード行で置き換えられます。

![[呼び出し履歴] ウィンドウの [外部コードの表示]](../debugger/media/dbg_justmycode_showexternalcode.png "[外部コードの表示]")

> [!NOTE]
> **[外部コードの表示]** は、ユーザーが開いているすべての言語のすべてのプロジェクトに適用される、現在のユーザー プロファイラー設定です。

**[呼び出し履歴]** ウィンドウで展開されている外部コード行をダブルクリックすると、ソース コード内の呼び出し元のコード行が緑色で強調表示されます。 DLL またはその他のモジュールが見つからないか、読み込まれていない場合、シンボルまたはソースが見つからないというページが表示されることがあります。

## <a name="net-just-my-code"></a><a name="BKMK__NET_Framework_Just_My_Code"></a>.NET での "マイ コードのみ"

.NET プロジェクトでは、"マイ コードのみ" はシンボル ( *.pdb*) ファイルとプログラムの最適化を使用して、ユーザー コードと非ユーザー コードを分類します。 .NET デバッガーでは、最適化されたバイナリと読み込まれていない *.pdb* ファイルが非ユーザー コードと見なされます。

次の 3 つのコンパイラ属性も、.NET デバッガーでユーザー コードと見なされるものに影響を与えます。

- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute> は、適用先のコードがユーザー コードでないことをデバッガーに通知します。
- <xref:System.Diagnostics.DebuggerHiddenAttribute> は、"マイ コードのみ" がオフになっていても、コードをデバッガーから見えないようにするための属性です。
- <xref:System.Diagnostics.DebuggerStepThroughAttribute> は、適用先のコードを (ステップ インではなく) ステップ スルーするよう、デバッガーに伝えます。

.NET デバッガーでは、他のすべてのコードがユーザー コードであると見なされます。

.NET のデバッグ中:

- 非ユーザー コードで **[デバッグ]**  >  **[ステップ イン]** を選択すると (または **F11** キーを押すと)、コードがユーザー コードの次の行にステップ オーバーされます。
- 非ユーザー コードで **[デバッグ]**  >  **[ステップ アウト]** を選択すると (または **Shift**+**F11** キーを押すと)、ユーザー コードの次の行まで実行されます。

それ以上のユーザー コードがない場合、デバッグはそれが終わるか、別のブレークポイントにヒットするか、エラーがスローされるまで続行されます。

<a name="BKMK_NET_Breakpoint_behavior"></a> デバッガーが非ユーザー コードで中断した場合 (たとえば、 **[デバッグ]** > **[すべて中断]** を使用して非ユーザー コードで一時停止する場合)、 **[No Source]\(ソースがありません\)** ウィンドウが表示されます。 次に、 **[デバッグ]**  >  **[ステップ]** コマンドを使用して、ユーザー コードの次の行に進むことができます。

ハンドルされない例外が非ユーザー コードで発生した場合、デバッガーは例外が生成されたユーザー コード行で停止します。

初回例外がその例外に対して有効になっている場合、ユーザー コード行の呼び出しがソース コード内で緑で強調表示されます。 **[呼び出し履歴]** ウィンドウに、 **[外部コード]** というラベルの注釈付きフレームが表示されます。

## <a name="c-just-my-code"></a><a name="BKMK_C___Just_My_Code"></a>C++ での "マイ コードのみ"

Visual Studio 2017 バージョン 15.8 以降では、コードのステップ実行に対して "マイ コードのみ" もサポートされています。 この機能では、[/JMC (マイ コードのみのデバッグ)](/cpp/build/reference/jmc) コンパイラ スイッチを使用する必要もあります。 このスイッチは、C++ プロジェクトでは既定で有効になっています。 **[呼び出し履歴]** ウィンドウと "マイ コードのみ" での呼び出し履歴のサポートには、/JMC スイッチは必要ありません。

<a name="BKMK_CPP_User_and_non_user_code"></a> ユーザー コードとして分類されるためには、ユーザー コードを含むバイナリの PDB がデバッガーによって読み込まれる必要があります (これを確認するには、 **[モジュール]** ウィンドウを使用します)。

**[呼び出し履歴]** ウィンドウなどの呼び出し履歴の動作については、C++ の "マイ コードのみ" では、これらの関数のみが "*非ユーザーコード*" と見なされます。

- シンボル ファイル内に除去されたソース情報がある関数。
- シンボル ファイルがスタック フレームに対応するソース ファイルがないことを示す関数。
- *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* フォルダー内の *\*.natjmc* ファイル内で指定された関数。

コードのステップ実行動作については、C++ の "マイ コードのみ" では、これらの関数のみが "*非ユーザーコード*" と見なされます。

- 対応する PDB ファイルがデバッガーに読み込まれていない関数。
- *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* フォルダー内の *\*.natjmc* ファイル内で指定された関数。

> [!NOTE]
> "マイ コードのみ" のコードのステップ実行動作については、Visual Studio 15.8 Preview 3 以降では MSVC コンパイラを使用して C++ コードをコンパイルし、/JMC コンパイラ スイッチを有効にする (既定で有効になっています) 必要があります。 詳細については、「[C++ の呼び出し履歴とコードのステップ実行動作をカスタマイズする](#BKMK_CPP_Customize_call_stack_behavior)」とこの[ブログ記事](https://devblogs.microsoft.com/cppblog/announcing-jmc-stepping-in-visual-studio/)を参照してください。 以前のコンパイラを使用してコンパイルされたコードの場合、 *.natstepfilter* ファイルは、"マイ コードのみ" に依存しないコードのステップ実行をカスタマイズする唯一の方法です。 [C++ ステップ実行動作のカスタマイズ](#BKMK_CPP_Customize_stepping_behavior)に関するセクションを参照してください。

<a name="BKMK_CPP_Stepping_behavior"></a> C++ のデバッグ中:

- 非ユーザー コードで **[デバッグ]**  >  **[ステップ イン]** を選択すると (または **F11** キーを押すと)、コードがユーザー コードの次の行にステップ オーバーされます。
- 非ユーザー コードで **[デバッグ]**  >  **[ステップ アウト]** を選択すると (または **Shift**+**F11** キーを押すと)、ユーザー コードの次の行まで実行されます。

それ以上のユーザー コードがない場合、デバッグはそれが終わるか、別のブレークポイントにヒットするか、エラーがスローされるまで続行されます。

デバッガーによって非ユーザー コードで実行が中断された場合 (たとえば、 **[デバッグ]**  >  **[すべて中断]** を使用して非ユーザー コードで一時停止した場合)、その非ユーザー コードでステップ実行が続行されます。

デバッガーの実行中に例外が発生すると、デバッガーはユーザー コードまたは非ユーザー コードの実行中であっても、その例外で停止します。 **[例外設定]** ダイアログ ボックスの **[ユーザーにハンドルされていないとき]** オプションは無視されます。

### <a name="customize-c-call-stack-and-code-stepping-behavior"></a><a name="BKMK_CPP_Customize_call_stack_behavior"></a> C++ の呼び出し履歴とコードのステップ実行動作をカスタマイズする

C++ プロジェクトでは、 **[呼び出し履歴]** ウィンドウで非ユーザー コードとして扱うモジュール、ソース ファイル、関数を、 *\*.natjmc* ファイルで指定することができます。 最新のコンパイラを使用している場合は、このカスタマイズもコードのステップ実行に適用されます (「[C++ での "マイ コードのみ"](#BKMK_CPP_User_and_non_user_code)」を参照)。

- Visual Studio コンピューターのすべてのユーザーの非ユーザー コードを指定するには、 *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* フォルダーに *.natjmc* ファイルを追加します。
- 個々のユーザーに非ユーザー コードを指定するには、 *%USERPROFILE%\My Documents\\<Visual Studio のバージョン\>\Visualizers* フォルダーに *.natjmc* ファイルを追加します。

*.natjmc* ファイルは、次の構文を持つ XML ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<NonUserCode xmlns="http://schemas.microsoft.com/vstudio/debugger/jmc/2015">

  <!-- Modules -->
  <Module Name="ModuleSpec" />
  <Module Name="ModuleSpec" Company="CompanyName" />

  <!-- Files -->
  <File Name="FileSpec"/>

  <!-- Functions -->
  <Function Name="FunctionSpec" />
  <Function Name="FunctionSpec" Module ="ModuleSpec" />
  <Function Name="FunctionSpec" Module ="ModuleSpec" ExceptionImplementation="true" />

</NonUserCode>

```

 **Module 要素の属性**

|属性|説明|
|---------------|-----------------|
|`Name`|必須です。 モジュールの完全パス。 Windows のワイルドカード文字、`?` (0 個または 1 個の文字) および `*` (0 個以上の文字) を使用できます。 たとえば、オブジェクトに適用された<br /><br /> `<Module Name="?:\3rdParty\UtilLibs\*" />`<br /><br /> では、ドライブの *\3rdParty\UtilLibs* 内のすべてのモジュールを外部コードとして扱うことをデバッガーに指示します。|
|`Company`|任意。 実行可能ファイルに埋め込まれているモジュールを発行する会社の名前。 この属性を使用して、モジュールのあいまいさを解消することができます。|

 **File 要素の属性**

|属性|説明|
|---------------|-----------------|
|`Name`|必須です。 外部コードとして扱うソース ファイルの完全パス。 パスを指定するときに Windows のワイルドカード文字、`?` および `*` を使用できます。|

 **Function 要素の属性**

|属性|説明|
|---------------|-----------------|
|`Name`|必須です。 外部コードとして扱う関数の完全修飾名。|
|`Module`|任意。 関数を含むモジュールの名前または完全パス。 この属性を使用して、同じ名前の関数のあいまいさを解消することができます。|
|`ExceptionImplementation`|`true` に設定すると、この関数ではなく、例外をスローした関数が呼び出し履歴に表示されます。|

### <a name="customize-c-stepping-behavior-independent-of-just-my-code-settings"></a><a name="BKMK_CPP_Customize_stepping_behavior"></a> "マイ コードのみ" の設定とは関係なく、C++ のステップ実行動作をカスタマイズする

C++ プロジェクトでは、ステップ オーバーする関数を指定できます。そのためには、 *\*.natstepfilter* ファイルにそれらを非ユーザー コードとして記述します。 *\*.natstepfilter* ファイルに記述された関数は、"マイ コードのみ" の設定に依存しません。

- Visual Studio のすべてのローカル ユーザーに非ユーザー コードを指定するには、 *.natstepfilter* ファイルを *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* フォルダーに追加します。
- 個々のユーザーに対して非ユーザー コードを指定するには、 *%USERPROFILE%\My Documents\\<Visual Studio のバージョン\>\Visualizers* フォルダーに *.natstepfilter* ファイルを追加します。

*.natstepfilter* ファイルは、次の構文を持つ XML ファイルです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<StepFilter xmlns="http://schemas.microsoft.com/vstudio/debugger/natstepfilter/2010">
    <Function>
        <Name>FunctionSpec</Name>
        <Action>StepAction</Action>
    </Function>
    <Function>
        <Name>FunctionSpec</Name>
        <Module>ModuleSpec</Module>
        <Action>StepAction</Action>
    </Function>
</StepFilter>

```

|要素|説明|
|-------------|-----------------|
|`Function`|必須です。 1 つ以上の関数を非ユーザー関数として指定します。|
|`Name`|必須です。 一致を照合する完全な関数名を指定する ECMA-262 書式の正規表現。 次に例を示します。<br /><br /> `<Name>MyNS::MyClass.*</Name>`<br /><br /> は、`MyNS::MyClass` のすべてのメソッドが非ユーザー コードと見なされることをデバッガーに知らせます。 一致照合では、大文字と小文字が区別されます。|
|`Module`|任意。 関数を含むモジュールへの完全パスを指定する ECMA-262 書式の正規表現。 一致では、大文字と小文字を区別しません。|
|`Action`|必須です。 大文字と小文字が区別される以下のいずれかの値です。<br /><br /> `NoStepInto` - 関数をステップ オーバーすることをデバッガーに指示します。<br /> `StepInto` - 関数にステップ インし、一致した関数のその他の `NoStepInto` をオーバーライドすることをデバッガーに指示します。|

## <a name="javascript-just-my-code"></a><a name="BKMK_JavaScript_Just_My_Code"></a>JavaScript での "マイ コードのみ"

<a name="BKMK_JS_User_and_non_user_code"></a>JavaScript の "マイ コードのみ" では、以下のいずれかの方法でコードを分類することによって、ステップ実行と呼び出し履歴表示が制御されます。

|分類|説明|
|-|-|
|**MyCode**|ユーザーが所有および制御するユーザー コード。|
|**LibraryCode**|ユーザーが通常使用し、アプリが正しく機能するために必要なライブラリからの非ユーザー コード (WinJS や jQuery など)。|
|**UnrelatedCode**|自分が所有していないアプリ内の、アプリが正しく機能するために依存していない非ユーザー コード。 たとえば、広告を表示する広告 SDK は、UnrelatedCode の可能性があります。 UWP プロジェクトでは、HTTP または HTTPS URI からアプリに読み込まれるコードも UnrelatedCode と見なされます。|

JavaScript デバッガーでは、次の順序でコードがユーザー コードまたは非ユーザー コードとして分類されます。

1. 既定の分類。
   - ホスト提供の `eval` 関数に文字列を渡すことで実行されるスクリプトは、**MyCode** です。
   - `Function` コンストラクターに文字列を渡すことで実行されるスクリプトは、**LibraryCode** です。
   - WinJS や Azure SDK などのフレームワーク参照内のスクリプトは、**LibraryCode** です。
   - `setTimeout`、`setImmediate`、または `setInterval` 関数に文字列を渡すことで実行されるスクリプトは、**UnrelatedCode** です。

2. *%VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json* ファイル内のすべての Visual Studio JavaScript プロジェクトに対して指定された分類。

3. 現在のプロジェクトの *mycode.json* ファイルでの分類。

分類の各手順で、前の手順はオーバーライドされます。

他のコードはすべて、**MyCode** として分類されます。

既定の分類を変更し、特定のファイルと URL をユーザー コードまたは非ユーザー コードとして分類することができます。そのためには、*mycode. json* という名前の *.json* ファイルを JavaScript プロジェクトのルート フォルダーに追加します。 「[JavaScript のマイ コードのみをカスタマイズする](#BKMK_JS_Customize_Just_My_Code)」を参照してください。

<a name="BKMK_JS_Stepping_behavior"></a> JavaScript のデバッグ中:

- 関数が非ユーザー コードの場合、 **[デバッグ]**  >  **[ステップ イン]** (または **F11**) は、 **[デバッグ]**  >  **[ステップ オーバー]** (または **F10**) と同様に動作します。
- ステップが非ユーザー (**LibraryCode** または **UnrelatedCode**) コードで始まる場合、ステップ実行は一時的に "マイ コードのみ" が有効でないように動作します。 ユーザー コードに戻ると、"マイ コードのみ" のステップ実行が再び有効になります。
- ユーザー コードのステップ実行によって現在の実行コンテキストがそのままになると、デバッガーは次に実行されるユーザー コード行で停止します。 たとえば、コールバックが **LibraryCode** コードで実行されると、デバッガーはユーザー コードの次の行が実行されるまで続行されます。
- **[ステップ アウト]** を選択すると (または **Shift**+**F11** キーを押すと)、ユーザー コードの次の行で停止します。

それ以上のユーザー コードがない場合、デバッグはそれが終わるか、別のブレークポイントにヒットするか、エラーがスローされるまで続行されます。

コードに設定されたブレークポイントは常にヒットしますが、コードは分類されます。

- `debugger` キーワードが **LibraryCode** で発生した場合、デバッガーは常に中断されます。
- `debugger` キーワードが **UnrelatedCode** で発生した場合、デバッガーは停止しません。

<a name="BKMK_JS_Exception_behavior"></a> **MyCode** または **LibraryCode** コードでハンドルされない例外が発生した場合、デバッガーは常に中断されます。

**UnrelatedCode** でハンドルされない例外が発生し、呼び出し履歴に **MyCode** または **LibraryCode** コードがある場合、デバッガーは中断されます。

初回例外がその例外に対して有効になっていて、例外が **LibraryCode** または **UnrelatedCode** で発生する場合:

- 例外が処理される場合、デバッガーは中断されません。
- 例外が処理されない場合、デバッガーは中断します。

### <a name="customize-javascript-just-my-code"></a><a name="BKMK_JS_Customize_Just_My_Code"></a> JavaScript の "マイ コードのみ" をカスタマイズする

単一の JavaScript プロジェクトのユーザー コードと非ユーザー コードを分類するには、プロジェクトのルート フォルダーに *mycode.json* という名前の *.json* ファイルを追加します。

このファイルの仕様によって、既定の分類と *mycode.default.wwa.json* ファイルがオーバーライドされます。 *mycode.json* ファイルに、すべてのキーと値のペアが記述されている必要はありません。 **MyCode**、**Libraries**、および **Unrelated** の値は空の配列にすることができます。

*Mycode.json* ファイルでは、次の構文が使用されます。

```json
{
    "Eval" : "Classification",
    "Function" : "Classification",
    "ScriptBlock" : "Classification",
    "MyCode" : [
        "UrlOrFileSpec",
        . . .
        "UrlOrFileSpec"
    ],
    "Libraries" : [
        "UrlOrFileSpec",
        . .
        "UrlOrFileSpec"
    ],
    "Unrelated" : [
        "UrlOrFileSpec",
        . . .
        "UrlOrFileSpec"
    ]
}

```

**Eval、Function、および ScriptBlock**

**Eval**、**Function**、および **ScriptBlock** のキーと値のペアで、動的に生成されたコードを分類する方法が決まります。

|名前|説明|
|-|-|
|**Eval**|ホスト提供の `eval` 関数に文字列を渡すことで実行されるスクリプト。 既定では、Eval スクリプトは **MyCode** として分類されます。|
|**Function**|`Function` コンストラクターに文字列を渡すことで実行されるスクリプト。 既定では、Function スクリプトは **LibraryCode** として分類されます。|
|**ScriptBlock**|`setTimeout`、`setImmediate`、または `setInterval` 関数に文字列を渡すことで実行されるスクリプト。 既定では、ScriptBlock スクリプトは **UnrelatedCode** として分類されます。|

以下のいずれかのキーワードに値を変更できます。

- `MyCode` では、スクリプトが **MyCode** として分類されます。
- `Library` では、スクリプトが **LibraryCode** として分類されます。
- `Unrelated` では、スクリプトが **UnrelatedCode** として分類されます。

**MyCode、Libraries、および Unrelated**

**MyCode**、**Libraries**、および **Unrelated** のキーと値のペアでは、分類に含める URL またはファイルを指定します。

|名前|説明|
|-|-|
|**MyCode**|**MyCode** として分類される URL またはファイルの配列。|
|**Libraries**|**LibraryCode** として分類される URL またはファイルの配列。|
|**Unrelated**|**UnrelatedCode** として分類される URL またはファイルの配列。|

URL またはファイルの文字列には、0 個以上の文字に一致する `*` 文字を 1 つ以上含めることができます。 `*` は、正規表現 `.*` と同じです。
