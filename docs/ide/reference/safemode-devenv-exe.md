---
title: -SafeMode (devenv.exe)
description: devenv の SafeMode コマンドライン スイッチを使用して Visual Studio をセーフ モードで起動し、既定の環境とサービスのみを読み込む方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /SafeMode Devenv switch
- Devenv, /SafeMode switch
- SafeMode switch
ms.assetid: b191f6a5-8f12-47ec-bcc7-b68149a22aa8
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1626776ec41bdbdfe5ad2b611516e62ada4f15a3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99957869"
---
# <a name="safemode-devenvexe"></a>/SafeMode (devenv.exe)

Visual Studio をセーフ モードで起動し、既定の環境とサービスのみを読み込みます。

## <a name="syntax"></a>構文

```shell
devenv /SafeMode
```

## <a name="remarks"></a>Remarks

このスイッチでは、Visual Studio が起動したときに、すべてのサード パーティ VSPackage を読み込まないようにするため、実行が安定したものになります。

## <a name="example"></a>例

次の例では、Visual Studio をセーフ モードで起動します。

```shell
devenv /safemode
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
