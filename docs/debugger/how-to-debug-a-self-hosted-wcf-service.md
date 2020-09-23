---
title: セルフホステッド WCF サービスをデバッグする | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, WCF
- WCF, self-hosted service
- WCF, debugging
ms.assetid: 288922be-ba3f-411e-af50-bba39c9529cc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ac58c187e147040c5ef82320a3b44e86912ed5b8
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852192"
---
# <a name="how-to-debug-a-self-hosted-wcf-service"></a>方法: セルフホストされている WCF サービスをデバッグする
*セルフホストされているサービス*とは、IIS 内部で実行されていない WCF サービス、WCF サービス ホスト、または [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 開発サーバーです。 セルフホストされている WCF をデバッグする最も簡単な方法は、 **[デバッグ]** メニューの **[デバッグ開始]** をクリックしたときにクライアントとサーバーの両方を起動するよう、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] を構成することです。

 NT サービスなど、この方法で起動できないプロセス内部で WCF サービスがセルフホストされている場合、この手法は使用できません。 代わりに、次の方法のいずれかを使用できます。

- ホスト プロセスにデバッガーを手動でアタッチします。 詳細については、[実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)に関するページを参照してください。

     または

- クライアントでデバッグを開始し、次にサービスへの呼び出しにステップ インします。 これを行うには、app.config ファイルでデバッグを有効にする必要があります。 詳細については、「[WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)」を参照してください。

### <a name="to-start-both-client-and-host-from-visual-studio"></a>Visual Studio からクライアントとホストの両方を起動するには

1. クライアント プロジェクトとサーバー プロジェクトの両方を含む [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ソリューションを作成します。

2. ソリューションを構成して、 **[デバッグ]** メニューの **[開始]** をクリックしたときにクライアント プロセスとサーバー プロセスの両方を起動します。

   1. **ソリューション エクスプローラー**でソリューション名を右クリックします。

   2. **[スタートアップ プロジェクトの設定]** をクリックします。

   3. **[ソリューション \<name> プロパティ]** ダイアログ ボックスで、 **[マルチ スタートアップ プロジェクト]** を選択します。

   4. **[マルチ スタートアップ プロジェクト]** グリッドのサーバー プロジェクトに対応する行で、 **[アクション]** をクリックし、 **[開始]** を選択します。

   5. クライアント プロジェクトに対応する行で、 **[アクション]** をクリックし、 **[開始]** を選択します。

   6. **[OK]** をクリックします。

## <a name="see-also"></a>関連項目
- [WCF サービスのデバッグ](../debugger/debugging-wcf-services.md)
- [WCF デバッグの制約](../debugger/limitations-on-wcf-debugging.md)
- [方法: WCF サービスにステップインする](../debugger/how-to-step-into-wcf-services.md)