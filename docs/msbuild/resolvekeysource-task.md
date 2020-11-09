---
title: ResolveKeySource タスク | Microsoft Docs
description: 厳密な名前のキー ソースを決定する MSBuild ResolveKeySource タスクのパラメーターについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2ed7bf0e831153d1120789d97b2a27aa77822a6b
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048589"
---
# <a name="resolvekeysource-task"></a>ResolveKeySource タスク

厳密な名前のキーのソースを確認します。

## <a name="task-parameters"></a>タスク パラメーター

 `ResolveKeySource` タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
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

## <a name="remarks"></a>Remarks

 上記のパラメーター以外に、このタスクは <xref:Microsoft.Build.Tasks.TaskExtension> クラスからパラメーターを継承します。このクラス自体は、<xref:Microsoft.Build.Utilities.Task> クラスから継承されます。 これらの追加のパラメーターの一覧とその説明については、「[TaskExtension Base Class](../msbuild/taskextension-base-class.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [タスク](../msbuild/msbuild-tasks.md)
- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
