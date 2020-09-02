---
title: Windows インストーラー展開の拡張機能を準備する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- vsix msi
ms.assetid: 5ee2d1ba-478a-4cb7-898f-c3b4b2ee834e
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 76d7f879fade99914bf3f56ade0ec1270e14f4c7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65694587"
---
# <a name="preparing-extensions-for-windows-installer-deployment"></a>Windows インストーラーの配置に関する拡張機能を準備する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows インストーラーパッケージ (MSI) を使用して VSIX パッケージを配置することはできません。 ただし、MSI の展開用に VSIX パッケージのコンテンツを抽出することはできます。 このドキュメントでは、既定の出力がセットアッププロジェクトに含める VSIX パッケージであるプロジェクトを準備する方法について説明します。  
  
## <a name="preparing-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラー配置用の拡張機能プロジェクトの準備  
 セットアッププロジェクトに追加する前に、新しい拡張機能プロジェクトでこれらの手順を実行します。  
  
#### <a name="to-prepare-an-extension-project-for-windows-installer-deployment"></a>Windows インストーラー配置用の拡張機能プロジェクトを準備するには  
  
1. VSPackage、MEF コンポーネント、エディターの表示要素、または VSIX マニフェストを含むその他の機能拡張プロジェクトの種類を作成します。  
  
2. コードエディターで VSIX マニフェストを開きます。  
  
3. VSIX マニフェストの [に設定されている Msi 要素をに設定 `true` します。 VSIX マニフェストの詳細については、「 [Vsix 拡張機能スキーマ2.0 リファレンス](../extensibility/vsix-extension-schema-2-0-reference.md)」を参照してください。  
  
     これにより、VSIX インストーラーはコンポーネントをインストールしようとしません。  
  
4. **ソリューションエクスプローラー**でプロジェクトを右クリックし、[**プロパティ**] をクリックします。  
  
5. [ **VSIX** ] タブを選択します。  
  
6. [ **VSIX コンテンツを次の場所にコピーする** ] チェックボックスをオンにし、セットアッププロジェクトがファイルを取得するパスを入力します。  
  
## <a name="extracting-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからのファイルの抽出  
 ソースファイルがない場合に既存の VSIX パッケージの内容をセットアッププロジェクトに追加するには、次の手順を実行します。  
  
#### <a name="to-extract-files-from-an-existing-vsix-package"></a>既存の VSIX パッケージからファイルを抽出するには  
  
1. の名前を変更します。 *ファイル名*から拡張子が *ファイル名 .zip に含ま*れる vsix ファイル。  
  
2. .Zip ファイルの内容をディレクトリにコピーします。  
  
3. ディレクトリから [Content_types] .xml ファイルを削除します。  
  
4. 前の手順で示したように、VSIX マニフェストを編集します。  
  
5. 残りのファイルをセットアッププロジェクトに追加します。  
  
## <a name="see-also"></a>参照  
 [Visual Studio インストーラーの展開](https://msdn.microsoft.com/121be21b-b916-43e2-8f10-8b080516d2a0)   
 [チュートリアル: カスタム動作の作成](https://msdn.microsoft.com/4bd4b63a-2b91-431e-839c-5752443f0eaf)
