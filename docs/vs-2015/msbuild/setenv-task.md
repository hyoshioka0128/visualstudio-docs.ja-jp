---
title: SetEnv タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- vc.task.setenv
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), tasks
- SetEnv task (MSBuild (Visual C++))
ms.assetid: fd9e4225-68cb-4608-8b27-468b0218c936
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 960ebb94cf03ef293011645e732a0f0379d0fd47
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2020
ms.locfileid: "75852243"
---
# <a name="setenv-task"></a>SetEnv タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

指定された環境変数の値を設定または削除します。  
  
## <a name="parameters"></a>パラメーター  
 **SetEnv** タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|**Name**|必須の **String** 型のパラメーターです。<br /><br /> 環境変数の名前。|  
|**OutputEnvironmentVariable**|省略可能な **String** 型の出力パラメーターです。<br /><br /> **Name** パラメーターによって指定される環境変数に割り当てられる値が含まれます。|  
|**Prefix**|必須の `Boolean` パラメーターです。<br /><br /> `true` の場合、**Name** パラメーターによって指定される環境変数値の前に **Value** パラメーターの値を連結し、結果を環境変数に割り当てます。 `false` の場合、**Value** パラメーターの値のみを環境変数に割り当てます。|  
|**Target**|省略可能な **String** 型のパラメーターです。<br /><br /> 環境変数が保存される場所を指定します。 "`User`" または "`Machine`" を指定します。<br /><br /> 詳細については、[MSDN](https://msdn.microsoft.com/) Web サイトの "EnvironmentVariableTarget Enumeration" (EnvironmentVariableTarget 列挙型) をご覧ください|  
|**[値]**|省略可能な **String** 型のパラメーターです。<br /><br /> **Name** パラメーターによって指定される環境変数に割り当てられる値。 **Value** が空で変数が存在する場合、変数が削除されます。 変数が存在しない場合、操作が実行できなくてもエラーは発生しません。<br /><br /> 詳細については、[MSDN](https://msdn.microsoft.com/) Web サイトの "Environment::SetEnvironmentVariable Method" (Environment::SetEnvironmentVariable メソッド) を参照してください。|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>関連項目  
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)
