---
title: VS パッケージ内のリソース |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 493e9834e3d7cf6d82cebb8dd93d5369678c7be0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80705602"
---
# <a name="resources-in-vspackages"></a>VSPackage のリソース
ローカライズされたリソースは、ネイティブのサテライト UI DLL、マネージ サテライト DLL、またはマネージ VSPackage 自体に埋め込むことができます。

 VS パッケージに埋め込めないリソースがあります。 次のマネージ型を埋め込むことができます。

- 文字列

- パッケージの読み込みキー (文字列でもある)

- ツール ウィンドウのアイコン

- コンパイル済みコマンド・テーブル出力 (CTO) ファイル

- CTO ビットマップ

- コマンド ライン ヘルプ

- ダイアログ ボックスデータについて

  管理パッケージ内のリソースは、リソース ID によって選択されます。 例外は CTO ファイルで、CTMENU という名前を付ける必要があります。 CTO ファイルは、 としてリソース テーブルに`byte[]`表示される必要があります。 その他すべてのリソース項目は、タイプによって識別されます。

  属性を<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>使用して、管理対象リソース[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]が使用可能であることを示すことができます。

  [!code-csharp[VSSDKResources#1](../../extensibility/internals/codesnippet/CSharp/resources-in-vspackages_1.cs)]
  [!code-vb[VSSDKResources#1](../../extensibility/internals/codesnippet/VisualBasic/resources-in-vspackages_1.vb)]

  この<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>方法で設定すると、[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]を使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A>してリソースを検索する場合に、アンマネージ サテライト DLL を無視する必要があることを示します。 同[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]じリソース ID を持つ 2 つ以上のリソースが検出された場合、最初に検出されたリソースが使用されます。

## <a name="example"></a>例
 次の例は、ツール ウィンドウ アイコンのマネージ表現です。

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

 次の例は、CTO バイト配列を埋め込む方法を示しています。

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
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可能な限り VS パッケージの読み込みを遅延します。 VSPackage に CTO ファイルを埋め込んだ結果は[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]、マージされたコマンド テーブルを構築するセットアップ中に、このような VSPackage をメモリに読み込む必要があります。 VSPackage でコードを実行せずにメタデータを調べることによって、VSPackage からリソースを抽出できます。 VSPackage は現在初期化されていないため、パフォーマンスの低下は最小限です。

 セットアップ[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]後に VSPackage からリソースを要求すると、そのパッケージは既に読み込まれて初期化されている可能性が高いので、パフォーマンスの低下は最小限に抑えられます。

## <a name="see-also"></a>関連項目
- [VSPackage の管理](../../extensibility/managing-vspackages.md)
- [MFC アプリケーションのローカライズされたリソース: サテライト DLL](/cpp/build/localized-resources-in-mfc-applications-satellite-dlls)
