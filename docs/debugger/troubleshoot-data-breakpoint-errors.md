---
title: 'エラー: データブレークポイントを設定できません |Microsoft Docs'
ms.date: 12/3/2019
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.unable_to_set_data_breakpoint
dev_langs:
- CSharp
helpviewer_keywords:
- debugging [Visual Studio], managed
- debugging managed code, data breakpoint
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: wardengnaw
ms.author: waan
manager: caslan
ms.workload:
- multiple
ms.openlocfilehash: 18fa63f2a6f4b6d789bad6f813cb3956a636a2d2
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404084"
---
# <a name="troubleshooting-data-breakpoint-errors"></a>データブレークポイントエラーのトラブルシューティング
このページでは、[値の変更時に中断] を使用したときに発生する一般的なエラーの解決について説明します。

## <a name="diagnosing-unable-to-set-data-breakpoint-errors"></a>"データブレークポイントを設定できません" エラーの診断
> [!IMPORTANT]
> マネージデータブレークポイントは、.NET Core 3.0 以降でサポートされています。 最新版は[こちら](https://dotnet.microsoft.com/download)からダウンロードできます。

次に示すのは、マネージデータのブレークポイントを使用する場合に発生する可能性があるエラーの一覧です。 エラーが発生した理由と、エラーを解決するための解決策または回避策について、追加の説明が含まれています。

- *"ターゲットプロセスで使用されている .NET のバージョンでは、データブレークポイントはサポートされていません。データブレークポイントには、x86 または x64 で実行されている .NET Core 3.0 以降が必要です。 "*

    - マネージデータブレークポイントのサポートは、.NET Core 3.0 で開始されました。 現在、.NET Framework または .NET Core のバージョン3.0 ではサポートされていません。 
    
    - **解決策**: この問題を解決するには、プロジェクトを .net Core 3.0 にアップグレードします。

- *"値はマネージドヒープで見つからず、追跡できません。"*
    - 変数がスタックで宣言されています。
        - 関数が終了すると、この変数は無効になるため、スタックで作成された変数のデータブレークポイントの設定はサポートされません。
        - **回避策**: 変数が使用されている行にブレークポイントを設定します。

    - ドロップダウンから展開されていない変数で、値が変化したときに中断します。
        - デバッガーは、追跡するフィールドを含むオブジェクトを内部的に認識している必要があります。ガベージコレクターは、オブジェクトをヒープ内で移動して、追跡する変数を保持しているオブジェクトをデバッガーが認識できるようにすることができます。 
        - **回避策**: データブレークポイントを設定するオブジェクト内のメソッドがある場合は、1つ上のフレームにアクセスし、[`locals/autos/watch`] ウィンドウを使用してオブジェクトを展開し、データブレークポイントに必要なフィールドを設定します。

- *"データブレークポイントは、静的フィールドまたは静的プロパティではサポートされていません。"*
    
    - 現時点では、静的フィールドおよび静的プロパティはサポートされていません。 この機能に関心がある場合は、[フィードバック](#provide-feedback)を提供してください。

- *"構造体のフィールドとプロパティを追跡できません。"*

    - 現時点では、構造体のフィールドとプロパティはサポートされていません。 この機能に関心がある場合は、[フィードバック](#provide-feedback)を提供してください。

- *"プロパティ値が変更され、追跡できなくなりました。"*

    - プロパティは、実行時の計算方法を変更する場合があります。この場合、プロパティが依存している変数の数が増加し、ハードウェアの制限を超える可能性があります。 この後の「`"The property is dependent on more memory than can be tracked by the hardware."`」を参照してください。

- *"プロパティは、ハードウェアによって追跡できる量よりも多くのメモリに依存しています。"*
    
    - 各アーキテクチャには、サポート可能なバイト数とハードウェアデータブレークポイントが設定されています。また、データブレークポイントを設定するプロパティは制限を超えています。 使用しているアーキテクチャでサポートされているハードウェアのデータブレークポイントとバイト数を確認するには、「[データブレークポイントのハードウェアの制限](#data-breakpoint-hardware-limitations)」の表を参照してください。 
    - **回避策**: プロパティ内で変更される可能性のある値にデータブレークポイントを設定します。

- *"従来C#の式エバリュエーターを使用する場合、データブレークポイントはサポートされません。"*

    - データブレークポイントは、レガシC#以外の式エバリュエーターでのみサポートされています。 
    - **解決策**: レガシC#式エバリュエーターを無効にするには `Debug -> Options` に移動し、[`Debugging -> General`] の下の [`"Use the legacy C# and VB expression evaluators"`] をオフにします。

## <a name="data-breakpoint-hardware-limitations"></a>データブレークポイントのハードウェアの制限

プログラムによって実行されるアーキテクチャ (プラットフォーム構成) には、使用できるハードウェアデータブレークポイントの数が制限されています。 次の表は、アーキテクチャごとに使用できるレジスタの数を示しています。

| アーキテクチャ | ハードウェアでサポートされているデータブレークポイントの数 | 最大バイトサイズ|
| :-------------: |:-------------:| :-------------:|
| x86 | 4 | 4 |
| x64 | 4 | 8 |
| ARM | 1 | 4 |
| ARM64 | 2 | 8 |

## <a name="provide-feedback"></a>フィードバックの提供
この機能に関する問題またはご提案については、IDE または[開発者コミュニティ](https://developercommunity.visualstudio.com/)で[問題を報告する](../ide/how-to-report-a-problem-with-visual-studio.md)ために、フィードバックの送信 > ヘルプ > にお知らせください。

## <a name="see-also"></a>関連項目
- [.Net Core 3.0 の "値が変更されたときに中断" を使用し](using-breakpoints.md#BKMK_set_a_data_breakpoint_native_cplusplus)ます。
- [DevBlog: 値が変更されると中断: Visual Studio 2019 での .NET Core のデータブレークポイント](https://devblogs.microsoft.com/visualstudio/break-when-value-changes-data-breakpoints-for-net-core-in-visual-studio-2019/)
