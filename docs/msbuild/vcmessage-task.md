---
title: VCMessage タスク | Microsoft Docs
description: MSBuild で VCMessage タスクを使用して、C++ プロジェクトのビルド中に警告とエラーのメッセージをログに記録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 06/27/2018
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
- VCMessage task (MSBuild (C++))
- MSBuild (C++), VCMessage task
ms.assetid: 956675fd-05dc-40b4-856f-616145103498
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: c8db60044080726b61a02a59cad68d93f683e282
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99908822"
---
# <a name="vcmessage-task"></a>VCMessage タスク

ビルド時の警告およびエラー メッセージをログに記録します。

## <a name="remarks"></a>注釈

 このタスクは C++ プロジェクト用の MSBuild の実装に役立ちます。ユーザーによる呼び出しは意図されていません。 詳細については、「<xref:Microsoft.Build.Utilities.TaskLoggingHelper>」を参照してください。

## <a name="parameters"></a>パラメーター

 **VCMessage** タスクのパラメーターの説明を次の表に示します。

|パラメーター|説明|
|---------------|-----------------|
|**引数**|省略可能な **String** 型のパラメーターです。<br /><br /> 表示するメッセージをセミコロンで区切った一覧です。|
|**コード**|必須の **String** 型のパラメーターです。<br /><br /> メッセージに付けられるエラー番号です。|
|**Type**|省略可能な **String** 型のパラメーターです。<br /><br /> 発信するメッセージの種類を指定します。 警告メッセージを発信する場合は "Warning" を、エラー メッセージを発信する場合は "Error" を指定します。|

## <a name="see-also"></a>関連項目

- [タスク リファレンス](../msbuild/msbuild-task-reference.md)
