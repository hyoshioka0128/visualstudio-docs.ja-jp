---
title: プロジェクトタイプの配置 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 835e85ade4d309d0b5692aa9b857476cd6b5927a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708783"
---
# <a name="deploy-project-types"></a>プロジェクトの種類の配置
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]新しいプロジェクトタイプのアグリゲータ *(ProjectAggregator2.dll)* と再配布用の Windows インストーラ パッケージ (*ProjectAggregator2.msi*) がインストールされます。 マネージ コード プロジェクトの種類には、新しいアグリゲータを使用する必要があります。 ProjectAggregator2 は、マネージ コード[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトの種類が正しく動作しないようにするプロジェクト アグリゲータの制限を回避します。 次の手順では、VSPackage を変更して新しいアグリゲーターを使用する方法について説明します。

1. ソリューションからネイティブ階層ラッパー プロジェクトを削除します。

2. セットアップから任意のネイティブ階層ラッパー バイナリを削除します。

3. *セットアップにプロジェクトアグリゲータ2.msi*を追加します。
