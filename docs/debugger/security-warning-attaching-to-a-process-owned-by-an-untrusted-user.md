---
description: この警告ダイアログ ボックスは、部分的に信頼されているコードを含むプロセスや、信頼関係のないユーザーが所有するプロセスにアタッチしようとすると表示されます。
title: セキュリティ警告:信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。 以下の情報に関して疑わしい点がある場合や不明な場合はこのプロセスにアタッチしないでください | Microsoft Docs
ms.date: 1/15/2021
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 9fe65e753a0e825eed0c09fdefc4e93168d27ecb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160317"
---
# <a name="security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process"></a>セキュリティ警告:信頼されていないユーザーが所有するプロセスにアタッチするには危険が伴います。 以下の情報に関して疑わしい点がある場合や、不明な場合は、このプロセスにアタッチしないでください。

この警告ダイアログ ボックスは、部分的に信頼されているコードを含むプロセスや、信頼関係のないユーザーが所有するプロセスにアタッチしようとすると表示されます。 悪意のあるコードを含む信頼関係のないプロセスによって、デバッグを実行しているコンピューターに障害が発生する可能性があります。 何らかの理由によりプロセスを信頼していない場合は、 **[キャンセル]** をクリックしてデバッグを回避します。

IIS のシナリオでは、信頼されていないカスタム アプリケーション プールを使用すると、この警告が表示される場合があります。

正当なシナリオをデバッグするときに、この警告を表示しないようにするには:

1. Visual Studio を閉じます。

1. `DisableAttachSecurityWarning` レジストリ キーの値を 1 に設定します。

   `HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\<version>\Debugger` でキーを検索または作成し、1 に設定します。

   Visual Studio 2017 以降では、レジストリの完全な設定を表示する場合、プライベート レジストリ ハイブを読み込む必要があります。 詳細については、「[Visual Studio 2017 レジストリを調べる方法](https://github.com/microsoft/VSProjectSystem/blob/master/doc/overview/examine_registry.md)」をご覧ください。 Visual Studio を起動する前に、必ずプライベート レジストリ ハイブをアンロードしてください。

1. Visual Studio を再起動します。

1. シナリオのデバッグが終わったら、値を 0 にリセットし、Visual Studio を再起動します。

"信頼できるユーザー" には、ユーザー自身と、.NET Framework がインストールされているコンピューターで一般に定義される標準ユーザーのグループ (`aspnet`、`localsystem`、`networkservice`、`localservice` など) が含まれます。

## <a name="uielement-list"></a>UIElement の一覧

 名前: デバッグが要求されたアセンブリの名前

 ユーザー: 現在のユーザー

 アタッチ: 押すと、アタッチによるデバッグが継続されます

 アタッチしない: プロセスにアタッチしません

## <a name="see-also"></a>関連項目
- [実行中のプロセスへのアタッチ](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
