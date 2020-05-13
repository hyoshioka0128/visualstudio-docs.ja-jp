---
title: AL (アセンブリ リンカー) タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AL
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- AL task [MSBuild]
- MSBuild, AL task
ms.assetid: 2ddefbf2-5662-4d55-99a6-ac383bf44560
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 85fb11429822d49d1a86697d9480f3a8ab0759de
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2019
ms.locfileid: "65684690"
---
# <a name="al-assembly-linker-task"></a>AL (アセンブリ リンカー) タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

AL タスクは、[!INCLUDE[winsdklong](../includes/winsdklong-md.md)] と共に配布されるツールである AL.exe をラップします。 アセンブリ リンカー ツールは、モジュールまたはリソース ファイルである 1 つ以上のファイルから、マニフェストを含むアセンブリを作成するために使われます。 これらの機能はコンパイラおよび開発環境で既に提供されていることがあるので、ほとんどの場合、このタスクを直接使う必要はありません。 アセンブリ リンカーは、混合言語の開発から生成されるものなど、複数のコンポーネント ファイルから 1 つのアセンブリを作成する必要がある開発者に適しています。 このタスクでは、複数のモジュールが 1 つのアセンブリ ファイルに結合されることはありません。生成されたアセンブリを正しく読み込むためには、やはり個々のモジュールを配布して使用できるようにする必要があります。 AL.exe について詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」をご覧ください。  
  
## <a name="parameters"></a>パラメーター  
 `AL` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AlgorithmID`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリ マニフェストを含むファイルを除き、マルチファイル アセンブリ内の全ファイルをハッシュするためのアルゴリズムを指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/algid` オプションのドキュメントをご覧ください。|  
