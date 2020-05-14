---
title: 逆アセンブリデータ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9dcf3316ba57bbb25ee171cba7e4edc4923fa270
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737284"
---
# <a name="disassemblydata"></a>DisassemblyData
統合開発環境 (IDE) で表示する 1 つの逆アセンブリ命令について説明します。

## <a name="syntax"></a>構文

```cpp
typedef struct tagDisassemblyData {
    DISASSEMBLY_STREAM_FIELDS dwFields;
    BSTR                      bstrAddress;
    BSTR                      bstrAddressOffset;
    BSTR                      bstrCodeBytes;
    BSTR                      bstrOpcode;
    BSTR                      bstrOperands;
    BSTR                      bstrSymbol;
    UINT64                    uCodeLocationId;
    TEXT_POSITION             posBeg;
    TEXT_POSITION             posEnd;
    BSTR                      bstrDocumentUrl;
    DWORD                     dwByteOffset;
    DISASSEMBLY_FLAGS         dwFlags;
} DisassemblyData;
```

```csharp
public struct DisassemblyData { 
    public uint          dwFields;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrCodeBytes;
    public string        bstrOpcode;
    public string        bstrOperands;
    public string        bstrSymbol;
    public ulong         uCodeLocationId;
    public TEXT_POSITION posBeg;
    public TEXT_POSITION posEnd;
    public string        bstrDocumentUrl;
    public uint          dwByteOffset;
    public uint          dwFlags;
};
```

## <a name="members"></a>メンバー
`dwFields`\
入力するフィールドを指定する[DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)定数。

`bstrAddress`\
開始点 (通常は関連付けられた関数の先頭) からのオフセットとしてのアドレス。

`bstrCodeBytes`\
この命令のコードバイト。

`bstrOpcode`\
この命令のオペコード。

`bstrOperands`\
この命令のオペランド。

`bstrSymbol`\
アドレス (パブリック シンボル、ラベルなど) に関連付けられているシンボル名 (存在する場合)。

`uCodeLocationId`\
この逆アセンブルされた行のコードの場所の識別子。 ある行のコード コンテキスト アドレスが別のコード コンテキスト アドレスよりも大きい場合、最初のコードの逆アセンブルされた場所識別子も、2 番目のコードの場所識別子よりも大きくなります。

`posBeg`\
逆アセンブリ データが開始されるドキュメント内の位置に対応する[TEXT_POSITION。](../../../extensibility/debugger/reference/text-position.md)

`posEnd`\
分解データが終了するドキュメント内の位置に対応する[TEXT_POSITION。](../../../extensibility/debugger/reference/text-position.md)

`bstrDocumentUrl`\
ファイル名として表すことができるテキスト ドキュメントの`bstrDocumentUrl`場合、フィールドには、 形式`file://file name`を使用してソースが見つかるファイル名がフィールドに入力されます。

ファイル名として表現できないテキスト ドキュメントの場合は`bstrDocumentUrl`、ドキュメントの一意の識別子であり、デバッグ エンジンは[、GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)メソッドを実装する必要があります。

このフィールドには、チェックサムに関する追加情報を含めることもできます。 詳細については、「解説」を参照してください。

`dwByteOffset`\
命令がコード行の先頭からのバイト数です。

`dwFlags`\
アクティブなフラグを指定する[DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)定数。

## <a name="remarks"></a>Remarks
各`DisassemblyData`構造体は、分解の 1 つの命令を記述します。 これらの構造体の配列は[、Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)メソッドから返されます。

[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)構造は、テキストベースの文書にのみ使用されます。 この命令のソース コード範囲は、ステートメントまたは行から生成された最初の命令に対してのみ入力`dwByteOffset == 0`されます 。

非テキストドキュメントの場合、ドキュメント コンテキストはコードから取得でき、`bstrDocumentUrl`フィールドは null 値にする必要があります。 フィールドが`bstrDocumentUrl`前`bstrDocumentUrl``DisassemblyData`の配列要素のフィールドと同じである場合は、 を`bstrDocumentUrl`null 値に設定します。

