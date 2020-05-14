---
title: 既存プロジェクトの追加コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.addexistingproject
helpviewer_keywords:
- Add Existing Project command
- File.AddExistingProject
ms.assetid: 71cf3e31-c76b-405b-ad6a-1b1bc654bd40
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 73d8e54938659920227b3614046b8a8f933023ff
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670216"
---
# <a name="add-existing-project-command"></a>AddExistingProject コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

既存のプロジェクトを現在のソリューションに追加します。

## <a name="syntax"></a>構文

```
File.AddExistingProject filename
```

## <a name="arguments"></a>引数
 `filename` 省略可能。 ソリューションに追加するプロジェクトの完全なパスとプロジェクト名 (拡張子付き)。

 `filename` 引数にスペースが含まれる場合は、引用符で囲む必要があります。

 ファイル名が指定されていない場合、ファイルを開くダイアログ ボックスが表示され、ユーザーがプロジェクトを選択できます。

## <a name="remarks"></a>解説
 オート コンプリートでは、入力された正しいパスとファイル名の検索を試みます。

## <a name="example"></a>例
 この例では、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] プロジェクトの TestProject1 を現在のソリューションに追加します。

```
>File.AddExistingProject "c:\visual studio projects\TestProject1.vbproj"
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
