---
title: AspNetCompiler タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AspNetCompiler
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, AspNetCompiler task
- AspNetCompiler task [MSBuild]
ms.assetid: f811c019-a67b-4d54-82e6-e29549496f6e
caps.latest.revision: 14
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1267ddbb093f59eaa60fae0eef2d83f6b7ba2e24
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187057"
---
# <a name="aspnetcompiler-task"></a>AspNetCompiler タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`AspNetCompiler` タスクは、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションをプリコンパイルするためのユーティリティである aspnet_compiler.exe をラップします。  
  
## <a name="task-parameters"></a>タスク パラメーター  
 `AspNetCompiler` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`AllowPartiallyTrustedCallers`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、厳密な名前のアセンブリは部分的に信頼された呼び出し元を許可します。|  
|`Clean`|省略可能な `Boolean` 型のパラメーターです<br /><br /> このパラメーターが `true` の場合、プリコンパイルされたアプリケーションはクリーン ビルドされます。 以前にコンパイルされたコンポーネントは、再コンパイルされます。 既定値は `false` です。 このパラメーターは、aspnet_compiler.exe の **-c** スイッチに対応します。|  
|`Debug`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、コンパイル中にデバッグ情報 (.PDB ファイル) が生成されます。 既定値は `false` です。 このパラメーターは、aspnet_compiler.exe の **-d** スイッチに対応します。|  
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、アセンブリは作成時に完全に署名されません。|  
|`FixedNames`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、コンパイルされたアセンブリに固定名が指定されます。|  
|`Force`|省略可能な `Boolean` 型のパラメーターです<br /><br /> このパラメーターが `true` の場合、タスクはターゲット ディレクトリが既に存在する場合は上書きします。 既存の内容は失われます。 既定値は `false` です。 このパラメーターは、aspnet_compiler.exe の **-f** スイッチに対応します。|  
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> 厳密な名前のキー コンテナーを指定します。|  
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 厳密な名前のキー ファイルへの物理パスを指定します。|  
|`MetabasePath`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの IIS メタベースの完全パスを指定します。 このパラメーターを `VirtualPath` または `PhysicalPath` パラメーターと組み合わせることはできません。 このパラメーターは、aspnet_compiler.exe の **-m** スイッチに対応します。|  
|`PhysicalPath`|省略可能な `String` 型のパラメーターです。<br /><br /> コンパイルされるアプリケーションの物理パスを指定します。 このパラメーターを指定しないと、アプリケーションの場所の特定には IIS メタベースが使われます。 このパラメーターは、aspnet_compiler.exe の **-p** スイッチに対応します。|  
|`TargetFrameworkMoniker`|省略可能な `String` 型のパラメーターです。<br /><br /> 使う必要がある aspnet_compiler.exe の .NET Framework バージョンを示す TargetFrameworkMoniker を指定します。 .NET Framework モニカーのみを受け付けます。|  
|`TargetPath`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションのコンパイル先の物理パスを指定します。 指定しないと、アプリケーションはインプレースでプリコンパイルされます。|  
|`Updateable`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、プリコンパイルされたアプリケーションは更新可能です。  既定値は `false` です。 このパラメーターは、aspnet_compiler.exe の **-u** スイッチに対応します。|  
|`VirtualPath`|省略可能な `String` 型のパラメーターです。<br /><br /> コンパイル対象のアプリケーションの仮想パス。 `PhysicalPath` を指定すると、アプリケーションの場所の指定に物理パスが使われます。 それ以外の場合は IIS メタベースが使われ、アプリケーションは既定のサイトにあるものと想定されます。 このパラメーターは、aspnet_compiler.exe の **-v** スイッチに対応します。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.ToolTaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.ToolTask> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[ToolTaskExtension 基本クラス](../msbuild/tooltaskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例では、`AspNetCompiler` タスクを使って [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] アプリケーションをプリコンパイルします。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="PrecompileWeb">  
        <AspNetCompiler  
            VirtualPath="/MyWebSite"  
            PhysicalPath="c:\inetpub\wwwroot\MyWebSite\"  
            TargetPath="c:\precompiledweb\MyWebSite\"  
            Force="true"  
            Debug="true"  
        />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
