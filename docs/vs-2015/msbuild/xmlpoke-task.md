---
title: XmlPoke タスク | Microsoft Docs
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
- XmlPoke task [MSBuild]
- MSBuild, XmlPoke task
ms.assetid: 6ba1953c-be3b-4df8-8561-e133408f8270
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1ba57c1578bd69d71ed0abdac45907d937b89ecb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198968"
---
# <a name="xmlpoke-task"></a>XmlPoke タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML ファイルに XPath クエリで指定された値を設定します。  
  
## <a name="parameters"></a>パラメーター  
 `XmlPoke` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Namespaces`|省略可能な `String` 型のパラメーターです。<br /><br /> XPath クエリ プレフィックスの名前空間を指定します。|  
|`Query`|省略可能な `String` 型のパラメーターです。<br /><br /> XPath クエリを指定します。|  
|`Value`|必須の <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> 出力ファイルを指定します。|  
|`XmlInputPath`|省略可能な <xref:Microsoft.Build.Framework.ITaskItem> 型のパラメーターです。<br /><br /> XML 入力をファイル パスとして指定します。|  
  
## <a name="remarks"></a>Remarks  
 表に示されているパラメーターを使用できるだけでなく、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は <xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加パラメーターとその説明の一覧については、「 [Taskextension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
