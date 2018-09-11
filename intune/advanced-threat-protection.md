---
title: Microsoft Intune에서 Windows Defender ATP 사용 - Azure | Microsoft Docs
description: Intune 및 Windows Defender 보안 센터(ATP 포털)에서 ATP 켜기 등 종단 간 시나리오에서 Windows Defender ATP(Advanced Threat Protection)를 사용하도록 설정하고, ATP 구성 프로필을 사용하여 장치를 등록하고, Intune 장치 준수 정책을 만들고, Azure AD 조건부 액세스 정책을 만들고, 장치 준수를 모니터링하는 방법을 확인합니다.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 5/23/2018
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.technology: ''
ms.reviewer: joglocke
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: d43e95b2f236dc4c03bb3f63670b2b1400243531
ms.sourcegitcommit: 0303e3b8c510f56e191e6079e3dcdccfc841f530
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40251497"
---
# <a name="enable-windows-defender-atp-with-conditional-access-in-intune"></a>Intune에서 조건부 액세스로 Windows Defender ATP 사용

Windows Defender ATP(Advanced Threat Protection) 및 Microsoft Intune은 함께 작동하여 보안 위반을 방지하고 조직 내에서 위반 영향을 제한합니다.

이 기능은 Windows 10 장치에 적용됩니다.

예를 들어 누군가가 포함된 악성 코드가 있는 Word 첨부 파일을 조직 내의 사용자에게 전송합니다. 사용자가 첨부 파일을 열고 콘텐츠를 활성화합니다. 상승된 권한 공격이 시작되고, 원격 컴퓨터의 공격자가 공격 대상 장치에 대한 관리자 권한을 갖게 됩니다. 그런 다음, 공격자가 사용자의 다른 장치에 원격으로 액세스합니다.

이 보안 위반은 전체 조직에 영향을 미칠 수 있습니다.

Windows Defender ATP는 이 시나리오와 같은 보안 이벤트를 해결할 수 있습니다. Windows Defender 보안 센터(ATP 콘솔)는 장치를 “높은 위험”으로 보고하고 의심스러운 활동의 자세한 보고서를 포함합니다. 이 예제에서 Windows Defender ATP는 장치에서 비정상적인 코드가 실행되었으며, 프로세스 권한 에스컬레이션이 발생하고 악성 코드가 삽입되고 의심스러운 원격 셸이 실행되었음을 감지합니다. 그런 다음, Windows Defender ATP는 위협을 완화하는 옵션을 제공합니다.

Intune을 사용하여 허용되는 위험 수준을 결정하는 준수 정책을 만들 수 있습니다. 장치가 이 위험을 초과하면 비규격 상태가 됩니다. Azure AD(Active Directory) 조건부 액세스와 결합할 경우 회사 리소스에 대한 사용자 액세스가 차단됩니다.

이 문서에서는 다음 방법을 보여 줍니다.

- ATP에서 Intune을 사용하도록 설정하고, Intune에서 ATP를 사용하도록 설정합니다. 이러한 작업은 Intune과 Windows Defender ATP 간에 서비스-서비스 연결을 만듭니다. 이 연결을 통해 Windows Defender ATP에서 Intune 장치에 대한 컴퓨터 위험을 작성할 수 있습니다.
- Intune에서 준수 정책을 만듭니다.
- 위협 수준에 따라 장치의 Azure AD(Active Directory)에서 조건부 액세스를 사용하도록 설정합니다.

## <a name="prerequisites"></a>전제 조건

Intune에서 ATP를 사용하려면 다음을 구성했으며 사용할 준비가 되었는지 확인합니다.

- Enterprise Mobility + Security E3 및 Windows E5(또는 Microsoft 365 Enterprise E5)에 대한 라이선스가 부여된 테넌트
- Azure AD에 연결된 [Intune 관리](windows-enroll.md) Windows 10 장치가 포함된 Microsoft Intune 환경
- [Windows Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection) 및 Windows Defender 보안 센터(ATP 포털)에 대한 액세스 권한

## <a name="enable-windows-defender-atp-in-intune"></a>Intune에서 Windows Defender ATP 사용

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링하고 **Microsoft Intune**을 선택합니다.
3. **장치 준수** > **Windows Defender ATP** > **Windows Defender 보안 센터 열기**를 차례로 선택합니다.

    ![Windows Defender 보안 센터 열기 선택](./media/atp-device-compliance-open-windows-defender.png)

4. **Windows Defender 보안 센터**에서 다음을 수행합니다.
    1. **설정** > **고급 기능**을 선택합니다.
    2. **Microsoft Intune 연결**에서 **켜기**를 선택합니다.

        ![Intune에 대한 연결을 사용하도록 설정](./media/atp-security-center-intune-toggle.png)

    3. **기본 설정 저장**을 선택합니다.

