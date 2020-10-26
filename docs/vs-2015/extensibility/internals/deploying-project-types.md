---
title: プロジェクトの種類の配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], managed-code
- projects [Visual Studio SDK], aggregator
ms.assetid: 7f132f67-8589-464c-90dc-0d57ae02aa8f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0fda84d5f7467a65b254d3b12b0466b6ab415d61
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196879"
---
# <a name="deploying-project-types"></a>プロジェクト タイプの配置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] 新しいプロジェクトタイプアグリゲーター (ProjectAggregator2.dll) と、再配布用の Windows インストーラーパッケージ (ProjectAggregator2.msi) をインストールします。 マネージコードプロジェクトの種類には、新しいアグリゲーターを使用する必要があります。 ProjectAggregator2 は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] マネージコードプロジェクトの種類が正しく動作しないようにするプロジェクトアグリゲーターの制限事項を回避します。 次の手順では、新しいアグリゲーターを使用するように VSPackage を変更する方法について説明します。  
  
1. ソリューションから NativeHierarchyWrapper プロジェクトを削除します。  
  
2. セットアップから NativeHierarchyWrapper バイナリを削除します。  
  
3. セットアップに ProjectAggregator2.msi を追加します。
