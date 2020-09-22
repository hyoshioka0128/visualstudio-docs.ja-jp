---
title: コマンドの可用性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, context
- menu items, visibility contexts
ms.assetid: c74e3ccf-d771-48c8-a2f9-df323b166784
caps.latest.revision: 35
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f060f6c49fc02c75b3fe9f792133c9ee88c6d56c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841380"
---
# <a name="command-availability"></a>コマンドの可用性
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio のコンテキストによって、使用できるコマンドが決まります。 コンテキストは、現在のプロジェクト、現在のエディター、読み込まれている Vspackage、および統合開発環境 (IDE) のその他の側面によって変わります。  
  
## <a name="command-contexts"></a>コマンドコンテキスト  
 最も一般的なコマンドコンテキストは次のとおりです。  
  
- **IDE** IDE によって提供されるコマンドは、常に使用できます。  
  
- **VSPackage** Vspackage では、コマンドを表示するか非表示にするかを定義できます。  
  
- **プロジェクト** プロジェクトコマンドは、現在選択されているプロジェクトに対してのみ表示されます。  
  
- **エディター** 一度にアクティブにできるエディターは1つだけです。 アクティブなエディターのコマンドを使用できます。 エディターは言語サービスと密接に連携します。 言語サービスは、関連付けられているエディターのコンテキストでコマンドを処理する必要があります。  
  
- **ファイルの種類** エディターでは、複数の種類のファイルを読み込むことができます。 使用可能なコマンドは、ファイルの種類によって変わることがあります。  
  
- **アクティブウィンドウ** 最後のアクティブなドキュメントウィンドウは、キーバインドのユーザーインターフェイス (UI) コンテキストを設定します。 ただし、内部 Web ブラウザーに似たキーバインドテーブルを持つツールウィンドウでは、UI コンテキストを設定することもできます。 HTML エディターなどの複数タブのドキュメントウィンドウでは、すべてのタブに異なるコマンドコンテキスト GUID があります。 ツールウィンドウが登録されると、常に [ **表示** ] メニューから使用できるようになります。  
  
- **UI コンテキスト** UI コンテキストは、クラスの値によって識別され <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT> <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid> ます。たとえば、ソリューションがビルドされている場合や、 <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid> デバッガーがアクティブな場合などです。 複数の UI コンテキストを同時にアクティブにすることができます。  
  
## <a name="defining-custom-context-guids"></a>定義 (カスタムコンテキスト Guid を)  
 適切なコマンドコンテキスト GUID がまだ定義されていない場合は、VSPackage で定義してから、コマンドの可視性を制御するために必要に応じてアクティブまたは非アクティブにするようにプログラムを設定できます。  
  
1. メソッドを呼び出してコンテキスト Guid を登録 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> します。  
  
2. メソッドを呼び出して、コンテキスト GUID の状態を取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> ます。  
  
3. メソッドを呼び出して、コンテキスト Guid のオンとオフを切り替え <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> ます。  
  
    > [!CAUTION]
    > VSPackage が既存のコンテキスト Guid に影響しないことを確認してください。他の Vspackage が依存している可能性があります。  
  
## <a name="see-also"></a>参照  
 [選択コンテキストオブジェクト](../../extensibility/internals/selection-context-objects.md)   
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
