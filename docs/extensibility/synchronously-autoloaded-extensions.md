---
title: 同期的に自動的に読み込む拡張機能
ms.date: 12/11/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ab62d235fd6ed4e47e765fc23868acd5c56efcb2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699368"
---
# <a name="synchronously-autoloaded-extensions"></a>同期的に自動的に読み込む拡張機能

同期的に自動読み込まれた拡張機能は、Visual Studio のパフォーマンスに悪影響を及ぼし、代わりに非同期自動読み込みを使用するように変換する必要があります。 既定では、Visual Studio 2019 は、任意の拡張機能から同期的に自動読み込まれたパッケージをブロックし、ユーザーに通知します。

![拡張機能の互換性に関する警告](media/extension-compatibility-warning-16-1.png.png)

次のようにすることができます。

- [**同期自動ロードを許可する]** をクリックして、拡張機能の自動ロードを許可します。 Visual Studio のオプションでこの設定を変更するには、[環境]、[ 拡張機能] の順にクリックし、[拡張機能の同期自動ロードを許可する] チェック ボックスをオンにします。 

- **[パフォーマンスの管理**] をクリックして、[[パフォーマンス マネージャ] ダイアログ](#performance-manager-dialog)を開き、拡張機能とツール ウィンドウのパフォーマンスの問題を表示します。

- **[現在の拡張機能の場合は、このメッセージを表示しない**] をクリックして通知を消去し、既存のインストール済み拡張機能からの今後の通知を禁止します。 同期的に自動ロードする新しい拡張機能を追加すると、この通知が再び表示されます。 他の Visual Studio 機能に関する通知を引き続き取得します。

## <a name="performance-manager-dialog"></a>[パフォーマンス マネージャ]ダイアログ

![パフォーマンス マネージャー ダイアログ](media/performance-manager.png)

任意のユーザー セッションでパッケージを同期的に読み込んだすべての拡張機能は **、[非推奨の API]** タブに表示されます。

* 廃止予定の API に**関する詳細情報**を収集するには、この問題の詳細情報をクリックしてください。
* 移行の進行状況については、拡張機能のベンダーに問い合わせてください。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>グループ ポリシーを使用して同期自動読み込み設定を指定する

管理者は、同期自動読み込みを許可するグループ ポリシーを有効にできます。 これを行うには、次のキーでレジストリ ベースのポリシーを設定します。

**HKEY_LOCAL_MACHINE\ソフトウェア\ポリシー\マイクロソフト\ビジュアルスタジオ\同期自動ロード**

入力 =**許可**

値 = (DWORD)
* **0**は同期自動ロードが許可されていません
* **1**は同期自動ロードが許可されています

## <a name="extension-authors"></a>拡張著者
拡張機能の作成者は、非同期自動読み込みにパッケージを移行する手順については、「 [AsyncPackage に移行する 」を参照](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)してください。

## <a name="see-also"></a>関連項目
Visual Studio 2019 での同期自動読み込みの設定の詳細については、「[同期自動読み込みの動作](https://devblogs.microsoft.com/visualstudio/updates-to-synchronous-autoload-of-extensions-in-visual-studio-2019/)」ページを参照してください。
