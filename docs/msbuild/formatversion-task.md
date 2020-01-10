---
title: FormatVersion タスク | Microsoft Docs
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
ms.openlocfilehash: 0b36c4eb63c503132aaf434c64249e4a5fdd3872
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595255"
---
# <a name="formatversion-task"></a>FormatVersion タスク
バージョン番号にリビジョン番号を追加します。

- ケース 1:入力:Version=\<undefined>;  Revision=\<don't care>;   Output:OutputVersion="1.0.0.0"

- ケース 2:入力:Version="1.0.0.*"  Revision="5"  Output:OutputVersion="1.0.0.5"

- ケース 3:入力:Version="1.0.0.0"  Revision=\<don't care>;  Output:OutputVersion="1.0.0.0"

## <a name="parameters"></a>パラメーター
 `FormatVersion` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|`FormatType`|省略可能な `String` 型のパラメーターです。<br /><br /> 形式の種類を指定します。<br /><br /> -   "Version" = バージョン<br />-   "Path" = "." を "_" で置換|
|`OutputVersion`|省略可能な `String` 型の出力パラメーターです。<br /><br /> リビジョン番号を含む出力バージョンを指定します。|
|`Revision`|省略可能な `Int32` 型のパラメーターです。<br /><br /> バージョンに追加するリビジョンを指定します。|
|`Version`|省略可能な `String` 型のパラメーターです。<br /><br /> 書式設定するバージョン番号文字列を指定します。|

## <a name="remarks"></a>Remarks
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
