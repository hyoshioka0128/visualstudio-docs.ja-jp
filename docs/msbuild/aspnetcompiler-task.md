---
title: AspNetCompiler タスクを使用して ASP.NET をプリコンパイルする
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 43b7ccc11e8d265c0b1490e7e8de0bd33d903904
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90036185"
---
# <a name="aspnetcompiler-task"></a>AspNetCompiler タスク

`AspNetCompiler` タスクは、ASP.NET アプリケーションをプリコンパイルするためのユーティリティである *aspnet_compiler.exe* をラップします。

## <a name="task-parameters"></a>タスク パラメーター

`AspNetCompiler` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`AllowPartiallyTrustedCallers`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、厳密な名前のアセンブリは部分的に信頼された呼び出し元を許可します。|
|`Clean`|省略可能な `Boolean` 型のパラメーターです<br /><br /> このパラメーターが `true` の場合、プリコンパイルされたアプリケーションはクリーン ビルドされます。 以前にコンパイルされたコンポーネントは、再コンパイルされます。 既定値は `false` です。 このパラメーターは、*aspnet_compiler.exe* の **-c** スイッチに対応します。|
|`Debug`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、コンパイル中にデバッグ情報 (.PDB ファイル) が生成されます。 既定値は `false` です。 このパラメーターは、*aspnet_compiler.exe* の **-d** スイッチに対応します。|
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、アセンブリは作成時に完全に署名されません。|
|`FixedNames`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、コンパイルされたアセンブリに固定名が指定されます。|
|`Force`|省略可能な `Boolean` 型のパラメーターです<br /><br /> このパラメーターが `true` の場合、タスクはターゲット ディレクトリが既に存在する場合は上書きします。 既存の内容は失われます。 既定値は `false` です。 このパラメーターは、*aspnet_compiler.exe* の **-f** スイッチに対応します。|
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> 厳密な名前のキー コンテナーを指定します。|
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 厳密な名前のキー ファイルへの物理パスを指定します。|
|`MetabasePath`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションの IIS メタベースの完全パスを指定します。 このパラメーターを `VirtualPath` または `PhysicalPath` パラメーターと組み合わせることはできません。 このパラメーターは、*aspnet_compiler.exe* の **-m** スイッチに対応します。|
|`PhysicalPath`|省略可能な `String` 型のパラメーターです。<br /><br /> コンパイルされるアプリケーションの物理パスを指定します。 このパラメーターを指定しないと、アプリケーションの場所の特定には IIS メタベースが使われます。 このパラメーターは、*aspnet_compiler.exe* の **-p** スイッチに対応します。|
|`TargetFrameworkMoniker`|省略可能な `String` 型のパラメーターです。<br /><br /> 使う必要がある *aspnet_compiler.exe* の .NET Framework バージョンを示す TargetFrameworkMoniker を指定します。 .NET Framework モニカーのみを受け付けます。|
|`TargetPath`|省略可能な `String` 型のパラメーターです。<br /><br /> アプリケーションのコンパイル先の物理パスを指定します。 指定しないと、アプリケーションはインプレースでプリコンパイルされます。|
|`Updateable`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> このパラメーターが `true` の場合、プリコンパイルされたアプリケーションは更新可能です。  既定値は `false` です。 このパラメーターは、*aspnet_compiler.exe* の **-u** スイッチに対応します。|
|`VirtualPath`|省略可能な `String` 型のパラメーターです。<br /><br /> コンパイル対象のアプリケーションの仮想パス。 `PhysicalPath` を指定すると、アプリケーションの場所の指定に物理パスが使われます。 それ以外の場合は IIS メタベースが使われ、アプリケーションは既定のサイトにあるものと想定されます。 このパラメーターは、*aspnet_compiler.exe* の **-v** スイッチに対応します。|

[!INCLUDE [ToolTaskExtension arguments](includes/tooltaskextension-base-params.md)]

## <a name="example"></a>例

次のコード例では、`AspNetCompiler` タスクを使って ASP.NET アプリケーションをプリコンパイルします。

```xml
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

* [タスク](../msbuild/msbuild-tasks.md)
* [タスク リファレンス](../msbuild/msbuild-task-reference.md)
