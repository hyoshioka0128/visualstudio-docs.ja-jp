---
title: テキストマネージャーを使用したグローバル設定の監視 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - monitor global settings
- editors [Visual Studio SDK], legacy - text manager
ms.assetid: 023e7671-cf65-419c-9bc1-3c4ee92aa436
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ece51450b8344ae4715a912399ec538171a26a5c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695468"
---
# <a name="using-the-text-manager-to-monitor-global-settings"></a>グローバル設定を監視するためのテキスト マネージャーの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コアエディターを実装する場合は、グローバル設定に加えられた変更を監視する必要があります。これは、これらの変更がエディターのインスタンスに影響を与える可能性があるためです。 テキストマネージャーによって発生したイベントをリッスンすることによって、変更を追跡できます。 たとえば、ドキュメントデータオブジェクトなど、コアエディターのコンポーネントの外観または動作に対してグローバル設定を指定すると、テキストマネージャーはこの情報を保存し、影響を受けるすべてのクライアントに通知します。  
  
## <a name="text-manager-functions"></a>テキストマネージャーの関数  
 テキストマネージャーは、次のようなさまざまな設定のイベントを発生させます。  
  
- バッファーがソースコード管理されているかどうか  
  
- ファイル変更通知に登録する方法  
  
- 特定のバッファーに関連付けられているビューを追跡する方法  
  
- テキストの色づけの基本設定  
  
- タブとスペースの設定  
  
  特定の言語に固有の設定は、テキストマネージャーによって管理されません。 これらの設定は、各言語サービスで管理する必要があります。  
  
  テキストマネージャーのイベント通知は、インターフェイスによって提供され <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents> ます。 テキストマネージャーを発生させたイベントを処理するには、このインターフェイスをクライアントオブジェクトに実装します。 これらのイベントに登録するには、テキストマネージャーのインターフェイスを使用し <xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer> ます。  
  
## <a name="see-also"></a>参照  
 [コアエディター内](../extensibility/inside-the-core-editor.md)   
 [エディターの機能](https://msdn.microsoft.com/bdac940d-1f14-4019-a01f-fd0bb3dc7198)
