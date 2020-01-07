---
title: T4 CleanUpBehavior ディレクティブ
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa5883cd8a1e30e007db41d5aa73f882e1d7edd2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591880"
---
# <a name="t4-cleanupbehavior-directive"></a>T4 CleanUpBehavior ディレクティブ

テキスト テンプレートを処理した後、appDomain を削除するには、次の行を含めます。

```
<#@ CleanupBehavior processor="T4VSHost" CleanupAfterProcessingtemplate="true" #>
```

テキスト テンプレートは、ホスト プロセスから分離した appDomain で処理されます。 ほとんどの場合、1 つのテキスト テンプレートが処理されると、次のテンプレートを処理するために appdomain が再度使用されます。 ただし、CleanupBehavior を指定した場合、appDomain は削除され、新しい appDomain で次のテンプレートが処理されます。

これによってテキスト処理は遅くなりますが、リソースが破棄されたことを確認するうえで役立ちます。

このディレクティブは、Visual Studio ホストでのみ動作します。
