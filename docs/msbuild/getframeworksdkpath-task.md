---
title: GetFrameworkSdkPath タスク | Microsoft Docs
description: MSBuild GetFrameworkSdkPath タスクを使用して、Windows SDK へのパスを取得する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GetFrameworkSdkPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- GetFrameworkSdkPath task [MSBuild]
- MSBuild, GetFrameworkSdkPath task
ms.assetid: 2ef82b98-02b6-40cf-a9b5-f0e882fb5064
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e4061dbe96c84648aacf136c0d59b92a2af037e2
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436805"
---
# <a name="getframeworksdkpath-task"></a>GetFrameworkSdkPath タスク

Windows ソフトウェア開発キット (SDK) へのパスを取得します。
## <a name="task-parameters"></a>タスク パラメーター

`GetFrameworkSdkPath` タスクのパラメーターの説明を次の表に示します。
`GetFrameworkSdkPath` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`FrameworkSdkVersion20Path`|省略可能な `String` 型の読み取り専用の出力パラメーターです。<br /><br /> 存在する場合、.NET SDK バージョン 2.0 のパスを返します。 それ以外の場合は、`String.Empty` を返します。|
|`FrameworkSdkVersion35Path`|省略可能な `String` 型の読み取り専用の出力パラメーターです。<br /><br /> 存在する場合、.NET SDK バージョン 3.5 のパスを返します。 それ以外の場合は、`String.Empty` を返します。|
|`FrameworkSdkVersion40Path`|省略可能な `String` 型の読み取り専用の出力パラメーターです。<br /><br /> 存在する場合、.NET SDK バージョン 4.0 のパスを返します。 それ以外の場合は、`String.Empty` を返します。|
|`Path`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 何らかのバージョンが存在する場合、最新の .NET SDK のパスが含まれます。 それ以外の場合は、`String.Empty` を返します。|

## <a name="remarks"></a>Remarks

上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="example"></a>例

次の例では、`GetFrameworkSdkPath` タスクを使用して、Windows SDK へのパスを `SdkPath` プロパティに保存します。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="GetPath">
        <GetFrameworkSdkPath>
            <Output
                TaskParameter="Path"
                PropertyName="SdkPath" />
        </GetFrameworkSdkPath>
        <Message Text="$(SdkPath)"/>
    </Target>
</Project>
```

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
