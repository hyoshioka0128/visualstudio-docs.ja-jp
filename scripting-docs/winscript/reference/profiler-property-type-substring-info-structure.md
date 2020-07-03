---
title: PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 構造体 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3845c872-4302-47b6-8912-7b2d7a3b3357
caps.latest.revision: 4
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 3dd3f1e95436805ccc6e07ca45b5864666e52188
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835395"
---
# <a name="profiler_property_type_substring_info-structure"></a>PROFILER_PROPERTY_TYPE_SUBSTRING_INFO 構造体
リレーションシップで使用される部分文字列の型に関する情報を表します。 [PROFILER_HEAP_OBJECT_RELATIONSHIP 構造体](../../winscript/reference/profiler-heap-object-relationship-structure.md)で使用されます。  
  
## <a name="syntax"></a>構文  
  
```cpp
typedef struct _PROFILER_PROPERTY_TYPE_SUBSTRING_INFO {    UINT length;    LPCWSTR value; } PROFILER_PROPERTY_TYPE_SUBSTRING_INFO;  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|種類|説明|  
|------------|----------|-----------------|  
|length|UINT|オブジェクトは UINT です。|  
|value|LPCWSTR|オブジェクトは LPCWSTR です。|