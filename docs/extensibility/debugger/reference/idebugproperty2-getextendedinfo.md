---
title: プロパティ 2::取得拡張情報 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetExtendedInfo
helpviewer_keywords:
- IDebugProperty2::GetExtendedInfo
ms.assetid: 0c9c0b2b-7540-4424-adb5-fce7aa37a026
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 34d6cd880ccae520bf000ad01b52223857f4f10f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721485"
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
[in]取得する拡張情報の種類を決定する GUID。 詳細については、「解説」を参照してください。

`pExtendedInfo`\
[アウト]拡張プロパティ`VARIANT`情報の取得に使用できる (C++) またはオブジェクト (C#) を返します。 たとえば、このパラメーターは`IUnknown`[、IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)インターフェイスに対してクエリを実行できるインターフェイスを返す場合があります。 詳細については、「解説」を参照してください。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 取得`S_GETEXTENDEDINFO_NO_EXTENDEDINFO`する拡張情報がない場合に返します。

## <a name="remarks"></a>Remarks
 このメソッドは[、GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)メソッドを呼び出すことによって取得されるに適さない情報を取得するために存在します。

 通常、次の GUID は、このメソッドで認識されます (GUID 値は、どのアセンブリでも名前を使用できないので、C# に対して指定されます)。 内部で使用するために追加の GUID を作成できます。

|名前|GUID|説明|
|----------|----------|-----------------|
|guidドキュメント|{3f98de84-fee9-11d0-b47f-00a0244a1dd2}|ドキュメントへの`IUnknown`インターフェイスを返します。 通常、この`IUnknown`インターフェイスから[IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)インターフェイスを取得できます。|
|コードコンテキストを指定します。|{e2fc65e-56ce-11d1-b528-00aax004a8797}|ドキュメント`IUnknown`コンテキストへのインターフェイスを返します。 通常、この`IUnknown`インターフェイスから[IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)インターフェイスを取得できます。|
|カスタムビューアーをサポート|{d9c9da31-ffbe-4eeb-9186-23121e3c088c}|カスタム ビューアーの CLSID を含む文字列を返します。|
|GUID 拡張情報スロット|{6df235ad-82c6-4292-9c97-7389770bc42f}|このプロパティがマネージ コードのローカル アドレスを表す場合は、目的のスロット番号を表す 32 ビットの数値を返します。|
|を使用します。|{b5fb6d46-f805-417f-96a3-8ba737073ffd}|プロパティ オブジェクトに関連付けられた変数のシグネチャを含む文字列を返します。|

## <a name="see-also"></a>関連項目
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
