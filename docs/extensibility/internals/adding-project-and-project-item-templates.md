---
title: プロジェクトおよびプロジェクト項目テンプレートの追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 14eb1a9e2e63fa6e63d3ba2efa4426421e6b5593
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710206"
---
# <a name="add-project-and-project-item-templates"></a>プロジェクトおよびプロジェクト項目テンプレートの追加
独自のプロジェクトタイプを作成する場合は、標準[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]の統合開発環境 (IDE) ダイアログボックスを使用して、新しいプロジェクトおよびプロジェクト項目の追加をサポートする必要があります。 次のトピックでは、プロジェクトおよびプロジェクト項目を追加するためのさまざまな手法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクトコンテキスト](../../extensibility/internals/project-context.md)

 プロジェクトが環境内で起きるものに関するコンテキスト情報のほとんどを提供することを説明します。

- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)

 プロジェクト項目は、通常、どのプロジェクトを使用してアイテムを開くのかのあいまいさを避けるために、1 つのプロジェクトのメンバーであることを説明します。

- [その他のファイル プロジェクト](../../extensibility/internals/miscellaneous-files-project.md)

 プロジェクト内のファイルを開くために使用できる 2 種類のエディターと、プロジェクト項目を開いたときにどのエディターを使用するかを決定する際にプロジェクトが果たす役割について説明します。

- [プロジェクトおよび項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)

 プロジェクトの作成時に発生する[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]処理について説明します。

- [[新しい項目の追加] ダイアログ ボックスに項目を追加する](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 **[新しい項目**の追加] ダイアログ ボックスに項目を追加するプロセスについて説明します。

- [[新しいプロジェクト] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 VSPackage で使用できるカスタム テンプレートを含む新しいディレクトリを登録する例を示します。

- [[新しい項目の追加] ダイアログ ボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 [新しい項目の追加] ダイアログ ボックスのディレクトリの新しいセットを登録する例**を示**します。

- [プロジェクトシステムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 プロジェクト システムの拡張に使用されるさまざまな種類のコマンド項目を示します。

- [プロジェクトの拡張に通常使用されるオブジェクトの CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 プロジェクト システムの拡張[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]に使用されるオブジェクトの CATID[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]を[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]一覧表示します。

## <a name="related-sections"></a>関連項目
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクトの特定のエディターに固有の項目を開く手順について説明します。

- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)

 標準エディターを開く手順について説明します。

- [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)

 プロジェクト サブタイプの概念トピックへのリンクを示します。 プロジェクトのサブタイプは[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]、[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]既存のプロジェクトとプロジェクトを拡張します。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 新しいプロジェクトの種類のデザイン方法に関する情報を提供するその他のトピックへのリンクを示します。
