---
title: IDE での選択と通貨 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d0a0b999a1a6e6ed2364060031f68378e7222ec0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155810"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE での選択と通貨
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]統合開発環境 (IDE) は、選択*コンテキスト*を使用して、ユーザーの現在選択されているオブジェクトに関する情報を保持します。 選択コンテキストを使用すると、Vspackage は次の2つの方法で通貨追跡に参加できます。  
  
- Vspackage に関する通貨情報を IDE に伝達する。  
  
- IDE 内でユーザーの現在アクティブな選択を監視します。  
  
## <a name="selection-context"></a>選択コンテキスト  
 Ide では、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 独自のグローバル選択コンテキストオブジェクトで ide の通貨がグローバルに追跡されます。 次の表は、選択コンテキストを構成する要素を示しています。  
  
|要素|説明|  
|-------------|-----------------|  
|現在の階層|通常は現在のプロジェクトです。現在の階層が NULL である場合は、ソリューション全体が最新であることを示します。|  
|現在の ItemID|現在の階層内で選択されている項目。プロジェクトウィンドウに複数の選択肢がある場合は、現在の項目が複数存在する可能性があります。|  
|現在の `SelectionContainer`|プロパティウィンドウがプロパティを表示する必要がある1つ以上のオブジェクトを保持します。|  
  
 さらに、環境では次の2つのグローバルリストが保持されます。  
  
- アクティブな UI コマンド識別子の一覧  
  
- 現在アクティブな要素の型のリスト。  
  
### <a name="window-types-and-selection"></a>ウィンドウの種類と選択  
 IDE では、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ウィンドウが次の2つの一般的な種類に分類されます。  
  
- 階層型 windows  
  
- フレームウィンドウ (ツールウィンドウやドキュメントウィンドウなど)  
  
  IDE では、これらのウィンドウの種類ごとに異なる方法で通貨を追跡します。  
  
  最も一般的なプロジェクトの種類のウィンドウは、IDE が制御するソリューションエクスプローラーです。 プロジェクトの種類のウィンドウは、グローバルな選択コンテキストのグローバル階層と ItemID を追跡し、ウィンドウは現在の階層を決定するためにユーザーの選択に依存します。 プロジェクトの種類が windows の場合、環境は、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> vspackage が開いている要素の現在の値を監視できるグローバルサービスを提供します。 環境でのプロパティの参照は、このグローバルサービスによって行われます。  
  
  一方、フレームウィンドウでは、フレームウィンドウ内の DocObject を使用して SelectionContext 値 (hierarchy/ItemID/Selectioncontext trio) をプッシュします。 . フレームウィンドウ <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> この目的のためにサービスを使用します。 DocObject は、選択コンテナーの値のみをプッシュできます。これは、MDI 子ドキュメントの場合と同様に、hierarchy および ItemID のローカル値は変更されません。  
  
### <a name="events-and-currency"></a>イベントと通貨  
 環境の通貨の概念に影響するイベントには、次の2種類があります。  
  
- グローバルレベルに反映され、ウィンドウフレーム選択コンテキストを変更するイベント。 この種のイベントの例としては、開いている MDI 子ウィンドウ、開かれているグローバルツールウィンドウ、または開いているプロジェクトの種類のツールウィンドウなどがあります。  
  
- ウィンドウのフレーム選択コンテキスト内でトレースされた要素を変更するイベント。 例としては、DocObject 内での選択の変更や、プロジェクトタイプウィンドウでの選択の変更などがあります。  
  
## <a name="see-also"></a>参照  
 [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)   
 [ユーザーへのフィードバック](../../extensibility/internals/feedback-to-the-user.md)
