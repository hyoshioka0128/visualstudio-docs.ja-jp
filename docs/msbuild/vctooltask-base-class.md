---
title: VCToolTask クラス | Microsoft Docs
description: VCToolTask 基底クラスによって継承されるタスクに追加されるいくつかのパラメーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: b2e45d7c672ebc2177c2bb197399133e7b077a5c
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046742"
---
# <a name="vctooltask-base-class"></a>VCToolTask 基底クラス

多くのタスクは最終的に <xref:Microsoft.Build.Utilities.Task> クラスおよび [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) クラスから継承します。 このクラスは、それから派生するタスクにいくつかのパラメーターを追加します。 このドキュメントでは、これらのパラメーターを示します。

## <a name="parameters"></a>パラメーター

以下の表では、 **VCToolTask** 基底クラスのパラメーターについて説明します。

|パラメーター|[説明]|
|---------------|-----------------|
|**ActiveToolSwitchesValues**|省略可能な **Dictionary\<string, ToolSwitch>** パラメーターです。|
|**AdditionalOptions**|省略可能な **string** 型のパラメーターです。|
|**EffectiveWorkingDirectory**|省略可能な **string** 型のパラメーターです。|
|**EnableErrorListRegex**|省略可能な **bool** 型のパラメーターです。<br/><br/>既定値は `true` です。|
|**ErrorListRegex**|省略可能な **ITaskItem[]** パラメーターです。|
|**ErrorListListExclusion**|省略可能な **ITaskItem[]** パラメーターです。|
|**GenerateCommandLine**|省略可能な **string** 型のパラメーターです。<br/><br/>値 **CommandLineFormat** *format* [default = CommandLineFormat.ForBuildLog] および **EscapeFormat** *escapeFormat* [default = EscapeFormat.Default] を使用します。|
|**GenerateCommandLineExceptSwitches**|省略可能な **string** 型のパラメーターです。<br/><br/>値 **string[]** *switchesToRemove* , **CommandLineFormat** *format* [default = CommandLineFormat.ForBuildLog], および **EscapeFormat** *escapeFormat* [default = EscapeFormat.Default] を使用します。|

## <a name="see-also"></a>参照

[タスク リファレンス](../msbuild/msbuild-task-reference.md)<br/>
[タスク](../msbuild/msbuild-tasks.md)
