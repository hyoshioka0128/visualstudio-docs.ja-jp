---
title: リモート コンピューターが [リモート接続] ダイアログに表示されない | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5392a6219b1bf8bf42146cacf8216a63f1fa3832
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852564"
---
# <a name="error-remote-machine-does-not-appear-in-a-remote-connections-dialog"></a>エラー :リモート コンピューターが [リモート接続] ダイアログに表示されません
リモート コンピューターが [リモート接続] ダイアログ ボックスに表示されない場合、下記の一般的な原因を確認してください。

 マネージド互換モードを使用している場合は、Visual Studio 2010 用のマニュアル:「[リモート デバッグのトラブルシューティング - Visual Studio 2010](/previous-versions/visualstudio/visual-studio-2010/2ys11ead(v=vs.100))」を調べてください。

### <a name="common-causes-for-this-error"></a>このエラーの一般的な原因

- リモート コンピューターが別のサブネット内に存在するコンピューター上で実行されています。 この問題を解決するには、[修飾子] ダイアログ ボックスで、コンピューター名または IP アドレスを手動で入力します。

- リモート デバッガーがリモート コンピューター上で実行されていません。 この問題を解決するには、リモート デバッガーを起動します。

- ファイアウォールで、Visual Studio とリモート コンピューター間の通信がブロックされています。 これを解決するには、Visual Studio とリモート デバッガー (msvsmon) の通信を許可するようにファイアウォールを構成します。

- ウイルス対策ソフトウェアで、Visual Studio とリモート コンピューター間の通信がブロックされています。 これを解決するには、Visual Studio とリモート デバッガー (msvsmon) の通信を許可するようにウイルス対策ソフトウェアを構成します。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)