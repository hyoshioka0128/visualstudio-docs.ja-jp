---
title: Vspackage | のリソースMicrosoft Docs
description: Vspackage に埋め込むことができるローカライズされたリソースの種類について説明します。 また、ネイティブサテライト UI Dll またはマネージサテライト Dll にリソースを埋め込むこともできます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c4863fb40bc6f70556d8f00305d882e6edd93a0e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074393"
---
# <a name="resources-in-vspackages"></a>VSPackage のリソース
ローカライズされたリソースは、ネイティブサテライト UI Dll、マネージサテライト Dll、またはマネージ VSPackage 自体に埋め込むことができます。

 一部のリソースは Vspackage に埋め込むことができません。 次のマネージ型を埋め込むことができます。

- 文字列

- パッケージ読み込みキー (文字列でもあります)

- ツールウィンドウのアイコン

- コンパイルされたコマンドテーブル出力 (CTO) ファイル

- CTO ビットマップ

- コマンドラインヘルプ

- ダイアログボックスのデータについて

  マネージパッケージ内のリソースは、リソース ID によって選択されます。 例外は、CTO ファイルです。このファイルには、CTMENU という名前を付ける必要があります。 CTO ファイルは、リソーステーブルにとして表示される必要があり `byte[]` ます。 他のすべてのリソース項目は、型によって識別されます。

  属性を使用 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] して、マネージリソースが使用可能であることを示すことができます。

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  この方法でを設定すると、は、 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] などを使用してリソースを検索するときに、アンマネージサテライト dll を無視することを示し <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A> ます。 が [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 同じリソース ID を持つ2つ以上のリソースを検出した場合は、最初に検出されたリソースを使用します。

## <a name="example"></a>例
 次の例は、ツールウィンドウアイコンのマネージ表現です。

```
<data name="1001"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyToolWinIcon.bmp;
     System.Drawing.Bitmap,
     System.Drawing,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

 次の例は、CTO のバイト配列を埋め込む方法を示しています。この配列には、CTMENU という名前を付ける必要があります。

```
<data name="CTMENU"
type="System.Resources.ResXFileRef,System.Windows.Forms">
     <value>
     MyPackage.cto;
     System.Byte[],
     mscorlib,
     Version=1.0.0.0,
     Culture=neutral,
     PublicKeyToken=b03f5f7f11d50a3a
     </value>
</data>
```

## <a name="implementation-notes"></a>実装に関するメモ
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可能な限り、Vspackage の読み込みを遅延します。 VSPackage に CTO ファイルを埋め込むと、は、 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] セットアップ中に、マージされたコマンドテーブルを構築するときに、このようなすべての vspackage をメモリに読み込む必要があります。 リソースを VSPackage から抽出するには、VSPackage でコードを実行せずにメタデータを調べます。 VSPackage は現時点で初期化されていないため、パフォーマンスが低下することは少なくありません。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]がセットアップ後に VSPackage からリソースを要求した場合、そのパッケージは既に読み込まれて初期化される可能性があるため、パフォーマンスが低下することはほとんどありません。

## <a name="see-also"></a>こちらもご覧ください
- [VSPackage の管理](../../extensibility/managing-vspackages.md)
- [MFC アプリケーションのローカライズされたリソース: サテライト Dll](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
