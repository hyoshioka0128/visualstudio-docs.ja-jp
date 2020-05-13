---
title: IDE での選択と通貨 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f580b7c8e1651dcbcd053476ae756399a0ac3482
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705580"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE での選択と通貨
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]統合開発環境 (IDE) は、選択*コンテキスト*を使用して、現在選択されているオブジェクトに関する情報を保持します。 選択コンテキストでは、VSPackages は、次の 2 つの方法で通貨の追跡に参加できます。

- VS パッケージに関する通貨情報を IDE に伝達します。

- IDE 内でユーザーが現在アクティブな選択を監視する。

## <a name="selection-context"></a>選択コンテキスト
 IDE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]は、独自のグローバル選択コンテキストオブジェクト内の IDE 通貨をグローバルに追跡します。 次の表は、選択コンテキストを構成する要素を示しています。

|要素|説明|
|-------------|-----------------|
|現在の階層|通常は現在のプロジェクト。現在の階層が NULL の場合、ソリューション全体が現在の階層であることを示します。|
|現在のアイテム ID|現在の階層内で選択された項目。プロジェクト ウィンドウに複数の選択がある場合は、現在の項目が複数存在する可能性があります。|
|現在の`SelectionContainer`|プロパティ ウィンドウにプロパティを表示する対象の 1 つまたは複数のオブジェクトを保持します。|

 さらに、環境は 2 つのグローバル リストを保持します。

- アクティブな UI コマンド ID のリスト

- 現在アクティブな要素の種類のリスト。

### <a name="window-types-and-selection"></a>ウィンドウの種類と選択
 IDE[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]では、ウィンドウが 2 つの一般的なタイプに編成されます。

- 階層タイプウィンドウ

- ツール ウィンドウやドキュメント ウィンドウなどのフレーム ウィンドウ

  IDE では、これらのウィンドウの種類ごとに異なる方法で通貨を追跡します。

  最も一般的なプロジェクトの種類のウィンドウは、IDE が制御するソリューション エクスプ ローラーです。 プロジェクトタイプウィンドウは、グローバル選択コンテキストのグローバル階層と ItemID を追跡し、ウィンドウは現在の階層を決定するためにユーザーの選択に依存します。 プロジェクトタイプのウィンドウでは、環境は、VSPackages<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>が開いている要素の現在の値を監視できるグローバルサービスを提供します。 環境でのプロパティの参照は、このグローバル サービスによって駆動されます。

  一方、フレーム ウィンドウは、フレーム ウィンドウ内の DocObject を使用して、選択コンテキスト値 (階層/項目 ID/選択コンテナ トリオ) をプッシュします。 . フレーム ウィンドウは、<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>この目的のためにサービスを使用します。 DocObject は、MDI 子ドキュメントの一般的なように、階層および ItemID のローカル値を変更せずに、選択コンテナーの値のみをプッシュできます。

### <a name="events-and-currency"></a>イベントと通貨
 環境の通貨の概念に影響を与える 2 種類のイベントが発生する可能性があります。

- グローバル レベルに伝達され、ウィンドウ フレーム選択コンテキストを変更するイベント。 この種のイベントの例としては、開いている MDI 子ウィンドウ、開いているグローバル ツール ウィンドウ、または開いているプロジェクト型のツール ウィンドウなどがあります。

- ウィンドウ フレーム選択コンテキスト内でトレースされる要素を変更するイベント。 たとえば、DocObject 内での選択の変更や、プロジェクトタイプのウィンドウでの選択の変更などがあります。

## <a name="see-also"></a>関連項目
- [コンテキスト オブジェクトの選択](../../extensibility/internals/selection-context-objects.md)
- [ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)
