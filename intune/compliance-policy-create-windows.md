---
title: Microsoft Intune의 Windows 10 규정 준수 설정 - Azure | Microsoft Docs
description: Microsoft Intune에서 Windows 10, Windows Holographic 및 Surface Hub 디바이스에 대한 규정 준수를 설정할 때 사용할 수 있는 모든 설정 목록을 참조하세요. 최소 및 최대 운영 체제에 대한 규정 준수 여부, 암호 제한 및 길이 설정, 파트너 AV(바이러스 백신) 솔루션 검사, 데이터 스토리지에 대한 암호화 설정 등을 확인합니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/04/2019
ms.topic: reference
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8d956526d483a74ca5929180a48ea2dcd8b3eab7
ms.sourcegitcommit: 02803863eba37ecf3d8823a7f1cd7c4f8e3bb42c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59423631"
---
# <a name="windows-10-and-later-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Intune을 사용하여 디바이스를 규격 또는 비규격으로 표시하는 Windows 10 이상 설정

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

이 문서에서는 Intune의 Windows 10 이상 디바이스에서 구성할 수 있는 다양한 규정 준수 설정을 나열하고 설명합니다. MDM(모바일 디바이스 관리) 솔루션의 일부로, 이러한 설정을 사용하여 BitLocker를 요구하고, 최소 및 최대 운영 체제를 설정하고, Windows Defender ATP(Advanced Threat Protection)를 사용하여 위험 수준을 설정하는 등의 작업을 수행합니다.

이 기능은 다음에 적용됩니다.

- Windows 10 이상
- Windows Holographic for Business
- Surface Hub

Intune 관리자는 이러한 규정 준수 설정을 통해 조직 리소스를 보호할 수 있습니다. 규정 준수 정책 및 정책 수행에 대한 자세한 내용은 [디바이스 규정 준수 시작](device-compliance-get-started.md)을 참조하세요.

## <a name="before-you-begin"></a>시작하기 전에

