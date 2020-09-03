---
title: テンプレートポリシーと [プロパティ] ウィンドウ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Properties window, template policy
ms.assetid: 1d8019d3-5e57-47ba-b358-526b0796a63b
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1c67150c5a71a3d70df85669319795a405c60f4a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156024"
---
# <a name="template-policy-and-the-properties-window"></a>テンプレート ポリシーとプロパティ ウィンドウ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

エンタープライズテンプレートプロジェクト内にプロジェクトが含まれている場合、そのエンタープライズテンプレートプロジェクトでポリシーを適用できます。 テンプレートポリシーは、プロパティの既定値を設定したり、プロパティを非表示にしたり、プロパティを追加したりするために使用できる制約システムになります。  
  
 テンプレートポリシーを使用して、[ **プロパティ** ] ウィンドウでの情報の表示を制御することは、の実装とは異なり <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> コンポーネントレベルでオブジェクトのプロパティを処理します。テンプレートポリシーを使用して、ソリューションレベルまたはプロジェクトレベルでオブジェクトのプロパティを制約できます。 要するにあの  
  
- にメソッドを実装して <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 、特定のオブジェクトの [ **プロパティ** ] ウィンドウに表示される内容を決定します。  
  
- ソリューションおよびプロジェクトレベルでテンプレートポリシーを使用して、以前に指定したオブジェクトの [ **プロパティ** ] ウィンドウに表示される内容を決定します。  
  
  テンプレートポリシーを使用して、指定された種類のプロジェクト項目が**ソリューションエクスプローラー**で選択されている場合に、[**プロパティ**] ウィンドウで特定のプロパティを選択的に制限することができます。これは、プロジェクトで作業している開発チームのすべてのメンバーに役立ちます。 たとえば、テンプレートポリシーを使用すると、開発者がデータベース内のすべての接続文字列情報を設定し、接続文字列を読み取り専用にすることができます。 このようにして、各開発者がデータアクセスに適切なパスを使用するようにするための簡単な方法を提供できます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing>   
 [プロパティの拡張](../../extensibility/internals/extending-properties.md)
