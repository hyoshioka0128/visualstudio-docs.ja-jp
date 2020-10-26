---
title: レジストリ設定を使用してプライベートギャラリーを管理する
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSIX private galleries, managing
- managing VSIX private galleries
ms.assetid: 86b86442-4293-4cad-9fe2-876eef65f426
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2dcbacbe415eac6829dc51e95442905bba932d6a
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90038544"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>方法: レジストリ設定を使用してプライベートギャラリーを管理する
分離シェル拡張機能の管理者または開発者は、Visual Studio ギャラリー、サンプルギャラリー、またはプライベートギャラリーで、コントロール、テンプレート、およびツールへのアクセスを制御できます。 ギャラリーを利用できるようにする、または使用できないようにするには、変更されたレジストリキーとその値を記述する、 *pkgdef* ファイルを作成します。

## <a name="manage-private-galleries"></a>プライベートギャラリーの管理
 複数のコンピューター上のギャラリーへのアクセスを制御するために、 *pkgdef* ファイルを作成できます。 このファイルの形式は次のとおりである必要があります。

```
[$RootKey$\ExtensionManager\Repositories\{UniqueGUID}]
@={URI}  (REG_SZ)
Disabled=0 | 1 (DWORD)
Priority=0 (highest priority) ... MaxInt (lowest priority) (DWORD) (uint)
Protocol=Atom Feed|Sharepoint (REG_SZ)
DisplayName={DisplayName} (REG_SZ)
DisplayNameResourceID={ID} (REG_SZ)
DisplayNamePackageGuid={GUID} (REG_SZ)

```

 キーは、 `Repositories` 有効または無効にするギャラリーを参照します。 Visual Studio ギャラリーとサンプルギャラリーでは、次のリポジトリ Guid を使用します。

- Visual Studio ギャラリー: 0F45E408-7995-4375-9485-86B8DB553DC9

- サンプルギャラリー: AEB9CB40-D8E6-4615-B52C-27E307F8506C

  この `Disabled` 値は省略可能です。 既定では、ギャラリーが有効になっています。

  この `Priority` 値は、[ **オプション** ] ダイアログボックスでギャラリーが表示される順序を決定します。 Visual Studio ギャラリーの優先度は10で、サンプルギャラリーの優先度は20です。 プライベートギャラリーは、優先順位100で開始します。 複数のギャラリーに同じ優先順位値が設定されている場合、それらが表示される順序は、ローカライズされた属性の値によって決まり `DisplayName` ます。

  この `Protocol` 値は、Atom ベースまたは SharePoint ベースのギャラリーに必須です。

  `DisplayName`、、またはの両方を `DisplayNameResourceID` `DisplayNamePackageGuid` 指定する必要があります。 All を指定した場合は、 `DisplayNameResourceID` との `DisplayNamePackageGuid` ペアが使用されます。

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>Pkgdef ファイルを使用して Visual Studio ギャラリーを無効にする
 *Pkgdef*ファイルでギャラリーを無効にすることができます。 次のエントリは、Visual Studio ギャラリーを無効にします。

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 次のエントリは、サンプルギャラリーを無効にします。

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>参照
- [プライベート ギャラリー](../extensibility/private-galleries.md)
