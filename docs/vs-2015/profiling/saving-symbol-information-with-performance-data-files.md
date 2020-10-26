---
title: パフォーマンス データ ファイルを使ったシンボル情報の保存 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- packsymbols, in profiling tools reports
- profiling tools, packsymbols
ms.assetid: 8b802505-e94d-4ee0-83e4-fdd790a332c1
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e9d2e8b0414746523d0f76e8266f6463d9c05574
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160298"
---
# <a name="saving-symbol-information-with-performance-data-files"></a>パフォーマンス データ ファイルを使ったシンボル情報の保存
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 統合開発環境 (IDE: Integrated Development Environment) を使用してファイルを分析している場合、VSP ファイルを別のコンピューターに移動するには、シンボルをレポート ファイルに保存するか*シリアル化*するようにパフォーマンス プロジェクトの設定を行う必要があります。 この結果、レポート ファイルのサイズが大きくなります。 シンボルのシリアル化は次の 2 つの理由で必要になります。  
  
- ターゲット アセンブリが一時的なストレージから失われる前に、コード シンボルをパフォーマンス レポートに埋め込むため。  
  
- パフォーマンス レポートをプロファイルされたコンピューターから移植し、異なるシンボルを保持する別のコンピューターで分析するためにそのレポートを開いたときに同じ情報が出力されるようにシンボルを保存するため。  
  
  **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
  シンボルは、次の方法で [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE やコマンド ラインからシリアル化できます。  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE でシンボルをシリアル化するには、メニュー バーの **[ツール]** をポイントし、**[オプション]** をクリックします。 **[オプション]** ウィンドウで、**[パフォーマンス ツール]** を選択し、**[シンボル情報を自動的にシリアル化]** チェック ボックスをオンにします。  
  
- PACKSYMBOLS は、これに相当するレポート ファイル保存時のコマンド ライン オプションです。 シンボルをシリアル化するには、「**vsperfreport /summary:all /packsymbols filename.vsp**」と入力します。  
  
## <a name="troubleshooting-symbol-problems"></a>シンボルに関する問題のトラブルシューティング  
 独自のコードでシンボルを確認できない場合は、次のような一般的な解決方法がいくつかあります。  
  
- コマンド ラインで vsperfreport /debugsympath を実行して、プロファイラーのコンポーネントがシンボル情報を読み込む場所と、使用されているシンボル ファイルがプロジェクトで使用しているファイルと一致するかどうかに関する情報の一覧を表示します。  
  
- /PACKSYMBOLS フラグを指定して vsperfreport を実行していること、または [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE のパフォーマンス エクスプローラーの全般的なオプションでシンボル情報をシリアル化するオプションが選択されていることを確認します。  
  
- 型のデータを収集した場合、vsperfreport コマンド ラインに /SUMMARY:TYPE を追加します。  
  
  Windows やその他の Microsoft プログラムからシンボルを確認できない場合は、次のように解決します。  
  
- Windows シンボル キャッシュのパスを設定したことを確認します。 シンボル キャッシュのパスを設定するには、次のいずれかを実行します。  
  
  - [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE の [デバッガ―] -> [シンボル] のオプションで正しいパスを設定します。  
  
  - VSPerfReport コマンド ラインに -symbolpath オプションを追加して、シンボルを含めます。  
  
- [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] でシンボルを確認できない場合は、ASP サーバーにシンボル サーバーが正しくセットアップされていることを確認します。  
  
## <a name="repacking-symbols"></a>シンボルの再パック  
 シンボルをレポートに再度パックする場合は、VsPerfReport コマンド ライン ツールを使用してこの操作を実行できます。 次のコマンド ラインを使用します。  
  
 VsPerfReport -clearpackedsymbols filename.vsp  
  
 VsPerfReport -packsymbols -summary:all filename.vsp  
  
## <a name="see-also"></a>参照  
 [パフォーマンスツールデータの保存とエクスポート](../profiling/saving-and-exporting-performance-tools-data.md)   
 [方法: Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)   
 [VSPerfReport](../profiling/vsperfreport.md)
