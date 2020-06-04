---
title: データ連結 ActiveX コントロールのデバッグ | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 82376be37eeb7dd7946b44556a2931e761e2824d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738239"
---
# <a name="debugging-a-data-bound-activex-control"></a>データ連結 ActiveX コントロールのデバッグ
データ ソース コントロールに連結する ActiveX コントロールを開発している場合、独自のコンテナー アプリケーションを作成し、そのコンテナーを使用して ActiveX コントロールをデバッグできます。

 たとえば、ダイアログ ベースの MFC アプリケーションを作成して、ダイアログ ボックスにデータ連結コントロールとデータ ソース コントロールを配置します。 この MFC アプリケーションは、データ連結 ActiveX コントロールをデバッグするためのコンテナー実行可能ファイルとして、ランタイム テストに使用できます。

## <a name="using-the-test-container"></a>テスト コンテナーの使用
 簡単に変更できるコンテナーでコントロールまたはコンテナーのさまざまなインターフェイスをサポートする場合は、デバッグ セッションの実行可能ファイルとして ActiveX テスト コンテナーを使用します。 ActiveX テスト コンテナーで、 **[コンテナー]** メニューの **[オプション]** をクリックしてさまざまなインターフェイスを有効にします。 詳細については、「[テスト コンテナーでのプロパティとイベントのテスト](/cpp/mfc/testing-properties-and-events-with-test-container)」を参照してください。

 デバッグ中にコンテナーのコードにステップ インする必要がある場合は、デバッグ バージョンのコンテナーを使用するか、デバッグ バージョンの ActiveX テスト コンテナーを使用します。 詳細については、「[TSTCON のサンプル: ActiveX コントロール テスト コンテナー](https://msdn.microsoft.com/library/72fa40ef-27d3-400c-813f-10b03236e600)」を参照してください。

## <a name="see-also"></a>関連項目
- [COM および ActiveX のデバッグ](../debugger/com-and-activex-debugging.md)
- [ActiveX コントロール](/cpp/mfc/activex-controls)