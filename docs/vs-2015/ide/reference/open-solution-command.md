---
title: Open Solution コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.opensolution
helpviewer_keywords:
- Open Solution command
- File.OpenSolution command
ms.assetid: 61de76c8-69d7-4cdb-b605-e132f45d05d9
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b9c9ab66d2885137e9c470f577996ab861b554d5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671903"
---
# <a name="open-solution-command"></a>OpenSolution コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

開いている他のソリューションを閉じ、既存のソリューションを開きます。

## <a name="syntax"></a>構文

```
File.OpenSolution filename
```

## <a name="arguments"></a>引数
 `Filename` 必須。 開くソリューションの完全パスとファイル名。

 `filename` 引数の構文の場合、空白を含むパスで引用符を使用する必要があります。

## <a name="remarks"></a>解説
 オート コンプリートでは、入力された正しいパスとファイル名の検索を試みます。

## <a name="example"></a>例
 この例では、Test1.sln というソリューションを開きます。

```
>File.OpenSolution "c:\MySolutions\Test1\Test1.sln"
```

## <a name="see-also"></a>関連項目
 [Visual Studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)の[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
