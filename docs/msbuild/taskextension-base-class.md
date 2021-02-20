---
title: TaskExtension 基本クラス | Microsoft Docs
description: Microsoft.Build.Tasks.TaskExtension 基底クラスから継承されるタスクに追加されるパラメーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tool task base class
- tool task base class [MSBuild]
ms.assetid: 08bb8059-b7e2-4565-89ba-d9034d4f0e16
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6692cb16b3861d72bf713c22b2ecfb2ee95bc036
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965981"
---
# <a name="taskextension-base-class"></a>TaskExtension 基底クラス

多くのタスクが <xref:Microsoft.Build.Tasks.TaskExtension> クラスを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承します。 この継承チェーンにより、これらのクラスから派生したタスクにいくつかのパラメーターが追加されます。 このドキュメントでは、これらのパラメーターを示します。

## <a name="parameters"></a>パラメーター

 基本クラスのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|<xref:Microsoft.Build.Utilities.Task.BuildEngine%2A>|省略可能な <xref:Microsoft.Build.Framework.IBuildEngine> 型のパラメーターです。<br /><br /> タスクで使用できるビルド エンジン インターフェイスを指定します。 ビルド エンジンは、自動的にこのパラメーターを設定して、タスクによるコールバックを可能にします。|
|<xref:Microsoft.Build.Utilities.Task.BuildEngine2%2A>|省略可能な <xref:Microsoft.Build.Framework.IBuildEngine2> 型のパラメーターです。<br /><br /> タスクで使用できるビルド エンジン インターフェイスを指定します。 ビルド エンジンは、自動的にこのパラメーターを設定して、タスクによるコールバックを可能にします。<br /><br /> この便利なプロパティにより、このクラスから継承するタスクの作成者は、`IBuildEngine2` から `IBuildEngine` に値をキャストする必要がなくなります。|
|<xref:Microsoft.Build.Utilities.Task.BuildEngine3%2A>|省略可能な <xref:Microsoft.Build.Framework.IBuildEngine3> 型のパラメーターです。<br /><br /> ホストによって提供されるビルド エンジン インターフェイスを指定します。|
|<xref:Microsoft.Build.Utilities.Task.HostObject%2A>|省略可能な <xref:Microsoft.Build.Framework.ITaskHost> 型のパラメーターです。<br /><br /> ホスト オブジェクト インスタンスを指定します (null も指定できます)。 ビルド エンジンは、ホスト IDE によってホスト オブジェクトがこの特定のタスクに関連付けられている場合にこのプロパティを設定します。|
|<xref:Microsoft.Build.Tasks.TaskExtension.Log%2A>|省略可能な <xref:Microsoft.Build.Utilities.TaskLoggingHelper> 型の読み取り専用パラメーターです。<br /><br /> タスク ログ メソッドを格納している `TaskLoggingHelperExtension` オブジェクトを取得します。|

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
- [タスク](../msbuild/msbuild-tasks.md)
