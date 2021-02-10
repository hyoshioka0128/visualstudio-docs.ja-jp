---
title: ResolveComReference タスク | Microsoft Docs
description: MSBuild で ResolveComReference タスクを使用して、1 つまたは複数のタイプ ライブラリ名または .tlb ファイルの一覧を取得し、ディスク上の場所に解決する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 07/25/2019
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveComReference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveCOMReference task
- ResolveCOMReference task [MSBuild]
ms.assetid: c9bf5fcf-6453-40ea-b50f-a212adc3e9b5
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0384ee6cbfa749589e15ab073cc31ffebb53985e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912531"
---
# <a name="resolvecomreference-task"></a>ResolveComReference タスク

1 つ以上のタイプ ライブラリ名または *.tlb* ファイルから成る一覧を使用して、これらのタイプ ライブラリのディスク上の位置を解決します。

## <a name="parameters"></a>パラメーター

 `ResolveCOMReference` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`DelaySign`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、公開鍵がアセンブリに配置されます。 `false` の場合、アセンブリに完全署名されます。|
|`EnvironmentVariables`|省略可能な `String[]` 型のパラメーターです。<br /><br /> 等号で区切られた環境変数のペアの配列です。 これらの変数は、標準の環境ブロックに加え (または標準の環境ブロックを選択的にオーバーライドして)、子の *tlbimp.exe* および *aximp.exe* に渡されます。|
|`ExecuteAsTool`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、アウトプロセスで適切なターゲット フレームワークの *tlbimp.exe* および *aximp.exe* が実行されて、必要なラッパー アセンブリが生成されます。 このパラメーターはマルチ ターゲットを有効にします。|
|`IncludeVersionInInteropName`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、typelib バージョンはラッパー名に含まれます。 既定値は、`false` です。|
|`KeyContainer`|省略可能な `String` 型のパラメーターです。<br /><br /> 公開キーと秘密キーのペアを保持するコンテナーを指定します。|
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 公開キーと秘密キーのペアを含む項目を指定します。|
|`NoClassMembers`|省略可能な `Boolean` 型のパラメーターです。|
|`ResolvedAssemblyReferences`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 解決されたアセンブリ参照を指定します。|
|`ResolvedFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> このタスクの入力として指定されたタイプ ライブラリの物理的な位置に対応するディスク上の完全修飾ファイルを指定します。|
|`ResolvedModules`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。|
|`SdkToolsPath`|省略可能な <xref:System.String?displayProperty=fullName> 型のパラメーターです。<br /><br /> `ExecuteAsTool` が `true` の場合、このパラメーターを、対象となっているフレームワークのバージョンの SDK ツール パスに設定する必要があります。|
|`StateFile`|省略可能な `String` 型のパラメーターです。<br /><br /> COM コンポーネントのタイムスタンプのキャッシュ ファイルを指定します。 存在しない場合は、実行するたびにすべてのラッパーが再生成されます。|
|`TargetFrameworkVersion`|省略可能な `String` 型のパラメーターです。<br /><br /> プロジェクトのターゲット フレームワークのバージョンを指定します。<br /><br /> 既定値は、`String.Empty` です。 その場合、ターゲット フレームワークに基づく参照のフィルター処理はありません。|
|`TargetProcessorArchitecture`|省略可能な `String` 型のパラメーターです。<br /><br /> 優先されるターゲットのプロセッサ アーキテクチャを指定します。 変換後、*tlbimp.exe*/machine フラグに渡されます。<br /><br /> パラメーター値は <xref:Microsoft.Build.Utilities.ProcessorArchitecture> のメンバーである必要があります。|
|`TypeLibFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> COM 参照へのタイプ ライブラリ ファイル パスを指定します。 このパラメーターに含まれる項目には、項目のメタデータが含まれます。 詳細については、後述する「[TypeLibFiles 項目メタデータ](#typelibfiles-item-metadata)」を参照してください。|
|`TypeLibNames`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> 解決するタイプ ライブラリ名を指定します。 このパラメーターに含まれる項目には、項目メタデータをいくつか含める必要があります。 詳細については、後述する「[TypeLibNames 項目メタデータ](#typelibnames-item-metadata)」を参照してください。|
|`WrapperOutputDirectory`|省略可能な `String` 型のパラメーターです。<br /><br /> 生成された相互運用機能アセンブリが配置されるディスク上の場所。 この項目メタデータが指定されていない場合、タスクはプロジェクト ファイルがあるディレクトリの絶対パスを使用します。|

## <a name="typelibnames-item-metadata"></a>TypeLibNames 項目メタデータ

 次の表に、`TypeLibNames` パラメーターに渡された項目に使用可能な項目メタデータを示します。

|メタデータ|説明|
|--------------|-----------------|
|`GUID`|必要な項目メタデータです。<br /><br /> タイプ ライブラリの GUID。 この項目メタデータが指定されていないと、タスクが失敗します。|
|`VersionMajor`|必要な項目メタデータです。<br /><br /> タイプ ライブラリのメジャー バージョンです。 この項目メタデータが指定されていないと、タスクが失敗します。|
|`VersionMinor`|必要な項目メタデータです。<br /><br /> タイプ ライブラリのマイナー バージョンです。 この項目メタデータが指定されていないと、タスクが失敗します。|
|`EmbedInteropTypes`|省略可能な `Boolean` メタデータ。<br /><br />  `true` の場合は、相互運用 DLL を生成するのではなく、この参照から直接アセンブリに相互運用機能型を埋め込みます。|
|`LocaleIdentifier`|省略可能な項目メタデータです。<br /><br /> タイプ ライブラリのロケール識別子 (LCID) です。 これは、ユーザー、リージョン、またはアプリケーションで優先される人間の言語を識別する 32 ビット値として指定されます。 この項目メタデータが指定されていないと、タスクは "0" の既定のロケール識別子を使用します。|
|`WrapperTool`|省略可能な項目メタデータです。<br /><br /> このタイプ ライブラリのアセンブリ ラッパーを生成するために使用されるラッパー ツールを指定します。 この項目メタデータが指定されていないと、タスクは、"tlbimp" の既定のラッパー ツールを使用します。 使用可能な大文字と小文字を区別しない typelibs の選択肢は次のとおりです。<br /><br /> -   `Primary`:COM コンポーネントの既に生成されたプライマリ相互運用機能アセンブリを使用する場合には、このラッパー ツールを使用します。 このラッパー ツールを使用する場合は、ラッパーの出力ディレクトリを指定しないでください。指定すると、タスクが失敗します。<br />-   `TLBImp`:COM コンポーネントの相互運用機能アセンブリを作成する場合には、このラッパー ツールを使用します。<br />-   `AXImp`: ActiveX コントロールの相互運用機能アセンブリを作成する場合には、このラッパー ツールを使用します。|

## <a name="typelibfiles-item-metadata"></a>TypeLibFiles 項目メタデータ

 次の表に、`TypeLibFiles` パラメーターに渡された項目に使用可能な項目メタデータを示します。

|メタデータ|説明|
|--------------|-----------------|
|`EmbedInteropTypes`|省略可能な `Boolean` 型のパラメーターです。<br /><br />  `true` の場合は、相互運用 DLL を生成するのではなく、この参照から直接アセンブリに相互運用機能型を埋め込みます。|
|`WrapperTool`|省略可能な項目メタデータです。<br /><br /> このタイプ ライブラリのアセンブリ ラッパーを生成するために使用されるラッパー ツールを指定します。 この項目メタデータが指定されていないと、タスクは、"tlbimp" の既定のラッパー ツールを使用します。 使用可能な大文字と小文字を区別しない typelibs の選択肢は次のとおりです。<br /><br /> -   `Primary`:COM コンポーネントの既に生成されたプライマリ相互運用機能アセンブリを使用する場合には、このラッパー ツールを使用します。 このラッパー ツールを使用する場合は、ラッパーの出力ディレクトリを指定しないでください。指定すると、タスクが失敗します。<br />-   `TLBImp`:COM コンポーネントの相互運用機能アセンブリを作成する場合には、このラッパー ツールを使用します。<br />-   `AXImp`:ActiveX コントロールの相互運用機能アセンブリを作成する場合には、このラッパー ツールを使用します。|

> [!NOTE]
> タイプ ライブラリを一意に識別するために提供する情報が多いほど、タスクがディスク上の正しいファイルに解決される可能性が大きくなります。

## <a name="remarks"></a>Remarks

上記のパラメーターに加えて、このタスクは <xref:Microsoft.Build.Utilities.Task> クラスからパラメーターを継承します。 これらの追加パラメーターのリストとその説明については、「[Task 基底クラス](../msbuild/task-base-class.md)」を参照してください。

このタスクを機能させるために、COM DLL をコンピューターに登録する必要はありません。

## <a name="msb4803-error"></a>MSB4803 エラー

`dotnet` CLI コマンドから `ResolveCOMReference` タスクを使用するプロジェクトを実行しようとすると、次のエラーが発生します。

```output
MSB4803: The task "ResolveComReference" is not supported on the .NET Core version of MSBuild. Please use the .NET Framework version of MSBuild.
```

このタスクは、MSBuild の .NET Core バージョンではサポートされていません。これは、コマンド ラインから `dotnet build` コマンドを実行するときに使用されるものです。 Visual Studio 開発者コマンド プロンプトから [MSBuild.exe](msbuild-command-line-reference.md) を呼び出してプロジェクトをビルドしてみてください。これには MSBuild の .NET Framework バージョンが使用されるためです。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
