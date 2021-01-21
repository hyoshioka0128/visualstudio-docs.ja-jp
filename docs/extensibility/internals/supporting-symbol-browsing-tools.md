---
title: サポート Symbol-Browsing ツール |Microsoft Docs
description: Visual Studio には、Visual Studio のシンボル参照機能が用意されています。 コンポーネント内のシンボル用のライブラリを使用して、これらの機能を拡張する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbols, symbol-browsing tools
- browsers, symbol browsers
- symbol-browsing tools
- libraries
- IVsLibrary2 interface, symbol-browsing tools
- IVsSimpleLibrary2 interface, symbol-browsing tools
- symbol-browsing tools, library manager
- symbols
- libraries, symbol-browsing tools
ms.assetid: 70d8c9e5-4b0b-4a69-b3b3-90f36debe880
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0adf586831e21c2448931215d4ef4a89d16a63f8
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97876442"
---
# <a name="supporting-symbol-browsing-tools"></a>シンボル参照ツールのサポート
**オブジェクトブラウザー**、 **クラスビュー**、 **呼び出しブラウザー** および **検索シンボル結果** ツールは、Visual Studio のシンボル参照機能を提供します。 これらのツールでは、シンボルの階層ツリービューが表示され、ツリー内のシンボル間の関係が表示されます。 シンボルは、さまざまなコンポーネントに含まれる名前空間、オブジェクト、クラス、クラスメンバー、およびその他の言語要素を表すことができます。 コンポーネントには、Visual Studio プロジェクト、外部 .NET Framework コンポーネント、および型 (.tlb) ライブラリが含まれます。 詳細については、「[コードの構造の表示](../../ide/viewing-the-structure-of-code.md)」を参照してください。

## <a name="symbol-browsing-libraries"></a>Symbol-Browsing ライブラリ
 言語の実装者は、コンポーネント内のシンボルを追跡するライブラリを作成し、一連のインターフェイスを使用して Visual Studio オブジェクトマネージャーにシンボルの一覧を提供することにより、Visual Studio のシンボル参照機能を拡張できます。 ライブラリは、インターフェイスによって記述され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2> ます。 Visual Studio オブジェクトマネージャーは、ライブラリからデータを取得して整理することにより、シンボル参照ツールからの新しいデータの要求に応答します。 その後、要求されたデータを使用してツールを設定または更新します。 Visual Studio オブジェクトマネージャーへの参照を取得するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2> <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> サービス ID をメソッドに渡し `GetService` ます。

 各ライブラリは、すべてのライブラリの情報を収集する Visual Studio オブジェクトマネージャーに登録する必要があります。 ライブラリを登録するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> メソッドを呼び出します。 要求を開始するツールに応じて、Visual Studio オブジェクトマネージャーは適切なライブラリを検索し、データを要求します。 データは、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] インターフェイスによって記述されたシンボルの一覧で、ライブラリとオブジェクトマネージャーの間を移動し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> ます。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクトマネージャーは、ライブラリに格納されている最新のデータを反映するために、シンボル参照ツールを定期的に更新する役割を担います。

 次の図には、ライブラリと Visual Studio オブジェクトマネージャー間の要求/データ交換プロセスの主要要素のサンプルが含まれています。 図のインターフェイスは、マネージコードアプリケーションの一部です。

 ![ライブラリとオブジェクト マネージャー間のデータ フロー](../../extensibility/internals/media/callbrowserdiagram.gif "CallBrowserDiagram")

 Visual Studio オブジェクトマネージャーにシンボルのリストを提供するには、最初にメソッドを呼び出して、Visual Studio オブジェクトマネージャーにライブラリを登録する必要があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A> ます。 ライブラリが登録されると、Visual Studio のオブジェクトマネージャーによって、ライブラリの機能に関する特定の情報が要求されます。 たとえば、メソッドとメソッドを呼び出すことによって、ライブラリフラグとサポートされるカテゴリを要求し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A> ます。 ある時点で、いずれかのツールがこのライブラリからデータを要求すると、オブジェクトマネージャーはメソッドを呼び出して、最上位レベルのシンボルリストを要求し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A> ます。 応答として、ライブラリによってシンボルのリストが製造され、インターフェイスを通じて Visual Studio オブジェクトマネージャーに公開され <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2> ます。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]オブジェクトマネージャーは、メソッドを呼び出すことによって、リスト内の項目数を特定し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A> ます。 次の要求はすべて、リスト内の特定の項目に関連付けられ、各要求に項目のインデックス番号を指定します。 Visual Studio オブジェクトマネージャーは、メソッドを呼び出すことによって、項目の型、アクセシビリティ、およびその他のプロパティに関する情報を収集し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A> ます。

 メソッドを呼び出して項目の名前を決定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A> し、メソッドを呼び出すことによってアイコン情報を要求し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A> ます。 項目名の左側にアイコンが表示され、項目の種類、アクセシビリティ、およびその他のプロパティが示されます。

 オブジェクトマネージャーは、メソッドを呼び出して、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A> 特定のリスト項目が展開可能で、子項目があるかどうかを確認します。 UI が要素を展開する要求を送信する場合、オブジェクトマネージャーはメソッドを呼び出すことによって、シンボルの子リストを要求し <xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A> ます。 プロセスは、ツリーのさまざまな部分を必要に応じて構築し続けます。

> [!NOTE]
> ネイティブコードシンボルプロバイダーを実装するには、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2> インターフェイスとインターフェイスを使用し <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2> ます。

## <a name="see-also"></a>関連項目
- [方法: オブジェクト マネージャーを使用したライブラリの登録](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [方法: ライブラリでのシンボルの識別](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
