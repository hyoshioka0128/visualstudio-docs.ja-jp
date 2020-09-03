---
title: 例外の後にシステム コードを調べる | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging, exceptions
- exceptions, debugging
ms.assetid: a38ad49b-7cf3-483d-91c4-eb3116eba50c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9fe2dcc283f84bbcd5cd0b5a04dd5d1c300d9e14
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85349654"
---
# <a name="how-to-examine-system-code-after-an-exception"></a>方法: 例外の後にシステム コードを調べる
例外が発生した場合、システム コール内のコードを調べて、例外の原因を判断する必要がある場合があります。 システム コードのシンボルが読み込まれていない場合、または [マイ コードのみ] が有効な場合にこの操作を行う方法を次の手順に示します。

### <a name="to-examine-system-code-following-an-exception"></a>例外の後にシステム コードを調べるには

1. **[呼び出し履歴]** ウィンドウを右クリックし、 **[外部コードの表示]** をクリックします。

     [マイ コードのみ] が有効でない場合、ショートカット メニューにこのオプションは表示されず、既定でシステム コードが表示されます。

2. **[呼び出し履歴]** ウィンドウに表示される外部コード フレームを右クリックします。

3. **[シンボルの読み込み元]** をポイントし、 **[Microsoft シンボル サーバー]** をクリックします。

    1. [マイ コードのみ] が有効な場合、ダイアログ ボックスが表示されます。 [マイ コードのみ] が無効になったことが示されます。 これは、システム コールにステップ インするために必要です。

    2. **[パブリック シンボルをダウンロードしています]** ダイアログ ボックスが表示されます。 このダイアログ ボックスは、ダウンロードが終了すると消えます。

4. **[呼び出し履歴]** ウィンドウおよび他のウィンドウで、システム コードを調べることができるようになります。 たとえば、呼び出し履歴のフレームをダブルクリックすると、ソースや **[逆アセンブル]** ウィンドウ内のコードを表示できます。

## <a name="see-also"></a>関連項目
- [デバッガーでの例外の管理](../debugger/managing-exceptions-with-the-debugger.md)