|`BaseAddress`|省略可能な `String` 型のパラメーターです。<br /><br /> 実行時にユーザーのコンピューターに DLL を読み込む先のアドレスを指定します。 オペレーティング システムにプロセス空間内で DLL を再配置させる代わりに DLL のベース アドレスを指定しておくと、アプリケーションの読み込み速度が速くなります。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の /base[address] オプションに対応します。|  
|`CompanyName`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Company` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/comp[any]` オプションのドキュメントをご覧ください。|  
|`Configuration`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Configuration` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/config[uration]` オプションのドキュメントをご覧ください。|  
|`Copyright`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Copyright` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/copy[right]` オプションのドキュメントをご覧ください。|  
|`Culture`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリに関連付けるカルチャ文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/c[ulture]` オプションのドキュメントをご覧ください。|  
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> アセンブリに公開キーのみを置く場合は `true`、アセンブリを完全に署名する場合は `false` です。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/delay[sign]` オプションのドキュメントをご覧ください。|  
|`Description`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Description` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/descr[iption]` オプションのドキュメントをご覧ください。|  
|`EmbedResources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> アセンブリ マニフェストを含むイメージに指定したリソースを埋め込みます。 このタスクは、リソース ファイルの内容をイメージにコピーします。 このパラメーターに渡すアイテムには、`LogicalName` および `Access` という名前の省略可能なメタデータを添付することができます。 `LogicalName` メタデータは、リソースの内部識別子を指定するために使われます。  リソースを他のアセンブリから見えないようにするには、`Access` メタデータを `private` に設定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/embed[resource]` オプションのドキュメントをご覧ください。|  
|`EvidenceFile`|省略可能な `String` 型のパラメーターです。<br /><br /> `Security.Evidence` というリソース名を持つアセンブリに、指定したファイルを埋め込みます。<br /><br /> 通常のリソースに対して `Security.Evidence` を使うことはできません。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/e[vidence]` オプションに対応します。|  
|`ExitCode`|省略可能な `Int32` 型の読み取り専用出力パラメーターです。<br /><br /> 実行されたコマンドによって提供される終了コードを指定します。|  
|`FileVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `File Version` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/fileversion` オプションのドキュメントをご覧ください。|  
|`Flags`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Flags` フィールドに値を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/flags` オプションのドキュメントをご覧ください。|  
|`GenerateFullPaths`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> エラー メッセージで報告されるすべてのファイルについて絶対パスを使うよう、タスクに指定します。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/fullpaths` オプションに対応します。|  
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> キー ペアを保持するコンテナーを指定します。 これにより、公開キーがアセンブリ マニフェストに挿入され、アセンブリに署名 (厳密な名前が指定) されます。 次に、タスクは最終的なアセンブリに秘密キーで署名します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/keyn[ame]` オプションのドキュメントをご覧ください。|  
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリに署名するためのキー ペアまたは公開キーだけを含むファイルを指定します。 コンパイラは、アセンブリ マニフェストに公開キーを挿入し、最終的なアセンブリに秘密キーで署名します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/keyf[ile]` オプションのドキュメントをご覧ください。|  
|`LinkResources`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 指定したリソース ファイルをアセンブリにリンクします。 リソースはアセンブリの一部になりますが、ファイルはコピーされません。 このパラメーターに渡すアイテムには、`LogicalName`、`Target`、および `Access` という名前の省略可能なメタデータを添付することができます。 `LogicalName` メタデータは、リソースの内部識別子を指定するために使われます。 `Target` メタデータでは、タスクがファイルをコピーする先のパスとファイル名を指定できます。その後は、この新しいファイルがアセンブリにコンパイルされます。 リソースを他のアセンブリから見えないようにするには、`Access` メタデータを `private` に設定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/link[resource]` オプションのドキュメントをご覧ください。|  
|`MainEntryPoint`|省略可能な `String` 型のパラメーターです。<br /><br /> モジュールを実行可能ファイルに変換するときに、エントリ ポイントとして使うメソッドの完全修飾名 (*class.method*) を指定します。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/main` オプションに対応します。|  
|`OutputAssembly`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> このタスクで生成されるファイルの名前を指定します。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/out` オプションに対応します。|  
|`Platform`|省略可能な `String` 型のパラメーターです。<br /><br /> このコードを実行できるプラットフォームを制限します。`x86`、`Itanium`、`x64`、または `anycpu` のいずれかでなければなりません。 既定値は、`anycpu` です。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/platform` オプションに対応します。|  
|`ProductName`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Product` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/prod[uct]` オプションのドキュメントをご覧ください。|  
|`ProductVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `ProductVersion` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/productv[ersion]` オプションのドキュメントをご覧ください。|  
|`ResponseFiles`|省略可能な `String[]` 型のパラメーターです。<br /><br /> アセンブリ リンカーに渡す追加のオプションが含まれる応答ファイルを指定します。|  
|`SdkToolsPath`|省略可能な `String` 型のパラメーターです。<br /><br /> resgen.exe などの SDK ツールのパスを指定します。|  
|`SourceModules`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> アセンブリにコンパイルする 1 つ以上のモジュール。 モジュールは生成されるアセンブリのマニフェストに列記され、アセンブリを読み込むにはモジュールを配布して使用できるようにする必要があります。 このパラメーターに渡すアイテムには、`Target` という名前の追加メタデータを指定できます。このメタデータでは、タスクがファイルをコピーする先のパスとファイル名を指定します。その後は、この新しいファイルがアセンブリにコンパイルされます。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」のドキュメントをご覧ください。 このパラメーターは、特定のスイッチを指定しないで Al.exe に渡されるモジュールのリストに対応します。|  
|`TargetType`|省略可能な `String` 型のパラメーターです。<br /><br /> 出力ファイルのファイル形式として、`library` (コード ライブラリ)、`exe` (コンソール アプリケーション)、または `win` (Windows ベースのアプリケーション) を指定します。 既定値は、`library` です。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/t[arget]` オプションに対応します。|  
|`TemplateFile`|省略可能な `String` 型のパラメーターです。<br /><br /> カルチャ フィールドを除く、すべてのアセンブリ メタデータの継承元であるアセンブリを指定します。 指定するアセンブリには厳密な名前が必要です。<br /><br /> `TemplateFile` パラメーターを指定して作成したアセンブリは、サテライト アセンブリになります。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/template` オプションに対応します。|  
|`Timeout`|省略可能な `Int32` 型のパラメーターです。<br /><br /> タスク実行を終了するまでの時間をミリ秒単位で指定します。 既定値は `Int.MaxValue` であり、タイムアウト期限がないことを示します。|  
|`Title`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Title` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/title` オプションのドキュメントをご覧ください。|  
|`ToolPath`|省略可能な `String` 型のパラメーターです。<br /><br /> タスクが基になる実行可能ファイル (Al.exe) を読み込む場所を指定します。 このパラメーターを指定しないと、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] を実行しているフレームワークのバージョンに対応する SDK インストール パスがタスクに使用されます。|  
|`Trademark`|省略可能な `String` 型のパラメーターです。<br /><br /> アセンブリの `Trademark` フィールドに文字列を指定します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/trade[mark]` オプションのドキュメントをご覧ください。|  
|`Version`|省略可能な `String` 型のパラメーターです。<br /><br /> このアセンブリのバージョン情報を指定します。 文字列の形式は、*major.minor.build.revision* です。 既定値は 0 です。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/v[ersion]` オプションのドキュメントをご覧ください。|  
|`Win32Icon`|省略可能な `String` 型のパラメーターです。<br /><br /> .ico ファイルをアセンブリに挿入します。 この .ico ファイルは、エクスプローラーにおける出力ファイルの視覚的な表現を提供します。 このパラメーターは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」の `/win32icon` オプションに対応します。|  
|`Win32Resource`|省略可能な `String` 型のパラメーターです。<br /><br /> Win32 リソース (.res ファイル) を出力ファイルに挿入します。 詳しくは、「[Al.exe (アセンブリ リンカー)](https://msdn.microsoft.com/library/b5382965-0053-47cf-b92f-862860275a01)」で `/win32res` オプションのドキュメントをご覧ください。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.ToolTask> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[ToolTaskExtension 基本クラス](../msbuild/tooltaskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、指定したオプションでアセンブリを作成します。  
  
```  
<AL  
    EmbedResources="@(EmbeddedResource)"  
    Culture="%(EmbeddedResource.Culture)"  
    TemplateFile="@(IntermediateAssembly)"  
    KeyContainer="$(KeyContainerName)"  
    KeyFile="$(KeyOriginatorFile)"  
    DelaySign="$(DelaySign)"  
  
    OutputAssembly=  
       "%(EmbeddedResource.Culture)\$(TargetName).resources.dll">  
  
    <Output TaskParameter="OutputAssembly"  
        ItemName="SatelliteAssemblies"/>  
</AL>  
```  
  
## <a name="see-also"></a>関連項目
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [タスク](../msbuild/msbuild-tasks.md)
