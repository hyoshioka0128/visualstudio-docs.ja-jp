---
title: Vspackage | を登録していますMicrosoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80705745"
---
# <a name="registering-vspackages"></a>VSPackage の登録
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、VSPackage を記述および検索するために、pkgdef ファイルに依存しています。 Pkgdef ファイルには、システムレジストリに追加されるすべての登録情報が含まれています。 マネージ Vspackage は、ソースコードに属性を追加し、結果のアセンブリで [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md) を実行して、pkgdef ファイルを生成することによって登録されます。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackage ファイルの場所を VS Shell に指定する](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 Vspackage の読み込みパスについて説明します。

- [VSPackage の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)

 VSPackage を登録する方法について説明します。
