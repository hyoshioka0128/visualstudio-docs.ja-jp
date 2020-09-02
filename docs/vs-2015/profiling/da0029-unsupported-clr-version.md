---
title: 'DA0029: サポートされていない CLR バージョンです | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.29
- vs.performance.rules.DA0029
helpviewer_keywords:
- vs.performance.29
- vs.performance.DA0029
- vs.performance.rules.DA0029
ms.assetid: 76247259-c6f3-44c4-b3f9-d8dac16b5e0d
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 532427618f476e1e187d8a1c88749810f9d157c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68152641"
---
# <a name="da0029-unsupported-clr-version"></a>DA0029:サポートされていない CLR バージョンです
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0029 |  
|Category |プロファイルツール使用法 |  
|プロファイル方法 |コマンドラインからのプロファイリング |  
|Message |コレクション中にサポートされていない CLR バージョンが検出されました。 マネージド シンボルが正しく解決されない可能性があります。|  
|ルールの種類 |情報 |。  
  
## <a name="cause"></a>原因  
 プロファイリング ツールでサポートされていない [!INCLUDE[net_v11_long](../includes/net-v11-long-md.md)] を使用するアプリケーションをプロファイリングしようとしています。  
  
## <a name="rule-description"></a>ルールの説明  
 アプリケーションで実行されているマネージド コードのシンボルをプロファイリング ツールが解決できないため、この警告が発生します。 プロファイリング ツールは、[!INCLUDE[net_v11_long](../includes/net-v11-long-md.md)] を実行しているアプリケーションのマネージド コード シンボルを解決できません。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 なし。
