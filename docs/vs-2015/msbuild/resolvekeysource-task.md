---
title: ResolveKeySource タスク | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#ResolveKeySource
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ResolveKeySource task [MSBuild]
- MSBuild, ResolveKeySource task
ms.assetid: 449f06c2-e9aa-4236-ab1e-c45c25452b2e
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: bd5cbe2f4998ab78ce39cde4b26a38b13c70b2f8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193718"
---
# <a name="resolvekeysource-task"></a>ResolveKeySource タスク
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

厳密な名前のキーのソースを確認します。  
  
## <a name="task-parameters"></a>タスク パラメーター  
 `ResolveKeySource` タスクのパラメーターの説明を次の表に示します。  
  
|パラメーター|[説明]|  
|---------------|-----------------|  
|`AutoClosePasswordPromptShow`|省略可能な `Int32` 型のパラメーターです。<br /><br /> カウント ダウン メッセージを表示する時間 (秒単位) を取得または設定します。|  
|`AutoClosePasswordPromptTimeout`|省略可能な `Int32` 型のパラメーターです。<br /><br /> パスワードのプロンプト ダイアログを閉じるまでの待機時間 (秒) を取得または設定します。|  
|`CertificateFile`|省略可能な `String` 型のパラメーターです。<br /><br /> 証明書ファイルのパスを取得または設定します。|  
|`CertificateThumbprint`|省略可能な `String` 型のパラメーターです。<br /><br /> 証明書の拇印を取得または設定します。|  
|`KeyFile`|省略可能な `String` 型のパラメーターです。<br /><br /> キー ファイルのパスを取得または設定します。|  
|`ResolvedKeyContainer`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 解決済みのキー コンテナーを取得または設定します。|  
|`ResolvedKeyFile`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 解決済みのキー ファイルを取得または設定します。|  
|`ResolvedThumbprint`|省略可能な `String` 型の出力パラメーターです。<br /><br /> 解決済みの証明書の拇印を取得または設定します。|  
|`ShowImportDialogDespitePreviousFailures`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> `true` の場合、以前のエラーにかかわらず、インポート ダイアログを表示します。|  
|`SuppressAutoClosePasswordPrompt`|省略可能な `Boolean` 型のパラメーターです。<br /><br /> パスワード入力のダイアログを自動終了させない必要があるかどうかを指定するブール値を取得または設定します。|  
  
## <a name="remarks"></a>解説  
 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加パラメーターとその説明の一覧については、「 [Taskextension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [タスク](../msbuild/msbuild-tasks.md)   
 [タスクリファレンス](../msbuild/msbuild-task-reference.md)
