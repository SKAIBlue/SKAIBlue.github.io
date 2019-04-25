---
layout: post
title: [Runner] 2. 런 게임 만들기 - 초기 셋팅과 끝없이 이어지는 바닥
description: >
  Cocos2d-x와 Cocos creator로 런 장르의 게임을 만들어 봅니다.
tags: [cocos2d]
---

디자인은 뒤로하고 게임 규칙부터 구현해보겠습니다. 런 장르 게임에서 가장 기본이 되는 캐릭터가 달리는것을 구현하려면 끝없이 이어지는 바닥이 필요합니다. 이런 바닥을 만들어 보겠습니다.

cocos2d-x와 Cocos Creator로 프로젝트는 이미 만들어 둔 상태입니다. Creator 프로젝트의 템플릿은 Empty로 만들어 주세요. 그 외 초기 설정은 [이 링크](https://skaiblue.github.io/2019/04/21/cocos2d-start/)를 참고해 주세요.

1. Cocos Creator에서 디자인할 화면 크기를 설정하겠습니다. 툴바에서 Project->Project Settings... 를 선택합니다. Project Preview에서 아래 사진과 같이 설정합니다. 
   ![](/assets/img/posts/cocos/run/1.png "Project Setting")

2. Cocos Creator의 에셋 뷰에서 Scenes, Textures 폴더를 추가합니다.

3. Command(Ctrl) + n을 눌러 새 씬을 만듭니다.

4. 64*64 크기의 바닥 스프라이트를 구합니다. 저는 아래 이미지를 대충 만들어서 사용했습니다. 다운받아서 사용하셔도 괜찮습니다.

   ![](/assets/img/posts/cocos/run/floor.png "floor")

5. Node Tree에서 Canvas를 오른쪽 클릭한뒤 Create->Create Empty Node를 선택합니다.

6. Properties에서 생성된 Node의 이름을 Floors로 바꿉니다.

7. Finder에서 바닥 스프라이트를 Assets의 Textrues 폴더로 드래그하면 애셋에 손쉽게 추가할 수 있습니다. 에셋에 추가된 바닥 스프라이트를 Node Tree의 Floors 하위로 드래그 하여 추가합니다.
8. Properties에서 추가한 Floor의 크기를 128 * 128로 변경하고, 위치는 -640, -360으로 설정하였습니다.
9. Node Tree에서 바닥 스프라이트를 선택한 후 Command + d를 누르면 노드가 복제됩니다. 복제된 노드를 x축 방향으로 +128 간격으로 10개 더 만듭니다.
10. Node Tree에서 만들어진 11개의 바닥을 선택해서 Command + d를 눌러 복제합니다. 
11. Floors의 첫 번째에서 11번째 자식 노드를 선택한 후 아래 그림처럼 아래로 조금 옮겨주세요. 이렇게 하는 이유는 스마트폰의 16:9 화면 비율보다 세로 비율이 큰 경우 검은 영역을 없애기 위해서입니다.
  ![](/assets/img/posts/cocos/run/2.png "floor design")
12. 툴바에서 Project->LuaCpp Support->Build Now를 눌러 프로젝트를 빌드합니다.
13. XCode의 프로젝트 탐색기에서 HelloWorldScene.h와 HelloWorldScene.cpp 파일을 삭제합니다. 휴지통으로 보내 완전히 제거해 주세요.
14. 프로젝트 탐색기에서 Classes를 오른쪽 클릭한뒤 New File...를 선택하고 C++ File 템플릿으로  타겟은 mobile과 desktop 모두 체크하시고 CreatorScene이라는 이름으로 생성합니다. 
15. CreatorScene.cpp 파일과 CreatorScene.hpp 파일이 생성됩니다. hpp 파일의 확장자를 h로 변경해 줍니다.

    ※ 앞으로 언급이 없더라도 항상 hpp확장자는 h로 변경해 주시길 바랍니다.
16. CreatorScene.hpp에 다음 코드를 작성합니다.
17. 
    ```CPP
    #ifndef CreatorScene_hpp
    #define CreatorScene_hpp

    #include "cocos2d.h"

    class CreatorScene
    {
    public:
    
        CreatorScene(std::string path);
    
        cocos2d::Scene* getScene();
    
    protected:

        cocos2d::Scene* scene;
    };
    #endif /* CreatorScene_hpp */
    ```

18. CreatorScene.cpp에 다음 코드를 작성합니다.

    ```CPP
    #include "CreatorScene.h"
    #include "reader/CreatorReader.h"

    USING_NS_CC;

    CreatorScene::CreatorScene(std::string path)
    {
        auto reader = creator::CreatorReader::createWithFilename(path);
        reader->setup();
        scene = reader->getSceneGraph();
    }

    Scene* CreatorScene::getScene()
    {
        return this->scene;
    }

    ```

19. GamePlayScene.h 파일과 GamePlayScene.cpp 파일을 추가한 뒤 다음 코드를 작성합니다.
    
    ```CPP
    /* GamePlayScene.h */
    #ifndef GamePlayScene_h
    #define GamePlayScene_h

    #include "cocos2d.h"
    #include "CreatorScene.h"

    class GamePlay: public CreatorScene
    {
    public:
    
        GamePlay();
    
    };

    #endif /* GamePlayScene_hpp */
    ```

    ```CPP
    #include "GamePlayScene.h"
    #include "reader/CreatorReader.h"

    USING_NS_CC;

    GamePlay::GamePlay():CreatorScene("creator/Scenes/GamePlay.ccreator")
    { 
        // 씬 초기화 작업
    }

    ```

20. AppDelegate.cpp 파일을 열어 다음 #include "HelloWorldScene.h"를 #include "GamePlayScene.h"로 변경합니다.
    
21. 120 라인 부근에 아래 코드를 지워주세요
    ```CPP
    auto scene = HelloWorld::createScene();
    ```

22. 3에서 지운 위치에 다음 코드를 추가합니다.
    ```CPP
    auto scene = GamePlay().getScene();
    ```

23. 실행이 잘 되는지 테스트해봅니다.
    ![](/assets/img/posts/cocos/run/3.png "First run")

24. 이제 바닥이 움직이는 기능을 구현합니다. 씬에 있는 노드에 컴포넌트를 붙이는 방식으로 만들 생각입니다. 당장은 이 방법말곤 좋은 생각이 떠오르지 않네요. CDecoMovement.h와 CDecoMovement.cpp를 추가하여 다음 코드를 작성합니다.

    ```CPP
    /*CDecoMovement.h*/
    #ifndef CDecoMovement_hpp
    #define CDecoMovement_hpp

    #include "cocos2d.h"

    class CDecoMovement : public cocos2d::Component
    {
        virtual void update(float delta);
    };

    #endif /* CDecoMovement_hpp */
    ```

    ```CPP
    /*CDecoMovement.cpp*/
    #include "CDecoMovement.h"

    void CDecoMovement::update(float delta)
    {
        auto pos = _owner->getPosition();
        _owner->setPosition(pos.x - 100 * delta, pos.y);
    }
    ```

25. Definitions.h 파일을 추가하여 다음 코드를 작성합니다. Definitions.h에는 상수나 여러 함수를 정의할 것입니다.

    ```CPP
    #ifndef Definitions_h
    #define Definitions_h

    #include "cocos2d.h"

    cocos2d::Component* AutoRelease(cocos2d::Component* comp)
    {
        comp->autorelease();
        return comp;
    }

    #endif /* Definitions_h */
    ```


26. GamePlayScene.cpp 파일을 다음과 같이 수정합니다.

    ```CPP
    #include "GamePlayScene.h"
    #include "reader/CreatorReader.h"
    #include "CDecoMovement.h"
    #include "Definitions.h"
    
    USING_NS_CC;

    GamePlay::GamePlay():CreatorScene("creator/Scenes/GamePlay.ccreator")
    {
        auto canvas = scene->getChildByName("Canvas");
        auto floors = canvas->getChildByName("Floors");

        floors->addComponent(AutoRelease(new CDecoMovement()));
    }

27. 실행을 해보면 바닥이 왼쪽으로 움직이는 것을 볼 수 있습니다. 하지만 바닥의 길이에는 한계가 있어서 왼쪽으로 이동하다 보면 바닥이 끊기는 것을 볼 수 있습니다. 약간의 트릭으로 바닥이 무한히 이어지도록 만들겠습니다.
    ![](/assets/img/posts/cocos/run/4.png "finite floor")

28. CDecoMovement.cpp에서 update 함수를 다음과 같이 수정해 봅시다.

    ```CPP
    auto pos = _owner->getPosition();
    auto nX = pos.x - 100 * delta;
    if(nX < 512)
        nX += 128;
    _owner->setPosition(nX, pos.y);
    ```

29. 실행해보면 시간이 지나도 바닥이 끊기지 않는 것을 볼 수 있습니다.
    ![](/assets/img/posts/cocos/run/5.png "Infinite floor")