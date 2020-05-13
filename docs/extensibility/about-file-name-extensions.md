---
title: ファイル名拡張子について |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740345"
---
# <a name="about-file-name-extensions"></a>ファイル名拡張子について
VSPackage のファイル拡張子を登録する場合は、その拡張子を のバージョン[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]に関連付けます。 これは、複数のバージョンが[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]コンピュータにインストールされている場合に重要です。

 VSPackage のファイル拡張子は **、** 関連付けられたプログラム識別子 (ProgID) を指す既定値を持つHKEY_CLASSES_ROOTキーの下に登録されます。

 次の例は *、.vcproj*ファイル拡張子の登録情報を示しています。

```
HKEY_CLASSES_ROOT\
   .vcproj\
      (default)=" VisualStudio.vcproj.8.0"
```

 関連付けられている[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ファイルには、バージョン管理された ProgID `VisualStudio.vcproj.8.0`(など) が必要です。 バージョン管理された ProgID を使用すると、製品のサイド バイ サイド インストールを使用して、製品バージョン間でファイル拡張子の関連付けを維持できます。 バージョン固有の ProgID を使用すると、他のアプリケーションやバージョンで上書きしたり上書きしたりすることなく、標準動詞[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)](開く、編集など) を使用することもできます。

 場合によっては、ファイル拡張子に関連付けられた ProgID を変更しないでください。 たとえば *、.htm*ファイル拡張子 (progid = htmlfile) の ProgID は、オペレーティング システムの多くの場所でハードコーディングされており、広く知られており *、.htm*および *.html*ファイルと関連付けて使用されています。

## <a name="see-also"></a>関連項目
- [サイド バイ サイド展開のファイル名拡張子を登録する](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [ファイル名拡張子のファイル ハンドラーを指定する](../extensibility/specifying-file-handlers-for-file-name-extensions.md)
