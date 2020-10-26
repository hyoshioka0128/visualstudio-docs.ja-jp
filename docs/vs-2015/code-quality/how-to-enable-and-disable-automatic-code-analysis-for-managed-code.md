---
title: '方法: マネージコードの自動コード分析を有効または無効にする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
ms.assetid: 7c22d194-5fea-4f23-b02d-19344fa64a64
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d87cc57b31e63ae7aafa53c335df2b56f86a0409
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658096"
---
# <a name="how-to-enable-and-disable-automatic-code-analysis-for-managed-code"></a>方法: マネージド コードの自動コード分析を有効/無効にする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コード分析は、マネージコードプロジェクトの各ビルドの前に実行するように構成できます。 構成ごとに異なるコード分析プロパティを設定でき [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] ます。

### <a name="to-enable-or-disable-automatic-code-analysis"></a>自動コード分析を有効または無効にするには

1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[**プロパティ**] をクリックします。

2. プロジェクトの [プロパティ] ダイアログボックスで、[ **コード分析**] をクリックします。

3. [ **構成** ] でビルドの種類を指定し、[ **プラットフォーム**] でターゲットプラットフォームを指定します。

4. 自動コード分析を有効または無効にするには、[ **ビルド時にコード分析を有効にする (CODE_ANALYSIS 定数を定義する)** ] チェックボックスをオンまたはオフにします。
