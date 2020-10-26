---
title: -Diff | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 5377fedb-632a-4e86-a947-7c11c86451e7
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fd76b0803f43a7694ec0d689eeb8489f491f8464
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657759"
---
# <a name="diff"></a>/Diff
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

2 つのファイルを比較します。 相違点は特殊な Visual Studio のウィンドウに表示されます。

## <a name="syntax"></a>構文

```
devenv /Diff SourceFile, TargetFile, [SourceDisplayName],[TargetDisplayName]
```

## <a name="arguments"></a>引数
 `SourceFile` 必須。 比較する最初のファイルの完全パスと名前。

 `TargetFile` 必須。 比較する 2 番目のファイルの完全パスと名前。

 `SourceDisplayName` 省略可能。 最初のファイルの表示名。

 `TargetDisplayName` 省略可能。 2 番目のファイルの表示名。
