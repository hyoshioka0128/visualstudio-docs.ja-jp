---
title: ファイル名拡張子について |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- file extensions
- file name extensions
ms.assetid: 99f4f9ff-fb84-4258-9787-6890f308a57f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03e07ec233ef975441a1f10507f0db872051558f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80740345"
---
# <a name="about-file-name-extensions"></a>ファイル名拡張子について
VSPackage のファイル拡張子を登録すると、それをのバージョンに関連付けることに [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] なります。 これは、1台のコンピューターに複数のバージョンの [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] がインストールされている場合に重要です。

 Vspackage のファイル拡張子は **HKEY_CLASSES_ROOT** キーの下に登録され、関連付けられているプログラム Id (ProgID) を指す既定値が設定されます。

 次の例では、 *.vcproj* ファイル拡張子の登録情報を示します。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 に関連付けられたファイルには、のように [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] バージョン管理された ProgID が必要 `VisualStudio.vcproj.8.0` です。 バージョン付きの ProgID を使用すると、製品のバージョン間のファイル拡張子の関連付けを維持するために、製品をサイドバイサイドでインストールできます。 また、バージョン固有の ProgID を使用すると、標準の動詞 (open、edit など) を使用することもできます。この場合、上書きや、の他のアプリケーションやバージョンによる上書きは考慮されません [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

 場合によっては、ファイル拡張子に関連付けられている ProgID を変更しないでください。 たとえば、 *.htm* ファイル拡張子の progid (progid = htmlfile) は、オペレーティングシステムのさまざまな場所にハードコーディングされており、 *.htm* ファイルと *.html* ファイルとの関連付けで広く知られています。

## <a name="see-also"></a>関連項目
- [サイドバイサイド配置のためにファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [ファイル名拡張子のファイルハンドラーを指定する](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
