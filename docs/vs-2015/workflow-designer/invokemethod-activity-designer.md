---
title: InvokeMethod アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fcfba979ba7fce4aeffab1fe9e9a5a3728e513af
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658997"
---
# <a name="invokemethod-activity-designer"></a>InvokeMethod アクティビティ デザイナー
**InvokeMethod** デザイナーは、アクティビティを作成および構成するために使用 <xref:System.Activities.Statements.InvokeMethod> します。

## <a name="the-invokemethod-activity"></a>InvokeMethod アクティビティ
 <xref:System.Activities.Statements.InvokeMethod> は、指定されたオブジェクトまたは型のパブリック メソッドを呼び出します。

### <a name="using-the-invokemethod-activity-designer"></a>InvokeMethod アクティビティ デザイナーの使用
 **InvokeMethod**アクティビティデザイナーは、[**ツールボックス]** の [**プリミティブ**] カテゴリにあります。このカテゴリにアクセスするには、[**ツールボックス**] タブをクリックします [!INCLUDE[wfd2](../includes/wfd2-md.md)] (または、[**表示**] メニューの [**ツールバー** ] を選択するか、ctrl + ALT + X キーを押します)。

 **InvokeMethod**アクティビティデザイナーは、[**ツールボックス**] からドラッグして、 [!INCLUDE[wfd2](../includes/wfd2-md.md)] アクティビティを通常配置している画面 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 この操作により、InvokeMethod という既定の <xref:System.Activities.Statements.InvokeMethod> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **InvokeMethod** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-invokemethod-properties"></a>InvokeMethod プロパティ
 次の表に、<xref:System.Activities.Statements.InvokeMethod> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドで編集できます。また、その一部は[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイナー画面で編集できます。

|プロパティ名|必須|使用|
|-------------------|--------------|-----------|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.InvokeMethod> アクティビティの表示名。 既定値は InvokeMethod です。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|○|アクティビティの実行時に呼び出すメソッドの名前。 呼び出されたメソッドは **パブリック**として宣言されなければなりません。 このプロパティは、デザイナー画面で設定することもできます。 これは必須プロパティです。|
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|×|呼び出されたメソッドのパラメーター コレクション。 パラメーターは、メソッド シグネチャ内で出現する順序でコレクションに追加する必要があります。 プロパティグリッドで、[ **パラメーター** ] フィールドの省略記号ボタンをクリックすると、[ **パラメーター** ] ダイアログボックスが表示され、このプロパティを設定できます。 [ **引数の作成** ] ボタンをクリックして、パラメーターを追加します。|
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|×|メソッド呼び出しの戻り値。|
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|○|メソッドが非同期で呼び出されるかどうかを指定します。 既定値は **False**です。|
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|×|呼び出すメソッドを格納するオブジェクト。 このプロパティは、デザイナー画面で設定することもできます。<br /><br /> <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> および <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> のいずれかを設定する必要があります。|
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|×|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> の型。 このプロパティは、デザイナー画面で編集できます。 このプロパティは、メソッド呼び出しが静的である場合にのみ設定する必要があります。|

 パラメーターを C# の**out**パラメーターとして渡すには (たとえば、 `Method1(out myParam)),` **InOutArgument**ではなく**outargument<int>** を使用する必要があります。

 **TargetObject**または**Result**という引数を持つメソッドは、アクティビティを使用して呼び出すことはできません <xref:System.Activities.Statements.InvokeMethod> 。 これは、<xref:System.Activities.Statements.InvokeMethod> アクティビティによって <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A>、<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>、および <xref:System.Activities.Statements.InvokeMethod.Result%2A> が <xref:System.Activities.Activity.CacheMetadata%2A> に登録されるためです。

 <xref:System.Activities.Activity.CacheMetadata%2A> にパラメーターを登録するアルゴリズムは次のとおりです。

1. <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 引数を登録します。

2. <xref:System.Activities.Statements.InvokeMethod.Result%2A> 引数を登録します。

3. <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> コレクションを繰り返し処理し、各引数を登録します。

   結果の例外の種類は <xref:System.Activities.InvalidWorkflowException> となり、メッセージの内容は、"'InvokeMethod': 名前が 'TargetObject' の変数 RuntimeArgument または DelegateArgument は既に存在します" となります。 名前は、環境スコープ内で一意であることが必要です。

   この制限は、<xref:System.Activities.Statements.InvokeMethod.TargetType%2A> および <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A> には適用されません。これらはワークフロー引数ではなく、したがって、<xref:System.Activities.Activity.CacheMetadata%2A> メソッド内の <xref:System.Activities.Statements.InvokeMethod> アクティビティの <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> コレクションに登録されないためです。

## <a name="see-also"></a>参照
 [プリミティブ](../workflow-designer/primitives-activity-designers.md)[割り当て](../workflow-designer/assign-activity-designer.md)[遅延](../workflow-designer/delay-activity-designer.md) [WriteLine](../workflow-designer/writeline-activity-designer.md)