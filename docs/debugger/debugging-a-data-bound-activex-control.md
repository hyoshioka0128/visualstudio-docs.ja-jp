---
title: データ連結 ActiveX コントロールのデバッグ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- data-bound controls, ActiveX
- ActiveX controls, debugging
- controls [Visual Studio], ActiveX
ms.assetid: 9f6e1f00-e25b-48a9-8484-7e67a1232461
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ccca00387e701d62e47eee0a93adff44a4765fa2
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89600070"
---
# <a name="debugging-a-data-bound-activex-control"></a>データ連結 ActiveX コントロールのデバッグ
データ ソース コントロールに連結する ActiveX コントロールを開発している場合、独自のコンテナー アプリケーションを作成し、そのコンテナーを使用して ActiveX コントロールをデバッグできます。

 たとえば、ダイアログ ベースの MFC アプリケーションを作成して、ダイアログ ボックスにデータ連結コントロールとデータ ソース コントロールを配置します。 この MFC アプリケーションは、データ連結 ActiveX コントロールをデバッグするためのコンテナー実行可能ファイルとして、ランタイム テストに使用できます。

## <a name="using-the-test-container"></a>テスト コンテナーの使用
 簡単に変更できるコンテナーでコントロールまたはコンテナーのさまざまなインターフェイスをサポートする場合は、デバッグ セッションの実行可能ファイルとして ActiveX テスト コンテナーを使用します。 ActiveX テスト コンテナーで、 **[コンテナー]** メニューの **[オプション]** をクリックしてさまざまなインターフェイスを有効にします。 詳細については、「[テスト コンテナーでのプロパティとイベントのテスト](/cpp/mfc/testing-properties-and-events-with-test-container)」を参照してください。

 デバッグ中にコンテナーのコードにステップ インする必要がある場合は、デバッグ バージョンのコンテナーを使用するか、デバッグ バージョンの ActiveX テスト コンテナーを使用します。 詳細については、「[TSTCON のサンプル: ActiveX コントロール テスト コンテナー](/previous-versions/f9adb5t5(v=vs.100))」を参照してください。

## <a name="see-also"></a>関連項目
- [COM および ActiveX のデバッグ](../debugger/com-and-activex-debugging.md)
- [ActiveX コントロール](/cpp/mfc/activex-controls)