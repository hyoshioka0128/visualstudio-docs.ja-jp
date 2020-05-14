---
title: 'チュートリアル: カスタム エディターの作成 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7eb376637fd72f3856415ee2527ec622fea02950
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697684"
---
# <a name="walkthrough-create-a-custom-editor"></a>チュートリアル: カスタム エディターを作成する
VSPackage プロジェクト テンプレートは、C++ で簡単なカスタム エディターを作成できます。 VSPackage プロジェクト テンプレートでは、C# または Visual Basic プロジェクトをサポートしなくなりました。 詳細については、「 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレート
 Visual Studio パッケージ プロジェクト テンプレートは、[**新しいプロジェクト**] ダイアログの **[C++ 拡張機能**] フォルダーにあります。

### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>Visual Studio パッケージ テンプレートを使用して VS パッケージを作成するには

1. Visual Studio パッケージ テンプレートを使用してプロジェクトを作成します。

2. [**カスタム エディタ**] オプションを選択し、[**次へ**] をクリックします。 [**エディタ オプション]** ページが表示されます。

3. [エディタ名] ボックスに、エディタの**名前**を入力します。 [ファイル拡張子] ボックスに、エディターに関連付ける**ファイル拡張子**を入力します。 この拡張子のファイルでは、エディタを使用できます。 ファイル拡張子は、Windows 用ではなく、Visual Studio にのみ登録されています。 エディターで作成した新しいドキュメントの既定のファイル名を **[既定のファイル名**] ボックスに入力します。

4. **[完了]** をクリックして、指定したフォルダーに VSPackage を作成します。

### <a name="to-test-your-custom-editor"></a>カスタム エディターをテストするには

1. [**ファイル**] メニューの **[新規作成**] をポイントし、[**ファイル**] をクリックします。

2. [**新しいファイル**] ダイアログ ボックスの [**インストールされているテンプレート**] ペインで、ファイル テンプレートを選択し、登録したファイルの種類を選択します。

3. [**開く**] をクリックして、ドキュメントを表示および編集します。

     このエディターは、カットアンドペースト、検索と置換、およびオープンアンドロード操作をサポートしています。

## <a name="see-also"></a>関連項目
- [VSPackages](../extensibility/internals/vspackages.md)
