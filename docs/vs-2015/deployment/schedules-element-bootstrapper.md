---
title: '&lt;スケジュール &gt; 要素 (ブートストラップ) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <Schedules> element [bootstrapper]
ms.assetid: 28d094cf-64f5-42b1-bd8a-3697082aab4f
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 85ffab2272a55bfe77c5f2a73c6e25967a203c85
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68206097"
---
# <a name="ltschedulesgt-element-bootstrapper"></a>&lt;スケジュール &gt; 要素 (ブートストラップ)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要素には、要素 `Schedules` `Schedule` によって定義されたコマンドを実行する特定の時刻を定義する要素が含まれ `Command` ます。  
  
## <a name="syntax"></a>Syntax  
  
```  
<Schedules>  
    <Schedule  
        Name  
    >  
        <BuildList />  
        <BeforePackage />  
        <AfterPackage />  
    </Schedule>  
</Schedules>  
```  
  
## <a name="elements-and-attributes"></a>要素と属性  
 要素は `Schedules` 要素の子です `Product` 。 各 `Product` 要素は、最大で1つの要素を持つことができ `Schedules` ます。 `Schedules` 要素に属性はありません。  
  
## <a name="schedule"></a>スケジュール  
 要素は `Schedule` 要素の子です `Schedules` 。 要素には、 `Schedules` 少なくとも1つの要素が必要 `Schedule` です。  
  
 `Schedule` には次の属性があります。  
  
|属性|説明|  
|---------------|-----------------|  
|`Name`|必須です。 スケジュール項目の名前。 これは `ScheduleName` 、要素のプロパティに対応 `Command` します。 は、指定されたスケジュールを参照するときに、 `Command` その要素によって示される時刻にのみ実行され `Schedule` ます。 スケジュールは、および要素に関連付けられている場合もあり `FailIf` `BypassIf` ます。これにより、指定したスケジュールでこれらの条件テストを実行することが制限されます。 詳細については、[\<Commands> 要素](../deployment/commands-element-bootstrapper.md)に関するページを参照してください。|  
  
 指定された `Schedule` 要素は、次の子のうち1つだけを持つことができます。  
  
## <a name="buildlist"></a>BuildList  
 要素は、 `BuildList` ブートストラップアプリケーションが開始された直後にコマンドを実行するようにインストーラーに指示します。  
  
## <a name="beforepackage"></a>BeforePackage  
 要素は、 `BeforePackage` 指定されたパッケージがインストールされる前にコマンドを実行するようにインストーラーに指示します。  
  
## <a name="afterpackage"></a>AfterPackage  
 要素は、 `AfterPackage` 指定されたパッケージのインストール後にコマンドを実行するようにインストーラーに指示します。  
  
## <a name="see-also"></a>参照  
 [\<Product> Element](../deployment/product-element-bootstrapper.md)   
 [製品およびパッケージ スキーマ リファレンス](../deployment/product-and-package-schema-reference.md)
