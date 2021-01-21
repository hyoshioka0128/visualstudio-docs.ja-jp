---
title: Visual Studio のその他の部分の拡張 |Microsoft Docs
description: 拡張できる Visual Studio UI の部分について説明します。 VSPackage を作成し、アクティビティログに書き込み、ツールボックスとステータスバーを拡張することができます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces
ms.assetid: 27d2f1e1-2503-4aca-9cfc-707abd07ccf0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7cc9a471b141cfd3302814844d63a2ce8d5b74c6
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96995838"
---
# <a name="extend-other-parts-of-visual-studio"></a>Visual Studio の他の部分を拡張する

拡張できる Visual Studio UI には、さらに多くの部分があります。 ここでは、ほんの一部を紹介します。

## <a name="create-a-vspackage"></a>VSPackage を作成する

Visual Studio 拡張機能の基本的な構成要素は Vspackage です。  VSPackage を追加する方法につい[ては、VSPackage を使用した拡張機能の作成に関する](../extensibility/creating-an-extension-with-a-vspackage.md)ページを参照してください。

## <a name="extend-the-toolbox"></a>ツールボックスの拡張

新しいコントロールやその他の項目をツールボックスに追加する方法と、ツールボックス機能の使用方法について説明します。

- [WPF ツールボックスコントロールの作成](../extensibility/creating-a-wpf-toolbox-control.md)

- [Windows フォームツールボックスコントロールを作成する](../extensibility/creating-a-windows-forms-toolbox-control.md)

## <a name="extend-the-status-bar"></a>ステータスバーを拡張する

ステータスバーと進行状況バーの読み取りと書き込みを行う方法、およびアニメーションとその他の UI を提供する方法について説明します。 [ステータスバーを拡張](../extensibility/extending-the-status-bar.md)します。

::: moniker range="vs-2017"

## <a name="create-custom-start-pages"></a>カスタムスタートページを作成する

独自のスタートページを作成する方法については、「最初から、またはダウンロード可能なスタートページのサンプル: [カスタムスタートページを作成](../extensibility/creating-a-custom-start-page.md)する」を参照してください。

::: moniker-end

## <a name="write-to-the-activity-log"></a>アクティビティログへの書き込み

アクティビティログへの書き込み方法については、「 [方法: アクティビティログを使用](../extensibility/how-to-use-the-activity-log.md)する」を参照してください。
