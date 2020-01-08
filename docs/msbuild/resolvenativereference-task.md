---
title: ResolveNativeReference タスク | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveNativeReference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveNativeReference task
- ResolveNativeReference task [MSBuild]
ms.assetid: 56acd101-de77-4eec-92c6-f5c6d2187579
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 417c4536f13aa90505ec5e69b2719219af0d7e81
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595164"
---
# <a name="resolvenativereference-task"></a>ResolveNativeReference タスク
ネイティブ参照を解決します。 <xref:Microsoft.Build.Tasks.ResolveNativeReference> クラスを実行します。 このクラスは、.NET Framework インフラストラクチャをサポートします。独自に作成したコードから直接使用するためのものではありません。

## <a name="task-parameters"></a>タスク パラメーター
 `ResolveNativeReference` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`AdditionalSearchPaths`|必須の <xref:System.String?displayProperty=fullName>`[]` 型のパラメーターです。<br /><br /> ネイティブ参照のアセンブリ ID を解決するための検索パスを取得または設定します。|
|`ContainedComComponents`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ アセンブリの COM コンポーネントを取得または設定します。|
|`ContainedLooseEtcFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ マニフェストに示されているルース *Etc* ファイルを取得または設定します。|
|`ContainedLooseTlbFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ アセンブリのルース *.tlb* ファイルを取得または設定します。|
|`ContainedPrerequisiteAssemblies`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> マニフェストを使用する前に存在する必要があるアセンブリを取得または設定します。|
|`ContainedTypeLibraries`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> ネイティブ アセンブリのタイプ ライブラリを取得または設定します。|
|`ContainingReferenceFiles`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型の出力パラメーターです。<br /><br /> 参照ファイルを取得または設定します。|
|`NativeReferences`|必須の <xref:Microsoft.Build.Framework.ITaskItem>`[]` 型のパラメーターです。<br /><br /> Win32 ネイティブ アセンブリ参照を取得または設定します。|

## <a name="remarks"></a>Remarks
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
