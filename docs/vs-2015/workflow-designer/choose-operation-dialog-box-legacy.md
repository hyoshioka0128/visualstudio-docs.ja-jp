---
title: '[操作の選択] ダイアログボックス (レガシ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Workflow.Activities.Design.OperationPickerDialog.UI
ms.assetid: bc3ec902-7797-494e-af48-e70c97eb6779
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f2736db7e18733a9477238cafad21088eb135e89
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72659159"
---
# <a name="choose-operation-dialog-box-legacy"></a>[操作の選択] ダイアログ ボックス (レガシ)
このトピックでは、従来のの **[操作の選択** ] ダイアログボックスの使用方法について説明し [!INCLUDE[wfd1](../includes/wfd1-md.md)] ます。 [!INCLUDE[wfd2](../includes/wfd2-md.md)] または [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] を対象とする必要がある場合は、従来の[!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)]を使用します。

 [ **操作の選択** ] ダイアログボックスは、アクティビティまたはアクティビティに関連付ける操作を選択するために使用され <xref:System.Workflow.Activities.ReceiveActivity> <xref:System.Workflow.Activities.SendActivity> ます。 これらのアクティビティでこのダイアログボックスを使用する方法の詳細については、「 [方法: Wcf コントラクト操作を実装する (レガシ)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md) 」および「 [方法: wcf コントラクト操作を呼び出す (レガシ)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md)」を参照してください。

 次の表では、 **[操作の選択** ] ダイアログボックスのユーザーインターフェイス (UI) 要素について説明します。

|UI 要素|説明|
|----------------|-----------------|
|**コントラクトの追加**|新しいコントラクトを作成します。 このコントラクトに対して新しい操作を定義できます  (この要素は <xref:System.Workflow.Activities.ReceiveActivity> でのみ使用されます)。|
|**操作の追加**|**[操作の選択**] ダイアログボックスで作成した新しいコントラクトに新しい操作を追加します。 **注:** **[操作の選択** ] ダイアログボックスで作成したコントラクトに対してのみ、新しい操作を追加できます。 <br /><br /> (この要素は <xref:System.Workflow.Activities.ReceiveActivity> でのみ使用されます)。|
|**インポート...**|以前に定義されたコントラクトをインポートし、そのコントラクトから操作を選択できます。|
|**操作の名前**|現在選択されている操作の名前。 このテキストボックスは、 **[操作の選択** ] ダイアログボックスを使用して操作を作成した場合にのみ編集できます。|
|**パラメーター**|現在選択されている操作のパラメータ定義が表示されるタブ。 **注:** **[操作の選択** ] ダイアログボックスを使用して操作を作成した場合にのみ、パラメーターの定義を変更できます。|
|**プロパティ**|クライアントとサービス間で送信されたメッセージの <xref:System.Net.Security.ProtectionLevel> 設定が表示されるタブ。 **注:**  このタブは、[ **操作の選択** ] ダイアログボックスを使用して操作を作成した場合にのみ有効になります。|
|**アクセス許可**|その操作の呼び出しを許可されているユーザーの <xref:System.Workflow.Activities.OperationInfoBase.PrincipalPermissionName%2A> プロパティおよび <xref:System.Workflow.Activities.OperationInfoBase.PrincipalPermissionRole%2A> プロパティが表示されるタブ。 たとえば、Administrators グループのユーザーのみがその操作の呼び出しを許可されていた場合は、[ **ロール** ] ボックスに「administrators」と記述します。<br /><br /> このタブは、[ **操作** の選択] ダイアログボックスを使用して作成された操作と、[ **インポート** ] ボタンを使用してインポートされた操作の両方に対して有効になります。|

> [!NOTE]
> **[操作の選択**] ダイアログボックスには、ワークフロー内の他のアクティビティによって使用されるコントラクトまたは操作のみが表示され <xref:System.Workflow.Activities.SendActivity> ます。 同様に、アクティビティの **[操作の選択** ] ダイアログボックスには、 <xref:System.Workflow.Activities.ReceiveActivity> ワークフロー内の他の **ReceiveActivity** アクティビティによって使用されるコントラクトまたは操作のみが表示されます。

## <a name="see-also"></a>参照
 [方法: Wcf コントラクト操作を実装する (レガシ)](../workflow-designer/how-to-implement-a-windows-communication-foundation-contract-operation-legacy.md) [方法: wcf コントラクト操作を呼び出す (レガシ)](../workflow-designer/how-to-invoke-a-windows-communication-foundation-contract-operation-legacy.md) [Windows Workflow Foundation UI ヘルプ用のレガシデザイナー](../workflow-designer/legacy-designer-for-windows-workflow-foundation-ui-help.md)