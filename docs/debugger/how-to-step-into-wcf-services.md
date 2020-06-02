---
title: '方法: WCF サービスにステップインする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, debugging
ms.assetid: 9893ad01-54af-499f-85a6-9d1cfe6eb640
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c405b4fcca91f8deddce4d65c8a4155b90af49e0
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72732598"
---
# <a name="how-to-step-into-wcf-services"></a>方法: WCF サービスにステップインする
[!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] では、WCF サービスにステップ インできます。 WCF サービスがクライアントと同じ [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ソリューションにある場合、WCF サービス内のブレークポイントに到達できます。

 ステップ実行を使用するには、app.config ファイルまたは Web.config ファイルでデバッグを有効にする必要があります。 デバッグを有効にする方法と WCF サービスにステップ インする際の制約については、「[WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)」を参照してください。

### <a name="to-step-into-a-wcf-service"></a>WCF サービスにステップ インするには

1. WCF クライアント プロジェクトと WCF サービス プロジェクトの両方を含む [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ソリューションを作成します。

2. ソリューション エクスプローラーで、WCF クライアント プロジェクトを右クリックして、 **[スタートアップ プロジェクトに設定]** をクリックします。

3. app.config ファイルまたは web.config ファイルでデバッグを有効にします。 詳細については、「[WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)」を参照してください。

4. クライアント プロジェクト内の、ステップ実行を開始する位置にブレークポイントを設定します。 通常、これは WCF サービス呼び出しの直前です。

5. ブレークポイントまで実行した後、ステップ実行を開始します。 デバッガーがサービスに自動的にステップ インします。

## <a name="see-also"></a>関連項目
- [WCF サービスのデバッグ](../debugger/debugging-wcf-services.md)
- [WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)
- [方法: セルフホストされている WCF サービスをデバッグする](../debugger/how-to-debug-a-self-hosted-wcf-service.md)