5. Intune, **장치 준수** > **Windows Defender ATP**로 돌아갑니다. **Windows 장치 버전 10.0.15063 이상을 Windows Defender ATP에 연결**을 **켜기**로 설정합니다.
6. **저장**을 선택합니다.

일반적으로 이 작업은 한 번 수행합니다. 따라서 Intune 리소스에서 이미 ATP를 사용하도록 설정한 경우에는 다시 이 작업을 수행하지 않아도 됩니다.

## <a name="onboard-devices-using-a-configuration-profile"></a>구성 프로필을 사용하여 장치 등록

Windows Defender에는 장치에 설치되는 온보드 구성 패키지가 포함되어 있습니다. 설치된 경우 패키지는 [Windows Defender ATP 서비스](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/windows-defender-advanced-threat-protection)와 통신하여 파일을 검색하고, 위협을 감지하며, Windows Defender ATP에 위험을 보고합니다. Intune을 통해 이 구성 패키지를 사용하는 구성 프로필을 만들 수 있습니다. 그런 다음, 처음 등록하는 장치에 이 프로필을 할당합니다.

구성 패키지를 사용하여 장치를 등록하고 나면 다시 등록할 필요가 없습니다. 일반적으로 일회성 작업입니다.

[그룹 정책 또는 SCCM(System Center Configuration Manager)](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-endpoints-windows-defender-advanced-threat-protection)을 사용하여 장치를 등록할 수도 있습니다.

다음 단계에서는 Intune을 사용하여 등록하는 방법을 보여 줍니다.

#### <a name="download-configuration-package"></a>구성 패키지 다운로드

