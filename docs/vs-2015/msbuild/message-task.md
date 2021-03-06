---
title: Message タスク | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Message
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Message task
- Message task [MSBuild]
ms.assetid: 2293309d-42b6-46dc-9684-8c146f66bc28
caps.latest.revision: 27
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 29b51a3e51610ee15bf9908e6c0465fbe1fd5cd6
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2018
ms.locfileid: "49285078"
---
# <a name="message-task"></a>Message タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
ビルド中のメッセージをログに記録します。  
  
## <a name="parameters"></a>パラメーター  
 `Message` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|`Importance`|省略可能な `String` 型のパラメーターです。<br /><br /> メッセージの重要度を指定します。 このパラメーターの値には、`high`、`normal`、または `low` を指定できます。 既定値は `normal` です。|  
|`Text`|省略可能な `String` 型のパラメーターです。<br /><br /> ログに記録するエラー テキスト。|  
  
## <a name="remarks"></a>Remarks  
 `Message` タスクを使用すると、[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] プロジェクトで、ビルド処理のさまざまな段階でロガーにメッセージを発行できます。  
  
 `Condition` パラメーターが `true` と評価されると、`Text` パラメーターの値がログに記録され、ビルド処理が継続されます。 `Condition` パラメーターが存在しない場合は、メッセージ テキストがログに記録されます。 ログ処理の詳細については、[ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)に関するページを参照してください。  
  
 既定では、メッセージは MSBuild のコンソール ロガーに送信されます。 これは、<xref:Microsoft.Build.Tasks.TaskExtension.Log%2A> プロパティを設定することにより変更できます。 ロガーによって `Importance` パラメーターが解釈されます。  
  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例は、登録されているすべてのロガーにメッセージをログ記録します。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="DisplayMessages">  
        <Message Text="Project File Name = $(MSBuildProjectFile)" />  
        <Message Text="Project Extension = $(MSBuildProjectExtension)" />  
    </Target>  
    ...  
</Project>  
```  
  
## <a name="see-also"></a>関連項目  
 [Task Reference (タスク リファレンス)](../msbuild/msbuild-task-reference.md)   
 [ビルド ログの取得](../msbuild/obtaining-build-logs-with-msbuild.md)