フィールドに`dwFlags`フラグが設定`DF_DOCUMENT_CHECKSUM`されている場合は、フィールドが指す文字列の後に追加のチェックサム`bstrDocumentUrl`情報が続きます。 具体的には、null 文字列ターミネータの後に、チェックサム アルゴリズムを識別する GUID の後に、チェックサムのバイト数を示す 4 バイト値が続き、その後にチェックサム バイトが続きます。 このフィールドをエンコードおよびデコードする方法については、このトピックの例[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]を参照してください。

## <a name="example"></a>例
フラグ`bstrDocumentUrl`が設定されている場合、フィールドには文字列以外の追加情報`DF_DOCUMENT_CHECKSUM`を含めることができます。 このエンコードされた文字列を作成して読み取るプロセスは[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]、 で簡単です。 しかし、[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]では、それは別の問題です。 興味のある人のために、次の例は、 から[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]エンコードされた文字列を作成する方法と、 で[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]エンコードされた文字列をデコードする 1 つの方法を示しています。

```csharp
using System;
using System.Runtime.InteropServices;

namespace MyNamespace
{
    class MyClass
    {
        string EncodeData(string documentString,
                          Guid checksumGuid,
                          byte[] checksumData)
        {
            string returnString = documentString;

            if (checksumGuid == null || checksumData == null)
            {
                // Nothing more to do. Just return the string.
                return returnString;
            }

            returnString += '\0'; // separating null value

            // Add checksum GUID to string.
            byte[] guidDataArray  = checksumGuid.ToByteArray();
            int    guidDataLength = guidDataArray.Length;
            IntPtr pBuffer        = Marshal.AllocCoTaskMem(guidDataLength);
            for (int i = 0; i < guidDataLength; i++)
            {
                Marshal.WriteByte(pBuffer, i, guidDataArray[i]);
            }
            // Copy guid data bytes to string as wide characters.
            // Assumption: sizeof(char) == 2.
            for (int i = 0; i < guidDataLength / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum count (a 32-bit value).
            Int32 checksumCount = checksumData.Length;
            Marshal.StructureToPtr(checksumCount, pBuffer, true);
            for (int i = 0; i < sizeof(Int32) / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum data.
            pBuffer = Marshal.AllocCoTaskMem(checksumCount);
            for (int i = 0; i < checksumCount; i++)
            {
                Marshal.WriteByte(pBuffer, i, checksumData[i]);
            }
            for (int i = 0; i < checksumCount / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }
            Marshal.FreeCoTaskMem(pBuffer);

            return returnString;
        }

        void DecodeData(    string encodedString,
                        out string documentString,
                        out Guid   checksumGuid,
                        out byte[] checksumData)
        {
            documentString = String.Empty;
            checksumGuid = Guid.Empty;
            checksumData = null;

            IntPtr pBuffer = Marshal.StringToBSTR(encodedString);
            if (null != pBuffer)
            {
                int bufferOffset = 0;

                // Parse string out. String is assumed to be Unicode.
                documentString = Marshal.PtrToStringUni(pBuffer);
                bufferOffset += (documentString.Length + 1) * sizeof(char);

                // Parse Guid out.
                // Read guid bytes from buffer and store in temporary
                // buffer that contains only the guid bytes. Then the
                // Marshal.PtrToStructure() can work properly.
                byte[] guidDataArray  = checksumGuid.ToByteArray();
                int    guidDataLength = guidDataArray.Length;
                IntPtr pGuidBuffer    = Marshal.AllocCoTaskMem(guidDataLength);
                for (int i = 0; i < guidDataLength; i++)
                {
                    Marshal.WriteByte(pGuidBuffer, i,
                                      Marshal.ReadByte(pBuffer, bufferOffset + i));
                }
                bufferOffset += guidDataLength;
                checksumGuid = (Guid)Marshal.PtrToStructure(pGuidBuffer, typeof(Guid));
                Marshal.FreeCoTaskMem(pGuidBuffer);

                // Parse out the number of checksum data bytes (always 32-bit value).
                int dataCount = Marshal.ReadInt32(pBuffer, bufferOffset);
                bufferOffset += sizeof(Int32);

                // Parse out the checksum data.
                checksumData = new byte[dataCount];
                for (int i = 0; i < dataCount; i++)
                {
                    checksumData[i] = Marshal.ReadByte(pBuffer, bufferOffset + i);
                }
            }
        }
    }
}
```

## <a name="see-also"></a>関連項目
- [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)
- [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
