---
title: Csc タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Csc
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Csc task [MSBuild]
- MSBuild, Csc task
ms.assetid: d8c19b36-f5ca-484b-afa6-8ff3b90e103a
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e0dd27fe64982e77872e37ec01dbdb71a0a141ae
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65694101"
---
# <a name="csc-task"></a>Csc タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CSC.exe をラップし、実行可能ファイル (.exe ファイル)、ダイナミック リンク ライブラリ (.dll ファイル)、またはコード モジュール (.netmodule ファイル) を生成します。 CSC.exe の詳細については、「[C# コンパイラ オプション](https://msdn.microsoft.com/library/d3403556-1816-4546-a782-e8223a772e44)」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 `Csc` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AdditionalLibPaths`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 参照を検索する追加のディレクトリを指定します。 詳しくは、「[/lib (C# コンパイラ オプション)](https://msdn.microsoft.com/library/b0efcc88-e8aa-4df4-a00b-8bdef70b7673)」をご覧ください。|  
|`AddModules`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリを構成する 1 つ以上のモジュールを指定します。 詳しくは、「[/addmodule (C# コンパイラ オプション)](https://msdn.microsoft.com/library/ed604546-0dc2-4bd4-9a3e-610a8d973e58)」をご覧ください。|  
|`AllowUnsafeBlocks`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、[unsafe](https://msdn.microsoft.com/library/7e818009-1c6e-4b9e-b769-3728a01586a0) キーワードを使用するコードをコンパイルします。 詳しくは、「[/unsafe (C# コンパイラ オプション)](https://msdn.microsoft.com/library/fdb77ed9-da03-45bd-bb7f-250704da1bcc)」をご覧ください。|  
|`ApplicationConfiguration`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリ バインド設定を含むアプリケーション構成ファイルを指定します。|  
|`BaseAddress`|省略可能な `String` 型のパラメーターです。<br /><br /> DLL を読み込む位置に推奨されるベース アドレスを指定します。 DLL の既定のベース アドレスは、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 共通言語ランタイムにより設定されます。 詳しくは、「[/baseaddress (C# コンパイラ オプション)](https://msdn.microsoft.com/library/ce13c965-dfe4-4433-94f5-63b476e3a608)」をご覧ください。|  
|`CheckForOverflowUnderflow`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> データ型の境界をオーバーフローする整数演算で、実行時に例外を発生させるかどうかを指定します。 詳しくは、「[/checked (C# コンパイラ オプション)](https://msdn.microsoft.com/library/fb7475d3-e6a6-4e6d-b86c-69e7a74c854b)」をご覧ください。|  
|`CodePage`|省略可能な `Int32` 型のパラメーターです。<br /><br /> コンパイルですべてのソース コード ファイルに使用するコード ページを指定します。 詳しくは、「[/codepage (C# コンパイラ オプション)](https://msdn.microsoft.com/library/75942989-b69a-4308-90a0-840c73d2c478)」をご覧ください。|  
|`DebugType`|省略可能な `String` 型のパラメーターです。<br /><br /> デバッグの種類を指定します。 `DebugType` には、`full` または `pdbonly` を指定できます。 既定値は `full` です。デバッガーを実行中のプログラムに添付できます。 `pdbonly` を指定すると、プログラムがデバッガーで開始されたとき、ソース コードのデバッグが有効になりますが、実行中のプログラムがデバッガーにアタッチされているときにのみアセンブラーが表示されます。<br /><br /> このパラメーターは `EmitDebugInformation` パラメーターをオーバーライドします。<br /><br /> 詳しくは、「[/debug (C# コンパイラ オプション)](https://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969)」をご覧ください。|  
|`DefineConstants`|省略可能な `String` 型のパラメーターです。<br /><br /> プリプロセッサ シンボルを定義します。 詳しくは、「[/define (C# コンパイラ オプション)](https://msdn.microsoft.com/library/f17d7b4d-82d0-4133-8563-68cced1cac6e)」をご覧ください。|  
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、完全署名されたアセンブリを必要とすることが指定されます。 `false` の場合、アセンブリに公開キーを含めることだけを要求するように指定されます。<br /><br /> `KeyFile` または `KeyContainer` パラメーターと併用しない限り、このパラメーターには何の効果もありません。<br /><br /> 詳しくは、「[/delaysign (C# コンパイラ オプション)](https://msdn.microsoft.com/library/bcb058eb-2933-4e7f-b356-5c941db4de75)」をご覧ください。|  
|`DisabledWarnings`|省略可能な `String` 型のパラメーターです。<br /><br /> 無効にする警告の一覧を指定します。 詳しくは、「[/nowarn (C# コンパイラ オプション)](https://msdn.microsoft.com/library/6dcbc5e8-ae67-4566-9df3-f63cfdd9c4e4)」をご覧ください。|  
|`DocumentationFile`|省略可能な `String` 型のパラメーターです。<br /><br /> ドキュメント コメントを XML ファイルに出力します。 詳しくは、「[/doc (C# コンパイラ オプション)](https://msdn.microsoft.com/library/849eea59-c936-4311-bad8-d07404480f2a)」をご覧ください。|  
|`EmitDebugInformation`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、このタスクはデバッグ情報を生成し、プログラム データベース (.pdb) ファイルにその情報を追加します。 `false` の場合、このタスクはデバッグ情報を生成しません。 既定値は `false` です。 詳しくは、「[/debug (C# コンパイラ オプション)](https://msdn.microsoft.com/library/e2b48c07-01bc-45cc-a52c-92e9085eb969)」をご覧ください。|  
|`ErrorReport`|省略可能な `String` 型のパラメーターです。<br /><br /> C# 内部エラーを Microsoft に報告する便利な方法を提供します。 このパラメーターの値には、`prompt`、`send`、または `none` を指定できます。 このパラメーターが `prompt` に設定されている場合、内部コンパイラにエラーが発生すると、プロンプトが表示されます。 このプロンプトで、Microsoft にバグ レポートを電子的に送信できます。 このパラメーターが `send` に設定されている場合、バグ レポートは自動的に送信されます。 このパラメーターが `none` に設定されている場合、コンパイラのテキスト出力でのみエラーが報告されます。 既定値は `none` です。 詳しくは、「[/errorreport (C# コンパイラ オプション)](https://msdn.microsoft.com/library/bd0e7493-b79d-4369-9c3f-ba26ebdfbedf)」をご覧ください。|  
|`FileAlignment`|省略可能な `Int32` 型のパラメーターです。<br /><br /> 出力ファイル内のセクションのサイズを指定します。 詳しくは、「[/filealign (C# コンパイラ オプション)](https://msdn.microsoft.com/library/15cf1c98-3798-4ced-9f08-60619308a073)」をご覧ください。|  
|`GenerateFullPaths`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラ出力に含まれるファイルの絶対パスが指定されます。 `false` の場合、ファイルの名前が指定されます。 既定値は `false` です。 詳しくは、「[/fullpaths (C# コンパイラ オプション)](https://msdn.microsoft.com/library/d2a5f857-cbb2-430b-879c-d648aaf0b8c4)」をご覧ください。|  
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キー コンテナーの名前を指定します。 詳しくは、「[/keycontainer (C# コンパイラ オプション)](https://msdn.microsoft.com/library/b3982b6d-2382-4f7e-bebd-ce98eaa30763)」をご覧ください。|  
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 暗号化キーを格納するファイル名を指定します。 詳しくは、「[/keyfile (C# コンパイラ オプション)](https://msdn.microsoft.com/library/0815f9de-ace4-4e98-b4c6-13c55dea40c2)」をご覧ください。|  
|`LangVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> 使用する言語のバージョンを指定します。 詳しくは、「[/langversion (C# コンパイラ オプション)](https://msdn.microsoft.com/library/3fb00b05-a0ff-4782-b313-13a4c0f62d94)」をご覧ください。|  
|`LinkResources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 出力ファイル内で [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] リソースへのリンクを作成します。リソース ファイルは出力ファイル内に置かれません。<br /><br /> このパラメーターに渡される項目には、「`LogicalName`」や「`Access`」という名前のメタデータ エントリを任意で指定できます。 `LogicalName` は `/linkresource` スイッチの `identifier` パラメーターに対応し、`Access` は `accessibility-modifier` パラメーターに対応します。 詳しくは、「[/linkresource (C# コンパイラ オプション)](https://msdn.microsoft.com/library/440c26c2-77c1-4811-a0a3-57cce3f5fc96)」をご覧ください。|  
|`MainEntryPoint`|省略可能な `String` 型のパラメーターです。<br /><br /> `Main` メソッドの場所を指定します。 詳細については、「[/main (C# コンパイラ オプション)](https://msdn.microsoft.com/library/975cf4d5-36ac-4530-826c-4aad0c7f2049)」を参照してください。|  
|`ModuleAssemblyName`|省略可能な `String` 型のパラメーターです。<br /><br /> このモジュールが一部となるアセンブリの名前を指定します。|  
|`NoConfig`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、csc.rsp ファイルを使用してコンパイルしないようにコンパイラに指示します。 詳しくは、「[/noconfig (C# コンパイラ オプション)](https://msdn.microsoft.com/library/cd26967e-e494-4c8c-b5c9-af13b2f78b2e)」をご覧ください。|  
|`NoLogo`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、コンパイラの著作権情報が表示されません。 詳しくは、「[/nologo (C# コンパイラ オプション)](https://msdn.microsoft.com/library/426afb36-a8fb-469d-9c45-a35d9512557c)」をご覧ください。|  
|`NoStandardLib`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、System 名前空間の全体を定義する mscorlib.dll がインポートされません。 独自の System 名前空間およびオブジェクトを定義または作成する場合は、このパラメーターを使用します。 詳しくは、「[/nostdlib (C# コンパイラ オプション)](https://msdn.microsoft.com/library/ec197989-fa49-4725-a455-e06b551eb65f)」をご覧ください。|  
|`NoWin32Manifest`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、既定の Win32 マニフェストを含めないでください。|  
|`Optimize`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、最適化が有効になります。 `false` の場合、最適化が無効になります。 詳しくは、「[/optimize (C# コンパイラ オプション)](https://msdn.microsoft.com/library/6dd5b6f2-cd1d-4593-a9f4-1c2ed9404ca0)」をご覧ください。|  
|`OutputAssembly`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 出力ファイルの名前を指定します。 詳しくは、「[/out (C# コンパイラ オプション)](https://msdn.microsoft.com/library/70d91d01-7bd2-4aea-ba8b-4e9807e9caa5)」をご覧ください。|  
|`PdbFile`|省略可能な `String` 型のパラメーターです。<br /><br /> デバッグ情報ファイルの名前を指定します。 既定の名前は、出力ファイルの名前に .pdb 拡張子が付いたものになります。|  
|`Platform`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのターゲットとするプロセッサ プラットフォームを指定します。 このパラメーターの値には、`x86`、`x64`、または `anycpu` を指定できます。 既定値は `anycpu` です。 詳しくは、「[/platform (C# コンパイラ オプション)](https://msdn.microsoft.com/library/c290ff5e-47f4-4a85-9bb3-9c2525b0be04)」をご覧ください。|  
|`References`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定したアイテムから現在のプロジェクトにパブリック型の情報をインポートするようにタスクに指示します。 詳しくは、「[/reference (C# コンパイラ オプション)](https://msdn.microsoft.com/library/8d13e5b0-abf6-4c46-bf71-2daf2cd0a6c4)」をご覧ください。<br /><br /> メタデータ `Aliases` を元の "参照" アイテムに追加することで、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] ファイルに [!INCLUDE[csprcs](../includes/csprcs-md.md)] 参照エイリアスを指定できます。 たとえば、次の "LS1" コマンド ラインにエイリアス を設定する場合:<br /><br /> `csc /r:LS1=MyCodeLibrary.dll /r:LS2=MyCodeLibrary2.dll *.cs`<br /><br /> 次を使用します。<br /><br /> `<Reference Include="MyCodeLibrary"> <Aliases>LS1</Aliases> </Reference>`|  
|`Resources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] リソースを出力ファイルに組み込みます。<br /><br /> このパラメーターに渡される項目には、「`LogicalName`」や「`Access`」という名前のメタデータ エントリを任意で指定できます。 `LogicalName` は `/resource` スイッチの `identifier` パラメーターに対応し、`Access` は `accessibility-modifier` パラメーターに対応します。 詳しくは、「[/resource (C# コンパイラ オプション)](https://msdn.microsoft.com/library/5212666e-98ab-47e4-a497-b5545ab15c7f)」をご覧ください。|  
|`ResponseFiles`|省略可能な `String` 型のパラメーターです。<br /><br /> このタスクのコマンドを含む応答ファイルを指定します。 詳しくは、「[@ (応答ファイルの指定)](https://msdn.microsoft.com/library/dda4fa9f-a02c-400f-8b6a-d58834e13d7f)」をご覧ください。|  
|`Sources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 1 つまたは複数の [!INCLUDE[csprcs](../includes/csprcs-md.md)] ソース ファイルを指定します。|  
|`TargetType`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのファイル形式を指定します。 このパラメーターには値として、コード ライブラリを作成する `library`、コンソール アプリケーションを作成する `exe`、モジュールを作成する `module`、Windows プログラムを作成する `winexe` を指定できます。 既定値は `library` です。 詳しくは、「[/target (C# コンパイラ オプション)](https://msdn.microsoft.com/library/a18bbd8e-bbf7-49e7-992c-717d0eb1f76f)」をご覧ください。|  
|`TreatWarningsAsErrors`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、すべての警告をエラーとして扱います。 詳しくは、「[/warnaserror (C# コンパイラ オプション)](https://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c)」をご覧ください。|  
|`UseHostCompilerIfAvailable`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> 利用できる場合、インプロセス コンパイラ オブジェクトを使用するようにタスクに指示します。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によってのみ使用されます。|  
|`Utf8Output`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> UTF-8 エンコードを使用してコンパイラ出力をログに記録します。 詳しくは、「[/utf8output (C# コンパイラ オプション)](https://msdn.microsoft.com/library/27ff7381-c281-45d7-b2eb-1ad644b1354e)」をご覧ください。|  
|`WarningLevel`|省略可能な `Int32` 型のパラメーターです。<br /><br /> コンパイラが表示する警告レベルを指定します。 詳しくは、「[/warn (C# コンパイラ オプション)](https://msdn.microsoft.com/library/5f80ff59-4991-4382-9f9a-77da18446e71)」をご覧ください。|  
|`WarningsAsErrors`|省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱う警告の一覧を指定します。 詳しくは、「[/warnaserror (C# コンパイラ オプション)](https://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c)」をご覧ください。<br /><br /> このパラメーターは `TreatWarningsAsErrors` パラメーターをオーバーライドします。|  
|`WarningsNotAsErrors`|省略可能な `String` 型のパラメーターです。<br /><br /> エラーとして扱わない警告の一覧を指定します。 詳しくは、「[/warnaserror (C# コンパイラ オプション)](https://msdn.microsoft.com/library/04680ec3-08d6-4e2e-a274-38310e10e33c)」をご覧ください。<br /><br /> このパラメーターは、`TreatWarningsAsErrors` パラメーターが `true` に設定されている場合にのみ役に立ちます。|  
|`Win32Icon`|省略可能な `String` 型のパラメーターです。<br /><br /> エクスプローラーで出力ファイルを適切に表示する .ico ファイルをアセンブリに挿入します。 詳細については、「[/win32icon (C# コンパイラ オプション)](https://msdn.microsoft.com/library/756d9b6d-ab07-41b7-ba58-5bd88f711138)」を参照してください。|  
|`Win32Manifest`|省略可能な `String` 型のパラメーターです。<br /><br /> 追加する Win32 マニフェストを指定します。|  
|`Win32Resource`|省略可能な `String` 型のパラメーターです。<br /><br /> Win32 リソース (.res) ファイルを出力ファイルに挿入します。 詳しくは、「[/win32res (C# コンパイラ オプション)](https://msdn.microsoft.com/library/3c33f750-6948-4c7e-a27e-bef98f77255b)」をご覧ください。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは `Microsoft.Build.Tasks.ManagedCompiler` クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスから継承されますが、それにはさらに <xref:Microsoft.Build.Utilities.ToolTask> クラスという継承元が存在します。 これらの追加のパラメーターの一覧とその説明については、「[ToolTaskExtension 基本クラス](../msbuild/tooltaskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Csc` タスクを使用し、`Compile` アイテム コレクションのソース ファイルから実行可能ファイルをコンパイルしています。  
  
```  
<CSC  
    Sources="@(Compile)"  
    OutputAssembly="$(AppName).exe"  
    EmitDebugInformation="true" />  
```  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)
