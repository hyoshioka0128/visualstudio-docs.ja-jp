---
title: ソース管理のサポート |マイクロソフトドキュメント
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
ms.openlocfilehash: 84de3120783528d209b1475477aee5087edac42b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704731"
---
# <a name="supporting-source-control"></a>ソース管理のサポート
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、プロジェクトまたはエディターのファイルチェックアウト、チェックイン、およびその他のソース管理操作がサポートされています。 ソース管理クライアントは、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]動的に定義されたファイルのセットのアーカイブ、バージョン管理、[!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)]および制御機能を提供する などのソース管理パッケージと対話するように設計されています。

## <a name="in-this-section"></a>このセクションの内容
- [ソース管理パッケージのモデル](../../extensibility/internals/model-for-source-control-packages.md)

 ソース管理をサポートするためにプロジェクトの種類が実装する必要があるインターフェイスについて説明します。

- [設計の決定](../../extensibility/internals/source-control-design-decisions.md)

 プロジェクトの種類の実装方法を変更する回答を示す質問を示します。

- [構成の詳細](../../extensibility/internals/source-control-configuration-details.md)

 ソース管理のサポートによってプロジェクトの種類の実装がどのように変わるかについて説明します。

- [プロジェクトとエディターに関する追加のガイドライン](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)

 プロジェクトの種類とエディターのベスト プラクティスについて説明します。

- [ランタイムの詳細](../../extensibility/internals/source-control-runtime-details.md)

 ユーザーがプロジェクトをソース管理システムに追加するときに、プロジェクトを登録する方法について説明します。

## <a name="reference"></a>リファレンス
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>ファイルがメモリ内で変更または保存されることを環境またはソース管理パッケージに示します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>プロジェクトと階層がソース管理に登録し、ソース管理の状態に関する情報を取得できるようにします。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>プロジェクト ファイルおよびプロジェクト項目のソース管理を提供するプロジェクト システムに実装されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>ソリューション内のファイルまたはディレクトリを追加、削除、または名前変更するためのアクセス許可を環境に問い合わせるためにプロジェクトによって使用されます。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>プロジェクト ファイルまたはディレクトリに加えられた変更をクライアントに通知します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 統合開発環境 (IDE) の基本的な構成要素としての[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]プロジェクトの概要を説明します。 プロジェクトがコードのビルドとコンパイルを制御する方法を説明する追加のトピックへのリンクが提供されています。
