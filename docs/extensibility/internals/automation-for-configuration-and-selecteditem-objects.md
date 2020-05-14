---
title: 構成オブジェクトと選択項目オブジェクトの自動化 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709969"
---
# <a name="automation-for-configuration-and-selecteditem-objects"></a>構成オブジェクトと SelectedItem オブジェクトのオートメーション

Visual Studio でビルドおよび選択した項目のプロセスを自動化できます。

## <a name="automation-for-builds"></a>ビルドの自動化

ビルドまたは構成には、 を実装<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider>するときに提供されるオートメーション モデルがあります。 詳しくは、「[ビルド構成について](../../ide/understanding-build-configurations.md)」をご覧ください。

VSPackage を作成し、構成オプションを制御する場合は、オートメーション モデルを使用する必要があります。

## <a name="automation-for-selecteditem"></a>選択されたアイテムのオートメーション

Visual Studio には標準の実装が含`SelectedItem`まれているため、オブジェクトの実装を提供する必要はありません。 ただし、必要に応じて`SelectedItem`オブジェクトを実装できます。 `SelectedItem`インターフェイスを含むオブジェクトを実装し、__VSHPROPIDに設定された<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>`VSITEMID`メソッドの呼び出しに応答を返す必要があります[。VSHPROPID_ExtSelectedItem](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtSelectedItem>).

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.GetPropertyPage%2A>
- [オートメーションモデルへの貢献](../../extensibility/internals/contributing-to-the-automation-model.md)
- [ビルド構成について](../../ide/understanding-build-configurations.md)
