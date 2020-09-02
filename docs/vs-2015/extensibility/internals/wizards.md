---
title: ウィザード |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], providing wizard support
ms.assetid: 59d9a77f-ee80-474b-a14f-90f477ab717b
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6e58ebd736f7bb9f35df6e41d5235f36f7037259
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687630"
---
# <a name="wizards"></a>ウィザード
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ウィザードを作成した後は、通常、 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 他のユーザーが使用できるように統合開発環境 (IDE) に追加します。 追加したウィザードは、[ **新しいプロジェクトの追加** ] または [ **新しい項目の追加** ] ダイアログボックスに表示されます。 [ **新しいプロジェクトの追加** ] または [ **新しい項目の追加** ] ダイアログボックスを表示するには、 **ソリューションエクスプローラー**で開いているソリューションを右クリックし、[ **追加**] をポイントして、[ **新しいプロジェクト** ] または [ **新しい項目**] をクリックします。  
  
 でウィザードを実装すると、ユーザーが [ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **新しいプロジェクトの追加** ] ダイアログボックスまたは [ **新しい項目の追加** ] ダイアログボックスを開いたとき、または **ソリューションエクスプローラー**内の項目を右クリックしたときに、使用可能な値のツリービューから選択できるようになります。  
  
 ウィザードでは、新しいプロジェクトまたはユーザーの名前をローカライズするオプションを指定できます。また、ウィザードを選択したときにユーザーに表示されるアイコンを決定することもできます。 また、使用可能な他の項目と比較して、新しい項目を表示する順序を制御することもできます。項目をアルファベット順に整理する必要はありません。  
  
 ウィザードを開いたときに渡されるカスタムパラメーターに基づいて、異なる方法で起動するウィザードを指定することもできます。  
  
 このセクションの各トピックでは、[ [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] **新しいプロジェクトの追加** ] ダイアログボックスと [ **新しい項目の追加** ] ダイアログボックスを使用してウィザードを一覧表示し、使用可能なウィザードとテンプレートを表示する方法、およびウィザードが IDE で正しく動作するために満たす必要がある要件について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [テンプレート ディレクトリの説明 (.Vsdir) ファイル](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)  
 テンプレートディレクトリ記述ファイルの概要と、ダイアログボックス内のプロジェクトに関連付けられているフォルダー、ウィザード .vsz ファイル、およびテンプレートファイルを IDE でどのように表示するかについて説明します。  
  
 [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)  
 IDE によるウィザードの起動方法と、.vsz ファイルの3つの部分の一覧を示します。  
  
 [ウィザード インターフェイス (IDTWizard)](../../extensibility/internals/wizard-interface-idtwizard.md)  
 `IDTWizard`IDE で動作するためにウィザードが実装する必要のあるインターフェイスについて説明します。  
  
 [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)  
 ウィザードの実装方法と、IDE がコンテキストパラメーターを実装に渡すときの動作について説明します。  
  
 [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)  
 ウィザードを起動した後に、カスタムパラメーターを使用してウィザードの操作を制御する方法について説明します。  
  
## <a name="related-sections"></a>関連項目  
 [プロジェクトの種類](../../extensibility/internals/project-types.md)  
 新しいプロジェクトの種類をデザインする方法に関する情報を提供するその他のトピックへのリンクを示します。  
  
 [チュートリアル : ウィザードの作成](https://msdn.microsoft.com/library/adb41fe9-fcca-4e87-bf4f-bf2fa68e8b06)  
 ウィザードの作成方法について説明します。  
  
 [プロジェクトの拡張](../../extensibility/extending-projects.md)  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] プロジェクトおよびソリューションを使用してコード ファイルとリソース ファイルを編成する方法、またソース管理を実装する方法について説明します。
