---
title: カスタムツール |Microsoft Docs
description: Visual Studio でカスタムツールを作成する方法について説明します。このツールは、プロジェクト内の項目にツールを関連付け、ファイルが保存されるたびにそのツールを実行します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7fdadad602a256b4740b4c4204704ca73864d612
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903022"
---
# <a name="custom-tools"></a>カスタム ツール
*カスタムツール* を使用すると、プロジェクト内の項目にツールを関連付け、ファイルが保存されるたびにそのツールを実行できます。 特定のカスタムツール ( *単一ファイルジェネレーター* と呼ばれることもあります) は、データからコードを生成したり、その逆の変換を行ったりするために頻繁に使用されます。 たとえば、単一ファイルジェネレーターは、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] *設定* ファイルと *.resx* ファイルからソースコードを作成します。 生成されたソースコードは、 *設定* ファイルおよび *.resx* ファイル内のデータへの厳密に型指定されたアクセスを提供します。 およびプロジェクトの種類では、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] カスタムツールがサポート [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] されます。プロジェクトの種類には対応していません。 独自のプロジェクトの種類で、カスタムツールをサポートすることもできます。

 カスタムツールは、インターフェイスを実装する登録済みのコンポーネントです `IVsSingleFileGenerator` 。

 カスタムツールはインターフェイスオブジェクトに関連付けられて `ProjectItem` おり、デザイナーやエディターに似ています。 カスタムツールは、によって表されるファイルを `ProjectItem` 入力として受け取り、そのファイル名がメソッドによって提供される新しいファイルを書き込み `DefaultExtension` ます。

## <a name="in-this-section"></a>このセクションの内容
- [単一ファイルジェネレーターを実装する](../../extensibility/internals/implementing-single-file-generators.md)

 インターフェイスを使用してカスタムツールを実装する方法について説明し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> ます。

- [1つのファイルジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)

 カスタムツールのすべてのレジストリエントリについて説明します。

- [ビジュアルデザイナーに型を公開する](../../extensibility/internals/exposing-types-to-visual-designers.md)

 プロジェクトシステムが、生成されたクラスと型に一時的なポータブル実行可能 (PE) ファイルを介してアクセスするためのサポートを提供する方法について説明します。

- [プロジェクト項目のプロパティを保持する](../../extensibility/persisting-the-property-of-a-project-item.md)

 ソースファイルの作成者などのプロジェクト項目のプロパティをプロジェクトファイルに保存する方法について説明します。

## <a name="reference"></a>リファレンス
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator><xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>1 つの入力ファイルをコンパイルしたりプロジェクトに追加したりできる1つの出力ファイルに変換する、の詳細について説明します。

 <xref:EnvDTE.ProjectItem>`ProjectItem`プロジェクト内の項目を表すインターフェイスについて説明します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>`DefaultExtension`出力ファイル名に指定されたファイル名拡張子を取得するメソッドについて詳しく説明します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの拡張](../../extensibility/extending-projects.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
