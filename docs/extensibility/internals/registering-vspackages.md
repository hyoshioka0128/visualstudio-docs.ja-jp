---
title: Vspackage | を登録していますMicrosoft Docs
description: Pkgdef ファイルには、システムレジストリに追加される情報が含まれています。 Visual Studio が pkgdef ファイルを使用して VSPackage を記述/検索する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9e2ed8d7c376f7d9f23e06786fefc1a955ebea3a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069466"
---
# <a name="registering-vspackages"></a>VSPackage の登録
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、VSPackage を記述および検索するために、pkgdef ファイルに依存しています。 Pkgdef ファイルには、システムレジストリに追加されるすべての登録情報が含まれています。 マネージ Vspackage は、ソースコードに属性を追加し、結果のアセンブリで [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md) を実行して、pkgdef ファイルを生成することによって登録されます。

## <a name="in-this-section"></a>このセクションの内容
- [VSPackage ファイルの場所を VS Shell に指定する](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)

 Vspackage の読み込みパスについて説明します。

- [VSPackage の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)

 VSPackage を登録する方法について説明します。
