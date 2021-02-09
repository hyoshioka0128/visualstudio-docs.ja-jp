---
title: 階層と選択 |Microsoft Docs
description: Visual Studio がプロジェクトなどの階層を処理する方法と、選択コンテキストを使用してユーザーに表示される内容を判断する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, hierarchies
- selection
- hierarchies
ms.assetid: cad0a859-7a84-4ce5-b0a9-f7f64e5f8ebb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 98f3dcfa73387f2b90ed829df198d3e9f0ccb2ed
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99880055"
---
# <a name="hierarchies-and-selection"></a>階層と選択
をカスタマイズするときは [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、がプロジェクトなどの [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 階層をどのように処理するか、およびユーザーに表示される内容を判断するために選択コンテキストを使用する方法を理解しておく必要があります。 ここでは、階層と選択の概念について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

## <a name="in-this-section"></a>このセクションの内容
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)

 プロジェクト階層と、階層の一般的な概念について説明します。

- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE: integrated development environment) がユーザーの現在アクティブなオブジェクトについての情報をどのように維持し、vspackage track の通貨を使用するかについて説明します。

- [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)

 ウィンドウに対するユーザーの選択コンテキストフォーカスを判断する方法のモデルについて説明します。

- [ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)

 の使用可能な機能 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] が、ユーザーの現在の選択コンテキストと IDE コンテキスト全体にどのように基づいているかについて説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類のアーキテクチャ](../../extensibility/internals/project-types-architecture.md)

 プロジェクトの種類に関する詳細な技術情報を提供します。
