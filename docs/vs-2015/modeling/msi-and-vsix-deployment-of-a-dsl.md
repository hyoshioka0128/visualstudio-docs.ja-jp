---
title: DSL | の VSIX 配置Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 6ce16f06-1978-4e19-8cdc-441ee65a3fb2
caps.latest.revision: 4
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: be9d3d44bfceaae1f2912086c3d20c90ce1e094b
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916546"
---
# <a name="vsix-deployment-of-a-dsl"></a>DSL の VSIX 配置
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ドメイン固有言語は、自分のコンピューターまたは他のコンピューターにインストールできます。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、ターゲットコンピューターに既にインストールされている必要があります。

## <a name="Installing"></a>VSX を使用して DSL をインストールおよびアンインストールする
 DSL がこの方法でインストールされている場合、ユーザーは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]内から DSL ファイルを開くことができますが、Windows エクスプローラーからファイルを開くことはできません。

#### <a name="to-install-a-dsl-by-using-the-vsix"></a>VSIX を使用して DSL をインストールするには

1. コンピューターで、DSL パッケージプロジェクトによって作成された **.vsix**ファイルを見つけます。

    1. **ソリューションエクスプローラー**で、 **[dslpackage]** プロジェクトを右クリックし、 **[エクスプローラーでフォルダーを開く]** をクリックします。

    2. _YourProject_ **\\\*\\** ファイルの bin を見つけ**ます。DslPackage。 .vsix**

2. DSL をインストールするターゲットコンピューターに .vsix ファイルをコピー**します。** 自分のコンピューターでも別のコンピューターでもかまいません。

    - ターゲットコンピューターは、実行時に Dsl をサポートする [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] のいずれかのエディションを搭載している必要があります。 詳細については、「[サポートされている Visual Studio エディションの視覚化 & モデリング SDK](../modeling/supported-visual-studio-editions-for-visualization-amp-modeling-sdk.md)」を参照してください。

    - 対象のコンピューターには、 **DslPackage\source.extensions.manifest**で指定された [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] のいずれかのエディションが必要です。

3. ターゲットコンピューターで、 **.vsix**ファイルをダブルクリックします。

     **Visual Studio 拡張機能インストーラー** が起動され、拡張機能がインストールされます。

4. [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]を起動または再起動します。

5. DSL をテストするには、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用して、DSL 用に定義した拡張子を持つ新しいファイルを作成します。

#### <a name="to-uninstall-a-dsl-that-was-installed-by-using-vsx"></a>VSX を使用してインストールされた DSL をアンインストールするには

1. **[ツール]** メニューの **[拡張機能マネージャー]** をクリックします。

2. **[インストール済みの拡張機能]** を展開します。

3. DSL が定義されている拡張機能を選択し、 **[アンインストール]** をクリックします。

   拡張機能の障害が原因で読み込みが失敗し、エラー ウィンドウにレポートが生成されることがまれにありますが、それは拡張機能マネージャーには表示されません。 その場合は、以下の場所からファイルを削除して、拡張機能を削除します。

   *LocalAppData* **\Microsoft\VisualStudio\10.0\Extensions**
