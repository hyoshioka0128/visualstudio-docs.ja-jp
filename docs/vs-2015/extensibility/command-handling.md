---
title: コマンド処理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - command handling
ms.assetid: 78f67d92-77f7-45cb-ad75-6e3346379cc3
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 563f38cd2dc3854918fe637fdc11afe1d1a49b64
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184372"
---
# <a name="command-handling"></a>コマンド処理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

エディターでは、新しいコマンドを定義できます。 コマンドは、通常、メニュー、ツールバー、またはショートカットメニューに表示されます。  
  
 コマンドとメニューの定義の詳細については、「 [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)」を参照してください。  
  
 言語サービスでは、エディターに表示されるコンテキストメニューを、列挙をインターセプトすることによって制御でき <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> ます。 または、マーカーごとにコンテキストメニューを制御できます。 詳細については、「 [言語サービスフィルターの重要なコマンド](../extensibility/internals/important-commands-for-language-service-filters.md)」を参照してください。  
  
## <a name="adding-commands-to-the-editor-context-menu"></a>エディターコンテキストメニューへのコマンドの追加  
 ショートカットメニューにコマンドを追加するには、まず、特定のグループに属する一連のメニューコマンドを定義する必要があります。 次の例は、チュートリアル [「チュートリアル: カスタムエディターへの機能の追加](../extensibility/walkthrough-adding-features-to-a-custom-editor.md)」の一部として生成された vsct ファイルから取得されます。  
  
 \<Menu guid="guidCustomEditorCmdSet" id="IDMX_RTF" priority="0x0000" type="Context">  
  
 \<Parent guid="guidCustomEditorCmdSet" id="0"/>  
  
 \<Strings>  
  
 \<ButtonText>CustomEditor コンテキストメニュー\</ButtonText>  
  
 \<CommandName>CustomEditorContextMenu\</CommandName>  
  
 \</Strings>  
  
 \</Menu>  
  
 \</Menus>  
  
 上のテキストは、「 **Customeditor コンテキストメニュー」** というテキストを含むコンテキストメニューコマンドを追加します。 メニュー GUID は、このエディターで作成されるコマンドセットのものであり、型は "Context" です。  
  
 また、vsct ファイルで定義する必要がない定義済みコマンドを使用することもできます。 たとえば、Visual Studio パッケージテンプレートによって生成された EditorPane.cs ファイルを調べると、で定義されているような定義済みコマンドのセット <xref:Microsoft.VisualStudio.VSConstants.VSStd97CmdID> <xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97> が、onSelectAll メソッドなどのコマンドハンドラーで処理されることがわかります。  
  
## <a name="see-also"></a>参照  
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
