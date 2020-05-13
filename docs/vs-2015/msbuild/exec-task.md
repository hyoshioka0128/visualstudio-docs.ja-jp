---
title: Exec タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Exec
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Exec task [MSBuild]
- MSBuild, Exec task
ms.assetid: c9b7525a-b1c9-40fc-8bce-77a5b8f960d8
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2a69fc64c3371a2970c03ec0129d4c733f5ae9cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201751"
---
# <a name="exec-task"></a>Exec タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定された引数を使って、指定されたプログラムまたはコマンドを実行します。  
  
## <a name="parameters"></a>パラメーター  
 `Exec` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Command`|必須の `String` 型のパラメーターです。<br /><br /> 実行するコマンドです。 attrib などのシステム コマンド、または program.exe、runprogram.bat、setup.msi などの実行可能ファイルを指定できます。<br /><br /> このパラメーターで複数のコマンド行を指定できます。 または、複数のコマンドをバッチ ファイルに入れ、このパラメーターを使ってそれを実行することもできます。|  
|`CustomErrorRegularExpression`|省略可能な `String` 型のパラメーターです。<br /><br /> ツールの出力でエラー行を示すために使う正規表現を指定します。 これは、普通とは異なる書式設定の出力を生成するツールに便利です。|  
|`CustomWarningRegularExpression`|省略可能な `String` 型のパラメーターです。<br /><br /> ツールの出力で警告行を示すために使う正規表現を指定します。 これは、普通とは異なる書式設定の出力を生成するツールに便利です。|  
|`ExitCode`|省略可能な `Int32` 型の読み取り専用出力パラメーターです。<br /><br /> 実行したコマンドの終了コードを示します。|  
|`IgnoreExitCode`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、タスクは実行したコマンドで提供されている終了コードを無視します。 それ以外の場合、実行されたコマンドが 0 以外の終了コードを返すときは、タスクは `false` を返します。|  
|`IgnoreStandardErrorWarningFormat`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `false` の場合は、標準エラー/警告の形式に一致する出力行を選び、エラー/警告としてログに記録します。 `true` の場合は、この動作は無効になります。|  
|`Outputs`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> タスクからの出力項目を含みます。 `Exec` タスク自体はこれらを設定しません。 代わりに、タスクが設定したかのようにユーザーが提供して、プロジェクトの後の処理で使うことができます。|  
|`StdErrEncoding`|省略可能な `String` 型の出力パラメーターです。<br /><br /> キャプチャしたタスクの標準エラー ストリームのエンコーディングを指定します。 既定値は、現在のコンソール出力のエンコーディングです。|  
|`StdOutEncoding`|省略可能な `String` 型の出力パラメーターです。<br /><br /> キャプチャしたタスクの標準出力ストリームのエンコーディングを指定します。 既定値は、現在のコンソール出力のエンコーディングです。|  
|`WorkingDirectory`|省略可能な `String` 型のパラメーターです。<br /><br /> コマンドを実行するディレクトリを指定します。|  
  
## <a name="remarks"></a>解説  
 このタスクは、実行したいジョブの特定の [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] タスクを使用できないときに便利です。 ただし、`Exec` タスクは、固有のタスクとは異なり、実行したツールまたはコマンドから出力を収集することはできません。  
  
 `Exec` タスクは、プロセスを直接呼び出す代わりに cmd.exe を呼び出します。  
  
 このドキュメントにリストされているパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.ToolTask> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[ToolTaskExtension 基本クラス](../msbuild/tooltaskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Exec` タスクを使ってコマンドを実行します。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <Binaries Include="*.dll;*.exe"/>  
    </ItemGroup>  
  
    <Target Name="SetACL">  
        <!-- set security on binaries-->  
        <Exec Command="echo y| cacls %(Binaries.Identity) /G everyone:R"/>  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
