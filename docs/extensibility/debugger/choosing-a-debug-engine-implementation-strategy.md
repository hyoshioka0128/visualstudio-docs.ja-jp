---
title: デバッグ エンジン実装戦略の選択 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739131"
---
# <a name="choose-a-debug-engine-implementation-strategy"></a>デバッグ エンジン実装戦略を選択する
ランタイム アーキテクチャを使用して、デバッグ エンジン (DE) 実装戦略を決定します。 デバッグ中のプログラムに対してデバッグ エンジンをインプロセスで作成できます。 デバッグ エンジンをインプロセスで作成して、Visual Studio セッション デバッグ マネージャー (SDM) にします。 または、両方のデバッグ エンジンのアウトプロセスを作成します。 次のガイドラインは、これら 3 つの戦略の中から選択する際に役立ちます。

## <a name="guidelines"></a>ガイドライン
 DE が SDM とデバッグしているプログラムの両方にアウトプロセスになることは可能ですが、通常はそうする理由はありません。 プロセス境界を越えた呼び出しは、比較的低速です。

 デバッグ エンジンは、Win32 ネイティブランタイム環境と共通言語ランタイム環境用に既に提供されています。 どちらの環境でも DE を置き換える必要がある場合は、SDM を使用して DE インプロセスを作成する必要があります。

 それ以外の場合は、De インプロセスを SDM に作成するか、デバッグ中のプログラムにインプロセスを作成します。 DE の式エバリュエーターがプログラムシンボルストアに頻繁にアクセスする必要があるかどうかを考慮する必要があります。 または、シンボル ストアがメモリに読み込まれて高速アクセスできる場合。 また、次の方法も検討してください。

- 式エバリュエーターとシンボル ストアの間に多くの呼び出しがない場合、またはシンボル ストアを SDM メモリ空間に読み込むことができる場合は、SDM に対して DE インプロセスを作成します。 プログラムにアタッチする場合は、デバッグ エンジンの CLSID を SDM に返す必要があります。 SDM はこの CLSID を使用して DE のインプロセス インスタンスを作成します。

- DE がプログラムを呼び出してシンボル ストアにアクセスする必要がある場合は、そのプログラムを使用して DE インプロセスを作成します。 この場合、プログラムは DE のインスタンスを作成します。

## <a name="see-also"></a>関連項目
- [デバッガーの機能拡張](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
