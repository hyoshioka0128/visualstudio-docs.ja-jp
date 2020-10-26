---
title: Vspackage | を登録していますMicrosoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- managed VSPackages, registering
- registration, managed VSPackages
ms.assetid: 79b9424e-7e9b-4fc8-9b9f-00212674573c
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 053157b0ce1cb4250d8c666725431515c75b5fa2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157384"
---
# <a name="registering-vspackages"></a>VSPackage の登録
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は、VSPackage を記述および検索するために、pkgdef ファイルに依存しています。 Pkgdef ファイルには、システムレジストリに追加されるすべての登録情報が含まれています。 マネージ Vspackage は、ソースコードに属性を追加し、結果のアセンブリで [Createpkgdef ユーティリティ](../../extensibility/internals/createpkgdef-utility.md) を実行して、pkgdef ファイルを生成することによって登録されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [VSPackage ファイルの場所を VS Shell に指定する](../../extensibility/internals/specifying-vspackage-file-location-to-the-vs-shell.md)  
 Vspackage の読み込みパスについて説明します。  
  
 [VSPackage の登録と登録解除](../../extensibility/registering-and-unregistering-vspackages.md)  
 VSPackage を登録する方法について説明します。  
  
 [カスタム登録属性を使用した拡張機能の登録](../../misc/using-a-custom-registration-attribute-to-register-an-extension.md)  
 マネージ VSPackage のデプロイに使用できる登録マニフェストを作成する方法について説明します。
