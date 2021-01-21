---
title: プロジェクトの拡張 |Microsoft Docs
description: Visual Studio SDK で独自のカスタムプロジェクトの種類を作成する方法と、さまざまな種類の Visual Studio ソリューションを管理する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- projects [Visual Studio]
ms.assetid: 096d273d-4fe9-4f24-9b00-470bfbdf4bdf
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 181acea9a5188ba28a4ef109b5bec0e7c040b5da
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96994616"
---
# <a name="extend-projects"></a>プロジェクトの拡張
プロジェクトとソリューションは、Visual Studio がコードとリソースファイルをコンパイルおよび配置単位に整理する方法です。 プロジェクトの詳細については、 [「プロジェクト (Visual STUDIO SDK)](../extensibility/extending-projects.md)」を参照してください。

 独自のプロジェクトの種類を作成するには、Visual Studio SDK とプロジェクト用の Managed Package Framework を使用します。これは、 [プロジェクトのマネージパッケージフレームワーク](https://github.com/tunnelvisionlabs/MPFProj10)でダウンロードできます。 カスタムプロジェクトの実装方法を理解するには、「 [新しいプロジェクトの生成: 内部](../extensibility/internals/new-project-generation-under-the-hood-part-one.md) では、パート1と [新しいプロジェクトの生成: 内部ではパート 2](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 このセクションのトピックでは、カスタムプロジェクトを作成する方法と、さまざまな種類の Visual Studio ソリューションを管理する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [基本プロジェクトシステムを作成する (第1部)](../extensibility/creating-a-basic-project-system-part-1.md) カスタムプロジェクトシステムを作成する方法について説明します。

- [基本的なプロジェクトシステムを作成する (第2部)](../extensibility/creating-a-basic-project-system-part-2.md) カスタムプロジェクトシステムを作成する方法について説明します。

- [プロジェクトファイルにデータを保存](../extensibility/saving-data-in-project-files.md) するをプロジェクトに追加する方法について説明<em>します (.</em>proj *) ファイル。

- [実行時にプロジェクトのサブタイプを確認する](../extensibility/verifying-subtypes-of-a-project-at-run-time.md) 実行時にプロジェクトのサブタイプを確認する方法について説明します。

- [プロパティページの追加と削除](../extensibility/adding-and-removing-property-pages.md) カスタムプロジェクトのプロパティページをカスタマイズする方法について説明します。

- [プロジェクト項目に属性を追加する](../extensibility/adding-an-attribute-to-a-project-item.md) カスタムプロジェクト項目に属性を追加する方法について説明します。

- [プロジェクト項目のプロパティを保持する](../extensibility/persisting-the-property-of-a-project-item.md) カスタムプロジェクト項目のプロパティを永続化する方法について説明します。

- [ユニバーサル Windows プロジェクトを管理](../extensibility/managing-universal-windows-projects.md) するユニバーサルプロジェクトを管理する方法について説明します。
