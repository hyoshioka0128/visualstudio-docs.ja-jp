---
title: Vspackage の管理 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, autoloading
- VSPackages, delayed loading
- delay loading
- VSPackages, loading
ms.assetid: 386e0ce5-4107-4164-b0cd-1cf43eb5e7cf
caps.latest.revision: 36
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0b56ab490342cfbda9c16408aa0937abd80728c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194380"
---
# <a name="managing-vspackages"></a>VSPackage の管理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ほとんどの場合、Vspackage の管理について心配する必要はありません。プロジェクトと項目テンプレートによってパッケージが登録され、自動的に読み込まれるためです。 ただし、状況によっては、パッケージを管理するためにもう少し学習が必要になる場合があります。  
  
## <a name="using-the-experimental-instance"></a>実験用インスタンスの使用  
 実験用インスタンスの詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。  
  
## <a name="registering-and-unregistering-vspackages"></a>VSPackage の登録と登録解除  
 Vspackage とその他の種類の拡張機能を登録および登録解除する方法については、「 [vspackage の登録と](../extensibility/registering-and-unregistering-vspackages.md)登録解除」を参照してください。  
  
## <a name="loading-a-vspackage"></a>VSPackage を読み込んでいます  
 Vspackage は、特定の CMDUICONTEXT GUID が有効になっている場合に自動読み込みするように設定できます。 詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。  
  
## <a name="using-asyncpackage-to-load-vspackages-in-the-background"></a>AsyncPackage を使用してバックグラウンドで Vspackage を読み込む  
 AsyncPackage クラスを使用すると、バックグラウンドスレッドでのパッケージの読み込みが有効になり、Visual Studio での UI の応答性が向上します。 詳細については、「 [方法: AsyncPackage を使用してバックグラウンドで vspackage を読み込む](../extensibility/how-to-use-asyncpackage-to-load-vspackages-in-the-background.md)」を参照してください。  
  
## <a name="rule-based-ui-context-for-extensions"></a>拡張機能のルールベースの UI コンテキスト  
 ルールベースの UI コンテキストを使用すると、拡張機能の作成者は、UI コンテキストがアクティブ化され、関連付けられている Vspackage が読み込まれる正確な条件を定義できます。 詳細については、「 [方法: 規則ベースの UI コンテキストを Visual Studio 拡張機能に使用する](../extensibility/how-to-use-rule-based-ui-context-for-visual-studio-extensions.md)」を参照してください。  
  
## <a name="troubleshooting-vspackages"></a>VSPackage のトラブルシューティング  
 読み込まれない、またはエラーが発生している Vspackage のトラブルシューティングの手法については、 [vspackage](../extensibility/troubleshooting-vspackages.md)を参照してください。  
  
## <a name="see-also"></a>参照  
 [VSPackages](../extensibility/internals/vspackages.md)
