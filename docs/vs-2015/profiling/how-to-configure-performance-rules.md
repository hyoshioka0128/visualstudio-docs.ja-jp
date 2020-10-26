---
title: '方法: パフォーマンス規則を構成する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.ruleseditor
ms.assetid: a148b468-b849-4858-880a-808a6b47e596
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 71593496613c75485fd30481777d0fcc1102c11c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179585"
---
# <a name="how-to-configure-performance-rules"></a>方法: パフォーマンス規則を構成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio プロファイリング ツールのパフォーマンスの警告は、プロファイリング対象のアプリケーションにおいてプログラムの実行速度が低下する問題を示します。 警告は、有用なデータを収集するために、収集メソッドを変更する必要があることを示している場合もあります。 パフォーマンスの警告は、プロファイル セッションで自動的に生成され、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] でプロファイル データ ファイルを開いたときに、 **[エラー一覧]** ウィンドウに表示されます。 ただし、警告によっては、目的のシナリオに当てはまらないものや、誤って生成されるものもあります。 このため、特定の警告を表示または非表示にするよう、パフォーマンスの警告を構成できます。  
  
### <a name="to-configure-profiler-performance-warnings"></a>プロファイラーのパフォーマンス警告を構成するには  
  
1. **[ツール]** メニューの **[オプション]** をクリックします。  
  
2. **[パフォーマンス ツール]** を展開し、 **[規則]** をクリックします。  
  
3. 警告の **[ID]** および名前の隣にあるチェック ボックスをオンまたはオフにすることで、警告を有効または無効にすることができます。  
  
4. 規則の警告レベルを指定するには、規則の横の **[アクション]** セルをクリックして警告レベルをクリックします。  
  
    - **[無効]** - 規則を無効にします (これは、規則 ID の横のチェック ボックスをオフにするのと同じです)。  
  
    - **[警告]** - 規則を警告として表示します。  
  
    - **[エラー]** - プロファイリングの実行を停止し、規則をエラーとして表示します。  
  
    - **[情報]** - 規則を情報としてだけ表示します。
