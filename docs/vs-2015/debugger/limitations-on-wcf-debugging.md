---
title: WCF デバッグの制約 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, debugging limitations
ms.assetid: 8e0333c4-1ddc-4abe-8f1c-d19bf6a2a07a
caps.latest.revision: 33
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3faa57a0a2ca413898364c2d4ad1891df85f1ce8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176799"
---
# <a name="limitations-on-wcf-debugging"></a>WCF デバッグの制約
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

WCF サービスのデバッグを開始するには、次の 3 つの方法があります。  
  
- サービスを呼び出すクライアント プロセスをデバッグします。 デバッガーがサービスにステップ インします。 サービスは、クライアント アプリケーションと同じソリューションになくてもかまいません。  
  
- サービスを要求するクライアント プロセスをデバッグします。 サービスは、ソリューションの一部である必要があります。  
  
- **[プロセスにアタッチ]** を使用して、現在実行されているサービスにアタッチします。 サービス内部でデバッグが開始されます。  
  
  このトピックでは、これらのシナリオの制約について説明します。  
  
## <a name="limitations-on-stepping-into-a-service"></a>サービスへのステップ インの制約  
 デバッグ中のクライアント アプリケーションのサービスにステップ インするには、次の条件を満たす必要があります。  
  
- クライアントは、同期クライアント オブジェクトを使用してサービスを呼び出す必要があります。  
  
- コントラクト操作では、一方向の操作を使用できません。  
  
- サーバーが非同期の場合、サービスのコードを実行している間は、完全な呼び出し履歴を表示できません。  
  
- app.config ファイルまたは Web.config ファイルの次のコードでデバッグが有効にされている必要があります。  
  
    ```  
    <system.web>  
      <compilation debug="true" />  
    </system.web>  
    ```  
  
     このコードは一度だけ追加する必要があります。 コードを追加するには、.config ファイルを編集するか、 **[プロセスにアタッチ]** を使用してサービスにアタッチします。 サービスで **[プロセスにアタッチ]** を使用すると、デバッグ コードが自動的に .config ファイルに追加されます。 その後は、.config ファイルを編集せずにサービスをデバッグし、ステップ インできます。  
  
## <a name="limitations-on-stepping-out-of-a-service"></a>サービスからのステップ アウトの制約  
 サービスからステップ アウトしてクライアントに戻る際には、サービスへのステップ インと同じ制約があります。 また、デバッガーをクライアントにアタッチする必要があります。 クライアントをデバッグし、サービスにステップ インしても、デバッガーはサービスにアタッチしたままです。 これは、 **[デバッグ開始]** を使用してクライアントを起動する場合にも、 **[プロセスにアタッチ]** を使用してアタッチする場合にも当てはまります。 サービスにアタッチしてデバッグを開始した場合、デバッガーはまだクライアントにアタッチされていません。 このとき、サービスからステップ アウトしてクライアントに戻る必要がある場合は、最初に **[プロセスにアタッチ]** を使用して、クライアントに手動でアタッチする必要があります。  
  
## <a name="limitations-on-automatic-attach-to-a-service"></a>サービスへのオート アタッチの制約  
 サービスへのオート アタッチには、次の制約があります。  
  
- サービスは、デバッグしている [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションの一部である必要があります。  
  
- サービスはホストされている必要があります。 サービスは、Web サイト プロジェクト (ファイル システムおよび HTTP)、Web アプリケーション プロジェクト (ファイル システムおよび HTTP)、または WCF サービス ライブラリ プロジェクトの一部にすることができます。 WCF サービス ライブラリ プロジェクトは、サービス ライブラリまたはワークフロー サービス ライブラリです。  
  
- サービスは、WCF クライアントから起動される必要があります。  
  
- app.config ファイルまたは Web.config ファイルの次のコードでデバッグが有効にされている必要があります。  
  
    ```  
    <system.web>  
      <compilation debug="true" />  
    <system.web>  
    ```  
  
## <a name="self-hosting"></a>セルフホスト  
 *セルフホストされているサービス*とは、IIS 内部で実行されていない WCF サービス、WCF サービス ホスト、または [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 開発サーバーです。 セルフホストされているサービスをデバッグする方法については、「[方法: セルフホストされている WCF サービスをデバッグする](../debugger/how-to-debug-a-self-hosted-wcf-service.md)」を参照してください。  
  
## <a name="self-hosting"></a>セルフホスト  
 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 3.0 または 3.5 アプリケーションのデバッグを可能にするには、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] をインストールする前に [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] 3.0 または 3.5 をインストールする必要があります。 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] が [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 3.0 または 3.5 より前にインストールされていると、[!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 3.0 または 3.5 アプリケーションのデバッグ時にエラーが発生します。 エラー メッセージは、「サーバーに自動的にステップ インできません。」です。 この問題を解決するには、Windows の [ **コントロールパネル**] の [ **プログラムと機能** ] を使用してインストールを修復し [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] ます。  
  
## <a name="see-also"></a>参照  
 [WCF サービスのデバッグ](../debugger/debugging-wcf-services.md)   
 [方法: セルフホストされている WCF サービスをデバッグする](../debugger/how-to-debug-a-self-hosted-wcf-service.md)
