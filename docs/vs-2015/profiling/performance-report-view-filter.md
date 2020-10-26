---
title: パフォーマンス レポート ビュー フィルター | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, Profiler Report view filter
- Profiler Report View filter, profiling tools
ms.assetid: 35f89d86-4683-4db1-aa0c-ae0ce65fa524
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8620e5a372d764fef3a75126af52a6212ecc6cd8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161969"
---
# <a name="performance-report-view-filter"></a>パフォーマンス レポート ビュー フィルター
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[プロファイラー レポート ビュー フィルター] ウィンドウは [パフォーマンス レポート] ウィンドウの上部に表示されます。 このウィンドウが表示されない場合は、 **[フィルターの表示]** ボタンをクリックします。  
  
 各フィルター句を変更して、結果を絞り込むことができます。 フィルター ビルダーでは、次の列を利用できます。  
  
|フィルター項目|[説明]|  
|-----------------|-----------------|  
|および/または|この句と次の句の両方が成り立つものを結果として返す場合は、 **[And]** を選択します。 この句と次の句のいずれかが成り立つものを結果として返す場合は、 **[Or]** を選択します。|  
|フィールド|フィルター句で使用するフィールドを、現在のレポート ファイルで使用できるデータ フィールドの一覧から選択します。|  
|演算子|フィールドと値の関係を示す演算子を選択します。<br /><br /> =    等しい<br /><br /> <>  等しくない<br /><br /> <    より小<br /><br /> >    より大<br /><br /> <=  以下<br /><br /> >=  以上|  
|値|検索する値を選択または入力します。 フィールドによっては使用可能な値がリスト表示されます。|  
  
 最良の結果が得られると考えられるまでフィルターにフィルター句を追加できます。 **[フィルターの実行]** をクリックして、データ ファイルにフィルターを適用します。  
  
 **[マーク]** レポート ビューでフィルター句を生成して、レポート ビューのデータを、2 つのマークの間で収集されるデータに制限することができます。 レポート データを開始するマークと終了するマークを選択し、右クリックして **[マークにフィルターを追加]** または **[タイムスタンプにフィルターを追加]** を選択します。 どちらのフィルターも現在のデータ ファイルのデータを同じ範囲に制限します。 **[マークにフィルターを追加]** は他の .vsp ファイルに適用できます。  
  
 フィルターを保存するには、[パフォーマンス レポート] ツール バーの **[フィルターのエクスポート]** をクリックし、.vspf ファイルの場所とファイル名を指定します。 以前に保存したフィルターを読み込むには、 **[フィルターのインポート]** をクリックし、保存したフィルター ファイルを探します。 スタンドアロンのプロファイリング ツールがインストールされているコンピューター上のデータ ファイルをフィルター処理するために、フィルター ファイルを使用することもできます。 詳細については、「[VSPerfReport](../profiling/vsperfreport.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [パフォーマンスツールデータの分析](../profiling/analyzing-performance-tools-data.md)   
 [VSPerfReport](../profiling/vsperfreport.md)
