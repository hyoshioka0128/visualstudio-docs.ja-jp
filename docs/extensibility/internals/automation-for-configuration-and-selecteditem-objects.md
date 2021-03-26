---
title: Configuration オブジェクトと SelectedItem オブジェクトのオートメーション |Microsoft Docs
description: シェル相互運用機能の Configuration オブジェクトと SelectedItem オブジェクトを使用して、Visual Studio のビルドおよび選択された項目のプロセスを自動化する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f6e7f153e7d5b32e54cc51e3b7af06f14545cea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086262"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>構成オブジェクトと SelectedItem オブジェクトのオートメーション

Visual Studio では、ビルドと選択された項目プロセスを自動化できます。

## <a name="automation-for-builds"></a>ビルドの自動化

ビルドまたは構成には、を実装するときに提供されるオートメーションモデルがあり <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> ます。 詳しくは、「[ビルド構成について](../../ide/understanding-build-configurations.md)」をご覧ください。

VSPackage を作成し、構成オプションを制御する場合は、オートメーションモデルを使用する必要があります。

## <a name="automation-for-selecteditem"></a>SelectedItem の Automation

`SelectedItem`Visual Studio には標準の実装が含まれているため、オブジェクトの実装を指定する必要はありません。 ただし、必要に応じてオブジェクトを実装することもでき `SelectedItem` ます。 インターフェイスを含むオブジェクトを実装し、 `SelectedItem` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> を __VSHPROPID に設定して、メソッドへの呼び出しに対する応答を返す必要があり `VSITEMID` [ます。VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>)。

## <a name="see-also"></a>こちらもご覧ください

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [オートメーションモデルに貢献する](../../extensibility/internals/contributing-to-the-automation-model.md)
- [ビルド構成について](../../ide/understanding-build-configurations.md)
