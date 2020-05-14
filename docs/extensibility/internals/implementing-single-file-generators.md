---
title: 単一ファイル ジェネレーターの実装 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e700d09277edbb04b30676d3965b6c996d0a11f3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707654"
---
# <a name="implementing-single-file-generators"></a>単一ファイル ジェネレーターの実装
カスタム ツール (単一ファイル ジェネレーターとも呼ばれます) を使用して、 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]および プロジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]システムを で拡張できます。 カスタム ツールは、インターフェイスを実装する COM<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>コンポーネントです。 このインターフェイスを使用すると、カスタム ツールは 1 つの入力ファイルを 1 つの出力ファイルに変換します。 変換の結果は、ソース コード、または有用なその他の出力である可能性があります。 ツールによって生成されたカスタム コード ファイルの 2 つの例として、ビジュアル デザイナーの変更に応じて生成されるコードと、Web サービス記述言語 (WSDL) を使用して生成されたファイルがあります。

 カスタム ツールが読み込まれるか、入力ファイルが保存されると、プロジェクト システム<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A>はメソッドを呼び出し、<xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress>コールバック インターフェイスへの参照を渡します。

 カスタム ツールによって生成される出力ファイルが、入力ファイルに依存してプロジェクトに追加されます。 プロジェクト システムは、カスタム ツールの 実装によって返される文字列に基づいて、出力ファイルの<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A>名前を自動的に決定します。

 カスタム ツールは、インターフェイス<xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>を実装する必要があります。 オプションで、カスタム ツールは<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>、入力ファイル以外のソースから情報を取得するインターフェイスをサポートします。 いずれの場合も、カスタム ツールを使用する前に、システムまたはローカル レジストリに登録する[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]必要があります。 カスタム ツールの登録の詳細については、「[単一ファイル ジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ビジュアル デザイナーへのタイプの公開](../../extensibility/internals/exposing-types-to-visual-designers.md)
