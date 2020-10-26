---
title: コアエディターの内部 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - core editor
ms.assetid: 8265f31c-c45b-4858-882c-6d9f1e3b9083
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cf9bc42aec3aac5acc996487f99c7e1f29ca252c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203951"
---
# <a name="inside-the-core-editor"></a>コア エディターの内部
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]コアエディターは、テキスト情報の変更とクエリを実行できるいくつかのコンポーネントのセットです。 レガシ API を使用してコアエディターをカスタマイズした場合は、これらのカスタマイズを引き続き使用することができます。これらのカスタマイズは、エディターアダプターを通じてルーティングされます。 ただし、カスタマイズを新しいエディター API に適合させることをお勧めします。  
  
 コアエディターの重要な側面は次のとおりです。  
  
- テキストバッファー  
  
- テキストビュー  
  
- [コード ウィンドウ]  
  
- テキストマーカー  
  
- テキストマネージャー  
  
- 言語サービスとの統合  
  
## <a name="in-this-section"></a>このセクションの内容  
 [レガシ API を使用するコア エディターのインスタンス化](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)  
 を使用して <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 、コアエディターのインスタンスを作成する手順について説明します。  
  
 [レガシ API を使用するテキスト バッファーへのアクセス](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)  
 コアエディターのテキストバッファーの役割について説明し、バッファーへのアクセスに使用される関連システムについて説明し、テキストバッファーオブジェクトによって実装されるインターフェイスの一覧を示し <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> ます。  
  
 [レガシ API のテキスト バッファー イベント](../extensibility/text-buffer-events-in-the-legacy-api.md)  
 テキストバッファーイベントの通知に使用されるインターフェイスの一覧を示します。  
  
 [方法: レガシ API でテキスト バッファー イベントを登録する](../extensibility/how-to-register-for-text-buffer-events-with-the-legacy-api.md)  
 テキストバッファーイベントをアドバイズする方法について説明します。  
  
 [グローバル設定を監視するためのテキスト マネージャーの使用](../extensibility/using-the-text-manager-to-monitor-global-settings.md)  
 テキストマネージャーを使用して、コアエディターコンポーネントと共にグローバル基本設定情報を共有する方法と、テキストマネージャーイベントの通知を受信する方法について説明します。  
  
 [レガシ API を使用するテキスト ビューへのアクセス](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)  
 コアエディターでのテキストビューのロールについて説明し、オブジェクトによって実装されるインターフェイスの一覧を示し <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> ます。  
  
 [レガシ API を使用するコード ウィンドウのカスタマイズ](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)  
 コードウィンドウを使用してテキストビューを囲む方法、コードウィンドウマネージャーを使用してコードウィンドウに装飾を提供する方法、および新しいビューの通知を提供する方法について説明します。  
  
 [レガシ API を使用する表示設定の変更](../extensibility/changing-view-settings-by-using-the-legacy-api.md)  
 表示設定を強制する方法と、強制設定を削除する方法について、手順を追って説明します。  
  
 [言語サービスとコア エディター](../extensibility/language-services-and-the-core-editor.md)  
 言語サービスをインスタンス化してコードの装飾を制御する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [チュートリアル: コア エディターの作成とエディター ファイルの種類の登録](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)  
 マネージコードからコアエディターを起動する手順について説明します。  
  
 [ドロップダウン バー](../extensibility/drop-down-bar.md)  
 コードウィンドウでドロップダウンバーを使用する方法について説明し、ドロップダウンバーを実装するときに使用するインターフェイスについて説明します。  
  
 [レガシ API でのテキスト マーカーの使用](../extensibility/using-text-markers-with-the-legacy-api.md)  
 テキストマーカーの概念と、それがコアエディターでどのように使用されるかについて説明し、テキストマーカーにアクセスして管理するために使用されるインターフェイスの一覧を示します。  
  
 [方法: 標準のテキスト マーカーを追加する](../extensibility/how-to-add-standard-text-markers.md)  
 テキストマーカーを作成する方法、およびショートカットメニューにカスタムコマンドを追加する方法について、手順を追って説明します。  
  
 [方法: カスタム テキスト マーカーを作成する](../extensibility/how-to-create-custom-text-markers.md)  
 カスタムテキストマーカーを作成する方法と、マーカーの種類をサービスとして指定する方法について、手順を追って説明します。
