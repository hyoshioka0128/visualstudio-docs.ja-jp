---
title: カスタム ツール |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e60f1d8cb8b25ed50b0b20c5ebb538286687ad72
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708960"
---
# <a name="custom-tools"></a>カスタム ツール
*カスタム ツール*を使用すると、ツールをプロジェクト内の項目に関連付け、ファイルが保存されるたびにそのツールを実行できます。 一部のカスタム ツールは *、単一ファイル ジェネレーター*とも呼ばれますが、データからコードを生成するトランスレータを実装するためによく使用されます。 たとえば、単一ファイル ジェネレーターは[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]*、.settings*ファイルと[!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] *.resx*ファイルからコードを作成およびソース化します。 生成されたソース コードは *、.settings*ファイルと *.resx*ファイル内のデータに厳密に型指定されたアクセスを提供します。 および[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)][!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)]プロジェクトの種類は、カスタム ツールをサポートします。[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]プロジェクトの種類は使用しません。 独自のプロジェクトの種類は、カスタム ツールもサポートできます。

 カスタム ツールは、インターフェイスを実装`IVsSingleFileGenerator`する登録済みコンポーネントです。

 カスタム ツールは、インターフェイス`ProjectItem`オブジェクトに関連付けられており、デザイナーやエディターと同様です。 カスタム ツールは、 a で`ProjectItem`表されるファイルを入力として受け取り、メソッドによってファイル`DefaultExtension`名が指定された新しいファイルを書き込みます。

## <a name="in-this-section"></a>このセクションの内容
- [単一ファイル ジェネレーターの実装](../../extensibility/internals/implementing-single-file-generators.md)

 インターフェイスを使用してカスタム<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>ツールを実装する方法について説明します。

- [単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)

 カスタム ツールのすべてのレジストリ エントリについて説明します。

- [ビジュアル デザイナーに型を公開する](../../extensibility/internals/exposing-types-to-visual-designers.md)

 プロジェクト システムが、生成されたクラスおよび型に一時ポータブル実行可能 (PE) ファイルを介してアクセスするビジュアル デザイナーをサポートする方法について説明します。

- [プロジェクト項目のプロパティを永続化する](../../extensibility/persisting-the-property-of-a-project-item.md)

 ソース ファイルの作成者など、プロジェクト項目のプロパティをプロジェクト ファイルに永続化する方法について説明します。

## <a name="reference"></a>リファレンス
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>単一の<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>入力ファイルを、コンパイルまたはプロジェクトに追加できる単一の出力ファイルに変換する、 の詳細を提供します。

 <xref:EnvDTE.ProjectItem>プロジェクト内`ProjectItem`の項目を表すインターフェイスについて説明します。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>出力ファイル名に`DefaultExtension`指定されたファイル名拡張子を取得するメソッドの詳細を提供します。

## <a name="related-sections"></a>関連項目
- [プロジェクトの拡張](../../extensibility/extending-projects.md)

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
