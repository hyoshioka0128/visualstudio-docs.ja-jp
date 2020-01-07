---
title: OpenProject コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.openproject
helpviewer_keywords:
- op command
- File.OpenProject command
- Open Project command
ms.assetid: baa85f86-041b-49f4-9ced-0c397dc180e1
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 99596442f3aef9e4cb2d890438d29b96cdf4f083
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671921"
---
# <a name="open-project-command"></a>OpenProject コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

既存のプロジェクトを開きます。

## <a name="syntax"></a>構文

```
File.OpenProject filename
```

## <a name="arguments"></a>引数
 `filename` 必須。 開くプロジェクトの完全パスとファイル名。

 `filename` 引数の構文の場合、空白を含むパスで引用符を使用する必要があります。

## <a name="remarks"></a>解説
 オート コンプリートでは、入力された正しいパスとファイル名の検索を試みます。

 デバッグ中にこのコマンドを使用することはできません。

## <a name="example"></a>例
 この例では、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] プロジェクトの Test1 を開きます。

```
>File.OpenProject "C:\My Projects\Test1\Test1.vbproj"
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
