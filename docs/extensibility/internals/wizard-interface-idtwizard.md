---
title: Wizard インターフェイス (IDTWizard) |Microsoft Docs
description: IDE では、IDTWizard インターフェイスを使用してウィザードと通信します。 ウィザードは、IDE にインストールするために、このインターフェイスを実装する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b8dc88341bc72755ae0f5011d18182c5b78bb483
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074198"
---
# <a name="wizard-interface-idtwizard"></a>ウィザード インターフェイス (IDTWizard)
統合開発環境 (IDE: integrated development environment) は、インターフェイスを使用し <xref:EnvDTE.IDTWizard> てウィザードと通信します。 ウィザードは、IDE にインストールするために、このインターフェイスを実装する必要があります。

 メソッドは、 <xref:EnvDTE.IDTWizard.Execute%2A> インターフェイスに関連付けられている唯一のメソッドです <xref:EnvDTE.IDTWizard> 。 ウィザードはこのメソッドを実装し、IDE はインターフェイスに対してメソッドを呼び出します。 次の例は、メソッドのシグネチャを示しています。

```
/* IDTWizard Method */
STDMETHOD(Execute)(THIS_
   /* [in] */ IDispatch *Application,
   /* [in] */ long hwndOwner,
   /* [in] */ SAFEARRAY * *ContextParams,
   /* [in] */ SAFEARRAY * *CustomParams,
   /* [out] [in] */ wizardResult *RetVal
   );
```

 開始メカニズムは、 **新しいプロジェクト** と **新しい項目の追加** ウィザードの両方で似ています。 どちらかを開始するには、 <xref:EnvDTE.IDTWizard> Dteinternal. h で定義されているインターフェイスを呼び出します。 唯一の違いは、インターフェイスが呼び出されたときにインターフェイスに渡されるコンテキストとカスタムパラメーターのセットです。

 ここでは、 <xref:EnvDTE.IDTWizard> IDE で動作するためにウィザードで実装する必要があるインターフェイスについて説明し [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 IDE は、 <xref:EnvDTE.IDTWizard.Execute%2A> ウィザードでメソッドを呼び出し、次のように渡します。

- DTE オブジェクト

     DTE オブジェクトは、オートメーションモデルのルートです。

- コードセグメントに示されているように、ウィンドウダイアログボックスを表示するハンドル `hwndOwner ([in] long)` 。

     ウィザードでは、これを `hwndOwner` ウィザードダイアログボックスの親として使用します。

- コードセグメントに示されているように、SAFEARRAY のバリアントとしてインターフェイスに渡されるコンテキストパラメーター `[in] SAFEARRAY (VARIANT)* ContextParams` 。

     コンテキストパラメーターには、開始するウィザードの種類とプロジェクトの現在の状態に固有の値の配列が含まれます。 IDE は、コンテキストパラメーターをウィザードに渡します。 詳細については、「 [コンテキストパラメーター](../../extensibility/internals/context-parameters.md)」を参照してください。

- コードセグメントに示されているように、SAFEARRAY のバリアントとしてインターフェイスに渡されるカスタムパラメーター `[in] SAFEARRAY (VARIANT)* CustomParams` 。

     カスタムパラメーターには、ユーザー定義パラメーターの配列が含まれています。 .Vsz ファイルは、IDE にカスタムパラメーターを渡します。 値は、ステートメントによって決定され `Param=` ます。 詳細については、「 [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)」を参照してください。

- インターフェイスの戻り値は、

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>こちらもご覧ください
- [コンテキストパラメーター](../../extensibility/internals/context-parameters.md)
- [カスタムパラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
