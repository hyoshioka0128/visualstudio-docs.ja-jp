---
title: ビジュアライザーのセキュリティに関する考慮事項 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- visualizers, security
- security [Visual Studio], visualizers
ms.assetid: cdd86bd5-b729-409b-a7c6-374efa091eb1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c1c18ec84a6a62da6cd564c69ef4b83ea76bcfd6
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73187149"
---
# <a name="visualizer-security-considerations"></a>ビジュアライザーのセキュリティに関する考慮事項
ビジュアライザーを作成すると、セキュリティ上の脅威が発生する可能性があります。 今のところ、この脅威が悪用された例はありませんが、開発者はこの脅威を認識し、以下に説明する適切なセキュリティ対策を講じることによって将来の攻略行為に対抗する必要があります。

 デバッガー ビジュアライザーでは、部分信頼アプリケーションが許可する以上の特権が必要です。 部分信頼コードで動作が停止した場合、ビジュアライザーは読み込まれません。 ビジュアライザーを使用してデバッグするには、完全信頼コードを実行する必要があります。

## <a name="possible-malicious-debuggee-component"></a>悪意のあるデバッグ対象コンポーネント
 ビジュアライザーは、1 つはデバッガー側、もう 1 つはデバッグ対象側の少なくとも 2 つのクラスで構成されます。 ビジュアライザーは、特別なディレクトリに配置された別個のアセンブリに配置されることがよくありますが、デバッグ対象から読み込むこともできます。 その場合、デバッガーはデバッグ対象からコードを取得し、そのコードをデバッガー内部で完全な信頼で実行します。

 デバッグ対象が完全に信頼されていないときにデバッグ対象側のコードを完全信頼で実行すると、問題になります。 そのため、ビジュアライザーが、デバッグ対象からデバッガーに部分信頼アセンブリを読み込もうとした場合、Visual Studio はビジュアライザーを終了します。

 それでもまだ小さな脆弱性が存在します。 デバッグ対象側は、デバッグ対象以外の別のソースから読み込んだものをデバッガー側に関連付けることができます。 これにより、デバッグ対象側は、その信頼されたデバッガー側に対し、代わりにアクションを実行するように指示できます。 そのため、信頼されたデバッガー側のクラスが、"このファイルを削除する" 機構などを公開している場合、ユーザーがビジュアライザーを呼び出すと、部分信頼デバッグ対象はこの機構を呼び出す可能性があります。

 このような脆弱性を軽減するために、ビジュアライザーによって公開されるインターフェイスに注意する必要があります。

## <a name="see-also"></a>関連項目
- [ビジュアライザーのアーキテクチャ](../debugger/visualizer-architecture.md)
- [方法: ビジュアライザーを記述する](create-custom-visualizers-of-data.md)
- [カスタム ビジュアライザーを作成する](../debugger/create-custom-visualizers-of-data.md)
- [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)