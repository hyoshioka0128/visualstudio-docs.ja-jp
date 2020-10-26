---
title: Configuration オブジェクトと SelectedItem オブジェクトのオートメーション |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], SelectedItem object
- automation [Visual Studio SDK], builds
ms.assetid: 120377f1-51aa-4445-b2f7-06ab7fc2b47f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0341cdf56b32b8b1ac77104b3f3e813ae0610767
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709969"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>構成オブジェクトと SelectedItem オブジェクトのオートメーション

Visual Studio では、ビルドと選択された項目プロセスを自動化できます。

## <a name="automation-for-builds"></a>ビルドの自動化

ビルドまたは構成には、を実装するときに提供されるオートメーションモデルがあり <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider> ます。 詳しくは、「[ビルド構成について](../../ide/understanding-build-configurations.md)」をご覧ください。

VSPackage を作成し、構成オプションを制御する場合は、オートメーションモデルを使用する必要があります。

## <a name="automation-for-selecteditem"></a>SelectedItem の Automation

`SelectedItem`Visual Studio には標準の実装が含まれているため、オブジェクトの実装を指定する必要はありません。 ただし、必要に応じてオブジェクトを実装することもでき `SelectedItem` ます。 インターフェイスを含むオブジェクトを実装し、 `SelectedItem` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A> を __VSHPROPID に設定して、メソッドへの呼び出しに対する応答を返す必要があり `VSITEMID` [ます。VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>)。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [オートメーションモデルに貢献する](../../extensibility/internals/contributing-to-the-automation-model.md)
- [ビルド構成について](../../ide/understanding-build-configurations.md)
