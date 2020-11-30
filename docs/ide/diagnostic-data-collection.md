---
title: 診断データとシステムによって生成されたログ
description: Visual Studio のシステムによって生成されたログ、収集されるデータの種類、およびそれを使用して問題を修正し、製品の品質を向上させる方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 05/24/2018
ms.topic: conceptual
author: jillre
ms.author: michma
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 93f450eab5879991f45f4a924338d4a277d13544
ms.sourcegitcommit: 66cda27b63c9b55782b1db223a6dbda9f8cabe13
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2020
ms.locfileid: "95005926"
---
# <a name="system-generated-logs-collected-by-visual-studio"></a>Visual Studio で収集したシステムによって生成されたログ

Visual Studio は、問題の修正と製品の品質向上のために、[Visual Studio カスタマー エクスペリエンス向上プログラム](visual-studio-experience-improvement-program.md)を介してシステムによって生成されたログを収集します。 この記事では、Microsoft が収集するデータの種類とその使用方法に関する情報を提供します。 また、拡張機能の作成者が個人情報や機密情報の不慮の漏洩を回避する方法に関するヒントも提供します。

## <a name="types-of-collected-data"></a>収集されるデータの種類

Visual Studio では、クラッシュ、UI の無応答、CPU またはメモリの使用率が高い状況のシステムで生成されたログが収集されます。 製品のインストールまたは使用中に発生したエラーに関する情報も収集します。 収集したデータは、エラーによって異なり、スタック トレース、メモリ ダンプ、例外情報が含まれる場合があります。

- 高い CPU 使用率と無応答については、関連する Visual Studio のスレッドのスタック トレースが収集されます。

- いくつかのスレッドのスタック トレースでは問題の原因を特定するために十分ではない場合、たとえば、クラッシュ、無応答、高いメモリ使用率については、メモリ *ダンプ* が収集されます。 ダンプは、エラーが発生したときのプロセスの状態を表します。

- ディスク上のファイルに書き込もうとしているときの例外など、予期しないエラー条件については、例外に関する情報を収集します。 この情報には、例外の名前、例外が発生したスレッドのスタック トレース、例外に関連するメッセージ、特定の例外に関連するその他の情報が含まれています。

   収集したデータの次の例では、例外の名前、スタック トレース、例外メッセージを示しています。

   ```text
   "Reserved.DataModel.Fault.Exception.TypeString": "System.IO.IOException",
   "Reserved.DataModel.Fault.Exception.StackTrace": "System.IO.__Error.WinIOError(Int32,String)\r\n
   System.IO.FileStream.Init(String,FileMode,FileAccess,Int32,Boolean,FileShare,Int32,FileOptions,SECURITY_ATTRIBUTES,String,Boolean,Boolean,Boolean)\r\n
   System.IO.FileStream..ctor(String,FileMode,FileAccess,FileShare,Int32,FileOptions,String,Boolean,Boolean,Boolean)\r\nSystem.IO.StreamWriter.CreateFile(String,Boolean,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean,Encoding,Int32,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean)\r\n
   System.IO.File.CreateText(String)\r\n
   Microsoft.VisualStudio.Setup.Services.FileSystem.CreateText(String,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.WriteChannelManifest(IChannelManifest,String,String)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.CacheManager.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.ChannelManager.\<UpdateAsync>d__37.MoveNext()\r\n”,
   "Reserved.DataModel.Fault.Exception.Message": " The process cannot access the file 'C:\\Users\\[UserName]\\AppData\\Local\\Microsoft\\VisualStudio\\Packages\\_Channels\\4CB340F5\\channelManifest.json' because it is being used by another process."
   ```

## <a name="how-we-use-system-generated-logs"></a>システムによって生成されたログの使用方法

エラーの根本原因を特定するワークフローは、エラーの種類とその重要度によって異なります。

### <a name="error-classification"></a>エラーの分類

ログに基づいて、エラーが分類され、調査の優先度付けのためにカウントされます。 たとえば、"System.IO.FileStream.Init" での "System.IO.\__Error.WinIOError" が、製品のバージョン \<x> で 500 回発生し、そのバージョンで発生率が最高になっていることを検出することがあります。

### <a name="work-items-for-tracking"></a>追跡のための作業項目

優先順位の高い個々のエラーの作業項目が作成され、調査のためのエンジニアに割り当てられています。 これらの作業項目には一般的に分類、優先度、エラーの種類に関連する診断情報が含まれます。 この情報は、収集したシステムによって生成されたエラーのログから取得されます。 たとえば、クラッシュの作業項目には、クラッシュが発生しているスタック トレースが含まれる場合があります。

### <a name="error-investigation"></a>エラーの調査

エンジニアは、エラーの根本原因を特定するのに作業項目で使用できる情報を使用します。 場合によっては、作業項目に存在する情報よりも多くの情報が必要になることがあります。その場合は、収集された元のシステムによって生成されたログを参照します。 たとえば、エンジニアは製品のクラッシュを理解するためにメモリ ダンプを調査する可能性があります。

## <a name="tips-for-extension-authors"></a>拡張機能の作成者のための関するヒント

拡張機能の作成者は、モジュール、種類、メソッドの名前に個人情報やその他の機密情報を使用しないようにすることで、個人情報の漏洩を制限する必要があります。 クラッシュまたはそれに似たエラー状態が、スタックのそのコードで発生した場合、その情報は、システムによって生成されたログの一部として収集されます。

## <a name="opt-out-of-data-collection"></a>データ収集のオプトアウト

収集するデータの目的とそのアクセスとリテンション期間の制約を考えた場合、Visual Studio および Windows の既定のプライバシー設定を使用することお勧めします。 ただし、Visual Studio エクスペリエンス向上プログラムへの参加は[オプトアウト](../ide/visual-studio-experience-improvement-program.md#opt-in-or-out)することができます。 すべてのプログラムのシステムによって生成されたログの収集をオプトアウトするには、「[Windows 10 の診断、フィードバック、プライバシー](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy)」を参照してください。 オプションは、ご使用の Windows のバージョンによって異なる場合があります。

## <a name="see-also"></a>関連項目

- [Visual Studio カスタマー エクスペリエンス向上プログラム](visual-studio-experience-improvement-program.md)
- [Windows 10 の診断、フィードバック、プライバシー](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy)