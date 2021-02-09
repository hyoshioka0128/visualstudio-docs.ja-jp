---
title: 'IDebugProperty2:: GetExtendedInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1bb9fe21b1dc004d5a124a1146e6f7610fbe8699
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99916060"
---
# <a name="idebugproperty2getextendedinfo"></a>IDebugProperty2::GetExtendedInfo
プロパティの拡張情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetExtendedInfo ( 
   REFGUID* guidExtendedInfo,
   VARIANT* pExtendedInfo
);
```

```csharp
int GetExtendedInfo ( 
   ref Guid guidExtendedInfo,
   out object pExtendedInfo
);
```

## <a name="parameters"></a>パラメーター
`guidExtendedInfo`\
から取得する拡張情報の種類を決定する GUID。 詳細については、「解説」を参照してください。

`pExtendedInfo`\
入出力 `VARIANT` 拡張プロパティ情報を取得するために使用できる (C++) またはオブジェクト (C#) を返します。 たとえば、このパラメーターは、 `IUnknown` [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) インターフェイスに対してクエリを実行できるインターフェイスを返す場合があります。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は、を返します。それ以外の場合は `S_OK` エラーコードを返します。 `S_GETEXTENDEDINFO_NO_EXTENDEDINFO`取得する拡張情報がない場合は、を返します。

## <a name="remarks"></a>解説
 このメソッドは、 [GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md) メソッドを呼び出すことによって取得されない情報を取得する目的で存在します。

 通常、次の Guid はこのメソッドによって認識されます (アセンブリでは名前が使用できないため、GUID 値は C# に対して指定されています)。 内部使用のために、追加の Guid を作成できます。

|名前|GUID|説明|
|----------|----------|-----------------|
|guidDocument|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|`IUnknown`ドキュメントへのインターフェイスを返します。 通常、このインターフェイスから [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md) インターフェイスを取得でき `IUnknown` ます。|
|guidCodeContext|{e2fc65e-56ce-11d1-b528-00aax004a8797}|`IUnknown`ドキュメントコンテキストへのインターフェイスを返します。 通常、このインターフェイスから [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスを取得でき `IUnknown` ます。|
|Guidcustomビューアサポート|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|カスタムビューアーの CLSID を含む文字列を返します。通常は、式エバリュエーターによって実装されます。|
|ガイド Xtenantdedinfoslot|{6df235ad-82c6-4292-9c97-7389770bc42f}|このプロパティがマネージコードローカルアドレスを表す場合は、目的のスロット番号を表す32ビットの値を返します。|
|ガイド Xtenantdedinfosignature|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|プロパティオブジェクトに関連付けられている変数のシグネチャを格納している文字列を返します。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
