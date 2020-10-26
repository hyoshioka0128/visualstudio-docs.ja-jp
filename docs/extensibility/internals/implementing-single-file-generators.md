---
title: 単一ファイルジェネレーターの実装 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707654"
---
# <a name="implementing-single-file-generators"></a>単一ファイル ジェネレーターの実装
カスタムツール (単一ファイルジェネレーターと呼ばれることもあります) を使用して、 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] のおよびプロジェクトシステムを拡張でき [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 カスタムツールは、インターフェイスを実装する COM コンポーネントです <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 。 このインターフェイスを使用すると、カスタムツールによって1つの入力ファイルが1つの出力ファイルに変換されます。 変換の結果は、ソースコード、またはその他の有用な出力である可能性があります。 カスタムツールによって生成されるコードファイルの2つの例は、ビジュアルデザイナーの変更と、Web サービス記述言語 (WSDL) を使用して生成されたファイルに応答して生成されるコードです。

 カスタムツールが読み込まれたとき、または入力ファイルが保存されると、プロジェクトシステムは <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> メソッドを呼び出し、コールバックインターフェイスへの参照を渡し <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> ます。これにより、ツールが進行状況をユーザーに報告できるようになります。

 カスタムツールによって生成される出力ファイルは、入力ファイルに対する依存関係があるプロジェクトに追加されます。 のカスタムツールの実装によって返された文字列に基づいて、出力ファイルの名前がプロジェクトシステムによって自動的に決定され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> ます。

 カスタムツールでは、インターフェイスを実装する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> ます。 必要に応じて、カスタムツールは、 <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> 入力ファイル以外のソースから情報を取得するためのインターフェイスをサポートします。 どのような場合でも、カスタムツールを使用する前に、システムまたはローカルレジストリに登録する必要があり [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 カスタムツールの登録の詳細については、「 [単一ファイルジェネレーターの登録](../../extensibility/internals/registering-single-file-generators.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [ビジュアル デザイナーへのタイプの公開](../../extensibility/internals/exposing-types-to-visual-designers.md)
