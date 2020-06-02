---
title: セキュリティ警告:信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。 以下の情報に関して疑わしい点がある場合や不明な場合はこのプロセスにアタッチしないでください | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.attachsecuritywarning
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 52246c1e-a371-40a0-b756-a435cc51876f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 05b78ea0ca06a0ba9670e61cc065cf539ea21ebc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729773"
---
# <a name="security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process"></a>セキュリティ警告:信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。 以下の情報に関して疑わしい点がある場合や、不明な場合は、このプロセスにアタッチしないでください。
この警告ダイアログ ボックスは、部分的に信頼されているコードを含むプロセスや、信頼関係のないユーザーが所有するプロセスにアタッチしようとすると表示されます。 悪意のあるコードを含む信頼関係のないプロセスによって、デバッグを実行しているコンピューターに障害が発生する可能性があります。 何らかの理由によりプロセスを信頼していない場合は、 **[キャンセル]** をクリックしてデバッグを回避します。

 正当なシナリオをデバッグするときにこの警告を表示しないようにするには、Visual Studio を終了し、レジストリ キー `HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\<version>\Debugger\DisableAttachSecurityWarning` の値を 1 に設定します。その後、Visual Studio を再起動します。 シナリオのデバッグが終わったら、値を 0 にリセットし、Visual Studio を再起動します。

 "信頼できるユーザー" には、ユーザー自身と、.NET Framework がインストールされているコンピューターで一般に定義される標準ユーザーのグループ (`aspnet`、`localsystem`、`networkservice`、`localservice` など) が含まれます。

## <a name="uielement-list"></a>UIElement の一覧
 名前: デバッグが要求されたアセンブリの名前

 ユーザー: 現在のユーザー

 アタッチ: 押すと、アタッチによるデバッグが継続されます

 アタッチしない: プロセスにアタッチしません

## <a name="see-also"></a>関連項目
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)