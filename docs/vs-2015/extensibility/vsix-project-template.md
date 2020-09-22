---
title: VSIX プロジェクトテンプレート |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- deploy packages
- publish extension
ms.assetid: b6c82167-e2a5-4cff-8c8b-2d72e2a9092c
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2386f1be805f6347fc32fba4ee8bfe57c8602329
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842145"
---
# <a name="vsix-project-template"></a>VSIX プロジェクト テンプレート
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSIX プロジェクトテンプレートを使用すると、VSIX プロジェクトで1つ以上の Visual Studio 拡張機能をラップし、 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web サイトでパッケージを発行できます。  
  
 VSIX 配置では、Vspackage、アセンブリ、MEF コンポーネント、プロジェクトテンプレート、項目テンプレート、ツールボックスコントロール、およびカスタム拡張型をサポートしています。  
  
> [!NOTE]
> VSIX プロジェクトを使用するには、Visual Studio SDK をインストールする必要があります。 Visual Studio SDK の詳細については、「 [Visual STUDIO sdk](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="where-to-find-the-vsix-project-template"></a>VSIX プロジェクトテンプレートの検索場所  
 [ **新しいプロジェクト** ] ダイアログボックスでは、VSIX プロジェクトテンプレートを使用できます。 [ **Visual Basic** ] ノードまたは [ **Visual C#** ] ノードを展開し、[ **機能拡張**] を選択します。  
  
> [!TIP]
> [ **新しいプロジェクト** ] ダイアログボックスの上部にあるドロップダウンで .NET Framework 4.5 以上が指定されていることを確認する必要があります。  
  
## <a name="uses-of-the-vsix-project-template"></a>VSIX プロジェクトテンプレートの使用  
 VSIX プロジェクトテンプレートには、主に次の2つの用途があります。  
  
- プロジェクトテンプレート、項目テンプレート、および VSIX がサポートされていないその他の拡張機能を配置する場合。  
  
- 複数の拡張機能の出力を1つの展開パッケージにラップすること。  
  
  Vsix プロジェクトテンプレートを使用して、既に VSIX をサポートしている Vspackage またはその他の種類の拡張機能を配置する必要はありません。  
  
## <a name="packaging-an-extension-in-an-empty-vsix-project"></a>空の VSIX プロジェクトで拡張機能をパッケージ化する  
 既存の拡張機能、またはまだ VSIX をサポートしていない拡張機能をパッケージ化するには、空の VSIX プロジェクトでラップします。 ラップする拡張機能は、 [VSIX スキーマ](../extensibility/vsix-extension-schema-2-0-reference.md)でサポートされている型である必要があります。  
  
#### <a name="to-package-an-extension-by-using-a-vsix-project"></a>VSIX プロジェクトを使用して拡張機能をパッケージ化するには  
  
1. 拡張機能を構成するプロジェクトをビルドします。  
  
2. Vsix **プロジェクト** テンプレートを使用して vsix プロジェクトを作成します。  
  
     Source.extension.vsixmanifest が **マニフェストデザイナー**で開きます。  
  
3. [ **アセット** ] タブで、[ **新規** ] ボタンをクリックします。  
  
     [ **新しい資産の追加** ] ダイアログボックスが表示されます。  
  
4. [ **種類** ] ボックスの一覧で、追加する拡張機能の種類を選択します。  
  
5. 現在のソリューションに含まれる拡張機能またはコンテンツ要素 (項目テンプレートやコンパイル済みアセンブリなど) を追加するには、次の手順を実行します。  
  
    1. [ **ソース** ] ボックスの一覧で、 **現在のソリューション内のプロジェクト**を選択します。  
  
    2. [ **プロジェクト** ] ボックスの一覧で、拡張機能の名前を選択します。  
  
    3. [ **このフォルダーに埋め込む** ] ボックスに、資産を埋め込むフォルダーの名前を入力し、[ **OK** ] をクリックします。  
  
6. 現在のソリューションに含まれていない拡張機能またはコンテンツ要素を追加するには、次の手順を実行します。  
  
    1. [ **ソース** ] ボックスの一覧で、[ **ファイルシステム上のファイル**] を選択します。  
  
    2. [ **パス** ] フィールドに、コンパイルまたは圧縮された拡張ファイルへの完全なパスを入力するか、[ **参照** ] ボタンを使用してファイルを参照します。  
  
    3. [ **このフォルダーに埋め込む** ] ボックスに、資産を埋め込むフォルダーの名前を入力し、[ **OK** ] をクリックします。  
  
7. パッケージに追加の拡張機能を含める場合は、同じ方法でパッケージを追加します。  
  
8. ソリューションをビルドします。  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] VSIX マニフェストファイル、[Content_Types] .xml ファイル、およびプロジェクトに追加したすべての拡張機能アセットを含む .vsix ファイルをビルドします。  
  
## <a name="see-also"></a>参照  
 [VSIX 拡張機能スキーマ2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)   
 [Visual Studio 拡張機能の検索と使用](../ide/finding-and-using-visual-studio-extensions.md)
