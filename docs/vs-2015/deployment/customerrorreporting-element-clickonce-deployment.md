---
title: '&lt;customErrorReporting &gt; 要素 (ClickOnce 配置) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <customErrorReporting> element [ClickOnce deployment manifest]
ms.assetid: 7d31816e-c692-46b5-9cc9-753284b3bcda
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b7e8a0db3e10a277fe1c4a2f8fcd2bb85fa69e69
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68187832"
---
# <a name="ltcustomerrorreportinggt-element-clickonce-deployment"></a>&lt;customErrorReporting &gt; 要素 (ClickOnce 配置)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エラー発生時に表示する URI を指定します。  
  
## <a name="syntax"></a>構文  
  
```  
<customErrorReporting  
   uri  
/>  
```  
  
## <a name="remarks"></a>解説  
 この要素は省略可能です。 このプロパティを指定しないと、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 例外スタックを示すエラーダイアログボックスが表示されます。 `customErrorReporting`要素が存在する場合、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] はパラメーターで示された URI を代わりに表示し `uri` ます。 ターゲット URI には、外部例外クラス、内部例外クラス、および内部例外メッセージがパラメーターとして含まれます。  
  
 この要素を使用して、エラー報告機能をアプリケーションに追加します。 生成された URI にはエラーの種類に関する情報が含まれているため、Web サイトはその情報を解析して、適切なトラブルシューティング画面などの表示を行うことができます。  
  
## <a name="example"></a>例  
 次のスニペットは、生成 `customErrorReporting` される可能性のある、生成される URI と共に要素を示しています。  
  
```  
<customErrorReporting uri=http://www.contoso.com/applications/error.asp />  
  
Example Generated Error:  
http://www.contoso.com/applications/error.asp? outer=System.Deployment.Application.InvalidDeploymentException&&inner=System.Deployment.Application.InvalidDeploymentException&&msg=The%20application%20manifest%20is%20signed,%20but%20the%20deployment%20manifest%20is%20unsigned.%20Both%20manifests%20must%20be%20either%20signed%20or%20unsigned.  
```  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md)
