---
title: Microsoft Intune-Azure와 디바이스 동기화 | Micrososft Docs
description: Microsoft Intune으로 등록되거나 관리되는 디바이스를 동기화하여 최신 정책과 작업을 가져옵니다. Azure Portal을 사용하여 동기화하는 단계를 포함하고 다시 시도할 수 있는 오류 코드를 나열합니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f13e00abad5b48dcd7996cf9df1cc5756f250d3
ms.sourcegitcommit: 25e6aa3bfce58ce8d9f8c054bc338cc3dff4a78b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57388109"
---
# <a name="sync-devices-to-get-the-latest-policies-and-actions-with-intune"></a>디바이스를 동기화하여 Intune에서 최신 정책과 작업 가져오기


[!INCLUDE [azure_portal](./includes/azure_portal.md)]

디바이스 **동기화** 작업은 선택한 디바이스가 Intune을 사용하여 즉시 체크 인하도록 강제합니다. 디바이스가 체크 인하면 디바이스에 할당된 보류 중인 작업 또는 정책을 즉시 받게 됩니다. 이 기능을 통해 예약된 다음 체크 인을 기다리지 않고 즉시 할당한 정책의 유효성을 검사하고 문제를 해결할 수 있습니다.

## <a name="supported-platforms"></a>지원되는 플랫폼

- Windows
- Windows Phone
- iOS
- macOS
- Android

## <a name="sync-a-device"></a>디바이스 동기화

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에 필터링한 다음, **Microsoft Intune**을 선택합니다. 
3. **Intune**에서 **디바이스** > **모든 디바이스**를 선택합니다.
4. 관리하는 디바이스 목록에서 디바이스를 선택하고 **자세히**를 선택한 다음, **동기화**를 선택합니다.
5. 확인하려면 **예**를 선택합니다.

동기화 작업의 상태를 확인하려면 **디바이스** > **디바이스 작업**을 선택합니다.

[주기 시간 새로 고침](device-profiles.md)에서 표준 Intune 정책 체크 인 빈도를 찾을 수 있습니다.

## <a name="retryable-error-codes"></a>다시 시도 가능 오류 코드

관리자가 **동기화** 디바이스 작업을 실행하는 경우 실패하고 다시 시도 가능 오류 코드가 발생한 iOS 및 Android 앱이 디바이스에 제공됩니다. 그러나 다시 시도 가능이 아닌 오류 코드가 발생한 앱은 디바이스에서 제공되기 전에 7일 동안 기다려야 합니다.


| 오류 코드  | 제안되는 설명 | 다시 시도 가능 |
|---|---|---|
| 2016330898 | 알 수 없는 오류가 발생했습니다. | 아니요 |
| 2016330897 | Intune 연결 시간이 초과되었습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330896 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330895 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330894 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예 |
| 2016330893 | 인터넷 연결이 끊어졌습니다. 연결을 다시 설정하십시오. | 예|
| 2016330892 | 국제 로밍을 사용하지 않습니다. | 아니요|
| 2016330891 | 전화 통화 중에는 이 디바이스의 셀룰러 데이터 연결에 액세스할 수 없습니다. 전화 통화가 완료될 때까지 기다리십시오. | 예|
| 2016330890 | 이 디바이스의 셀룰러 네트워크입니다. 이러한 디바이스는 이 시간에 사용하지 못했습니다. | 아니요|
| 2016330889 | 보안 연결에 실패했습니다. 연결을 다시 설정하십시오. | 예|
| 2016330888 | 서버 신뢰 평가에 실패했습니다. | 아니요|

## <a name="next-steps"></a>다음 단계

디바이스의 [세부 정보를 확인](device-inventory.md)할 수 있습니다.
 
