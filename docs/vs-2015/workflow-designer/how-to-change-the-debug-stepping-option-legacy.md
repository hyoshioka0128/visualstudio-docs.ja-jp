---
title: '方法: デバッグのステップ実行オプションを変更する (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
helpviewer_keywords:
- branch stepping
- debugging, stepping options
- debugging workflows, stepping options
- stepping, changing options
- instance stepping
ms.assetid: aedc06af-d58a-44d6-aee4-f397f1f923a0
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5126b3dc45d33471080ae154e06f4a327e21fef7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72663446"
---
# <a name="how-to-change-the-debug-stepping-option-legacy"></a>方法: デバッグのステップ実行オプションを変更する (レガシ)
このトピックでは、同時アクションを含む従来の [!INCLUDE[wf](../includes/wf-md.md)]で、[!INCLUDE[wfd1](../includes/wfd1-md.md)] アプリケーションのデバッグのステップ実行オプションを変更する方法について説明します。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 **Parallelactivity**や**Conditionedactivitygroup**など、同時実行を含む従来のアクティビティをデバッグする場合は、2つのオプションのいずれかを使用してコードをステップ実行できます。

 従来のワークフロー プロジェクトでデバッグのステップ実行オプションを変更するには、次の手順に従います。

## <a name="procedures"></a>手順

#### <a name="to-change-the-debug-stepping-option"></a>デバッグのステップ実行オプションを変更するには

1. Visual Studio を起動します。

2. 既存の従来のワークフロー プロジェクトを開くか、同時アクティビティを使用し、[!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] または [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] を対象とする新しいプロジェクトを作成します。

3. 従来のの [ **ワークフロー** ] メニューで、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] [ **デバッグ**] をポイントし、[ **ステップ実行オプション]** をポイントします。

4. [ **インスタンス** ] または [ **分岐**] を選択します。

## <a name="see-also"></a>参照
 [レガシワークフローのデバッグ](../workflow-designer/debugging-legacy-workflows.md)[ステップ実行オプションのデバッグ (レガシ)](../workflow-designer/debug-stepping-options-legacy.md)