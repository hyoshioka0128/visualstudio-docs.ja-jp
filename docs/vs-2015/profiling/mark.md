---
title: Mark | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 1d72cef3-bb09-4bbb-8864-6ea0ab623ff9
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e6d7902ec588af2687b048639a930847ec02b3fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68155786"
---
# <a name="mark"></a>Mark
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPerfCmd.exe の **Mark** オプションは、プロファイル データ ファイルに指定した情報を挿入します。 マークは個別の VSPerfReport レポートまたはプロファイラー UI のマーク レポート ビューに一覧表示できます。 **Mark** を使用して、レポートおよびビュー フィルターの開始点と終了点を指定できます。  
  
 コマンド ラインで指定するオプションは **Mark** オプションのみにする必要があります。  
  
## <a name="syntax"></a>構文  
  
```  
VSPerfCmd.exe /Mark:MarkID,[MarkName]  
```  
  
#### <a name="parameters"></a>パラメーター  
 `MarkID`  
 プロファイラー ビューおよびレポートにマーク ID として一覧表示される、ユーザー定義の整数。 `MarkID` は一意である必要はありません。  
  
 `MarkName`  
 (省略可能) プロファイラー ビューおよびレポートにマーク名として一覧表示される、ユーザー定義の文字列。 `MarkName` が指定されていない場合、マーク一覧のマーク名フィールドは空になります。 スペースやスラッシュ ("/") を含む文字列は引用符で囲みます。  
  
## <a name="example"></a>例  
 この例では、ID が 123 でマーク名が "TestMark" というマークを挿入します。  
  
```  
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp  
VSPerfCmd.exe /Launch:TestApp.exe  
VSPerfCmd.exe /Mark:123,TestMark  
```  
  
## <a name="see-also"></a>参照  
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [スタンドアロンアプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)   
 [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)   
 [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
