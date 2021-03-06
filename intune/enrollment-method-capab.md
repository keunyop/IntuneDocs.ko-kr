---
title: Windows 디바이스용 Intune 등록 방법 기능
titleSuffix: Microsoft Intune
description: Windows 디바이스의 각 등록 방법에 따른 기능입니다.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 09/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd1dbb3280fbbb93423796b18f6dd85a50a41f11
ms.sourcegitcommit: 484a898d54f5386fdbce300225aaa3495cecd6b0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/01/2019
ms.locfileid: "59567545"
---
# <a name="intune-enrollment-method-capabilities-for-windows-devices"></a>Windows 디바이스용 Intune 등록 방법 기능
[!INCLUDE[azure_portal](./includes/azure_portal.md)]

Intune에서 작업자의 디바이스를 등록하는 몇 가지 방법이 있습니다. 아래 표에 나와 있는 것처럼 각 방법에는 다른 모범 사례 및 기능이 포함됩니다.

## <a name="best-practices-by-enrollment-method"></a>등록 방법별 모범 사례
| **모범 사례** | **[Azure AD 조인됨](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Autopilot을 사용하여 Azure AD 조인됨(사용자 구동 모드)](enrollment-autopilot.md)** |**[Autopilot을 사용하여 Azure AD 조인됨(셀프 배포 모드)](enrollment-autopilot.md)** |**[대량](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[공동 관리](https://docs.microsoft.com/sccm/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|EDU에 일반적으로 사용됨|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|디바이스를 공유 디바이스로 사용 가능|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|개인 디바이스는 회사 리소스에 액세스해야 함|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|앱의 셀프 서비스|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|

## <a name="capabilities-by-enrollment-method"></a>등록 방법별 기능

| **기능** | **[Azure AD 조인됨](windows-enroll.md#enable-windows-10-automatic-enrollment)**|**[Autopilot을 사용하여 Azure AD 조인됨(사용자 구동 모드)](enrollment-autopilot.md)** |**[Autopilot을 사용하여 Azure AD 조인됨(셀프 배포 모드)](enrollment-autopilot.md)** |**[대량](windows-bulk-enroll.md)**|**[DEM](device-enrollment-manager-enroll.md)** | **[BYOD](device-enrollment.md#bring-your-own-device)** | **[GPO](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy)** | **[공동 관리](https://docs.microsoft.com/sccm/core/clients/manage/co-management-overview)** |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|조건부 액세스                                      |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|디바이스와 연결된 사용자                    |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|Azure AD Premium 필요                               |![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|디바이스는 CA에서 보호되는 리소스를 평가할 수 있음             |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|사용자는 해당 디바이스에서 관리자가 아니어야 함               |![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|디바이스 설치 환경을 구성하는 기능        |![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|
|사용자 개입 없이 디바이스를 등록하는 기능      |![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|PowerShell 스크립트를 실행하는 기능                       |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)| 
|AD 도메인 조인 후 자동 등록 지원      |![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|하이브리드 Azure AD 조인 후 자동 등록 지원|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|
|Azure AD 조인 후 자동 등록 지원       |![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![확인 표시](media/checkmark.png)|![X](media/xmark.png)|![X](media/xmark.png)|

## <a name="next-steps"></a>다음 단계

[Windows에 대한 등록 설정](windows-enroll.md)

