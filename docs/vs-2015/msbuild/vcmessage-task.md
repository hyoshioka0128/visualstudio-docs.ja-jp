---
title: VCMessage タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- vc.task.vcmessage
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- VCMessage task (MSBuild (Visual C++))
- MSBuild (Visual C++), VCMessage task
ms.assetid: 956675fd-05dc-40b4-856f-616145103498
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 508d1fe33046f6051c9c5c1b8e54036e78ae7d2f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193343"
---
# <a name="vcmessage-task"></a>VCMessage タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ビルド時の警告およびエラー メッセージをログに記録します。  
  
## <a name="remarks"></a>解説  
 このタスクは Visual C++ 用の MSBuild の実装に役立ちます。ユーザーによる呼び出しは意図されていません。 詳細については、「<xref:Microsoft.Build.Utilities.TaskLoggingHelper>」を参照してください。  
  
## <a name="parameters"></a>パラメーター  
 **VCMessage** タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|**引数**|省略可能な **String** 型のパラメーターです。<br /><br /> 表示するメッセージをセミコロンで区切った一覧です。|  
|**コード**|必須の **String** 型のパラメーターです。<br /><br /> メッセージに付けられるエラー番号です。|  
|**Type**|省略可能な **String** 型のパラメーターです。<br /><br /> 発信するメッセージの種類を指定します。 警告メッセージの場合は `"Warning"` を、エラー メッセージの場合は `"Error"` を指定します。|  
  
## <a name="see-also"></a>参照  
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
