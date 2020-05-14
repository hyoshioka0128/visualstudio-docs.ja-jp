---
title: シンボル参照ツールのサポート |マイクロソフトドキュメント
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
ms.openlocfilehash: 4998e47ccd6f99df2710833c18975d57e3bb92f5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80704764"
---
# <a name="supporting-symbol-browsing-tools"></a>シンボル参照ツールのサポート
**オブジェクト ブラウザー**、**クラス ビュー**、**呼び出しブラウザー** 、**およびシンボルの結果の検索**ツールは、Visual Studio でシンボル参照機能を提供します。 これらのツールは、シンボルの階層ツリービューを表示し、ツリー内のシンボル間の関係を表示します。 シンボルは、名前空間、オブジェクト、クラス、クラス メンバー、およびさまざまなコンポーネントに含まれるその他の言語要素を表すことができます。 コンポーネントには、Visual Studio プロジェクト、外部 .NET Framework コンポーネント、および型 (.tlb) ライブラリが含まれます。 詳細については、「[コードの構造の表示](../../ide/viewing-the-structure-of-code.md)」を参照してください。

## <a name="symbol-browsing-libraries"></a>シンボル参照ライブラリ
 言語実装者は、コンポーネント内のシンボルを追跡し、一連のインターフェイスを通じて Visual Studio オブジェクト マネージャーにシンボルのリストを提供するライブラリを作成することで、Visual Studio のシンボル参照機能を拡張できます。 ライブラリはインターフェイスによって記述されます<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2>。 Visual Studio オブジェクト マネージャーは、ライブラリからデータを取得し、それを整理することで、シンボル参照ツールから新しいデータの要求に応答します。 その後、要求されたデータを使用してツールを設定または更新します。 Visual Studio オブジェクト マネージャーへの参照を取得<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2>するには、`GetService`サービス<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>ID をメソッドに渡します。

 各ライブラリは Visual Studio オブジェクト マネージャーに登録する必要があります。 ライブラリを登録するには、メソッドを<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>呼び出します。 要求を開始するツールに応じて、Visual Studio オブジェクト マネージャーは適切なライブラリを検索し、データを要求します。 データは、インタフェースによって記述されたシンボルの[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]リスト内のライブラリーとオブジェクト・マネージャーの<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>間を移動します。

 オブジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]マネージャは、ライブラリに含まれる最新のデータを反映するために、シンボル参照ツールを定期的に更新します。

 次の図は、ライブラリと Visual Studio オブジェクト マネージャー間の要求/データ交換プロセスの主要な要素のサンプルを示しています。 ダイアグラム内のインターフェイスは、マネージ コード アプリケーションの一部です。

 ![ライブラリとオブジェクト マネージャー間のデータ フロー](../../extensibility/internals/media/callbrowserdiagram.gif "呼び出しブラウザ図")

 Visual Studio オブジェクト マネージャーにシンボルの一覧を提供するには、まず、メソッドを呼び出すことによって、Visual Studio<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager2.RegisterSimpleLibrary%2A>オブジェクト マネージャーでライブラリを登録する必要があります。 ライブラリが登録されると、Visual Studio オブジェクト マネージャーは、ライブラリの機能に関する特定の情報を要求します。 たとえば、 と メソッドを呼び出すことによって、ライブラリ<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetLibFlags2%2A>フラグ<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetSupportedCategoryFields2%2A>とサポートされているカテゴリを要求します。 ある時点で、ツールの 1 つがこのライブラリのデータを要求すると、オブジェクト マネージャーは、メソッドを呼び出すことによって<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleLibrary2.GetList2%2A>シンボルの最上位のリストを要求します。 これに対して、ライブラリはシンボルの一覧を作成し、インターフェイスを通じて Visual Studio<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2>オブジェクト マネージャーに公開します。 オブジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]マネージャーは、メソッドを呼び出すことによって、リスト内<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetItemCount%2A>の項目の数を決定します。 次のすべての要求は、リスト内の特定の項目に関連し、各要求で項目のインデックス番号を指定します。 Visual Studio オブジェクト マネージャーは、メソッドを呼び出すことによって、項目の型、アクセシビリティ、およびその他のプロパティに<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetCategoryField2%2A>関する情報を収集します。

 メソッドを呼び出すことによって項目の名前を<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetTextWithOwnership%2A>判別し、メソッドを呼び出して<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetDisplayData%2A>アイコン情報を要求します。 アイコンは、項目名の左側に表示され、項目の種類、アクセシビリティ、およびその他のプロパティが表示されます。

 オブジェクト[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]マネージャーは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetExpandable3%2A>メソッドを呼び出して、特定のリスト 項目が展開可能で子項目を持っているかどうかを判断します。 UI が要素を展開する要求を送信する場合、オブジェクト マネージャーは、メソッドを呼び<xref:Microsoft.VisualStudio.Shell.Interop.IVsSimpleObjectList2.GetList2%2A>出すことによってシンボルの子リストを要求します。 このプロセスは、オンデマンドで構築されるツリーのさまざまな部分で続行されます。

> [!NOTE]
> ネイティブ コード シンボル プロバイダーを実装するには<xref:Microsoft.VisualStudio.Shell.Interop.IVsLibrary2>、<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectList2>および インターフェイスを使用します。

## <a name="see-also"></a>関連項目
- [方法: オブジェクト マネージャーを使用したライブラリの登録](../../extensibility/internals/how-to-register-a-library-with-the-object-manager.md)
- [方法: ライブラリによって提供されるシンボルのリストをオブジェクト マネージャーに公開する](../../extensibility/internals/how-to-expose-lists-of-symbols-provided-by-the-library-to-the-object-manager.md)
- [方法: ライブラリでのシンボルの識別](../../extensibility/internals/how-to-identify-symbols-in-a-library.md)
