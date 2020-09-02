---
title: エディターと言語サービスの拡張 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK]
ms.assetid: 5653bac9-724f-4948-a820-68ce6aa96365
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7fa3e4be6ee44011eb1286e3ebf22ee69f8e3397
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65683114"
---
# <a name="editor-and-language-service-extensions"></a>エディターと言語サービスの拡張機能
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio code エディターのほとんどの機能を拡張できます。 このエディターは Windows Presentation Foundation (WPF) に基づいており、マネージコードで記述されています。 この設計は、以前のバージョンの Visual Studio の設計とは異なりますが、ほとんど同じ機能を提供します。 エディターを拡張するには、Managed Extensibility Framework (MEF) を使用します。  
  
 Visual Studio SDK には、以前のバージョン用に記述された Vspackage をサポートするための *shim* と呼ばれるアダプターが用意されています。 ただし、既存の VSPackage がある場合は、パフォーマンスと信頼性を向上させるために、新しいテクノロジに更新することをお勧めします。  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[エディターの項目テンプレートを使用した拡張機能の作成](../extensibility/creating-an-extension-with-an-editor-item-template.md)|エディター項目テンプレートの使用方法について説明します。|  
|[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)|コアエディターのデザインと機能を紹介するドキュメントへのリンクと、それを拡張する方法を示します。|  
|[エディターのレガシ インターフェイス](../extensibility/legacy-interfaces-in-the-editor.md)|既存のコードからコアエディターにアクセスする方法を説明するドキュメントへのリンクです。|  
|[カスタム エディターとデザイナーの作成](../extensibility/creating-custom-editors-and-designers.md)|カスタムエディターを作成する方法を説明するドキュメントへのリンク。|  
|[従来の言語サービスの機能拡張](../extensibility/internals/legacy-language-service-extensibility.md)|プログラミング言語を Visual Studio に統合する方法について説明するドキュメントへのリンクです。|  
|[MEF (Managed Extensibility Framework)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)|Managed Extensibility Framework (MEF) について説明します。|  
|[Windows Presentation Foundation](https://msdn.microsoft.com/library/f667bd15-2134-41e9-b4af-5ced6fafab5d)|Windows Presentation Foundation (WPF) について説明します。|
