---
title: FormatVersion タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 96e692f6-b581-46ca-8cc9-441a1861e371
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ee6e163bd6587d93c970a56ac1c08383084ddc0c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149624"
---
# <a name="formatversion-task"></a>FormatVersion タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

バージョン番号にリビジョン番号を追加します。  
  
- 例 #1: Input: Version=\<undefined>;  Revision=\<don't care>;   Output: OutputVersion="1.0.0.0"  
  
- 例 #2: Input: Version="1.0.0.*"  Revision="5"  Output: OutputVersion="1.0.0.5"  
  
- 例 #3: Input: Version="1.0.0.0"  Revision=\<don't care>;  Output: OutputVersion="1.0.0.0"  
  
## <a name="parameters"></a>パラメーター  
 `FormatVersion` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`FormatType`|省略可能な `String` 型のパラメーターです。<br /><br /> 形式の種類を指定します。<br /><br /> -   "Version" = バージョン<br />-   "Path" = "." を "_" で置換|  
|`OutputVersion`|省略可能な `String` 型の出力パラメーターです。<br /><br /> リビジョン番号を含む出力バージョンを指定します。|  
|`Revision`|省略可能な `Int32` 型のパラメーターです。<br /><br /> バージョンに追加するリビジョンを指定します。|  
|`Version`|省略可能な `String` 型のパラメーターです。<br /><br /> 書式設定するバージョン番号文字列を指定します。|  
  
## <a name="remarks"></a>解説  
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
