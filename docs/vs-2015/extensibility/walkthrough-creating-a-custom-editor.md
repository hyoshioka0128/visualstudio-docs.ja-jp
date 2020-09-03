---
title: 'チュートリアル: カスタムエディターの作成 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - create
ms.assetid: d090abb6-d99f-4083-a3db-cd16bf81ce7d
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4b1b4e59e43a4a5aeb129464a34b96ef3f665e72
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148865"
---
# <a name="walkthrough-creating-a-custom-editor"></a>チュートリアル: カスタム エディターを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VSPackage プロジェクトテンプレートでは、C++ で単純なカスタムエディターを作成できます。  VSPackage プロジェクトテンプレートでは、C# または Visual Basic プロジェクトはサポートされなくなりました。 詳細については、「 [Visual STUDIO SDK](../extensibility/visual-studio-sdk.md)」を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。  
  
## <a name="the-visual-studio-package-project-template"></a>Visual Studio パッケージプロジェクトテンプレート  
 Visual Studio パッケージプロジェクトテンプレートは、C++ 機能拡張フォルダーの [ **新しいプロジェクト** ] ダイアログにあります。  
  
### <a name="to-create-a-vspackage-using-the-visual-studio-package-template"></a>Visual Studio パッケージテンプレートを使用して VSPackage を作成するには  
  
1. Visual Studio パッケージテンプレートを使用してプロジェクトを作成します。  
  
2. [ **カスタムエディター** ] オプションを選択し、[ **次へ**] をクリックします。 [ **エディターオプション** ] ページが表示されます。  
  
3. [ **エディター名** ] ボックスにエディターの名前を入力します。 エディターに関連付けるファイル拡張子を [ **ファイル拡張子** ] ボックスに入力します。 エディターは、この拡張子を持つファイルに対して使用できます。 ファイル拡張子は Visual Studio に対してのみ登録され、Windows では登録されません。 エディターで作成した新しいドキュメントの既定のファイル名を [ **既定のファイル名** ] ボックスに入力します。  
  
4. **[完了]** をクリックして、指定したフォルダーに VSPackage を作成します。  
  
### <a name="to-test-your-custom-editor"></a>カスタムエディターをテストするには  
  
1. [ **ファイル** ] メニューの [ **新規作成** ] をポイントし、[ **ファイル**] をクリックします。  
  
2. [**新しいファイル**] ダイアログボックスの [**インストールされたテンプレート**] ペインで、ファイルテンプレートを選択し、先ほど登録したファイルの種類を選択します。  
  
3. ドキュメントを表示および編集するには、[ **開く** ] をクリックします。  
  
     このエディターでは、切り取りと貼り付け、検索と置換、および開く操作と読み込み操作をサポートしています。  
  
## <a name="see-also"></a>参照  
 [VSPackages](../extensibility/internals/vspackages.md)