[규정 준수 정책 만들기](create-compliance-policy.md#create-the-policy) **플랫폼**에 대해 **Windows 10 이상**을 선택합니다.

## <a name="device-health"></a>Device health

- **BitLocker 필요**: **필요**로 설정하면 디바이스가 꺼져 있거나 최대 절전 모드일 때 드라이브에 저장된 데이터를 무단 액세스로부터 보호할 수 있습니다. Windows BitLocker 드라이브 암호화는 Windows 운영 체제 볼륨에 저장된 모든 데이터를 암호화합니다. BitLocker는 TPM을 사용하여 Windows 운영 체제 및 사용자 데이터 보호를 지원합니다. 따라서 컴퓨터를 방치하거나 분실하거나 도난당하더라도 변조를 방지할 수 있습니다. 컴퓨터에 호환되는 TPM이 장착되어 있으면 BitLocker는 TPM을 사용하여 데이터를 보호하는 암호화 키를 잠급니다. 따라서 TPM에서 컴퓨터의 상태를 확인할 때까지 키에 액세스할 수 없습니다.

  **구성되지 않음**(기본값)으로 설정하면 이 설정은 규격 또는 비규격에 대해 평가되지 않습니다.

- **디바이스에서 보안 부팅을 사용하도록 설정해야 함**: **필요**로 설정하면 시스템이 팩터리 기본 상태로 강제로 부팅됩니다. 활성화되면 머신을 부팅하는 데 사용되는 핵심 구성 요소에는 디바이스를 제조한 조직에서 신뢰할 수 있는 올바른 암호화 서명이 있어야 합니다. UEFI 펌웨어에서 컴퓨터가 시작되도록 허용하기 전에 서명을 확인합니다. 해당 서명을 손상시키는 파일이 손상된 경우 시스템이 부팅되지 않습니다.

  **구성되지 않음**(기본값)으로 설정하면 이 설정은 규격 또는 비규격에 대해 평가되지 않습니다.

  > [!NOTE]
  > **디바이스에서 보안 부팅을 활성화해야 하는** 설정은 일부 TPM 1.2 및 2.0 디바이스에서 지원됩니다. TPM 2.0 이상을 지원하지 않는 디바이스의 경우 Intune의 정책 상태가 **호환되지 않음**으로 표시됩니다. 지원되는 버전에 대한 자세한 내용은 [디바이스 상태 증명](https://docs.microsoft.com/windows/security/information-protection/tpm/trusted-platform-module-overview#device-health-attestation)을 참조하세요.

- **코드 무결성 필요**: 코드 무결성은 메모리에 로드될 때마다 드라이버 또는 시스템 파일의 무결성을 확인하는 기능입니다. **필요**로 설정하면 코드 무결성은 서명되지 않은 드라이버 또는 시스템 파일이 커널로 로드되고 있는지 여부를 검색합니다. 또한 관리자 권한을 가진 사용자 계정으로 실행된 악성 소프트웨어가 시스템 파일을 변경했는지 여부를 검색합니다.

  **구성되지 않음**(기본값)으로 설정하면 이 설정은 규격 또는 비규격에 대해 평가되지 않습니다.

추가 리소스:

- [상태 증명 CSP](https://docs.microsoft.com/windows/client-management/mdm/healthattestation-csp)에는 HAS 서비스의 작동 방식에 대한 세부 정보가 포함되어 있습니다.
- [지원 팁: Intune 규정 준수 정책의 일부로 디바이스 상태 증명 설정 사용](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Using-Device-Health-Attestation-Settings-as-Part-of/ba-p/282643)

## <a name="device-properties"></a>디바이스 속성

- **최소 OS 버전**: 허용되는 최소 버전을 **주 버전.부 버전.빌드.CU 번호** 형식으로 입력합니다. 올바른 값을 얻으려면 명령 프롬프트를 열고 `ver`을 입력합니다. `ver` 명령은 버전을 다음 형식으로 반환합니다.

  `Microsoft Windows [Version 10.0.17134.1]`

  입력하는 OS 버전보다 이전 버전이 디바이스에 있으면 호환되지 않는 것으로 보고됩니다. 업그레이드 방법에 대한 정보를 제공하는 링크가 표시됩니다. 최종 사용자는 디바이스를 업그레이드하도록 선택할 수 있습니다. 업그레이드 후 회사 리소스에 액세스할 수 있습니다.

- **최대 OS 버전**: 허용되는 최대 버전을 **주 버전.부 버전.빌드.수정 번호** 형식으로 입력합니다. 올바른 값을 얻으려면 명령 프롬프트를 열고 `ver`을 입력합니다. `ver` 명령은 버전을 다음 형식으로 반환합니다.

  `Microsoft Windows [Version 10.0.17134.1]`

  디바이스가 입력된 버전보다 최신 OS 버전을 사용하는 경우 조직 리소스에 대한 액세스가 차단됩니다. IT 관리자에게 문의하라는 메시지가 최종 사용자에게 표시됩니다. OS 버전을 허용하도록 규칙이 변경될 때까지 디바이스는 조직 리소스에 액세스할 수 없습니다.

- **모바일 디바이스에 필요한 최소 OS**: 주 버전.부 버전.빌드 번호 형식으로 최소 허용 버전을 입력합니다.

  입력하는 OS 버전보다 이전 버전이 디바이스에 있으면 호환되지 않는 것으로 보고됩니다. 업그레이드 방법에 대한 정보를 제공하는 링크가 표시됩니다. 최종 사용자는 디바이스를 업그레이드하도록 선택할 수 있습니다. 업그레이드 후 회사 리소스에 액세스할 수 있습니다.

- **모바일 디바이스에 필요한 최대 OS**: 주 버전.부 버전.빌드 번호 형식으로 최대 허용 버전을 입력합니다.

  디바이스가 입력된 버전보다 최신 OS 버전을 사용하는 경우 조직 리소스에 대한 액세스가 차단됩니다. IT 관리자에게 문의하라는 메시지가 최종 사용자에게 표시됩니다. OS 버전을 허용하도록 규칙이 변경될 때까지 디바이스는 조직 리소스에 액세스할 수 없습니다.

- **유효한 운영 체제 빌드**: 최소 버전과 최대 버전을 포함하여 허용되는 운영 체제 버전의 범위를 입력합니다. 이러한 허용되는 OS 빌드 번호의 CSV(쉼표로 구분된 값) 파일 목록을 **내보낼** 수도 있습니다.

## <a name="configuration-manager-compliance"></a>Configuration Manager 준수

Windows 10 이상을 실행하는 공동 관리 디바이스에만 적용됩니다. Intune 전용 디바이스는 사용할 수 없음 상태를 반환합니다.

- **System Center Configuration Manager에서 디바이스 규정 준수 필요**: **필요**를 선택하여 System Center Configuration Manager에서 규정을 준수하도록 모든 설정을 강제 적용합니다. 

  예를 들어 모든 소프트웨어 업데이트를 디바이스에 설치해야 합니다. Configuration Manager에서 이 요구 사항의 상태는 “설치됨”입니다. 디바이스의 프로그램이 알 수 없는 상태에 있는 경우 디바이스는 Intune에서 비준수가 됩니다.
  
  **구성되지 않음**인 경우 Intune은 규정 준수에 대한 Configuration Manager 설정을 확인하지 않습니다.

## <a name="system-security"></a>시스템 보안

### <a name="password"></a>암호

- **모바일 디바이스의 잠금을 해제하는 데 암호 필요**: **필요**로 설정하면 사용자가 암호를 입력해야 디바이스에 액세스할 수 있습니다.
- **단순 암호**: **차단**으로 설정하면 사용자가 **1234** 또는 **1111** 같은 단순 암호를 만들 수 없습니다. **구성되지 않음**으로 설정하면 사용자가 **1234** 또는 **1111** 같은 암호를 만들 수 있습니다.
- **암호 유형**: 암호에 **숫자**만 사용해야 하는지 또는 숫자와 기타 문자(**영숫자**)를 함께 사용해야 하는지 선택합니다.

  - **암호에 포함해야 하는 영숫자가 아닌 문자 수**: **필수 암호 유형**이 **영숫자**로 설정된 경우 이 설정은 암호에 포함해야 하는 최소 문자 집합 수를 지정합니다. 4가지 문자 집합은 다음과 같습니다.
    - 소문자
    - 대문자
    - 기호
    - 숫자

    더 큰 값을 설정하면 사용자는 더욱 복잡한 암호를 만들어야 합니다.

- **최소 암호 길이**: 암호에 포함해야 하는 최소 자릿수 또는 문자 수를 입력합니다.
- **암호를 요구하기 전까지 최대 비활성 시간(분)**: 사용자가 해당 시간 내에 자신의 암호를 다시 입력해야 하는 유휴 시간을 입력합니다.
- **암호 만료(일)**: 암호가 만료되기 전에 새로 만들어야 하는 일수를 선택합니다.
- **재사용을 방지하기 위한 이전 암호 수**: 사용할 수 없는 이전에 사용된 암호 수를 입력합니다.
- **디바이스가 유휴 상태에서 되돌아올 때 암호 요구(Mobile 및 Holographic)**: 디바이스가 유휴 상태에서 돌아올 때마다 사용자가 암호를 입력해야 합니다.

### <a name="encryption"></a>암호화

- **장치의 데이터 스토리지 암호화**: **필요**를 선택하면 장치의 데이터 스토리지가 암호화됩니다.

  > [!NOTE]
  > **장치에서 데이터 스토리지 암호화** 설정은 일반적으로 장치가 암호화되었는지 확인합니다. 보다 강력한 암호화 설정을 위해 **BitLocker 필요**를 사용하는 것이 좋습니다. 그러면 Windows 디바이스 상태 증명을 활용하여 TPM 수준에서 Bitlocker 상태의 유효성을 검사합니다.

### <a name="device-security"></a>디바이스 보안

- **바이러스 백신**: **필수**로 설정하면 Symantec 및 Windows Defender와 같은 [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/)에 등록된 바이러스 백신 솔루션을 사용하여 규정 준수를 확인할 수 있습니다. **구성되지 않은** 경우 Intune은 디바이스에 설치된 모든 AV 솔루션을 확인하지 않습니다.
- **스파이웨어 방지**: **필수**로 설정하면 Symantec 및 Windows Defender와 같은 [Windows Security Center](https://blogs.windows.com/windowsexperience/2017/01/23/introducing-windows-defender-security-center/)에 등록된 스파이웨어 방지 솔루션을 사용하여 규정 준수를 확인할 수 있습니다. **구성되지 않은** 경우 Intune은 디바이스에 설치된 스파이웨어 방지 솔루션을 확인하지 않습니다.

## <a name="windows-defender-atp"></a>Windows Defender ATP

- **디바이스가 머신 위험 점수나 그 아래에 있어야 함**: 이 설정을 사용하여 위협 방지 서비스에서 준수 조건에 따라 위험 평가를 수행할 수 있습니다. 허용된 최대 위협 수준을 선택합니다.

  - **지우기**: 디바이스에 어떤 위협도 없으므로 이 옵션이 가장 안전합니다. 수준에 관계없이 위협이 발견된 디바이스는 비규격으로 평가됩니다.
  - **낮음**: 낮은 수준의 위협만 있는 경우 디바이스가 규정 준수로 평가됩니다. 더 높은 수준의 위협이 확인되는 디바이스는 비규격 상태로 설정됩니다.
  - **보통**: 디바이스의 기존 위협이 낮음 또는 보통 수준인 경우 디바이스가 규격으로 평가됩니다. 디바이스에 높은 수준의 위협이 있는 것으로 검색되면 비규격으로 결정됩니다.
  - **높음**: 이 옵션은 최소 보안이며 모든 위협 수준을 허용합니다. 이 수준은 이 솔루션을 보고 용도로만 사용하는 경우에 유용할 수 있습니다.
  
  방어 위협 서비스로 Windows Defender ATP(Advanced Threat Protection)를 설정하려면[조건부 액세스로 Windows Defender ATP 사용](advanced-threat-protection.md)을 참조하세요.

**확인** > **만들기**를 선택하여 변경 내용을 저장합니다.

## <a name="windows-holographic-for-business"></a>Windows Holographic for Business

Windows Holographic for Business는 **Windows 10 이상** 플랫폼을 사용합니다. Windows Holographic for Business는 다음과 같은 설정을 지원합니다.

- **시스템 보안** > **암호화** > **디바이스의 데이터 스토리지 암호화**.

Microsoft HoloLens에서 디바이스 암호화를 확인하려면 [디바이스 암호화 확인](https://docs.microsoft.com/hololens/hololens-encryption#verify-device-encryption)을 참조하세요.

## <a name="surface-hub"></a>Surface Hub

Surface Hub는 **Windows 10 이상** 플랫폼을 사용합니다. Surface Hub는 준수 및 조건부 액세스 둘 다에서 지원됩니다. Surface Hub에서 이러한 기능을 사용하려면 Intune에서 [Windows 10 자동 등록을 사용하도록 설정](windows-enroll.md)하고(Azure AD(Azure Active Directory) 필요), 디바이스 그룹으로 Surface Hub 디바이스를 대상으로 지정하는 것이 좋습니다. 규정 준수 및 조건부 액세스가 작동하려면 Surface Hub가 Azure AD에 연결되어야 합니다.

지침은 [Windows 디바이스에 대한 등록 설정](windows-enroll.md)을 참조하세요.

## <a name="next-steps"></a>다음 단계

- [비규격 디바이스에 대한 작업 추가](actions-for-noncompliance.md) 및 [범위 태그를 사용하여 정책 필터링](scope-tags.md).
- [규정 준수 정책 모니터링](compliance-policy-monitor.md).
- [Windows 8.1용 규정 준수 정책 설정](compliance-policy-create-windows-8-1.md) 디바이스를 참조하세요.