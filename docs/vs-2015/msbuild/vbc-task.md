---
title: Vbc タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6edc8b246055dcd8efdb32f4118f81a535635d55
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683835"
---
# <a name="vbc-task"></a>Vbc タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

実行可能ファイル (.exe)、ダイナミック リンク ライブラリ (.dll)、またはコード モジュール (.netmodule) を生成する vbc.exe をラップします。 vbc.exe の詳細については、「 [コマンドラインコンパイラの Visual Basic](https://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 `Vbc` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AdditionalLibPaths`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 参照属性に指定されているアセンブリを探す追加のフォルダーを指定します。|  
|`AddModules`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 指定ファイル内のすべての型情報を現在のコンパイル対象のプロジェクトで使用できるようにします。 このパラメーターは、vbc.exe コンパイラの [/addmodule](https://msdn.microsoft.com/library/fb4b89d4-4926-4f20-868d-427fa28497b2) スイッチに相当します。|  
|`BaseAddress`|省略可能な `String` 型のパラメーターです。<br /><br /> DLL のベース アドレスを指定します。 このパラメーターは、vbc.exe コンパイラの [/baseaddress](https://msdn.microsoft.com/library/c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47) スイッチに相当します。|  
|`CodePage`|省略可能な `Int32` 型のパラメーターです。<br /><br /> コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。 このパラメーターは、vbc.exe コンパイラの [/codepage](https://msdn.microsoft.com/library/be36ec33-6800-4505-838c-4124564f5cc9) スイッチに相当します。|  
|`DebugType`|省略可能な `String[]` 型のパラメーターです。<br /><br /> コンパイラにデバッグ情報を生成させます。 このパラメーターには、次の値を指定できます。<br /><br /> -   `full`<br />-   `pdbonly`<br /><br /> 既定値は `full` です。実行中のプログラムにデバッガーをアタッチできます。 値 `pdbonly` を指定すると、プログラムがデバッガーで開始されたとき、ソース コードのデバッグが可能になりますが、実行中のプログラムがデバッガーにアタッチされているときにのみアセンブリ言語コードが表示されます。 詳細については、「 [/debug (Visual Basic)](https://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2)」を参照してください。|  
|`DefineConstants`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 条件付きコンパイル定数を定義します。 次の構文に従い、シンボルと値のペアをセミコロン (;) で区切って指定します。<br /><br /> *symbol1* `=` *value1* `;` *symbol2* `=` *value2*<br /><br /> このパラメーターは、vbc.exe コンパイラの [/define](https://msdn.microsoft.com/library/f735c57d-1cf9-4f2f-a26f-0de630fd4077) スイッチに相当します。|  
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、公開鍵がアセンブリに配置されます。 `false` の場合、アセンブリに完全署名されます。 既定値は `false` です。`KeyFile` パラメーターまたは `KeyContainer` パラメーターと併用しない限り、このパラメーターは無効です。 このパラメーターは、vbc.exe コンパイラの [/delaysign](https://msdn.microsoft.com/library/c76e61a4-1884-4252-9fb2-377f99caa690) スイッチに相当します。|  
|`DisabledWarnings`|省略可能な `String` 型のパラメーターです。<br /><br /> 指定された警告の出力を抑制します。 警告 ID の数値だけを指定します。 複数の警告を指定するときは、セミコロン (;) で区切ります。 このパラメーターは、vbc.exe コンパイラの [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83) スイッチに相当します。|  
|`DocumentationFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 指定した XML ファイルにドキュメント コメントを出力します。 このパラメーターは `GenerateDocumentation` 属性をオーバーライドします。 詳細については、「 [/doc](https://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65)」を参照してください。|  
|`EmitDebugInformation`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、デバッグ情報が生成され、.pdb ファイルに格納されます。 詳細については、「 [/debug (Visual Basic)](https://msdn.microsoft.com/library/c2b0bea5-1d5e-499f-9bd5-4f6c6b715ea2)」を参照してください。|  
|`ErrorReport`|省略可能な `String` 型のパラメーターです。<br /><br /> 内部コンパイル エラーの報告方法を指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `prompt`<br />-   `send`<br />-   `none`<br /><br /> `prompt` を指定した場合、内部コンパイラ エラーが発生すると、ユーザーはエラー データを Microsoft に送信するかどうか選択するように求められます。<br /><br /> `send` を指定した場合、内部コンパイラ エラーが発生すると、エラー データが Microsoft に送信されます。<br /><br /> 既定値は `none` です。テキスト出力のみでエラーが報告されます。<br /><br /> このパラメーターは、vbc.exe コンパイラの [/errorreport](https://msdn.microsoft.com/library/a7fe83a2-a6d8-460c-8dad-79a8f433f501) スイッチに対応します。|  
|`FileAlignment`|省略可能な `Int32` 型のパラメーターです。<br /><br /> 出力ファイルでセクションをアラインするサイズをバイト単位で指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `512`<br />-   `1024`<br />-   `2048`<br />-   `4096`<br />-   `8192`<br /><br /> このパラメーターは、vbc.exe コンパイラの [/filealign](https://msdn.microsoft.com/library/cc61ec3d-ad38-4b28-9659-099d73cad099) スイッチに相当します。|  
|`GenerateDocumentation`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、ドキュメント情報が生成され、タスクが作成する実行可能ファイルまたはライブラリの名前が与えられた XML ファイルに格納されます。 詳細については、「 [/doc](https://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65)」を参照してください。|  
|`Imports`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定した項目コレクションから名前空間をインポートします。 このパラメーターは、vbc.exe コンパイラの [/imports](https://msdn.microsoft.com/library/9a93fb53-c080-497b-bf9b-441022dbbc39) スイッチに相当します。|  
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キー コンテナーの名前を指定します。 このパラメーターは、vbc.exe コンパイラの [/keycontainer](https://msdn.microsoft.com/library/6a9bc861-1752-4db1-9f64-b5252f0482cc) スイッチに相当します。|  
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キーを格納するファイル名を指定します。 詳細については、「 [/keyfile](https://msdn.microsoft.com/library/ffa82a4b-517a-4c6c-9889-5bae7b534bb8)」を参照してください。|  
|`LangVersion`|省略可能な [String](<!-- TODO: review code entity reference <xref:assetId:///String?qualifyHint=False&amp;autoUpgrade=True>  -->) のパラメーターです。<br /><br /> 言語バージョンとして "9" か "10" を指定します。|  
|`LinkResources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 出力ファイル内で .NET Framework リソースへのリンクを作成します。リソース ファイルは出力ファイル内に置かれません。 このパラメーターは、vbc.exe コンパイラの [/linkresource](https://msdn.microsoft.com/library/cf4dcad8-17b7-404c-9184-29358aa05b15) スイッチに相当します。|  
|`MainEntryPoint`|省略可能な `String` 型のパラメーターです。<br /><br /> `Sub Main` プロシージャを格納するクラスまたはモジュールを指定します。 このパラメーターは、vbc.exe コンパイラの [/main](https://msdn.microsoft.com/library/83fc339d-6652-415d-b205-b5133319b5b0) スイッチに相当します。|  
|`ModuleAssemblyName`|省略可能な `String` 型のパラメーターです。<br /><br /> このモジュールが一部となるアセンブリを指定します。|  
|`NoConfig`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> コンパイラで vbc.rsp ファイルを使用しないように指定します。 このパラメーターは vbc.exe コンパイラの [/noconfig](https://msdn.microsoft.com/library/a7405067-bd21-4171-adf4-a126fa3ad6c3) パラメーターに対応します。|  
|`NoLogo`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラの著作権情報が表示されません。 このパラメーターは、vbc.exe コンパイラの [/nologo](https://msdn.microsoft.com/library/25ef54b6-d676-4639-a2d2-a747a158bc07) スイッチに相当します。|  
|`NoStandardLib`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> コンパイラが標準ライブラリを参照しないようにします。 このパラメーターは、vbc.exe コンパイラの [/nostdlib](https://msdn.microsoft.com/library/140381b8-dc96-4ad5-ae11-792c9ed0be4d) スイッチに相当します。|  
|`NoVBRuntimeReference`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> 内部使用のみ。 true の場合、Microsoft.VisualBasic.dll の自動参照が禁止されます。|  
|`NoWarnings`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、すべての警告が非表示になります。 詳細については、「 [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83)」を参照してください。|  
|`Optimize`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラ最適化が有効になります。 このパラメーターは、vbc.exe コンパイラの [/optimize](https://msdn.microsoft.com/library/fcba4a97-3622-4b87-a891-0f77deab4998) スイッチに相当します。|  
|`OptionCompare`|省略可能な `String` 型のパラメーターです。<br /><br /> 文字列比較の方法を指定します。 このパラメーターには、次の値を指定できます。<br /><br /> -   `binary`<br />-   `text`<br /><br /> 値 `binary` を指定すると、バイナリ文字列比較が使用されます。 値 `text` を指定すると、テキスト文字列比較が使用されます。 このパラメーターの既定値は、`binary` です。 このパラメーターは、vbc.exe コンパイラの [/optioncompare](https://msdn.microsoft.com/library/7237b766-b44d-4cc5-9a3c-885348a7d9e4) スイッチに相当します。|  
|`OptionExplicit`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、変数の明示的宣言が必要になります。 このパラメーターは、vbc.exe コンパイラの [/optionexplicit](https://msdn.microsoft.com/library/5d296ab3-bafe-4c4d-9887-78f162ed86c7) スイッチに相当します。|  
|`OptionInfer`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、変数の型推論を許可します。|  
|`OptionStrict`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、厳密な型のセマンティックスが強制され、暗黙的な型変換が制限されます。 このパラメーターは、vbc.exe コンパイラの [/optionstrict](https://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da) スイッチに相当します。|  
|`OptionStrictType`|省略可能な `String` 型のパラメーターです。<br /><br /> 警告を生成する厳密な型のセマンティックスを指定します。 現在のところ、"custom" のみに対応しています。 このパラメーターは、vbc.exe コンパイラの [/optionstrict](https://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da) スイッチに相当します。|  
|`OutputAssembly`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 出力ファイルの名前を指定します。 このパラメーターは、vbc.exe コンパイラの [/out](https://msdn.microsoft.com/library/9f148c15-0909-4cb8-a2db-777f8a8b45ae) スイッチに相当します。|  
|`Platform`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのターゲットとするプロセッサ プラットフォームを指定します。 このパラメーターの値には、`x86`、`x64` 、`Itanium`、または `anycpu` を指定できます。 既定値は `anycpu` です。 このパラメーターは、vbc.exe コンパイラの [/platform](https://msdn.microsoft.com/library/f9bc61e6-e854-4ae1-87b9-d6244de23fd1) スイッチに相当します。|  
|`References`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定したアイテムから現在のプロジェクトにパブリック型の情報をインポートするようにタスクに指示します。 このパラメーターは、vbc.exe コンパイラの [/reference](https://msdn.microsoft.com/library/66bdfced-bbf6-43d1-a554-bc0990315737) スイッチに相当します。|  
|`RemoveIntegerChecks`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、整数オーバーフローのエラー チェックを無効にします。 既定値は `false` です。 このパラメーターは、vbc.exe コンパイラの [/removeintchecks](https://msdn.microsoft.com/library/c1835bd5-1e38-4fba-bd2f-6984774765d4) スイッチに相当します。|  
|`Resources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> .NET Framework のリソースを出力ファイルに埋め込みます。 このパラメーターは、vbc.exe コンパイラの [/resource](https://msdn.microsoft.com/library/eee2f227-91f2-4f2b-a9d6-1c51c5320858) スイッチに相当します。|  
|`ResponseFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> このタスクのコマンドを含む応答ファイルを指定します。 このパラメーターは、vbc.exe コンパイラの [@ (Specify Response File)](https://msdn.microsoft.com/library/a6847eaa-e5f9-4303-9421-45b55484b9ca) オプションに相当します。|  
|`RootNamespace`|省略可能な `String` 型のパラメーターです。<br /><br /> すべての型宣言に対してルート名前空間を指定します。 このパラメーターは、vbc.exe コンパイラの [/rootnamespace](https://msdn.microsoft.com/library/e9245edf-6bef-420d-a7c7-324117752783) スイッチに相当します。|  
|`SdkPath`|省略可能な `String` 型のパラメーターです。<br /><br /> mscorlib.dll および microsoft.visualbasic.dll の位置を指定します。 このパラメーターは、vbc.exe コンパイラの [/sdkpath](https://msdn.microsoft.com/library/fec8a3f1-b791-4a37-8af7-344859f8212d) スイッチに相当します。|  
|`Sources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 1 つまたは複数の [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ソース ファイルを指定します。|  
|`TargetCompactFramework`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、[!INCLUDE[Compact](../includes/compact-md.md)] が対象となります。 このスイッチは vbc.exe コンパイラの [/netcf](https://msdn.microsoft.com/library/db7cfa59-c315-401c-a59b-0daf355343d6) スイッチに相当します。|  
|`TargetType`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのファイル形式を指定します。 このパラメーターには値として、コード ライブラリを作成する `library`、コンソール アプリケーションを作成する `exe`、モジュールを作成する `module`、Windows プログラムを作成する `winexe` を指定できます。 既定値は `library` です。 このパラメーターは、vbc.exe コンパイラの [/target](https://msdn.microsoft.com/library/e0954147-548b-461f-9c4b-a8f88845616c) スイッチに相当します。|  
|`Timeout`|省略可能な `Int32` 型のパラメーターです。<br /><br /> タスク実行を終了するまでの時間をミリ秒単位で指定します。 既定値は `Int.MaxValue` であり、タイムアウト期限がないことを示します。|  
|`ToolPath`|省略可能な `String` 型のパラメーターです。<br /><br /> タスクが基になる実行可能ファイル (vbc.exe) を読み込む場所を指定します。 このパラメーターを指定しないと、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行しているフレームワークのバージョンに対応する SDK インストール パスがタスクに使用されます。|  
|`TreatWarningsAsErrors`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、すべての警告がエラーとして処理されます。 詳細については、「 [/warnaserror (Visual Basic)](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)」を参照してください。|  
|`UseHostCompilerIfAvailable`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> 利用できる場合、インプロセス コンパイラ オブジェクトを使用するようにタスクに指示します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によってのみ使用されます。|  
|`Utf8Output`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> UTF-8 エンコードを使用してコンパイラ出力をログに記録します。 このパラメーターは、vbc.exe コンパイラの [/utf8output](https://msdn.microsoft.com/library/8ab36b1e-027a-49ac-85b4-f48997d9e4d6) スイッチに相当します。|  
|`Verbosity`|省略可能な `String` 型のパラメーターです。<br /><br /> コンパイラ出力の詳細度を指定します。 詳細度は `Quiet`、`Normal` (既定)、または `Verbose` です。|  
|`WarningsAsErrors`|省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱う警告の一覧を指定します。 詳細については、「 [/warnaserror (Visual Basic)](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)」を参照してください。<br /><br /> このパラメーターは `TreatWarningsAsErrors` パラメーターをオーバーライドします。|  
|`WarningsNotAsErrors`|省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱わない警告の一覧を指定します。 詳細については、「 [/warnaserror (Visual Basic)](https://msdn.microsoft.com/library/49819f1d-a1bd-4201-affe-5afe6d9712e1)」を参照してください。<br /><br /> このパラメーターは、`TreatWarningsAsErrors` パラメーターが `true` に設定されている場合にのみ役に立ちます。|  
|`Win32Icon`|省略可能な `String` 型のパラメーターです。<br /><br /> エクスプローラーで出力ファイルを適切に表示する .ico ファイルをアセンブリに挿入します。 このパラメーターは、vbc.exe コンパイラの [/win32icon](https://msdn.microsoft.com/library/aecaab01-9353-46c5-941c-6edabd4eff92) スイッチに相当します。|  
|`Win32Resources`|省略可能な `String` 型のパラメーターです。<br /><br /> Win32 リソース (.res) ファイルを出力ファイルに挿入します。 このパラメーターは、vbc.exe コンパイラの [/win32resource](https://msdn.microsoft.com/library/e226946d-19ce-4cc9-91f5-aed24f77aa2b) スイッチに相当します。|  
  
## <a name="remarks"></a>Remarks  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.ToolTask> クラスから継承されます。 これらの追加パラメーターとその説明の一覧については、「 [Tooltaskextension Base Class](../msbuild/tooltaskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] プロジェクトがコンパイルされます。  
  
```  
<VBC  
   Sources="@(sources)"  
   Resources="strings.resources"  
   Optimize="true"  
   OutputAssembly="out.exe"/>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Basic のコマンド ライン コンパイラ](https://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c)   
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
