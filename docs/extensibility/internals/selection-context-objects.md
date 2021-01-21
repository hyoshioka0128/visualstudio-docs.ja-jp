---
title: 選択コンテキストオブジェクト |Microsoft Docs
description: Visual Studio IDE がグローバル選択コンテキストオブジェクトを使用して IDE に表示する内容を決定する方法の詳細について説明します。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: bf5e54f00ecbac03eaebe68c6fb4de410987b63f
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97875571"
---
# <a name="selection-context-objects"></a>コンテキスト オブジェクトの選択
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (ide: integrated development environment) は、グローバル選択コンテキストオブジェクトを使用して、ide に表示する内容を決定します。 IDE の各ウィンドウは、グローバル選択コンテキストにプッシュされた独自の選択コンテキストオブジェクトを持つことができます。 IDE は、ウィンドウにフォーカスがあるときに、グローバル選択コンテキストをウィンドウの値で更新します。 詳細については、「 [ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)」を参照してください。

 IDE 内の各ウィンドウフレームまたはサイトには、というサービスがあり <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> ます。 ウィンドウフレーム内に配置されている VSPackage によって作成されたオブジェクトは、その `QueryService` インターフェイスへのポインターを取得するためにメソッドを呼び出す必要があり <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> ます。

 フレームウィンドウを使用すると、選択コンテキスト情報の一部を、開始時にグローバル選択コンテキストに反映させることができます。 この機能は、空の選択によって開始する必要があるツールウィンドウに役立ちます。

 グローバル選択コンテキストを変更すると、Vspackage が監視できるイベントがトリガーされます。 Vspackage は、およびインターフェイスを実装することで、次のタスクを実行でき `IVsTrackSelectionEx` <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> ます。

- 階層内の現在アクティブなファイルを更新します。

- 特定の種類の要素に対する変更を監視します。 たとえば、VSPackage で特別な **プロパティ** ウィンドウを使用する場合は、[アクティブな **プロパティ** ] ウィンドウで変更を監視し、必要に応じて自分で再起動できます。

  次のシーケンスは、選択の追跡の典型的な例を示しています。

1. IDE は、新しく開いたウィンドウから選択コンテキストを取得し、グローバルな選択コンテキストに配置します。 選択コンテキストで HIERARCHY_DONTPROPAGATE または SELCONTAINER_DONTPROPAGATE が使用されている場合、その情報はグローバルコンテキストに反映されません。 詳細については、「 [ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)」を参照してください。

2. 通知イベントは、要求したすべての VSPackage にブロードキャストされます。

3. VSPackage は、階層を更新したり、ツールを再アクティブ化したり、その他の同様のタスクを実行したりすることによって、受信するイベントに対して動作します。

## <a name="see-also"></a>関連項目
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio での階層](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE での選択と通貨](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [プロジェクトの種類](../../extensibility/internals/project-types.md)
