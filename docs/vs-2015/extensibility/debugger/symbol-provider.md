---
title: シンボルプロバイダー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6af1af9d2e178241fa8a5957e18c1a5333fa4b09
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68178898"
---
# <a name="symbol-provider"></a>シンボル プロバイダー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

式エバリュエーターの実装は、変数と式を評価するために、言語コンパイラによって生成されるシンボリックデバッグ情報にアクセスする必要があります。 これを行うには、シンボルプロバイダー (SP) のインターフェイスを使用します。これは、シンボルハンドラーとも呼ばれます。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] マネージコード用の Sp と、プログラムデータベース (PDB) シンボルファイル形式を使用するネイティブコードを提供します。 カスタム形式で格納されているシンボルをプログラムで使用する必要がある場合を除き、によって提供される SPs を使用することをお勧め [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] します。  
  
## <a name="implementation-notes"></a>実装に関するメモ  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]デバッグエンジンは、共通言語ランタイム (CLR) インターフェイスを使用して SPs と通信することを想定しています。 そのため、Visual Studio デバッグエンジンで動作する SP は、CLR をサポートしている必要があります。 すべての CLR デバッグインターフェイスの完全な一覧については、「」の一部である debugref.doc を参照 [!INCLUDE[winsdklong](../../includes/winsdklong-md.md)] してください。  
  
 SP がカスタムデバッグエンジンでのみ動作する場合は、デバッグエンジンのニーズに応じて、必要に応じて SP を実装できます。  
  
## <a name="see-also"></a>参照  
 [デバッガーのコンポーネント](../../extensibility/debugger/debugger-components.md)
