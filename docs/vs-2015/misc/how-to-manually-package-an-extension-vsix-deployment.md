---
title: 'How to: Manually Package an Extension (VSIX Deployment) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: d25990e0-e782-4a79-9d9a-1caf3c56c6a2
caps.latest.revision: 10
manager: jillfra
ms.openlocfilehash: a615aea75ec00e49ee4d2837b8b4e2b1d20d3306
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74293618"
---
# <a name="how-to-manually-package-an-extension-vsix-deployment"></a>方法: 拡張機能を手動でパッケージ化する (VSIX 配置)
VSIX パッケージを作成して、配置用の [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 拡張機能をラップすることができます。 パッケージを作成するには、3 つの方法があります。  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] SDK に含まれている機能拡張テンプレートのいずれかを使用して、VSIX パッケージ プロジェクトを作成します。 これは、ほとんどのシナリオで最も簡単なオプションです。  
  
- 拡張プロジェクトの出力を空の [VSIX プロジェクト](../extensibility/vsix-project-template.md)でラップします。 テンプレート、サポートされていないアセンブリおよびカスタム型には、このオプションをお勧めします。  
  
- VSIX パッケージを手動で作成します。 このオプションは、その他の 2 つのオプションが利用できない場合にのみお勧めします。  
  
  ここでは、3 つ目のオプションについて説明します。  
  
## <a name="creating-a-vsix-package"></a>VSIX パッケージの作成  
 拡張機能を手動でパッケージ化するには、extension.manifest ファイルと [Content_Types].xml ファイルを拡張機能プロジェクトに追加し、ビルド出力と一緒に圧縮ファイルに含め、.vsix ファイル名拡張子を持つように圧縮ファイルの名前を変更します。 パッケージ化する拡張機能は、 [VSIX スキーマ](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)でサポートされている種類のものである必要があります。  
  
> [!NOTE]
> The names of files in VSIX packages must not include spaces, nor characters that are reserved in Uniform Resource Identifiers (URI), as defined under [\[RFC2396\]](https://go.microsoft.com/fwlink/?LinkId=90339).  
  
#### <a name="to-manually-create-a-vsix-package"></a>VSIX パッケージを手動で作成するには  
  
1. VSIX スキーマでサポートされている型の Visual Studio 拡張機能を作成します。  
  
2. XML ファイルを作成し、 `extension.vsixmanifest`という名前を付けます。  
  
3. VSIX スキーマに従って extension.vsixmanifest ファイルを入力します。 マニフェストの例については、「 [PackageManifest Element (Root Element, VSX Schema)](https://msdn.microsoft.com/f8ae42ba-775a-4d2b-976a-f556e147f187)」を参照してください。  
  
4. 2 つ目の XML ファイルを作成し、 `[Content_Types].xml`という名前を付けます。  
  
5. Fill in the [Content_Types].xml file as specified in [The Structure of the Content_types\].xml File](../extensibility/the-structure-of-the-content-types-dot-xml-file.md).  
  
6. ディレクトリ内に、配置する拡張機能と共に、両方の XML ファイルを配置します。  
  
     プロジェクト テンプレートや項目テンプレートでは、XML ファイルと同じフォルダーにテンプレートを含む .zip ファイルを配置します。 .zip ファイルに XML ファイルを配置しないでください。  
  
     その他のすべての場合においては、ビルド出力と同じディレクトリに XML ファイルを配置します。  
  
7. Windows エクスプローラーで、拡張コンテンツと 2 つの XML ファイルを含むフォルダーを右クリックし、 **[送信]** をクリックして、 **[圧縮 (zip 形式) フォルダー]** をクリックします。  
  
8. 結果として得られる .zip ファイルの名前を *Filename*.vsix に変更します。ここで *Filename* には、パッケージをインストールする再頒布可能なファイルの名前を指定します。  
  
## <a name="see-also"></a>参照  
 [Shipping Visual Studio Extensions](../extensibility/shipping-visual-studio-extensions.md)   
 [Anatomy of a VSIX Package](../extensibility/anatomy-of-a-vsix-package.md)   
 [PackageManifest Element (Root Element, VSX Schema)](https://msdn.microsoft.com/f8ae42ba-775a-4d2b-976a-f556e147f187)