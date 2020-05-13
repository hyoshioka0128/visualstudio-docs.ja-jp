---
title: -Setup (devenv.exe) | Microsoft ドキュメント
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- setup Devenv switch
- /setup Devenv switch
- Devenv, /setup switch
ms.assetid: 87608b7f-a156-400c-80f5-fc823f843e61
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a923d1f3532548ebc6ed651a0739e0e5792f7967
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663532"
---
# <a name="setup-devenvexe"></a>/Setup (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用できるすべての VSPackages にある、メニュー、ツール バー、およびコマンド グループを記述したリソース メタデータが [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] により強制的にマージされます。

## <a name="syntax"></a>構文

```
devenv /setup
```

## <a name="remarks"></a>解説
 このスイッチは引数を取りません。 `devenv /setup` コマンドは、一般的にインストール処理の最後の手順として提示されます。 `/setup` スイッチを使用しても、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]は起動しません。

 `devenv` スイッチおよび [devenv](../../ide/reference/setup-devenv-exe.md) スイッチを使用するには、管理者として [devenv](../../ide/reference/installvstemplates-devenv-exe.md) を実行する必要があります。

## <a name="example"></a>例
 この例は、VSPackages が含まれるバージョンの [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] のインストールの最後の手順を示しています。

```
devenv /setup
```

## <a name="see-also"></a>関連項目
 [Devenv コマンド ライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
