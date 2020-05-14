---
title: 提供されるサービス (ソース管理 VS パッケージ) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, source control packages
- source control packages, services
ms.assetid: 9db07d70-87d2-4401-bc88-e3a49d81e9a2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f08ebe49756b442ef474ac2a032a72894f6bec15
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705406"
---
# <a name="services-provided-source-control-vspackage"></a>提供されるサービス (ソース管理 VSPackage)
サービスは、機能が VSPackage 間で共有され、Visual Studio 統合開発環境 (IDE) とそのインストール済み VSPackages 間で共有される主要なメカニズムです。 Visual Studio IDE におけるサービスとその重要性の詳細については、「[サービスの使用と提供](../../extensibility/using-and-providing-services.md)」を参照してください。

## <a name="the-source-control-service"></a>ソース管理サービス
 Visual Studio には、IDE レベルのサービスとパッケージ レベルのサービスという 2 つの層のサービスが用意されています。 ネイティブでは、IDE レベルのサービスを提供します。 ソース管理パッケージは、これらのサービスの一部を消費します。 VSPackage としてのソース管理パッケージは、独自のプライベート ソース管理サービスを提供することによって、ソース管理機能を共有します。 ソース管理パッケージは、Visual Studio IDE で使用できるコントラクトの形式で、ソース管理関連のインターフェイスのセットをカプセル化します。

## <a name="see-also"></a>関連項目
- [デザイン要素](../../extensibility/internals/source-control-vspackage-design-elements.md)
