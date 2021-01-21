---
title: 同期的に自動的に読み込む拡張機能
description: Visual Studio 2019 以降の既定の動作について説明します。これは、任意の拡張機能から同期的に自動読み込みされたパッケージをブロックします。
ms.custom: SEO-VS-2020
ms.date: 12/11/2019
ms.topic: conceptual
ms.assetid: 822e3cf8-f723-4ff1-8467-e0fb42358a1f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 506c098f1f385ddf39c5d000f4571a8ee92c09fc
ms.sourcegitcommit: 94a57a7bda3601b83949e710a5ca779c709a6a4e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/21/2020
ms.locfileid: "97715445"
---
# <a name="synchronously-autoloaded-extensions"></a>同期的に自動的に読み込む拡張機能

同期的に自動読み込みされた拡張機能は、Visual Studio のパフォーマンスに悪影響を及ぼし、代わりに非同期の自動読み込みを使用するように変換する必要があります。 既定では、Visual Studio 2019 は、任意の拡張機能から同期的に自動読み込みされたパッケージをブロックし、ユーザーに通知します。

![拡張機能の互換性に関する警告](media/extension-compatibility-warning-16-1.png.png)

次のようにすることができます。

- [同期自動読み込みを **許可** する] をクリックして、拡張機能を自動読み込みできるようにします。 Visual Studio のオプションでこの設定を変更するには、[環境]、[拡張機能] の順にクリックし、[拡張機能の同期自動読み込みを許可する] チェックボックスをオンにします。 

- [ **パフォーマンスの管理** ] をクリックして [ [パフォーマンスマネージャー] ダイアログ](#performance-manager-dialog) を開き、拡張機能とツールウィンドウのパフォーマンスの問題を表示します。

- [ **現在の拡張機能にこのメッセージを表示しない** ] をクリックして通知を破棄し、インストール済みの既存の拡張からの今後の通知を防止します。 同期的に自動読み込みする新しい拡張機能を追加すると、この通知が再び表示されます。 その他の Visual Studio 機能に関する通知は引き続き表示されます。

## <a name="performance-manager-dialog"></a>パフォーマンスマネージャーダイアログ

![パフォーマンスマネージャーダイアログ](media/performance-manager.png)

ユーザーセッションのすべてのパッケージを同期的に読み込んだすべての拡張機能は、[ **非推奨の api** ] タブに表示されます。

* **この問題に関する詳細情報** をクリックすると、非推奨の api に関する詳細情報が収集されます。
* 移行の進行状況については、拡張機能のベンダーにお問い合わせください。

## <a name="specify-synchronous-autoload-settings-using-group-policy"></a>グループポリシーを使用して同期自動読み込みの設定を指定する

管理者は、グループポリシーを有効にして、同期自動読み込みを許可できます。 これを行うには、次のキーでレジストリ ベースのポリシーを設定します。

**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\SynchronousAutoload**

Entry = **許可**

値 = (DWORD)
* **0** は同期自動読み込みは許可されていません
* **1** 同期自動読み込みが可能

## <a name="extension-authors"></a>拡張機能の作成者
拡張機能の作成者は、「 [AsyncPackage への移行](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration)」の手順に従って、パッケージを非同期自動読み込みに移行する方法を確認できます。

## <a name="see-also"></a>関連項目
Visual Studio 2019 での同期自動読み込みの設定の詳細については、「同期自動読み込みの [動作](https://devblogs.microsoft.com/visualstudio/updates-to-synchronous-autoload-of-extensions-in-visual-studio-2019/) 」ページを参照してください。