1. [Windows Defender 보안 센터](https://securitycenter.windows.com)에서 **설정** > **온보딩**을 선택합니다.
2. 다음 설정을 입력합니다.
  - **운영 체제**: Windows 10
  - **시스템 등록** > **배포 방법**: 모바일 장치 관리/Microsoft Intune
3. **패키지 다운로드**를 선택하고 **WindowsDefenderATPOnboardingPackage.zip** 파일을 저장합니다. 파일을 추출합니다.

이 zip 파일에 포함된 **WindowsDefenderATP.onboarding**은 다음 단계에서 필요합니다.

#### <a name="create-the-atp-configuration-profile"></a>ATP 구성 프로필 만들기

이 프로필은 이전 단계에서 다운로드한 온보딩 패키지를 사용합니다.

1. [Azure Portal](https://portal.azure.com)에서 **모든 서비스**를 선택하고 **Intune**을 기준으로 필터링한 다음 **Microsoft Intune**을 선택합니다.
2. **장치 구성** > **프로필** > **프로필 만들기**를 선택합니다.
3. **이름**과 **설명**을 입력합니다.
4. **플랫폼**에서 **Windows 10 이상**을 선택합니다.
5. **프로필 유형**에서 **Windows Defender ATP(Windows 10 Desktop)** 를 선택합니다.
6. 설정을 구성합니다.

  - **구성 패키지 등록**: 다운로드한 **WindowsDefenderATP.onboarding** 파일을 찾아서 선택합니다. 이 파일을 통해 설정이 활성화되며, 장치가 Windows Defender ATP 서비스에 보고할 수 있습니다.
  - **모든 파일에 대한 샘플 공유**: 샘플을 수집하고 Windows Defender ATP와 공유할 수 있습니다. 예를 들어 의심스러운 파일을 발견할 경우 심층 분석을 위해 Windows Defender ATP에 제출할 수 있습니다.
  - **원격 분석 보고 주기 단축**: 높은 위험이 있는 장치의 경우 이 설정을 사용하도록 설정하여 Windows Defender ATP 서비스에 원격 분석을 더 자주 보고합니다.
  - **구성 패키지 등록 취소**: Windows Defender ATP 모니터링을 제거하거나 “등록 취소”하려는 경우 [Windows Defender 보안 센터](https://securitycenter.windows.com)에서 오프로드 패키지를 다운로드하고 추가할 수 있습니다. 이러한 경우가 아니면 이 속성을 건너뜁니다.

    [System Center Configuration Manager를 사용하여 Windows 10 컴퓨터 등록](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-endpoints-sccm-windows-defender-advanced-threat-protection)에는 Windows Defender ATP 설정에 대한 자세한 정보가 포함되어 있습니다.

7. **확인**, **만들기**를 차례로 선택하여 변경 내용을 저장하면 프로필이 생성됩니다.

## <a name="create-the-compliance-policy"></a>준수 정책 만들기
준수 정책은 장치에서 허용되는 위험 수준을 결정합니다.

1. [Azure Portal](https://portal.azure.com)에서 **모든 서비스**를 선택하고 **Intune**을 기준으로 필터링한 다음 **Microsoft Intune**을 선택합니다.
2. **장치 준수** > **정책** > **정책 만들기**를 선택합니다.
3. **이름**과 **설명**을 입력합니다.
4. **플랫폼**에서 **Windows 10 이상**을 선택합니다.
5. **Windows Defender ATP** 설정에서 **장치가 머신 위험 점수나 그 아래에 있어야 함**을 기본 설정 수준으로 설정합니다.

  - **지우기**: 이 수준이 가장 안전합니다. 장치가 어떠한 위협에도 노출되지 않았으며 회사 리소스에 계속 액세스할 수 있습니다. 어떠한 위협이든 확인되는 장치는 비규격으로 평가됩니다.
  - **낮음**: 낮은 수준의 위협만 있는 장치는 규격 장치입니다. 보통 또는 높은 위협 수준의 장치는 비규격 장치입니다.
  - **보통**: 낮음 또는 보통 수준의 위협이 있는 장치는 규격 장치입니다. 높은 수준의 위협이 검색되는 경우 해당 장치는 비규격으로 간주됩니다.
  - **높음**: 이 수준은 최소 보안이며 모든 위협 수준을 허용합니다. 따라서 높음, 보통 또는 낮은 위협 수준의 장치가 규격으로 간주됩니다.

6. **확인**, **만들기**를 차례로 선택하여 변경 내용을 저장하고 정책을 만듭니다.

## <a name="assign-the-policy"></a>정책 할당

1. [Azure Portal](https://portal.azure.com)에서 **모든 서비스**를 선택하고 **Intune**을 기준으로 필터링한 다음 **Microsoft Intune**을 선택합니다.
2. **장치 준수** > **정책** > Windows Defender ATP 준수 정책을 선택합니다.
3. **할당**을 선택합니다.
4. Azure AD 그룹을 포함하거나 제외하여 정책을 할당합니다.
5. 그룹에 정책을 배포하려면 **저장**을 선택합니다. 정책의 대상이 되는 사용자 장치의 준수 여부가 평가됩니다.

## <a name="create-an-azure-ad-conditional-access-policy"></a>Azure AD 조건부 액세스 정책 만들기
비규격 장치인 *경우* 조건부 액세스 정책에 따라 리소스 액세스가 차단됩니다. 따라서 장치가 위협 수준을 초과하는 경우 SharePoint 또는 Exchange Online과 같은 회사 리소스에 대한 액세스를 차단할 수 있습니다.

1. [Azure Portal](https://portal.azure.com)에서 **Azure Active Directory** > **조건부 액세스** > **새 정책**을 엽니다.
2. 정책 **이름**을 입력하고 **사용자 및 그룹**을 선택합니다. 포함 또는 제외 옵션을 사용하여 정책에 대한 그룹을 추가하고 **완료**를 선택합니다.
3. **클라우드 앱**을 선택한 다음 보호할 앱을 선택합니다. 예를 들어 **앱 선택**을 선택한 다음 **Office 365 SharePoint Online** 및 **Office 365 Exchange Online**을 선택합니다.

    **완료**를 선택하여 변경 내용을 저장합니다.

4. **조건** > **클라이언트 앱**을 선택하여 앱과 브라우저에 정책을 적용합니다. 예를 들어 **예**를 선택한 다음 **브라우저**와 **모바일 앱 및 데스크톱 클라이언트**를 사용하도록 설정합니다.

    **완료**를 선택하여 변경 내용을 저장합니다.

5. **권한 부여**를 선택하여 장치 준수에 따라 조건부 액세스를 적용합니다. 예를 들어 **액세스 권한 부여** > **장치가 규격으로 표시되어야 함**을 선택합니다.

    **선택**을 선택하여 변경 내용을 저장합니다.

6. **정책 사용**, **만들기**를 차례로 선택하여 변경 내용을 저장합니다.

[조건부 액세스란?](conditional-access.md)은 좋은 리소스입니다.

## <a name="monitor-device-compliance"></a>장치 준수 모니터링
다음으로, Windows Defender ATP 준수 정책이 있는 장치의 상태를 모니터링합니다.

1. [Azure Portal](https://portal.azure.com)에서 **모든 서비스**를 선택하고 **Intune**을 기준으로 필터링한 다음 **Microsoft Intune**을 선택합니다.
2. **장치 준수** > **정책 준수**를 선택합니다.
3. 목록에서 Windows Defender ATP 정책을 찾아 어떤 장치가 규격 또는 비규격인지 확인합니다.

## <a name="more-good-stuff"></a>기타 유용한 자료
[Windows Defender ATP 조건부 액세스](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/conditional-access-windows-defender-advanced-threat-protection)  
[Windows Defender ATP 위험 대시보드](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/dashboard-windows-defender-advanced-threat-protection)  
[장치 준수 정책 시작](device-compliance-get-started.md)  
[Azure AD의 조건부 액세스](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)