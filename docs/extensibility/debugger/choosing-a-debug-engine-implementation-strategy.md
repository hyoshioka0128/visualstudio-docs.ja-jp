---
title: デバッグエンジンの実装戦略を選択する |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, implementation strategies
ms.assetid: 90458fdd-2d34-4f10-82dc-6d8f31b66d8b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 05e66975a2d41108d3d9fb469da9e4a36a10d8d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739131"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>デバッグエンジンの実装方法を選択する
実行時アーキテクチャを使用して、デバッグエンジン (DE) 実装戦略を決定します。 デバッグ中のプログラムにデバッグエンジンをインプロセスで作成できます。 Visual Studio セッションデバッグマネージャー (SDM) にデバッグエンジンをインプロセスで作成します。 または、その両方に対してデバッグエンジンをアウトプロセスで作成します。 次のガイドラインは、これら3つの方法のいずれかを選択するのに役立ちます。

## <a name="guidelines"></a>ガイドライン
 SDM とデバッグ中のプログラムの両方に対してアウトプロセスを実行することはできませんが、通常はそうする必要はありません。 プロセス境界を越えた呼び出しは比較的低速です。

 デバッグエンジンは、Win32 ネイティブランタイム環境および共通言語ランタイム環境用に既に用意されています。 どちらの環境でも DE を置き換える必要がある場合は、SDM でインプロセスを作成する必要があります。

 それ以外の場合は、デバッグ中のプログラムに対して SDM またはインプロセスのインプロセスを作成します。 DE の式エバリュエーターがプログラムシンボルストアに頻繁にアクセスする必要があるかどうかを検討する必要があります。 または、高速アクセスのためにシンボルストアをメモリに読み込むことができます。 また、次の方法を検討してください。

- 式エバリュエーターとシンボルストアの間に多数の呼び出しがない場合、または、シンボルストアを SDM メモリ空間に読み取ることができる場合は、SDM へのインプロセスを作成します。 プログラムにアタッチするときは、デバッグエンジンの CLSID を SDM に返す必要があります。 SDM は、この CLSID を使用して、DE のインプロセスインスタンスを作成します。

- DE がシンボルストアにアクセスするためにプログラムを呼び出す必要がある場合は、プログラムでインプロセスインプロセスを作成します。 この場合、プログラムは DE のインスタンスを作成します。

## <a name="see-also"></a>関連項目
- [Visual Studio デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
