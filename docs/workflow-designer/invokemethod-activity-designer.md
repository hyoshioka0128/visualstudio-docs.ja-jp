---
title: ワークフローデザイナー-InvokeMethod アクティビティデザイナー
description: Invokemethod アクティビティについて、および invokemethod アクティビティデザイナーを使用して InvokeMethod アクティビティを作成および構成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.Activities.Statements.InvokeMethod.UI
ms.assetid: 15e6efdc-52ca-46d8-9c5e-063f7c8265a6
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 55162def18d2295e0767a3999ffde75d71e1233d
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/10/2020
ms.locfileid: "94437737"
---
# <a name="invokemethod-activity-designer"></a>InvokeMethod アクティビティ デザイナー

**InvokeMethod** デザイナーは、アクティビティを作成および構成するために使用 <xref:System.Activities.Statements.InvokeMethod> します。

## <a name="the-invokemethod-activity"></a>InvokeMethod アクティビティ

<xref:System.Activities.Statements.InvokeMethod> は、指定されたオブジェクトまたは型のパブリック メソッドを呼び出します。

### <a name="use-the-invokemethod-activity-designer"></a>InvokeMethod アクティビティデザイナーの使用

**ツールボックス** の [ **プリミティブ** ] カテゴリで、 **InvokeMethod** アクティビティデザイナーにアクセスします。 **InvokeMethod** アクティビティデザイナーは、[ **ツールボックス** ] からドラッグして、アクティビティが通常配置されているワークフローデザイナー画面 (内など) にドロップできます <xref:System.Activities.Statements.Sequence> 。 アクティビティデザイナーを削除 <xref:System.Activities.Statements.InvokeMethod> すると、既定値の InvokeMethod を持つアクティビティが作成さ <xref:System.Activities.Activity.DisplayName%2A> れます。 は、 <xref:System.Activities.Activity.DisplayName%2A> **InvokeMethod** アクティビティデザイナーのヘッダー、またはプロパティグリッドの [ **DisplayName** ] ボックスで編集できます。

### <a name="the-invokemethod-properties"></a>InvokeMethod プロパティ

次の表は、 <xref:System.Activities.Statements.InvokeMethod> プロパティと、デザイナーでのそれらの使用方法を示しています。 これらのプロパティは、プロパティグリッドで編集できます。また、ワークフローデザイナーサーフェイスで編集することもできます。

|プロパティ名|必須|使用法|
|-|--------------|-|
|<xref:System.Activities.Activity.DisplayName%2A>|×|<xref:System.Activities.Statements.InvokeMethod> アクティビティの表示名。 既定値は InvokeMethod です。<br /><br /> は <xref:System.Activities.Activity.DisplayName%2A> 厳密には必須ではありませんが、1つを使用することをお勧めします。|
|<xref:System.Activities.Statements.InvokeMethod.MethodName%2A>|○|アクティビティの実行時に呼び出すメソッドの名前。 呼び出されたメソッドは **パブリック** として宣言されなければなりません。 このプロパティは、デザイナー画面で編集でき、必須です。|
|<xref:System.Activities.Statements.InvokeMethod.Parameters%2A>|×|呼び出されたメソッドのパラメーター コレクション。 パラメーターは、メソッド シグネチャ内で出現する順序でコレクションに追加する必要があります。 このプロパティを設定できる [ **パラメーター** ] ダイアログボックスを表示するには、プロパティグリッドの [ **パラメーター** ] フィールドで、省略記号ボタンをクリックします。 [ **引数の作成** ] ボタンをクリックして、パラメーターを追加します。|
|<xref:System.Activities.Statements.InvokeMethod.Result%2A>|×|メソッド呼び出しの戻り値。|
|<xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A>|○|メソッドが非同期で呼び出されるかどうかを指定します。 既定値は **False** です。|
|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>|×|呼び出すメソッドを格納するオブジェクト。 このプロパティは、デザイナー画面で設定することもできます。<br /><br /> <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> および <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> のいずれかを設定する必要があります。|
|<xref:System.Activities.Statements.InvokeMethod.TargetType%2A>|×|<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> の型。 このプロパティは、デザイナー画面で編集できます。 このプロパティは、メソッド呼び出しが静的である場合にのみ設定する必要があります。|

パラメーターを C# の **out** パラメーターとして渡すには (たとえば、 `Method1(out myParam))` **InOutArgument** の代わりに **outargument<int>** を使用します。

**TargetObject** または **Result** という引数を持つメソッドは、アクティビティを使用して呼び出すことはできません <xref:System.Activities.Statements.InvokeMethod> 。 これは、<xref:System.Activities.Statements.InvokeMethod> アクティビティによって <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A>、<xref:System.Activities.Statements.InvokeMethod.TargetObject%2A>、および <xref:System.Activities.Statements.InvokeMethod.Result%2A> が <xref:System.Activities.Activity.CacheMetadata%2A> に登録されるためです。

<xref:System.Activities.Activity.CacheMetadata%2A> にパラメーターを登録するアルゴリズムは次のとおりです。

1. <xref:System.Activities.Statements.InvokeMethod.TargetObject%2A> 引数を登録します。

2. <xref:System.Activities.Statements.InvokeMethod.Result%2A> 引数を登録します。

3. <xref:System.Activities.Statements.InvokeMethod.Parameters%2A> コレクションを繰り返し処理し、各引数を登録します。

結果の例外の種類は <xref:System.Activities.InvalidWorkflowException> となり、メッセージの内容は、"'InvokeMethod': 名前が 'TargetObject' の変数 RuntimeArgument または DelegateArgument は既に存在します" となります。 名前は、環境スコープ内で一意であることが必要です。

この制限は、およびには適用されません <xref:System.Activities.Statements.InvokeMethod.TargetType%2A> <xref:System.Activities.Statements.InvokeMethod.RunAsynchronously%2A> 。 これらはワークフロー引数ではないため、 <xref:System.Activities.Statements.InvokeMethod.GenericTypeArguments%2A> メソッド内のアクティビティのコレクションに登録されません <xref:System.Activities.Statements.InvokeMethod> <xref:System.Activities.Activity.CacheMetadata%2A> 。

## <a name="see-also"></a>関連項目

- [プリミティブ](../workflow-designer/primitives-activity-designers.md)
- [Assign](../workflow-designer/assign-activity-designer.md)
- [[遅延]](../workflow-designer/delay-activity-designer.md)
- [WriteLine](../workflow-designer/writeline-activity-designer.md)
