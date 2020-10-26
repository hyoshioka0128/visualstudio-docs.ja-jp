---
title: '方法: スクリプト ドキュメントを表示する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Script Explorer
ms.assetid: 8b621e53-4508-4b4a-9995-70995b0b9ac8
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 88f923ab0447f1ac7d57e84d94f0ab442d912d67
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68189602"
---
# <a name="how-to-view-script-documents"></a>方法 : スクリプト ドキュメントを表示する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の以前のバージョンでは、サーバー側スクリプトによって生成されたクライアント側スクリプト ファイルは [スクリプト エクスプローラー] ウィンドウに表示されました。 [スクリプト エクスプローラー] ウィンドウは非表示のことが多く、クライアント側スクリプトが利用できるかどうかが常に明確とは限りませんでした。  
  
 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] では、サーバー側スクリプトによって生成されたクライアント側スクリプト ファイルは、既定で表示されるソリューション エクスプローラーに表示されます。 [スクリプト エクスプローラー] ウィンドウは削除されました。  
  
 クライアント側スクリプト ファイルは、デバッグ モードまたは中断モードのときにのみ表示されます。 これらは **[スクリプト ドキュメント]** ノードに表示されます。  
  
 サーバー側スクリプト ファイルは常に表示されます。 ノードに表示され **\<Website Pathname>** ます。 ノードの名前は次の例のようになります。 `c:\...\Website2\`  
  
### <a name="to-view-a-server-side-script-document"></a>サーバー側スクリプト ドキュメントを表示するには  
  
1. **ソリューション エクスプローラー**で、 **\<Website Pathname>** ノードを開きます。  
  
2. 表示するスクリプト ファイルをダブルクリックします。  
  
     サーバー側スクリプト ファイルがソース ウィンドウに表示されます。  
  
### <a name="to-view-a-client-side-script-document"></a>クライアント側スクリプト ドキュメントを表示するには  
  
1. **ソリューション エクスプローラー**で、 **[スクリプト ドキュメント]** ノードを開きます。  
  
2. 表示するスクリプト ファイルをダブルクリックします。  
  
     クライアント側スクリプト ファイルがソース ウィンドウに表示されます。  
  
## <a name="see-also"></a>参照  
 [デバッガーでのデータ表示](../debugger/viewing-data-in-the-debugger.md)
