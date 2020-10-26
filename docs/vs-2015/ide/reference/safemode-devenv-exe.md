---
title: -SafeMode (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /SafeMode Devenv switch
- Devenv, /SafeMode switch
- SafeMode switch
ms.assetid: b191f6a5-8f12-47ec-bcc7-b68149a22aa8
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 28480399238c1c915056d3929f8fd188cfff7eca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665511"
---
# <a name="safemode-devenvexe"></a>/SafeMode (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] をセーフ モードで起動し、既定の環境とサービスのみを読み込みます。

## <a name="syntax"></a>構文

```
devenv /SafeMode
```

## <a name="remarks"></a>解説
 このスイッチでは、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] が起動したときに、すべてのサード パーティ VSPackage を読み込まないようにするため、実行が安定したものになります。

## <a name="description"></a>説明
 次の例では、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] をセーフ モードで起動します。

## <a name="code"></a>コード

```
Devenv.exe /SafeMode
```

## <a name="see-also"></a>参照
 [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)
