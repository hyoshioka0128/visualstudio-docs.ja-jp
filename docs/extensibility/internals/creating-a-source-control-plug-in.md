---
title: ソース管理プラグインを作成する |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) にソース管理機能を追加するソース管理プラグインを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 489aea2ba5b12dafa161ce70a49f81f60b38ba5d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99878761"
---
# <a name="create-a-source-control-plug-in"></a>ソース管理プラグインを作成する
Visual Studio SDK には、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) にソース管理機能を追加できるリソースが用意されています。 このドキュメントに記載されているソース管理プラグイン API に準拠している任意のプラグイン DLL を使用できます。

## <a name="in-this-section"></a>このセクションの内容
- [作業開始](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

 ソース管理プラグインをインストールする方法について説明し、現在使用可能なソース管理プラグイン API バージョンについて説明します。

- [アーキテクチャ](../../extensibility/internals/source-control-plug-in-architecture.md)

 アーキテクチャ図を使用して、ソース管理プラグインと IDE との統合について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [テストガイド](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

 ソース管理プラグインのインストールと操作のテスト方法に関するガイダンスを提供します。

## <a name="related-sections"></a>関連項目
- [ソース管理 VSPackage を作成する](../../extensibility/internals/creating-a-source-control-vspackage.md)

 ソース管理機能を提供するだけでなく、ソース管理 UI を置き換えるソース管理 VSPackage を作成する方法について説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。

- [ソース管理プラグイン](../../extensibility/source-control-plug-ins.md)

 ソース管理プラグイン API のすべての要素の完全な一覧を提供します。

- [ソース管理](../../extensibility/internals/source-control.md)

 の統合機能としてソース管理を実装するためのオプションについて説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。
