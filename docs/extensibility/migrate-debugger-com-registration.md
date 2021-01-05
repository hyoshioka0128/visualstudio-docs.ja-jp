---
title: 64ビットデバッガー COM クラス登録の移行 |Microsoft Docs
description: HKEY_CLASSES_ROOT に書き込むことなくデバッガー拡張のために COM クラスを msvsmon に登録する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/10/2016
ms.topic: conceptual
ms.assetid: 45cfcee6-7a68-4d4f-b3f6-e2d8a0fa066a
author: gregg-miskelly
ms.author: greggm
manager: jillfra
ms.workload:
- greggm
ms.openlocfilehash: 6f28f8eb2935ed2dd8a848ccc3151b9f438fc437
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/04/2021
ms.locfileid: "97862888"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>64ビットデバッガーの COM クラス登録の移行

Regasm、regsvr32、またはレジストリへの直接書き込みを使用して HKEY_CLASSES_ROOT に COM クラスを登録し、 *msvsmon.exe* (リモートデバッガー) に読み込むデバッガー拡張機能の場合、HKEY_CLASSES_ROOT に書き込むことなく、msvsmon にこの登録を行うことができるようになりました。 これは、 *msvsmon.exe* プロセスに読み込むように構成されているレガシ .net デバッガー式エバリュエーターまたはデバッグエンジンに影響します。

## <a name="msvsmon-comclass-def"></a>msvsmon-comclass-def

この手法を使用するには、msvsmon (InstallDir: \Common7\IDE\Remote Debugger\x64 *) の横にある *ファイル *に.msvsmon-comclass-def.js** を追加します。

次に、1つのマネージクラスと1つのネイティブクラスを登録する msvsmon クラス def ファイルの例を示します。

ファイル名: *MyCompany.MyExample.msvsmon-comclass-def.js*

```json
{
  "managedCOMClasses": [
    {
      "clsid": "{C9F48B25-36ED-4B22-8210-98BC5BE4D1E7}",
      "assemblyName": "MyCompany.MyAssembly",
      "className": "MyCompany.MyNamespace.MyClass"
    }
  ],
  "nativeCOMClasses": [
    {
      "clsid": "{42A476E9-8FA7-44D5-ADFE-216AD371EEC9}",
      "dllPath": "MyExample.dll"
    }
  ]
}
```
