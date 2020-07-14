---
title: Forguncy Plugins - 플러그인 개발하기
tags: [Forguncy, Plugins, Addons, 프로젝트, C#, C Sharp, Coding, Programming]
keywords: Forguncy, 엑셀, Plugin, 플러그인, 연동
last_updated: Jul 10, 2020
summary: "Forguncy 플러그인을 개발하는 방법입니다."
sidebar: forguncy5_sidebar
permalink: forguncy5_plugins_development.html
folder: forguncy5_81_plugins
---

<br /><br />

> 알림 : 본 페이지와 하위 페이지의 내용은 비-개발자들을 위한 내용이 아닌 포건시 플러그인 개발자들을 위한 전문적인 내용을 담고 있습니다. 프로그래밍에 익숙하지 않으신 분들이 이해하기에 적합한 내용이 아닐 수 있습니다.

<br /><br />


<h2>포건시 플러그인 개요</h2>

포건시는 웹개발 도구이며, 그렇기 때문에 웹개발 시 맞닥드리게 되는 한계 또한 가지고 있는 도구입니다. 이를 해결하기 위해 포건시에서는 C# 및 JavaScript 코드를 이용하여 생성한 별도의 프로그램인 '플러그인(Plug-in)'을 연동하여 추가 기능들을 개발하여 사용할 수 있도록 설계되어 있습니다. 

  ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_01.png)

<br />

플러그인을 개발하시려면 포건시에서 지원하는 JavaScript API 및 Server API에 익숙해지셔야 합니다. 이와 관련한 자세한 내용은 [Forguncy API 페이지](https://forguncy-korea.github.io/fgc5jsapi_intro.html)를 참고해 주십시오.

<br /><br />


<h2>플러그인 개발 환경을 다운로드하고 개발 시작하기</h2>

1. [포건시 플러그인 생성 도구 다운로드]({{site.url}}/attached_files/Plugin_Files/etc/PluginTools_20200710.zip))하신 뒤 압축을 풀고, ForguncyPluginCreator.exe를 실행하십시오.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_02.png)

    <br />

2. 어떤 컴퓨터에서는 아래와 같은 오류 창이 발생할 수 있습니다. 윈도우 내 OS가 가진 인증서와 맞지 않다는 오류이므로, "추가 정보"를 클릭하신 후 "실행"을 클릭하시면 계속 진행됩니다.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_03.png)

    <br />

3. 아래와 같은 실행화면이 나타나면 정상적으로 ForguncyPluginCreator가 실행된 것입니다.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_04.png)

    <br />

4. 나타나는 실행 창에서 플러그인의 이름을 입력하신 후 플러그인 유형을 선택(셀 유형 혹은 명령 유형)해 주십시오. 

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_05.png)

    <br />

5. 마지막으로 플러그인의 출력 경로를 설정하신 후, '확인'을 클릭하십시오.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_06.png)

    <br />

6. 설정하신 출력 경로 아래에 아래와 같이 플러그인을 개발할 수 있는 환경이 갖추어 집니다.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_07.png)

<br /><br />


<h2>포건시 플러그인 제작 시작하기</h2>

※참고 : 여기서부터 진행되는 내용은 [Visual Studio Community Edition](https://visualstudio.microsoft.com/ko/vs/community/){:target="_blank"}을 먼저 설치하셨다고 전제 하고 진행합니다.

1. 플러그인 개발 환경을 생성하신 위치에서 .csproj 파일을 더블 클릭하시면 Visual Studio에서 프로젝트가 열립니다.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_08.png)

    <br />

2. VS의 솔루션 탐색기(Solution Explorer)에서 "참고"를 확장하신 후, 나타나는 Forguncy.CellTypes 및 Forguncy.PluginCommon을 제거하십시오.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_09.png)

    <br />

3. 다시 솔루션 탐색기의 "참조"에서 마우스 오른쪽 클릭하여 "참조 추가(Add Reference)"를 선택하십시오.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_10.png)

    <br />

4. "참조 추가"창의 하단에 있는 "찾아보기(Browse...)"을 클릭하신 후, 포건시 설치 폴더의 Website\bin 폴더로 이동하십시오.
    예를 들면, C:\Program Files (x86)\Forguncy\Website\bin 입니다.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_11.png)

    <br />

5. 그 후, 3개의 라이브러리 파일 GrapeCity.Forguncy.Plugin.dll, GrapeCity.Forguncy.CellTypes.dll, Forguncy.Commands.dll을 찾아 솔루션 탐색기에 추가하십시오.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_12.png)

    <br />

6. 해당 라이브러리 파일들을 추가하시려면 아래 화면에서 OK를 눌러 진행하십시오.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_13.png)

    <br />

7. 이후 해당 프로젝트의 .cs 파일을 열어 개발을 진행하시면 됩니다. 이에 대한 자세한 이야기는 이후의 예제 페이지들을 참고하여 주세요.

    ![]({{site.url}}/images/forguncy5/forguncy5_plugins_dev_14.png)

<br /><br />

관련하여 문의사항이 있으시면 언제든지 그레이프시티 코리아 기술지원(support-kor@grapecity.com)으로 연락 주십시오.

<br /><br />