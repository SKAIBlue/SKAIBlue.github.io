---
layout: post
title: Cocos2d-x 개발 시작하기
description: >
  Cocos2d-x 시작합니다. Cocos Creator로 c++ 프로젝트를 셋팅하는 방법까지
tags: [cocos2d]
---

Cocos2d-x는 크로스 플랫폼을 지원하는 2D 게임용 프레임워크입니다. 게임 엔진이라고 하기에는 유명한 Unity나 Unreal에 비해 부족한 점이 많습니다. 하지만 무료이고 아주 가볍다는 큰 장점을 가지고 있습니다. Unity나 Unreal도 물론 무료이긴 하지만 Unity는 일정 수익 이상의 성과를 받으면 유료 버전의 엔진을 구매해야 하고, Unreal 역시 일정 수익이 발생하면 수수료가 발생합니다. 완전한 무료는 아닌것이죠. 때문에 2D 게임을 개발할 때 Cocos2d-x를 선택하는것도 나쁘지 않은 선택입니다.

# 개발 환경
**Windows에서는 Visual Studio**로 개발하면 되고 **Mac에서는 XCode**에서 개발하시면 됩니다.
저는 Mac에서 개발하려고 합니다.

어떤 개발 환경을 선택하시든 프로젝트는 자신의 환경에서 스크립트를 실행하면 되기 때문에 제 글을 보고 배우시는 분들 중 Windows를 쓰시는 분이 있다면 개발 환경이 다르다고 해서 걱정하실 필요 없습니다.

# 언어
Cocos2d-x는 `c++`, `Javascript`, `Lua`를 지원합니다. 저는 c++로 개발할겁니다.

사실 저는 2014년 쯤에 Cocos2D-x를 c++로 개발하는 것으로 공부했었는데... 5년 가까이 지나다 보니 기억 나는게 별로 없습니다 ㅠㅠ 혹시 제가 잘못 아는게 있다거나 좀 더 나은 방법이 있다면 알려주시길 바랍니다.

