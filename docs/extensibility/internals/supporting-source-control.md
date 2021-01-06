---
title: サポートソース管理 |Microsoft Docs
description: Visual Studio がプロジェクトまたはエディターのファイルのチェックアウト、チェックイン、およびその他のソース管理操作をサポートする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e722770ad1db4b85dbc2a5a8754d9158b6ee436
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876455"
---
# <a name="supporting-source-control"></a>ソース管理のサポート
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] では、プロジェクトまたはエディターのファイルのチェックアウト、チェックイン、およびその他のソース管理操作がサポートされています。 ソース管理クライアントとして、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] は、 [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] 動的に定義された一連のファイルのアーカイブ、バージョン管理、および制御機能を提供する、などのソース管理パッケージと対話するように設計されています。

## <a name="in-this-section"></a>このセクションの内容
- [ソース管理パッケージのモデル](../../extensibility/internals/model-for-source-control-packages.md)

 ソース管理をサポートするためにプロジェクトの種類で実装する必要があるインターフェイスについて説明します。

- [設計上の決定](../../extensibility/internals/source-control-design-decisions.md)

 プロジェクトの種類の実装方法が変更されたことについて質問します。

- [構成の詳細](../../extensibility/internals/source-control-configuration-details.md)

 ソース管理のサポートによってプロジェクトの種類の実装がどのように変更されるかについて説明します。

- [プロジェクトとエディターに関する追加のガイドライン](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)

 プロジェクトの種類とエディターのベストプラクティスについて説明します。

- [ランタイムの詳細](../../extensibility/internals/source-control-runtime-details.md)

 ユーザーがプロジェクトをソース管理システムに追加するときにプロジェクトを登録する方法について説明します。

## <a name="reference"></a>リファレンス
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> ファイルがメモリ内で変更されようとしているか、保存されていることを環境またはソース管理パッケージに示します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> プロジェクトと階層がソース管理に自身を登録し、ソース管理の状態に関する情報を取得できるようにします。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> プロジェクトファイルおよびプロジェクト項目のソース管理を提供するために、プロジェクトシステムに実装されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> ソリューション内のファイルまたはディレクトリを追加、削除、または名前変更するためのアクセス許可を環境に照会するために、プロジェクトによって使用されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> プロジェクトファイルまたはディレクトリに加えられた変更をクライアントに通知します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 プロジェクトの概要を [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE: integrated development environment) の基本的な構成要素として提供します。 プロジェクトがコードのビルドとコンパイルを制御する方法について説明する追加のトピックへのリンクが用意されています。
