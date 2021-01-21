---
title: FormatVersion タスク | Microsoft Docs
description: MSBuild FormatVersion タスクによってバージョン番号にリビジョン番号を追加するさまざまな方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 96e692f6-b581-46ca-8cc9-441a1861e371
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 16da018e49e6cb456074ebabac52a8768d06c1c6
ms.sourcegitcommit: c4927ef8fe239005d7feff6c5a7707c594a7a05c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92436707"
---
# <a name="formatversion-task"></a>FormatVersion タスク

バージョン番号にリビジョン番号を追加します。

- ケース 1:入力:Version=\<undefined>;  Revision=\<don't care>;   Output:OutputVersion="1.0.0.0"

- 例 #2: Input: Version="1.0.0.*"  Revision="5"  Output: OutputVersion="1.0.0.5"

- ケース 3:入力:Version="1.0.0.0"  Revision=\<don't care>;  Output:OutputVersion="1.0.0.0"

## <a name="parameters"></a>パラメーター

 `FormatVersion` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`FormatType`|省略可能な `String` 型のパラメーターです。<br /><br /> 形式の種類を指定します。<br /><br /> -   "Version" = バージョン<br />-   "Path" = "." を "_" で置換|
|`OutputVersion`|省略可能な `String` 型の出力パラメーターです。<br /><br /> リビジョン番号を含む出力バージョンを指定します。|
|`Revision`|省略可能な `Int32` 型のパラメーターです。<br /><br /> バージョンに追加するリビジョンを指定します。|
|`Version`|省略可能な `String` 型のパラメーターです。<br /><br /> 書式設定するバージョン番号文字列を指定します。|

## <a name="remarks"></a>解説

 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
