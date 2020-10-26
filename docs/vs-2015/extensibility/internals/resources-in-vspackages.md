---
title: Vspackage | のリソースMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, resources in
- resources, managed VSPackages
- VSPackages, managed resources
ms.assetid: cc8c17a6-b190-4856-b001-0c1104f104b2
caps.latest.revision: 24
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 90674d17cdc3fb8956fd6eedeb3acb27226620cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696086"
---
# <a name="resources-in-vspackages"></a>VSPackage のリソース
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

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
  
  属性を使用 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] して、マネージリソースが使用可能であることを示すことができます。  
  
  [!code-csharp[VSSDKResources#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdkresources/cs/vssdkresourcespackage.cs#1)]
  [!code-vb[VSSDKResources#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkresources/vb/vssdkresourcespackage.vb#1)]  
  
  この方法でを設定すると、は、 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] などを使用してリソースを検索するときに、アンマネージサテライト dll を無視することを示し <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell.LoadPackageString%2A> ます。 が [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 同じリソース ID を持つ2つ以上のリソースを検出した場合は、最初に検出されたリソースを使用します。  
  
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
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 可能な限り、Vspackage の読み込みを遅延します。 VSPackage に CTO ファイルを埋め込むと、は、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] セットアップ中に、マージされたコマンドテーブルを構築するときに、このようなすべての vspackage をメモリに読み込む必要があります。 リソースを VSPackage から抽出するには、VSPackage でコードを実行せずにメタデータを調べます。 VSPackage は現時点で初期化されていないため、パフォーマンスが低下することは少なくありません。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]がセットアップ後に VSPackage からリソースを要求した場合、そのパッケージは既に読み込まれて初期化される可能性があるため、パフォーマンスが低下することはほとんどありません。  
  
## <a name="see-also"></a>参照  
 [マネージド Vspackage](../../misc/managed-vspackages.md)   
 [Vspackage の管理](../../extensibility/managing-vspackages.md)   
 [MFC アプリケーションのローカライズされたリソース: サテライト Dll](https://msdn.microsoft.com/library/3a1100ae-a9c8-47b5-adbd-cbedef5992ef)   
 [マネージド VSPackage](../../misc/managed-vspackages.md)
