---
title: テキスト マネージャーを使用して、グローバル設定を監視する |Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - monitor global settings
- editors [Visual Studio SDK], legacy - text manager
ms.assetid: 023e7671-cf65-419c-9bc1-3c4ee92aa436
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3678ec0cba6f46b65f5c1d6f84e9962b5487fa93
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937864"
---
# <a name="use-the-text-manager-to-monitor-global-settings"></a>テキスト マネージャーを使用して、グローバル設定を監視するには
コア エディターを実装する場合、エディターのインスタンスがこれらの変更の影響を与えるため、グローバル設定に加えられた変更を監視する必要があります。 変更を追跡するには、テキスト マネージャーによって生成されるイベントをリッスンします。 たとえば、そのドキュメント データ オブジェクトなどのコア エディターでの表示やコンポーネントの動作のグローバル設定を指定するとテキスト マネージャーはこの情報を格納し、影響を受けるすべてのクライアントと通信すること。  
  
## <a name="text-manager-functions"></a>テキスト マネージャー関数  
 テキスト マネージャーは、さまざまな設定は、次のようにイベントを発生させます。  
  
- バッファーはソース コード管理、かどうか  
  
- ファイル変更通知を登録する方法  
  
- ビューは、特定のバッファーに関連付けられたを追跡する方法  
  
- テキストの色づけの基本設定  
  
- タブとスペースの基本設定  
  
  特定の言語に固有の設定は、テキスト マネージャーによって管理されていません。 各言語サービスでは、これらの設定を管理する必要があります。  
  
  によって、テキスト マネージャーのイベント通知が提供される、<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManagerEvents>インターフェイス。 このインターフェイスを実装して、クライアントでイベントを処理するオブジェクトにはテキスト マネージャーが発生します。 使用してこれらのイベントの登録、<xref:Microsoft.VisualStudio.OLE.Interop.IConnectionPointContainer>テキスト マネージャーのインターフェイス。  
  
## <a name="see-also"></a>関連項目  
 [コア エディター](../extensibility/inside-the-core-editor.md)   
 [エディターの機能](https://msdn.microsoft.com/library/bdac940d-1f14-4019-a01f-fd0bb3dc7198)