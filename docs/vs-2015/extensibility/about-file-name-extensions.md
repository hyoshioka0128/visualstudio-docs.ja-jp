---
title: ファイル名拡張子について |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 866a30279ca2c79f4a490a040f76bc3a86c6a6e1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148032"
---
# <a name="about-file-name-extensions"></a>ファイル名拡張子について
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage のファイル拡張子を登録すると、それをのバージョンに関連付けることに [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] なります。 これは、1台のコンピューターに複数のバージョンの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] がインストールされている場合に重要です。  
  
 Vspackage のファイル拡張子は HKEY_CLASSES_ROOT キーの下に登録され、関連付けられているプログラム id (ProgID) を指す既定値が設定されます。  
  
 .Vcproj ファイル拡張子の登録情報の例を次に示します。  
  
```  
HKEY_CLASSES_ROOT\  
   .vcproj\  
      (default)=" VisualStudio.vcproj.8.0"   
```  
  
 に関連付けられたファイルには [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、製品 `VisualStudio.vcproj.8.0` バージョン間のファイル拡張子の関連付けを維持するために製品をサイドバイサイドでインストールできるように、バージョン管理された ProgID (など) が必要です。 また、バージョン固有の ProgID を使用すると、標準の動詞 (open、edit など) を使用することもできます。この場合、上書きや、の他のアプリケーションやバージョンによる上書きは考慮されません [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。  
  
 場合によっては、ファイル拡張子に関連付けられている ProgID を変更しないでください。 たとえば、.htm ファイル拡張子の ProgID (progid = htmlfile) は、オペレーティングシステムのさまざまな場所にハードコーディングされており、.htm ファイルと .html ファイルとの関連付けで広く知られています。  
  
## <a name="see-also"></a>参照  
 [サイドバイサイド配置のためにファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)   
 [ファイル名拡張子のファイル ハンドラーを指定する](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
