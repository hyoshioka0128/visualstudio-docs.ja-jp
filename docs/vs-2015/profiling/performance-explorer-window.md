---
title: '[パフォーマンス エクスプローラー] ウィンドウ | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performanceexplorer
- vs.performance.explorer
helpviewer_keywords:
- performance tools, Performance Explorer
ms.assetid: cb6a6efc-93a5-49a2-8d03-6969b5f3b6d7
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a370ae802408ecc821de4cd15824f9d1fca42b75
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195520"
---
# <a name="performance-explorer-window"></a>[パフォーマンス エクスプローラー] ウィンドウ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 統合開発環境 (IDE) の **[パフォーマンス エクスプローラー]** ウィンドウでは、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のプロファイリング ツールを使用してパフォーマンス セッションを構成および開始することができます。  
  
 **必要条件**  
  
- [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)], [!INCLUDE[vsPreLong](../includes/vsprelong-md.md)], [!INCLUDE[vsPro](../includes/vspro-md.md)]  
  
## <a name="performance-explorer-toolbar"></a>パフォーマンス エクスプローラーのツール バー  
 **パフォーマンス エクスプローラー**のツール バーでは以下のオプションを使用できます。  
  
- **パフォーマンス ウィザードの起動** - パフォーマンス ウィザードを表示し、[パフォーマンス エクスプローラー] ウィンドウに新しいパフォーマンス セッションを追加します。  
  
- **新しいパフォーマンス セッション** - 空のパフォーマンス セッションを [パフォーマンス エクスプローラー] ウィンドウに追加します。  
  
- **起動** - **[起動]** コマンド ボタン リストでは、ターゲット アプリケーションを開始する際に、プロファイリングを即時に有効にすること (**プロファイルを使用して起動**) も、プロファイリングを中断しておくこと (**プロファイルを一時停止して起動**) もできます。  
  
- **メソッド** - セッションのプロファイル方法をサンプリングにするか、インストルメンテーションにするかを指定します。  
  
- **停止** - ターゲット アプリケーションとプロファイラーを即時に終了します。  
  
- **アタッチ/デタッチ** - **[プロファイラーをプロセスにアタッチします]** ダイアログ ボックスを表示し、プロファイラーをアタッチする実行中のプロセスを選択します。  
  
## <a name="performance-explorer-window"></a>[パフォーマンス エクスプローラー] ウィンドウ  
 **[パフォーマンス エクスプローラー]** ウィンドウには、1 つ以上のパフォーマンス セッションのバイナリおよびレポート データ ファイルを表示するツリー コントロールが表示されます。  
  
- **セッション名** - ツリー コントロールのルートには、セッションの名前が含まれます。 セッション名を右クリックし、セッション プロパティを設定するか、ターゲット アプリケーションおよびプロファイラーを開始します。  
  
- **ターゲット** - セッションでプロファイリングされるバイナリの名前を表示します。 **[ターゲット]** を右クリックし、バイナリ、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロジェクト、Web サイトを追加または削除します。 ターゲット名を右クリックし、個々のバイナリのプロパティを設定します。  
  
- **レポート** - セッションに対して生成されるプロファイラー データ ファイルの名前を表示します。 **[レポート]** を右クリックし、既存のレポートの追加、または 2 つのプロファイラー データ ファイルの比較を行います。 レポート名を右クリックし、プロファイラー データ ファイルを開くか、削除するか、エクスポートします。  
  
## <a name="see-also"></a>参照  
 [概念](../profiling/overviews-performance-tools.md)   
 [パフォーマンスセッションの構成](../profiling/configuring-performance-sessions.md)   
 [データコレクションの制御](../profiling/controlling-data-collection.md)
