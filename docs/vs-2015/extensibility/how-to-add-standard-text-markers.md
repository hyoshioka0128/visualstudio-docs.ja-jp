---
title: '方法: 標準テキストマーカーを追加する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - standard text markers
ms.assetid: a39fca69-0014-474c-933f-51f0e9b9617e
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 912d5d7a225520fc825d832bf73f5cfc733a9486
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841365"
---
# <a name="how-to-add-standard-text-markers"></a>方法: 標準のテキスト マーカーを追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コアエディターで用意されている既定のテキストマーカーの種類のいずれかを作成するには、次の手順に従い [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
### <a name="to-create-a-text-marker"></a>テキストマーカーを作成するには  
  
1. 1次元または2次元の座標系を使用しているかどうかに応じて、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.CreateLineMarker%2A> メソッドまたはメソッドを呼び出して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.CreateStreamMarker%2A> 新しいテキストマーカーを作成します。  
  
     このメソッド呼び出しで、マーカーの種類、マーカーを作成するテキストの範囲、およびインターフェイスを指定し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient> ます。 このメソッドは、新しく作成されたテキストマーカーへのポインターを返します。 マーカーの種類は、列挙体から取得され <xref:Microsoft.VisualStudio.TextManager.Interop.MARKERTYPE> ます。 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient>マーカーイベントを通知する場合は、インターフェイスを指定します。  
  
    > [!NOTE]
    > メイン UI スレッドにのみテキストマーカーを作成します。 コアエディターはテキストバッファーの内容に依存してテキストマーカーを作成しますが、テキストバッファーはスレッドセーフではありません。  
  
## <a name="adding-a-custom-command"></a>カスタムコマンドの追加  
 インターフェイスを実装 `IVsTextMarkerClient` し、マーカーからポインターを指定すると、いくつかの方法でマーカーの動作が拡張されます。 まず、マーカーにヒントを提供したり、コマンドを実行したりすることができます。 これにより、個々のマーカーのイベント通知を受信したり、マーカーの上にカスタムコンテキストメニューを作成したりすることもできます。 マーカーのショートカットメニューにカスタムコマンドを追加するには、次の手順に従います。  
  
#### <a name="to-add-a-custom-command-to-the-context-menu"></a>コンテキストメニューにカスタムコマンドを追加するには  
  
1. コンテキストメニューが表示される前に、環境はメソッドを呼び出し、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.GetMarkerCommandInfo%2A> 影響を受けるテキストマーカーへのポインターとコンテキストメニューのコマンド項目数を渡します。  
  
     たとえば、コンテキストメニューのブレークポイント固有のコマンドには、次のスクリーンショットに示されているように、[ブレークポイントの **削除** ] [ **新しいブレーク**ポイント] があります。  
  
     ![マーカー コンテキスト メニュー](../extensibility/media/vsmarkercontextmenu.gif "vsMarkercontextmenu")  
  
2. カスタムコマンドの名前を識別するテキストをいくつか戻します。 たとえば、" **ブレークポイントの削除** " は、環境でまだ提供されていない場合、カスタムコマンドになることがあります。 また、コマンドがサポートされているかどうか、使用可能で有効になっているかどうか、またはオン/オフの切り替えも返されます。 環境では、この情報を使用して、ショートカットメニューのカスタムコマンドを正しい方法で表示します。  
  
3. コマンドを実行するために、環境は <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarkerClient.ExecMarkerCommand%2A> メソッドを呼び出し、テキストマーカーへのポインターとコンテキストメニューから選択されたコマンドの番号を渡します。  
  
     この呼び出しの情報を使用して、カスタムコマンドが指示するテキストマーカーの任意のアクションを実行します。  
  
## <a name="see-also"></a>参照  
 [レガシ API でのテキストマーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)   
 [方法: エラーマーカーを実装する](../extensibility/how-to-implement-error-markers.md)   
 [方法: カスタムテキストマーカーを作成する](../extensibility/how-to-create-custom-text-markers.md)   
 [方法: テキスト マーカーを使用する](../extensibility/how-to-use-text-markers.md)
