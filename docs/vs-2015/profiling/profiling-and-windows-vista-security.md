---
title: プロファイルと Windows Vista のセキュリティ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,security
- performance tools, security
ms.assetid: 842112fc-b886-4801-8cd7-a25b314b0393
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d7e485bc6289634e1bb6d4b4106d54c8dc82096b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683700"
---
# <a name="profiling-and-windows-vista-security"></a>プロファイルと Windows Vista のセキュリティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コンピューターの管理者が使用可能にした [!INCLUDE[wiprlhext](../includes/wiprlhext-md.md)] ユーザー アクセス許可の設定に応じて、個々のユーザーは、コンピューター上でプロセスをプロファイリングするためのセキュリティ アクセス許可を持っている場合があります。 次の例では、考えられるユーザーごとの違いについて説明します。  
  
- 管理者がドライバーとサービスが起動するように設定しているときには、一部のユーザーが高度なプロファイリング機能にアクセスできることがあります。  
  
- ドメイン ユーザーはサンプルのプロファイリングにのみアクセスできる場合があります。  
  
- 一部のユーザーが他のすべてのユーザーに対してプロファイリングへのアクセスを拒否することがあります。  
  
  詳細については、「[VSPerfCmd](../profiling/vsperfcmd.md)」の ADMIN オプションを参照してください。  
  
## <a name="cross-session-profiling"></a>セッション間プロファイリング  
 *セッション間プロファイリング*は、別のログオン セッションで実行しているプロセスをプロファイリングする機能です。 たとえば、サービスのほとんどはセッション 0 で実行され、ユーザーはセッション 0 で直接実行できません。 パフォーマンス エクスプローラーのツールバーで **[プロセスにアタッチ]** ボタン、または VSPerfCmd コマンド ライン ツールの /attach オプションを使用して、さまざまなログオン セッションでのほとんどのプロセスをプロファイリングすることができます。  
  
 プロセス間のプロファイルの表示オプションを設定すると、使用できるプロセスの一覧が表示できます。 これらのオプションは、**[プロセスにアタッチ]** をクリックすると表示される **[プロセスにアタッチ]** ウィンドウで利用できます。  
  
- **全ユーザーのプロセスを表示する**  
  
     このオプションを選択していない場合、一覧には、現在のユーザーによって所有されているプロセスのみが表示されます。 **[全ユーザーのプロセスを表示する]** を選択すると、一覧には、すべてのユーザーのプロセスが表示されます。  
  
- **すべてのセッションのプロセスを表示**  
  
     このオプションを選択していない場合、一覧には、現在のセッションのプロセスが表示されます。 このオプションを選択すると、一覧には、すべてのセッションのプロセスが表示されます。  
  
## <a name="see-also"></a>参照  
 [概念](../profiling/overviews-performance-tools.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [方法: 実行中のプロセスにアタッチする](https://msdn.microsoft.com/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4)
