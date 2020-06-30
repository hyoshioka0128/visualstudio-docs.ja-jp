---
title: '方法: プロファイル ツールの ETW レポートを作成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: bf5547b3-f6c7-4989-9d47-2fe4f1261444
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 7dc74f0486ac7196cf406994ee603bc6c0cf4c25
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548006"
---
# <a name="how-to-create-a-profiling-tools-etw-report"></a>方法: プロファイリング ツールの ETW レポートを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows イベント トレーシング (ETW) レポートには、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイル ツールのパフォーマンス セッションで記録された ETW イベントが一覧表示されます。 ETW データはバイナリ (.etl) ファイルで収集されます。 このレポートの詳細については、「[ETW (Event Tracing for Windows) レポート](../profiling/event-tracing-for-windows-etw-report.md)」を参照してください。  
  
> [!NOTE]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の場合、インターフェイスに ETW レポートを表示できません。  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のインターフェイスを利用して ETW データを収集する方法については、「[方法: ETW (Event Tracing for Windows) データを収集する](../profiling/how-to-collect-event-tracing-for-windows-etw-data.md)」を参照してください。  
  
- コマンド プロンプトから ETW データを収集する方法については、「[VSPerfCmd](../profiling/vsperfcmd.md)」と「[イベント](../profiling/events-vsperfcmd.md)」を参照してください。  
  
  ETW レポートは **VSReport/summary:etw** コマンドを利用して生成します。 ETW データを含む .etl は、プロファイル データ (.vsp または .vsps) ファイルと同じディレクトリに置く必要があります。 既定では、レポートはコンマ区切り値 (.csv) ファイルとして生成されます。 詳細については、「[VSPerfReport](../profiling/vsperfreport.md)」を参照してください。  
  
### <a name="to-generate-an-etw-report"></a>ETW レポートを生成するには  
  
- **[コマンド プロンプト]** ウィンドウで、次のコマンド ラインを入力します。  
  
     *ToolsPath* **VSPerfReport** *VSPFile*  **/Summary:ETW [/Xml]**  
  
    |Command 要素|説明|  
    |-|-|  
    |*ToolsPath*|プロファイリング ツール ユーティリティのパス。 詳細については、「[コマンド ライン ツールへのパスの指定](../profiling/specifying-the-path-to-profiling-tools-command-line-tools.md)」をご覧ください。|  
    |*VSPFile*|プロファイル データ (.vsp または .vsps) ファイル。 完全パスまたは部分パスで指定できます。|  
    |Xml|XML で書式設定されているレポートを生成します。|
