---
title: -Updateconfiguration (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /updateconfiguration Devenv switch
- Devenv, /updateconfiguration switch
- updateconfiguration Devenv switch
ms.assetid: 9a1084cc-8b68-4ccc-aaea-f95939164338
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 50773821b328ea81381744bc6f32b3907cd1c5bc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657914"
---
# <a name="updateconfiguration-devenvexe"></a>/Updateconfiguration (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] にシステム上の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] パッケージをマージさせ、MEF キャッシュに変更がないかを確認することを通知します。

## <a name="syntax"></a>構文

```
devenv /updateconfiguration
```

## <a name="remarks"></a>解説
 VSIX パッケージをインストールすると、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ではこのコマンドが自動的に実行されます。 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] が MEF キャッシュを更新するように、ファイルの修正プログラムを適用した後に `devenv.exe /updateconfiguration` を実行する必要があります。 これにより、修正が適切かどうかを評価することができます。

## <a name="example"></a>例
 次のコマンド ラインでは、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] にシステム上の [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] パッケージをマージさせ、MEF キャッシュに変更がないかを確認させます。

```
Devenv.exe /updateconfiguration
```

## <a name="see-also"></a>関連項目
 Visual Studio [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)[での開発設定のカスタマイズ](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)
