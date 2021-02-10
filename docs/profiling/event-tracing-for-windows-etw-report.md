---
title: Event Tracing for Windows (ETW) レポート | Microsoft Docs
description: Event Trace for Windows (ETW) レポートについて説明します。これには、Visual Studio プロファイル ツールのパフォーマンス セッションで記録された ETW イベントが一覧表示されます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Event tracing for Windows profiling report
- ETW profiling report
ms.assetid: 81e88162-b88a-40b6-8b85-a232c8096a47
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 1a5a962ba3eaeee2c9f1e26132bf4ce6b12d9347
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955295"
---
# <a name="event-tracing-for-windows-etw-report"></a>ETW (Event Tracing for Windows) レポート
Windows イベント トレーシング (ETW) レポートには、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイル ツールのパフォーマンス セッションで記録された ETW イベントが一覧表示されます。 ETW データはバイナリ (.*etl*) ファイルで収集されます。

> [!NOTE]
> [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] インターフェイスでは ETW レポートを表示できません。

- [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] インターフェイスのプロファイル ツールを利用して ETW データを収集する方法については、「[方法:ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)」を参照してください。

- [VSPerfCmd](../profiling/vsperfcmd.md) コマンド ライン ツールを利用して ETW データを収集する方法については、「[Events](../profiling/events-vsperfcmd.md)」を参照してください。

- ETW レポートは **VSReport/Summary:ETW** コマンドを利用して生成します。 詳細については、「[VSPerfReport](../profiling/vsperfreport.md)」を参照してください。

|列|説明|
|------------|-----------------|
|**Timestamp**|イベントが発生した日時を識別します。|
|**プロセス ID**|イベントを生成したプロセスを識別します。|
|**スレッド ID**|イベントを生成したスレッドを識別します。|
|**説明**|イベント プロバイダーを識別します。|
|**Type**|イベントの種類を識別します。|
|**Properties**|イベントのプロパティ。 各イベントは角かっこで囲まれた名前と値のペアになり、コンマで区切られます。|
