---
title: '方法: パフォーマンス データ ファイル名のオプションを設定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: d7a8d6b9-ab23-46fb-98ed-774781157860
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 71ac053a24b3f765a58fc050ceec84115e1a4e3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85548396"
---
# <a name="how-to-set-performance-data-file-name-options"></a>方法: パフォーマンス データ ファイル名のオプションを設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

既定では、次の構文を使用してプロファイル データ (.vsp) ファイルを保存します。  
  
 *Path\VSP-File\YYMMDD(N)* **.vsp**  
  
 いずれの名前付けパラメーターも、パフォーマンス セッションのプロパティ ダイアログ ボックスの [全般] ページで変更できます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
|構文要素|説明|  
|-|-|  
|*パス*|レポートを格納するディレクトリ。 既定の場所は、ソリューション フォルダーか、ユーザーのプロジェクトおよびソリューションの既定の場所です。|  
|*VSP-File*|プロファイル データ ファイルの名前。 既定の名前は、プロファイルされるソリューションまたは実行可能ファイルの名前です。|  
|*YYMMDD*|プロファイル データが収集された年月日を示す日付スタンプ。|  
|*(N)*|複数のプロファイル データ ファイルが存在する場合、かっこで囲まれたインクリメント数がファイル名に追加されます。|  
  
### <a name="to-change-the-naming-syntax-of-the-profiling-data-files-of-a-performance-session"></a>パフォーマンス セッションのプロファイル データ ファイルの名前付け構文を変更するには  
  
1. **パフォーマンス エクスプローラー**で、パフォーマンス セッションの名前を右クリックして、 **[プロパティ]** をクリックします。  
  
2. **[全般]** をクリックします。  
  
3. **[レポート]** で、以下のいずれかの設定を変更します。  
  
    |名前|説明|  
    |-|-|  
    |**レポートの場所**|プロファイル データ ファイルを格納するディレクトリを指定します。|  
    |**レポート名**|ファイルの基本名を指定します。|  
    |**新しいレポートをセッションに自動的に追加**|パフォーマンス セッションにデータ ファイルを自動的に追加するには、チェック ボックスをオンにします。|  
    |**生成されたレポートにインクリメンタル数を追加**|同じ名前のファイルが複数存在する場合に、ファイル名にインクリメント数を追加するにはチェック ボックスを選択します。 既存のファイルを上書きするには、チェック ボックスをオフにします。|  
    |**番号にタイムスタンプを使用**|ファイル名に日付スタンプを追加するには、チェック ボックスをオンにします。|
