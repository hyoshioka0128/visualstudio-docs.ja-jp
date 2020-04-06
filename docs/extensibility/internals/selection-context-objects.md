---
title: 選択コンテキストオブジェクト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4e4f33dd0168a667b8f266ea606cecf0c26d62f1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705509"
---
# <a name="selection-context-objects"></a>コンテキスト オブジェクトの選択
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) では、グローバル選択コンテキストオブジェクトを使用して、IDE に表示する内容を決定します。 IDE の各ウィンドウには、グローバル選択コンテキストにプッシュされる独自の選択コンテキストオブジェクトを持つことができます。 IDE は、ウィンドウにフォーカスがあるときに、ウィンドウの値を使用してグローバル選択コンテキストを更新します。 詳細については、「[ユーザーへのフィードバック」を](../../extensibility/internals/feedback-to-the-user.md)参照してください。

 IDE の各ウィンドウ フレームまたはサイトには<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>、 というサービスがあります。 ウィンドウ フレームにサイト化されている VSPackage によって作成されたオブジェクトは、`QueryService`<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>インターフェイスへのポインターを取得するメソッドを呼び出す必要があります。

 フレーム ウィンドウは、選択コンテキスト情報の一部が、起動時にグローバル選択コンテキストに反映されないようにすることができます。 この機能は、空の選択で開始する必要があるツール ウィンドウに役立ちます。

 グローバル選択コンテキストを変更すると、VSPackages が監視できるイベントがトリガーされます。 VSPackage は、実装`IVsTrackSelectionEx`とインターフェイスによって次<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>のタスクを実行できます。

- 階層内の現在アクティブなファイルを更新します。

- 特定の種類の要素に対する変更を監視します。 たとえば、VSPackage が特別な**プロパティ**ウィンドウを使用している場合は、アクティブな**プロパティ**ウィンドウで変更を監視し、必要に応じて再起動できます。

  次のシーケンスは、選択追跡の一般的なコースを示しています。

1. IDE は、新しく開いたウィンドウから選択コンテキストを取得し、グローバル選択コンテキストに配置します。 選択コンテキストがHIERARCHY_DONTPROPAGATEまたはSELCONTAINER_DONTPROPAGATEを使用している場合、その情報はグローバル コンテキストに伝達されません。 詳細については、「[ユーザーへのフィードバック」を](../../extensibility/internals/feedback-to-the-user.md)参照してください。

2. 通知イベントは、イベントを要求した VSPackage にブロードキャストされます。

3. VSPackage は、階層の更新、ツールの再アクティブ化、またはその他の同様のタスクなどのアクティビティを実行することによって、受信したイベントに対して動作します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [プロジェクトの種類](../../extensibility/internals/project-types.md)