# Cocos2d-x 다운로드
[Cocos2d-x 다운로드 페이지](https://cocos2d-x.org/download)
**Cocos creator**라는 것이 생겼네요. 뭔가 게임 엔진 처럼 Scene View가 있어서 저걸 쓰면 개발하기 편할것 같으니 써보겠습니다.
일단 자신의 환경에 맞게 `Cocos2D-x`는 다운 받으신 뒤 압축을 푸시고, `Cocos Creator`는 다운 받아서 설치하세요.

제가 다운받은 버전은 다음과 같습니다. 버전에 따라 다른점이 있으니 참고해주세요.
- Cocos2d-x: 3.17.1
- Cocos Creator: 2.1.0

# Cocos2d-x 초기 설정
Cocos2d-x를 사용하기 위해서 초기 설정 작업이 필요합니다. 저는 안드로이드 개발을 해왔기 때문에 이미 몇가지 셋팅이 되어 있어서 링크로 대체합니다.

[Mac cocos2d-x 초기 설정](http://theeye.pe.kr/archives/2848)

[Windows cocos2d-x 초기 설정](https://ggari.tistory.com/244)

# Cocos2d-x 프로젝트 생성
   초기 설정을 제대로 하셨으면 터미널에서 다음 명령어로 cpp 프로젝트를 생성할 수 있습니다.
   ```
   cocos new [프로젝트이름] -p [프로젝트 도메인] -l cpp -d [경로]
   ```
   예를 들면 다음과 같이 명령어를 실행하시면 됩니다.
   ```
   cocos new CocosCreatorTest -p com.skaiblue.cocoscreatortest -l cpp -d ~/Developments/Cocos2d-x
   ```

# [XCode]Cocos Creator 프로젝트 설정
1. 먼저 앞서 알려드린대로 명령어로 cpp 프로젝트를 먼저 생성하셔야 합니다. 프로젝트를 생성해주세요. 여기서 생성한 프로젝트 경로를 `cpp 프로젝트 루트`라고 부르겠습니다.
   
2. Cocos Creator 에서 프로젝트를 생성합니다. 테스트를 위해 Hello World 템플릿으로 프로젝트를 생성했습니다. 여기서 생성한 프로젝트 경로를 `creator 프로젝트 루트`라고 부르겠습니다. 프로젝트가 생성되면 Cocos Creator 개발 화면(?)이 뜰겁니다.
![](https://skaiblue.github.io/assets/img/posts/cocos/start/1.png "cocos creator 프로젝트 생성 화면")

3. 터미널에서 다음 명령어를 실행해 creator_to_cocos2dx 소스코드를 복제합니다.
   ```
   git clone https://github.com/cocos2d/creator_to_cocos2dx
   ```

4. creator_to_cocos2dx/creator_project/packages 폴더에 creator_luacpp_support 폴더가 있습니다. 이 폴더를 `creator 프로젝트 루트`/packages 폴더에 복사해 주세요
![](https://skaiblue.github.io/assets/img/posts/cocos/start/2.png "패키지 복사")

5. 제대로 복사 하셨으면 Cocos Creator 개발 화면의 콘솔 뷰에 아래와 같은 텍스트가 표시됩니다.
   ```
   [LuaCPP Support] version 0.4
   creator-luacpp-support loaded
   ```

6. 플러그인 셋업을 위해 툴바에서 Project->LuaCpp Support->Setup Target Project를 실행합니다.
![](https://skaiblue.github.io/assets/img/posts/cocos/start/3.png "타겟 프로젝트 셋업")

7. `cpp 프로젝트 루트`의 경로로 설정한 후 Build를 눌러주세요.
![](https://skaiblue.github.io/assets/img/posts/cocos/start/4.png "타겟 프로젝트 설정")

8. Finder에서 `cpp 프로젝트 루트`/proj.ios_mac에 찾아가면  CocosCreatorTest.xcodeproj파일이 있습니다. 실행하면 XCode가 실행이 됩니다.
   
9. XCode의 프로젝트 탐색기에서 프로젝트를 선택하면 보이는 페이지에서 아래 사진과 같이 PROJECT->[프로젝트 이름]->Build Settings에서 **Header Search Paths**를 찾아서 아래 path를 추가합니다.
   ```
   $(SRCROOT)/../Classes/reader
   ```
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/5.png "Header Search Paths")

10. Finder에서 `cpp 프로젝트 루트`/Classes에 찾아가면 reader 폴더가 있습니다. 이 폴더를 XCode의 프로젝트 탐색기에 Classes 하위로 드래그 합니다. 아래 사진과 같이 설정해 주시고 Finish를 눌러주세요.
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/6.png "코드 추가")

11. 프로젝트 탐색기에서 아래 네 개의 파일을 삭제해주세요. 휴지통으로 보내지마시고 **Remove References**를 눌러서 참조만 지우세요.
    ```
    Classes/reader/Android.mk
    Classes/reader/CMakeLists.txt
    Classes/reader/dragonbones/Android.mk
    Classes/reader/dragonbones/CMakeLists.txt
    ```
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/7.png "필요 없는 참조 삭제")
12. Finder에서 `cpp 프로젝트 루트`/Resources에 찾아가면 creator 폴더가 있습니다. 이 폴더를 XCode의 프로젝트 탐색기에 Resources 하위로 드래그 합니다. 아래 사진과 같이 설정해 주시고 Finish를 눌러주세요.
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/8.png "리소스 추가")

13. 마지막으로 command + R키를 눌러서 잘 되는지 실행해봅니다.

# Cocos Creator로 만든 씬 간단 테스트
1. 테스트를 위해 씬을 대충 수정해봤습니다. 적당히 수정 하셨으면 씬 저장 후 툴바에서 Project->LuaCpp Support->Build Now 로 빌드 합니다.
![](https://skaiblue.github.io/assets/img/posts/cocos/start/9.png "간단 씬")

2. XCode로 돌아와 AppDelegate.cpp 상단에 다음 헤더파일을 추가합니다.
    ```CPP
    #include "reader/CreatorReader.h"
    ```

3. 120 라인 부근에 아래 코드를 지워주세요
    ```CPP
    auto scene = HelloWorld::createScene();
    ```

4. 3에서 지운 위치에 다음 코드를 추가합니다.
    ```CPP
    // 파일 이름으로 ccreator를 읽어옵니다.
    auto reader = creator::CreatorReader::createWithFilename("creator/Scene/helloworld.ccreator");
    reader->setup();
    // scene graph를 가져옵니다.
    auto scene = reader->getSceneGraph();
    ```
5. command + r을 눌러 실행해 봅니다.
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/10.png "실행화면")

# [Visual Studio]Cocos Creator 프로젝트 설정
[XCode]Cocos Creator 프로젝트 설정의 7번까지의 과정이 동일합니다.
1. `cpp 프로젝트 루트`/proj.win32에 찾아가면 [프로젝트이름].sln 파일이 있습니다. 실행하면 Visual Studio가 실행이 됩니다.
2. 윈도우 탐색기로 `cpp 프로젝트 루트`/Classes에 찾아가 reader 폴더를 솔수션 탐색기에 [프로젝트이름]하위의 src로 드래그합니다.
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/11.png "Visual Studio")
3. Ctrl + F5키를 눌러서 잘 되는지 실행해봅니다.
    ![](https://skaiblue.github.io/assets/img/posts/cocos/start/12.png "Windows 실행화면")

    ※ 솔루션 탐색기에서 src 하위에 필터를 만들어서 reader의 소스 파일들을 정리하면 보기 편합니다.


# [Android Studio]Cocos Creator 프로젝트 설정
Android Build 때문에 이틀을 삽질했네요. 마지막으로 안드로이드 스튜디오 설정하는 방법입니다.
[XCode]Cocos Creator 프로젝트 설정의 7번까지의 과정이 동일합니다.

1. 안드로이드 스튜디오로 `cpp 프로젝트 루트`/proj.android를 열어주세요.
2. 프로젝트 탐색기에서 gradle.properties 파일을 열어 PROP_APP_ABI와 PROP_BUILD_TYPE 영역 내용을 다음과 같이 수정합니다. 제가 쓰는 cocos2d-x 버전이 기본적으로 CMake로 빌드하게 되어있습니다. ndk-build 시스템으로 빌드하기 위해 변경해줍니다. 또한 모든 타입의 ABI에 대해 빌드를 가능하게 합니다.
  
   ```Gradle
   PROP_APP_ABI=arm64-v8a:armeabi-v7a:x86:x86_64
   PROP_BUILD_TYPE=ndk-build
   ```

3. 텍스트 에디터로 `creator 프로젝트 루트`/packages/creator-luacpp-support/reader/Android.mk 파일을 열어 다음과 같이 수정합니다.
   
   ```CMake
   LOCAL_PATH := $(call my-dir)

   cpp_src := \
   animation/AnimateClip.cpp \
   animation/AnimationClip.cpp \
   animation/AnimationManager.cpp \
   animation/Easing.cpp \
   animation/Bezier.cpp \
   collider/Collider.cpp \
   collider/ColliderManager.cpp \
   collider/Contract.cpp \
   collider/Intersection.cpp \
   CreatorReader.cpp \
   ui/PageView.cpp \
   ui/RichtextStringVisitor.cpp

   # for cpp
   include $(CLEAR_VARS)
   path := $(LOCAL_PATH)

   LOCAL_MODULE := creator_reader
   LOCAL_MODULE_FILENAME := libcreatorreader
   LOCAL_ARM_MODE := arm
   LOCAL_SRC_FILES := $(cpp_src)

   LOCAL_EXPORT_C_INCLUDES := $(LOCAL_PATH)/.
   LOCAL_C_INCLUDES := $(LOCAL_PATH)/.
   LOCAL_STATIC_LIBRARIES := cc_static
   LOCAL_STATIC_LIBRARIES += dragonbones_static

   include $(BUILD_STATIC_LIBRARY)


   $(call import-add-path, $(path))
   $(call import-module, dragonbones)
   ```

4. 3. 텍스트 에디터로 `creator 프로젝트 루트`/packages/creator-luacpp-support/reader/dragonbones/Android.mk 파일을 열어 다음과 같이 수정합니다.
  
   ```CMake
   LOCAL_PATH := $(call my-dir)

   include $(CLEAR_VARS)

   LOCAL_MODULE := dragonbones_static

   LOCAL_MODULE_FILENAME := libdragonbones


   LOCAL_SRC_FILES :=       animation/Animation.cpp \
                            animation/AnimationState.cpp \
                            animation/TimelineState.cpp \
                            animation/WorldClock.cpp \
                            armature/Armature.cpp \
                            armature/Bone.cpp \
                            armature/Slot.cpp \
                            core/BaseObject.cpp \
                            events/EventObject.cpp \
                            factories/BaseFactory.cpp \
                            model/AnimationData.cpp \
                            model/ArmatureData.cpp \
                            model/DragonBonesData.cpp \
                            model/FrameData.cpp \
                            model/TimelineData.cpp \
                            parsers/DataParser.cpp \
                            parsers/JSONDataParser.cpp \
                            textures/TextureData.cpp \
                            cocos2dx/CCArmatureDisplay.cpp \
                            cocos2dx/CCFactory.cpp \
                            cocos2dx/CCSlot.cpp \
                            cocos2dx/CCTextureData.cpp


   LOCAL_C_INCLUDES := $(LOCAL_PATH)/..

   LOCAL_EXPORT_C_INCLUDES := $(LOCAL_PATH)/..

   LOCAL_STATIC_LIBRARIES := cc_static

   LOCAL_CFLAGS += -Wno-psabi
   LOCAL_EXPORT_CFLAGS += -Wno-psabi

   include $(BUILD_STATIC_LIBRARY)
   ```

5. Cocos creator에서 Project->LuaCpp Support->Build Now를 눌러 다시 빌드 합니다.

6. `cpp 프로젝트 루트`/proj.android/app/jni/Android.mk를 열어 다음과 같이 수정합니다.
   
   ```CMake
   LOCAL_PATH := $(call my-dir)

   include $(CLEAR_VARS)

   LOCAL_MODULE := MyGame_shared

   LOCAL_MODULE_FILENAME := libMyGame

   FILE_LIST := $(wildcard $(LOCAL_PATH)/../../../Classes/*.cpp)
   LOCAL_SRC_FILES := $(FILE_LIST:$(LOCAL_PATH)/%=%)
   LOCAL_SRC_FILES += hellocpp/main.cpp

   LOCAL_C_INCLUDES := $(LOCAL_PATH)/../../../Classes

   # _COCOS_HEADER_ANDROID_BEGIN
   # _COCOS_HEADER_ANDROID_END

   LOCAL_STATIC_LIBRARIES := cc_static
   # LOCAL_STATIC_LIBRARIES += creator_reader_lua  # for lua project
   LOCAL_STATIC_LIBRARIES += creator_reader   # add dependence

   # _COCOS_LIB_ANDROID_BEGIN
   # _COCOS_LIB_ANDROID_END

   include $(BUILD_SHARED_LIBRARY)

   $(call import-module, cocos)
   $(call import-module, ./../../Classes/reader)  # import module path

   LOCAL_PATH := $(call my-dir)
   ```

7. 안드로이드 스튜디오에서 빌드하고 실행이 잘 되는지 확인합니다.
   ![](https://skaiblue.github.io/assets/img/posts/cocos/start/13.png "Android 실행화면")