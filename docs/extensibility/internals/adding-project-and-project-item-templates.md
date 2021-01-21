---
title: プロジェクトおよびプロジェクト項目テンプレートの追加 |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) のダイアログボックスにプロジェクトおよびプロジェクト項目テンプレートを追加する方法について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 1e97b04294f0545c378210d39f343f3b009b6d15
ms.sourcegitcommit: b1b747063ce0bba63ad2558fa521b823f952ab51
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "96190175"
---
# <a name="add-project-and-project-item-templates"></a>プロジェクトおよびプロジェクト項目テンプレートの追加
独自のプロジェクトの種類を作成する場合は、標準の [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 統合開発環境 (IDE) のダイアログボックスを使用して、新しいプロジェクトとプロジェクト項目を追加するためのサポートを提供する必要があります。 次のトピックでは、プロジェクトおよびプロジェクト項目を追加するためのさまざまな手法について説明します。

## <a name="in-this-section"></a>このセクションの内容
- [プロジェクトのコンテキスト](../../extensibility/internals/project-context.md)

 環境内の発生に関するコンテキスト情報の大部分がプロジェクトによって提供されることについて説明します。

- [プロジェクトの優先順位](../../extensibility/internals/project-priority.md)

 プロジェクト項目は通常、1つのプロジェクトのメンバーであるため、項目を開くために使用されるプロジェクトがあいまいになるのを防ぐことができます。

- [その他のファイルプロジェクト](../../extensibility/internals/miscellaneous-files-project.md)

 プロジェクト内のファイルを開くために使用できる2種類のエディターに関する情報と、プロジェクト項目を開いたときに使用するエディターを決定するためにプロジェクトが果たす役割について説明します。

- [プロジェクトと項目テンプレートの登録](../../extensibility/internals/registering-project-and-item-templates.md)

 プロジェクトが作成されたときの動作について説明 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] します。

- [[新しい項目の追加] ダイアログボックスへの項目の追加](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 [ **新しい項目の追加** ] ダイアログボックスに項目を追加するプロセスについて説明します。

- [[新しいプロジェクト] ダイアログボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 VSPackage によって使用可能になったカスタムテンプレートを含む新しいディレクトリを登録する例を示します。

- [[新しい項目の追加] ダイアログボックスにディレクトリを追加する](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 [ **新しい項目の追加** ] ダイアログボックスに新しいディレクトリのセットを登録する例を示します。

- [プロジェクトシステムを拡張するための IDE 定義コマンド](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 プロジェクトシステムの拡張に使用されるさまざまな種類のコマンド項目を一覧表示します。

- [プロジェクトの拡張に通常使用されるオブジェクトの Catid](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 、、およびの各プロジェクトシステムを拡張するために使用されるオブジェクトの Catid の一覧を示し [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ます。

## <a name="related-sections"></a>関連項目
- [方法: プロジェクト固有のエディターを開く](../../extensibility/how-to-open-project-specific-editors.md)

 プロジェクトの特定のエディターに本質的にバインドされている項目を開く手順について説明します。

- [方法: 標準エディターを開く](../../extensibility/how-to-open-standard-editors.md)

 標準エディターを開く手順について説明します。

- [プロジェクトのサブタイプ](../../extensibility/internals/project-subtypes.md)

 プロジェクトのサブタイプの概念に関するトピックへのリンクを示します。 プロジェクトのサブタイプにより [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 、既存のプロジェクトとプロジェクトが拡張さ [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] れます。

- [プロジェクトの種類](../../extensibility/internals/project-types.md)

 新しいプロジェクトの種類をデザインする方法に関する情報を提供するその他のトピックへのリンクを示します。
