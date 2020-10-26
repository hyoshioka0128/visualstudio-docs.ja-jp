---
title: セキュリティの問題 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb6209882a7a71a68728299064edcc13afabff35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704420"
---
# <a name="security-issues"></a>セキュリティの問題
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio を使用してプログラムをデバッグするために必要なアクセス許可は、開発者がプログラムを実行するために必要なアクセス許可だけです。 これには、ほとんどの状況でのリモートデバッグが含まれます (インターネットインフォメーションサービスなど、他のサービスに関連する状況によっては、より高いレベルの権限が必要になる場合があります)。  
  
 Visual Studio の実行中、プロセスデバッグマネージャー (PDM) はローカルコンピューター上のデバッグプロセスを追跡します。 リモートデバッグを処理し、PDM を利用できるようにするために、開発者が msvsmon.exe と呼ばれるプログラムをリモートで起動します。 (msvsmon.exe はサービスではなく、そのコンピューターでリモートデバッグを有効にするために手動で開始する必要があることに注意してください。)Visual Studio (または msvsmon.exe) が実行されていない場合、デバッグのためにプロセスは追跡されません。  
  
 これは、開発者が特別なアクセス許可なしで自分で開始したプログラムをデバッグできることを意味します。 開発者は、他のユーザーが同じセキュリティグループのメンバーである場合に、他のユーザーによって開始されたプロセスをデバッグすることもできます。 リモートデバッグを有効にするには、必要なファイルをリモートコンピューターにコピーして msvsmon.exe を開始する必要があります (詳細については、「 [デバイスのリモートツールのセットアップ](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) 」を参照してください)。  
  
## <a name="see-also"></a>参照  
 [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)   
 [プロセスデバッグマネージャー](../../extensibility/debugger/process-debug-manager.md)   
 [デバイスのリモート ツールのセットアップ](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)
