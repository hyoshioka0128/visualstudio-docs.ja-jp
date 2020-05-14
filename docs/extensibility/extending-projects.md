---
title: プロジェクトの拡張 |マイクロソフトドキュメント
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
ms.openlocfilehash: 14108a304cc5f85c9a870bc66804df7daa98f3ca
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711752"
---
# <a name="extend-projects"></a>プロジェクトの拡張
プロジェクトとソリューションは、Visual Studio がコードファイルとリソース ファイルをコンパイル単位と配置単位に編成する方法です。 プロジェクトの詳細については、「[プロジェクト (Visual Studio SDK)」](../extensibility/extending-projects.md)を参照してください。

 Visual Studio SDK とマネージ パッケージ フレームワーク (マネージ パッケージ フレームワークでプロジェクト用) を使用して独自[のプロジェクトの種類を](https://github.com/tunnelvisionlabs/MPFProj10)作成できます。 カスタム プロジェクトの実装方法を理解するには、「[新しいプロジェクト生成: ボンネットの下で、パート 1](../extensibility/internals/new-project-generation-under-the-hood-part-one.md)と[新しいプロジェクト生成: ボンネットの下で、パート 2](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 このセクションのトピックでは、カスタム プロジェクトを作成する方法と、さまざまな種類の Visual Studio ソリューションを管理する方法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [基本プロジェクト システムの作成、パート 1](../extensibility/creating-a-basic-project-system-part-1.md)カスタム プロジェクト システムを作成する方法について説明します。

- [基本プロジェクト システムの作成、パート 2](../extensibility/creating-a-basic-project-system-part-2.md)カスタム プロジェクト システムを作成する方法について説明します。

- [プロジェクト ファイルにデータを保存する](../extensibility/saving-data-in-project-files.md)プロジェクトに追加する方法について説明します (<em>.</em>proj*) ファイル。

- [実行時にプロジェクトのサブタイプを確認する](../extensibility/verifying-subtypes-of-a-project-at-run-time.md)実行時にプロジェクトのサブタイプを検証する方法について説明します。

- [プロパティ ページの追加と削除](../extensibility/adding-and-removing-property-pages.md)カスタム プロジェクトのプロパティ ページをカスタマイズする方法について説明します。

- [プロジェクト項目に属性を追加する](../extensibility/adding-an-attribute-to-a-project-item.md)カスタム プロジェクト項目に属性を追加する方法について説明します。

- [プロジェクト項目のプロパティを永続化する](../extensibility/persisting-the-property-of-a-project-item.md)カスタム プロジェクト項目のプロパティを永続化する方法について説明します。

- [ユニバーサル Windows プロジェクトの管理](../extensibility/managing-universal-windows-projects.md)ユニバーサル プロジェクトを管理する方法について説明します。
