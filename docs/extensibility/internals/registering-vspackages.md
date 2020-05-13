---
title: VS パッケージの登録 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b40793a5ab317b6a467e55df13302f19cec82640
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705745"
---
# <a name="registering-vspackages"></a>VSPackage の登録
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を記述し、VS パッケージを検索するのに .pkgdef ファイルに依存します。 pkgdef ファイルには、システム レジストリに追加される登録情報がすべて含まれています。 マネージ VSPackages は、ソース コードに属性を追加し、結果のアセンブリで[CreatePkgDef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md)を実行して .pkgdef ファイルを生成することで登録されます。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackage ファイルの場所を VS Shell に指定する](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 VSPackages の読み込みパスについて説明します。

- [VSPackage の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)

 VS パッケージを登録する方法について説明します。
