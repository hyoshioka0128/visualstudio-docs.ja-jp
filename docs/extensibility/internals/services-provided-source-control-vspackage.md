---
title: 提供されるサービス (ソース管理 VSPackage) |Microsoft Docs
description: Vspackage がサービスを通じてどのように共有するかを説明します。これには、Visual Studio IDE とその Vspackage との対話が含まれます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: fe1d9ee9805e6e86595f3f7f3cf640114c7030b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080815"
---
# <a name="services-provided-source-control-vspackage"></a>提供されるサービス (ソース管理 VSPackage)
サービスは、Vspackage 間、および Visual Studio 統合開発環境 (IDE) とインストールされている Vspackage の間で機能を共有するための主要なメカニズムです。 Visual Studio IDE におけるサービスとその重要度の詳細については、「[サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。

## <a name="the-source-control-service"></a>ソース管理サービス
 Visual Studio には、IDE レベルのサービスとパッケージレベルのサービスの2つの層が用意されています。 IDE レベルのサービスは、Visual Studio IDE によってネイティブに提供されます。 ソース管理パッケージは、これらのサービスの一部を消費します。 VSPackage としてのソース管理パッケージは、独自のソース管理サービスを提供することによって、ソース管理機能を共有します。 ソース管理パッケージは、Visual Studio IDE で使用できるコントラクトの形式で、このによって実装されたソース管理関連のインターフェイスのセットをカプセル化します。

## <a name="see-also"></a>こちらもご覧ください
- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
