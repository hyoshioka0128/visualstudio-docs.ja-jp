---
title: メニューとツールバーのコマンドを最適化する |Microsoft Docs
description: Vspackage とそれに対応するコマンドを追加して、Visual Studio がコマンドの混乱を最小限に抑える方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], menus
- commands [Visual Studio], toolbars
- menus [Visual Studio SDK], commands
- menu commands, implementing
- toolbars [Visual Studio], commands
ms.assetid: 8385f1a6-1e98-4dca-83d2-fcbed7177242
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b35f3a87f819885685b54888031883f4c2776d04
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877599"
---
# <a name="optimizing-menu-and-toolbar-commands"></a>メニュー、ツール バー コマンドの最適化
Vspackage とそれに対応するコマンドが追加されると、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI が混雑する可能性があります。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI コマンドの混乱を最小限に抑える方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [コマンドを使用可能にする](../../extensibility/internals/making-commands-available.md)

 Vspackage を追加するときに UI の crowding を最小限に抑えるための一般的なガイドラインについて説明 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

- [配置のガイドライン](../../extensibility/internals/command-placement-guidelines.md)

 コマンドセットのサイズに従って VSPackage を実装するための特定のガイドラインを提供します。

## <a name="related-sections"></a>関連項目
- [コマンド、メニュー、およびツール バー](../../extensibility/internals/commands-menus-and-toolbars.md)

 メニュー、ツール バー、およびコマンド コンボ ボックスが含まれている UI を作成する方法について説明します。
