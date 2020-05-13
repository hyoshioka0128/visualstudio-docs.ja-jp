---
title: FormatUrl タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, FormatUrl task
- FormatUrl task [MSBuild]
ms.assetid: 81114b67-520f-43b5-8891-224f68a78516
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bb870bcc3c4297d5d1b403176f931f75e418d423
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149711"
---
# <a name="formaturl-task"></a>FormatUrl タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

URL を正しい URL 書式に変換します。  
  
## <a name="parameters"></a>パラメーター  
 `FormatUrl` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`InputUrl`|省略可能な `String` 型のパラメーターです。<br /><br /> 書式設定する URL を指定します。|  
|`OutputUrl`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 書式設定された URL を指定します。|  
  
## <a name="remarks"></a>解説  
 表にリストされているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目
 [タスク](../msbuild/msbuild-tasks.md)   
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
