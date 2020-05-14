---
title: ウィザード インターフェイス (IDTWizard) |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb1c8d728a76097321e4e1f16640cab97599d6ba
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703274"
---
# <a name="wizard-interface-idtwizard"></a>ウィザード インターフェイス (IDTWizard)
統合開発環境 (IDE) は、<xref:EnvDTE.IDTWizard>ウィザードとの通信にインターフェイスを使用します。 ウィザードは、IDE にインストールするためにこのインターフェイスを実装する必要があります。

 <xref:EnvDTE.IDTWizard.Execute%2A>このメソッドは、インターフェイスに関連付けられている<xref:EnvDTE.IDTWizard>唯一のメソッドです。 ウィザードはこのメソッドを実装し、IDE はインターフェイスでメソッドを呼び出します。 メソッドのシグネチャを次の例に示します。

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

 開始メカニズムは、**新しいプロジェクト**ウィザードと**新しい項目の追加**ウィザードの両方で似ています。 開始するには、Dteinternal.h で定義された<xref:EnvDTE.IDTWizard>インターフェイスを呼び出します。 唯一の違いは、インターフェイスが呼び出されたときにインターフェイスに渡されるコンテキストとカスタム パラメータのセットです。

 以下の情報は、ウィザード<xref:EnvDTE.IDTWizard>が IDE で動作するために実装する必要[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]があるインターフェイスについて説明します。 IDE は、<xref:EnvDTE.IDTWizard.Execute%2A>ウィザードでメソッドを呼び出し、次のメソッドを渡します。

- DTE オブジェクト

     DTE オブジェクトは、オートメーション モデルのルートです。

- コード セグメントに示すように、ウィンドウ ダイアログ ボックスのハンドル`hwndOwner ([in] long)`。

     ウィザードでは、ウィザード`hwndOwner`ダイアログ ボックスの親としてこれを使用します。

- コード セグメントに示すように、SAFEARRAY のバリアントとしてインターフェイスに渡されるコンテキスト`[in] SAFEARRAY (VARIANT)* ContextParams`パラメータです。

     コンテキスト パラメーターには、開始するウィザードの種類とプロジェクトの現在の状態に固有の値の配列が含まれます。 IDE は、コンテキストパラメータをウィザードに渡します。 詳細については、「コンテキスト[パラメータ](../../extensibility/internals/context-parameters.md)」を参照してください。

- コード セグメントに示すように、SAFEARRAY のバリアントとしてインターフェイスに渡されるカスタム`[in] SAFEARRAY (VARIANT)* CustomParams`パラメータです。

     カスタム パラメータには、ユーザー定義パラメータの配列が含まれます。 vsz ファイルは、IDE にカスタム パラメータを渡します。 値はステートメントによって`Param=`決定されます。 詳細については、「[カスタム パラメータ](../../extensibility/internals/custom-parameters.md)」を参照してください。

- インターフェイスの戻り値は次のとおりです。

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>関連項目
- [コンテキスト パラメーター](../../extensibility/internals/context-parameters.md)
- [カスタム パラメーター](../../extensibility/internals/custom-parameters.md)
- [ウィザード](../../extensibility/internals/wizards.md)
- [ウィザード (.Vsz) ファイル](../../extensibility/internals/wizard-dot-vsz-file.md)
