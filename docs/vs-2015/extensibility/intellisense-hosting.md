---
title: IntelliSense のホスト |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - IntelliSense hosting
ms.assetid: 20c61f8a-d32d-47e2-9c67-bf721e2cbead
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a5c378aec6822a436de0d8fc2656fcac7be4149f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203897"
---
# <a name="intellisense-hosting"></a>IntelliSense ホスティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio では、IntelliSense のホストが有効になります。 Intellisense ホスティングでは、Visual Studio テキストエディターでホストされていないコードに IntelliSense を提供できます。  
  
## <a name="intellisense-hosting-usage"></a>IntelliSense のホスト使用  
 Visual Studio では、入力候補セットとテキストバッファーにアクセスできるすべてのコードは、ユーザーインターフェイス (UI) の任意の場所から IntelliSense ウィンドウを取得できます。 このようなシナリオの例としては、[ **ウォッチ** ] ウィンドウまたは [ブレークポイントのプロパティ] ウィンドウの [条件] フィールドを使用する方法があります。  
  
### <a name="implementation-interfaces"></a>実装インターフェイス  
  
#### <a name="ivsintellisensehost"></a>IVsIntellisenseHost  
 IntelliSense ポップアップウィンドウをホストするすべての UI コンポーネントは、インターフェイスをサポートしている必要があり <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> ます。 既定のコアエディターのテキストビューには、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> 現在の IntelliSense 機能を保持するためのストックインターフェイスの実装が含まれています。 ほとんどの場合、インターフェイスのメソッドは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> インターフェイスに実装されているもののサブセットを表し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。 サブセットには、IntelliSense UI の処理、キャレットと選択の操作、および単純なテキスト置換機能が含まれます。 また、インターフェイスでは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> コンテキストに使用されているテキストバッファーに直接存在しないサブジェクトに対して intellisense を提供できるように、個別の intellisense "subject" と "context" が有効になります。  
  
#### <a name="ivsintellisensehostgethostflags"></a>IVsIntellisenseHost.GetHostFlags  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>インターフェイスプロバイダーは、メソッドを実装して、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetHostFlags%2A> ホストがサポートする IntelliSense 機能の種類をクライアントが判断できるようにする必要があります。  
  
 次に、 [IntelliSenseHostFlags](../extensibility/intellisensehostflags.md)で定義されているホストフラグの概要を示します。  
  
|IntelliSense ホストフラグ|説明|  
|----------------------------|-----------------|  
|IHF_READONLYCONTEXT|このフラグを設定すると、コンテキストバッファーは読み取り専用になり、編集は件名テキスト内でのみ行われます。|  
|IHF_NOSEPERATESUBJECT|このフラグを設定すると、別の IntelliSense の件名がないことを意味します。 サブジェクトは、従来の IntelliSense システムなどのコンテキストバッファーに存在し <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> ます。|  
|IHF_SINGLELINESUBJECT|このフラグを設定すると、[ **ウォッチ** ] ウィンドウの単一行の編集など、件名が複数行に対応していないことを意味します。|  
|IHF_FORCECOMMITTOCONTEXT|このフラグが設定されていて、コンテキストバッファーを更新する必要がある場合、ホストはコンテキストバッファーの読み取り専用フラグを無視し、編集を続行できるようにします。|  
|IHF_OVERTYPE|編集 (件名またはコンテキスト) は、上書きモードで実行する必要があります。|  
  
#### <a name="ivsintellisensehostbeforecompletorcommit-and-ivsintellisensehostaftercompletorcommit"></a>IVsIntellisenseHost BeforeCompletorCommit と IVsIntellisenseHost Torcommit  
 これらのコールバックメソッドは、テキストがコミットされる前後に完了ウィンドウによって呼び出され、前処理と後処理を可能にします。  
  
#### <a name="ivsintellisensecompletor"></a>IVsIntellisenseCompletor  
 インターフェイスは、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseCompletor> 統合開発環境 (IDE: integrated development environment) によって使用される標準の完了ウィンドウの共同作成可能なバージョンです。 すべての <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost> インターフェイスは、この一の tor インターフェイスを使用して IntelliSense を迅速に実装できます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.TextManager.Interop>
