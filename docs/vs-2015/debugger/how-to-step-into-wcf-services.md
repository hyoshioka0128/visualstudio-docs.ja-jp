---
title: '方法: WCF サービスにステップインする | Microsoft Docs'
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
- WCF, debugging
ms.assetid: 9893ad01-54af-499f-85a6-9d1cfe6eb640
caps.latest.revision: 27
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 951d5f39fbf3929d094cc18de5fe108b46753b09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68176524"
---
# <a name="how-to-step-into-wcf-services"></a>方法: WCF サービスにステップインする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] では、WCF サービスにステップ インできます。 WCF サービスがクライアントと同じ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションにある場合、WCF サービス内のブレークポイントに到達できます。  
  
 ステップ実行を使用するには、app.config ファイルまたは Web.config ファイルでデバッグを有効にする必要があります。 デバッグを有効にする方法と WCF サービスにステップ インする際の制約については、「[WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)」を参照してください。  
  
### <a name="to-step-into-a-wcf-service"></a>WCF サービスにステップ インするには  
  
1. WCF クライアント プロジェクトと WCF サービス プロジェクトの両方を含む [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ソリューションを作成します。  
  
2. ソリューション エクスプローラーで、WCF クライアント プロジェクトを右クリックして、 **[スタートアップ プロジェクトに設定]** をクリックします。  
  
3. app.config ファイルまたは web.config ファイルでデバッグを有効にします。 詳細については、「[WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)」を参照してください。  
  
4. クライアント プロジェクト内の、ステップ実行を開始する位置にブレークポイントを設定します。 通常、これは WCF サービス呼び出しの直前です。  
  
5. ブレークポイントまで実行した後、ステップ実行を開始します。 デバッガーがサービスに自動的にステップ インします。  
  
## <a name="see-also"></a>参照  
 [WCF サービスのデバッグ](../debugger/debugging-wcf-services.md)   
 [WCF デバッグに関する制限事項](../debugger/limitations-on-wcf-debugging.md)   
 [方法: セルフホストされている WCF サービスをデバッグする](../debugger/how-to-debug-a-self-hosted-wcf-service.md)
