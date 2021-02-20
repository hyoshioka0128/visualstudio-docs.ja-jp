---
title: プロジェクトの種類の配置 |Microsoft Docs
description: Visual Studio SDK で、新しいプロジェクトタイプアグリゲーターと再配布用の Windows インストーラーパッケージを使用して、マネージコードプロジェクトの種類を配置する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e717064318372b31e13d97381ee03d5986a9de2e
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965318"
---
# <a name="deploy-project-types"></a>プロジェクトの種類の配置
[!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 新しいプロジェクトタイプアグリゲーター (*ProjectAggregator2.dll*) と、再配布用の Windows インストーラーパッケージ (*ProjectAggregator2.msi*) をインストールします。 マネージコードプロジェクトの種類には、新しいアグリゲーターを使用する必要があります。 ProjectAggregator2 は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] マネージコードプロジェクトの種類が正しく動作しないようにするプロジェクトアグリゲーターの制限に対処します。 次の手順では、新しいアグリゲーターを使用するように VSPackage を変更する方法について説明します。

1. ソリューションから NativeHierarchyWrapper プロジェクトを削除します。

2. セットアップから NativeHierarchyWrapper バイナリを削除します。

3. セットアップに *ProjectAggregator2.msi* を追加します。
