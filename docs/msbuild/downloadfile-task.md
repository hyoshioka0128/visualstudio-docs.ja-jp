---
title: DownloadFile タスク | Microsoft Docs
ms.date: 11/04/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#DownloadFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- DownloadFile task [MSBuild]
- MSBuild, DownloadFile task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 16
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 06171f3a1543f6fa827c1b6fd477b992d099fff6
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75590476"
---
# <a name="downloadfile-task"></a>DownloadFile タスク
ハイパーテキスト転送プロトコル (HTTP) を使って、指定したファイルをダウンロードします。

>[!NOTE]
>DownloadFile タスクは MSBuild 15.8 以降でのみ使用できます。

## <a name="parameters"></a>パラメーター
`DownloadFile` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`DestinationFileName`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです<br /><br /> ダウンロードしたファイルに使用する名前です。  既定では、`SourceUrl` またはリモート サーバーに由来するファイル名が付けられます。|
|`DestinationFolder`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> ファイルのダウンロード先のフォルダーを指定します。  フォルダーが存在しない場合は作成されます。|
|`DownloadedFile`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型の出力パラメーターです。<br /><br /> ダウンロードされたファイルを指定します。|
|`Retries`|省略可能な `Int32` 型のパラメーターです。<br /><br /> ダウンロードに失敗した場合の再試行回数を指定します。 既定値はゼロです。|
|`RetryDelayMilliseconds`|省略可能な `Int32` 型のパラメーターです。<br /><br /> 再試行の間隔をミリ秒単位で指定します。 既定値は 5000 です。|
|`SkipUnchangedFiles`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、変更されていないファイルのダウンロードをスキップします。 既定値は `true` です。 `DownloadFile` タスクでは、リモート サーバーに従って、ファイルのサイズが等しく、最終更新時刻が等しい場合、ファイルは変更されていないものと見なされます。 <br /><br />**注:** HTTP サーバーによってはファイルの最終更新日時が示されておらず、その場合はファイルが再度ダウンロードされます。|
|`SourceUrl`|必須の `String` 型のパラメーターです。<br /><br /> ダウンロードする URL を指定します。|

## <a name="remarks"></a>Remarks
上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例
次の例では、プロジェクトをビルドする前にファイルをダウンロードし、それを `Content` 項目に含めます。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
      <MyUrl>https://raw.githubusercontent.com/Microsoft/msbuild/master/LICENSE</MyUrl>
    </PropertyGroup>

    <Target Name="DownloadContentFiles" BeforeTargets="Build">
        <DownloadFile
            SourceUrl="$(MyUrl)"
            DestinationFolder="$(MSBuildProjectDirectory)">
        <Output TaskParameter="DownloadedFile" ItemName="Content" />
      </DownloadFile>
    </Target>

</Project>
```

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
