---
title: '[.NET 型の参照と選択] ダイアログボックス (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.ComponentModel.Design.TypeBrowserDialog.UI
helpviewer_keywords:
- Browse and Select a .NET Type dialog box
ms.assetid: 1e66c9bc-94b2-46e2-bedf-871752e5f917
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 1e5045a62d0a654af968d50e0c309bcf8104b5cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72668986"
---
# <a name="browse-and-select-a-net-type-dialog-box-legacy"></a>[.NET 型の参照と選択] ダイアログ ボックス (レガシ)
このトピックでは、従来のの [ **.Net 型の参照と選択** ] ダイアログボックスの使用方法について説明し [!INCLUDE[wfd1](../includes/wfd1-md.md)] ます。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 [ **プロパティ** ] ウィンドウで、参照アセンブリの .NET Framework 型を受け取るプロパティを選択すると、プロパティのテキストボックスの最後に省略記号 **[...]** が表示されます。 **[...]** をクリックすると、[ **.net 型の参照と選択**] ダイアログボックスが開きます。 このダイアログ ボックスで、参照アセンブリのツリー表示から型を選択できます。 たとえば、アクティビティデザイナーを使用している場合は、[ **プロパティ** ] ウィンドウで **基底クラス** の省略記号 **[...]** をクリックして、[参照されたアセンブリ] ツリーからアクティビティの別の基本クラスを選択します。

 次の表では、[ **.Net 型の参照と選択** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**型名:**|現在選択されている型の名前。|
|**Type**|左側のペインには、参照アセンブリがツリー表示されます。 右側のペインには、左側のペインで選択した参照アセンブリから選択可能な型が表示されます。|

## <a name="see-also"></a>参照
 [従来のアクティビティ デザイナーの使用](../workflow-designer/using-the-legacy-activity-designer.md)