---
title: '方法 : レジストリ設定を使用してプライベート ギャラリーを管理する |マイクロソフトドキュメント'
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
ms.openlocfilehash: a2630fc71bea40a4d05e616ae336759ba62431a0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710934"
---
# <a name="how-to-manage-a-private-gallery-by-using-registry-settings"></a>方法: レジストリ設定を使用してプライベート ギャラリーを管理する
分離シェル拡張機能の管理者または開発者は、Visual Studio ギャラリー、サンプル ギャラリー、またはプライベート ギャラリーのコントロール、テンプレート、およびツールへのアクセスを制御できます。 ギャラリーを使用または使用不可にするには、変更されたレジストリ キーとその値を記述する *.pkgdef*ファイルを作成します。

## <a name="manage-private-galleries"></a>プライベート ギャラリーの管理
 複数のコンピュータ上のギャラリーへのアクセスを制御する *.pkgdef*ファイルを作成できます。 このファイルは、次の形式である必要があります。

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

 キー`Repositories`は、有効または無効にするギャラリーを指します。 Visual Studio ギャラリーとサンプル ギャラリーでは、次のリポジトリ GUID を使用します。

- ビジュアルスタジオギャラリー: 0F45E408-7995-4375-9485-86B8DB553DC9

- サンプルギャラリー : AEB9CB40-D8E6-4615-B52C-27E307F8506C

  値`Disabled`は省略可能です。 既定では、ギャラリーは有効になっています。

  この`Priority`値によって、[**オプション]** ダイアログ ボックスにギャラリーが表示される順序が決まります。 Visual Studio ギャラリーには優先度 10 があり、サンプル ギャラリーには優先度 20 があります。 プライベート ギャラリーは優先度 100 から始まります。 複数のギャラリーの優先度の値が同じである場合、表示される順序はローカライズされた`DisplayName`属性の値によって決まります。

  この`Protocol`値は、Atom ベースまたは SharePoint ベースのギャラリーに必要です。

  のいずれか`DisplayName`、または`DisplayNameResourceID` `DisplayNamePackageGuid`、のいずれか、または の を指定する必要があります。 すべて指定されている場合は、`DisplayNameResourceID`と`DisplayNamePackageGuid`のペアが使用されます。

## <a name="disable-the-visual-studio-gallery-using-a-pkgdef-file"></a>pkgdef ファイルを使用して Visual Studio ギャラリーを無効にする
 *.pkgdef*ファイルのギャラリーを無効にすることができます。 次のエントリは、Visual Studio ギャラリーを無効にします。

```
[$RootKey$\ExtensionManager\Repositories\{0F45E408-7995-4375-9485-86B8DB553DC9}]
"Disabled"=dword:00000001

```

 次のエントリは、サンプル ギャラリーを無効にします。

```
[$RootKey$\ExtensionManager\Repositories\{AEB9CB40-D8E6-4615-B52C-27E307F8506C}]
"Disabled"=dword:00000001

```

## <a name="see-also"></a>関連項目
- [プライベートギャラリー](../extensibility/private-galleries.md)
