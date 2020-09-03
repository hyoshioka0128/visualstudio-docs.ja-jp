---
title: デバッグエンジンの実装戦略を選択する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6b03e69892da217d84d56b39b7df61784907d2b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68183468"
---
# <a name="choosing-a-debug-engine-implementation-strategy"></a>デバッグ エンジンの実装方法の選択
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

実行時アーキテクチャを使用して、デバッグエンジン (DE) 実装戦略を決定します。 デバッグエンジンは、デバッグ対象のプログラムに対してインプロセスで作成したり、Visual Studio セッションデバッグマネージャー (SDM) に対してインプロセスで作成したり、その両方に対してプロセス外で作成したりすることができます。 次のガイドラインは、これら3つの方法のいずれかを選択するのに役立ちます。  
  
## <a name="guidelines"></a>ガイドライン  
 SDM とデバッグ対象のプログラムの両方に対してアウトプロセスを実行することはできませんが、通常、これを行う理由はありません。 プロセス境界を越えた呼び出しは比較的低速です。  
  
 デバッグエンジンは、Win32 ネイティブランタイム環境および共通言語ランタイム環境に対して既に用意されています。 これらの環境のいずれかの DE を置き換える必要がある場合は、SDM でインプロセスを作成する必要があります。  
  
 それ以外の場合は、デバッグ対象のプログラムに対して SDM またはインプロセスのインプロセスを作成するかどうかを選択できます。 DE の式エバリュエーターがプログラムシンボルストアに頻繁にアクセスする必要があるかどうか、および高速アクセスのためにシンボルストアをメモリに読み込むかどうかを検討することが重要です。 また、以下の点についても検討してください。  
  
- 式エバリュエーターとシンボルストアの間に多数の呼び出しがない場合、または、シンボルストアを SDM メモリ空間に読み取ることができる場合は、SDM へのインプロセスを作成します。 プログラムにアタッチするときは、デバッグエンジンの CLSID を SDM に返す必要があります。 SDM は、この CLSID を使用して、DE のインプロセスインスタンスを作成します。  
  
- DE がシンボルストアにアクセスするためにプログラムを呼び出す必要がある場合は、プログラムでインプロセスインプロセスを作成します。 この場合、プログラムは DE のインスタンスを作成します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio デバッガーの拡張性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
