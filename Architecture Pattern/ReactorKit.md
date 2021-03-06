# ReactorKit
ReactorKit 학습 & 경험을 정리합니다.

## ReactorKit 이란?

반응형 및 단방향 앱 아키텍쳐를 위한 프레임 워크이며, 단방향 아키텍쳐란? 페이스북에서 MVC 패턴으로 데이터 흐름을 관리하는데 많은 어려움을 겪어 이를 개선하기 위해 그 방법으로 단방향으로 데이터가 흐르는 방식을 적용한 것이라고 합니다.
리액터킷은 이런 방식이 적용 된 아키텍쳐 프레임워크입니다.
리액터킷의 데이터 흐름는 뷰 > 액션 > 리액터 > 스테이트 > 뷰 흐름으로 흐르게 되고
뷰는 사용자 인터랙션을 추상화하여 리액터에 전달하고, 리액터에서 전달받은 상태를 각각의 뷰 컴포넌트에 바인드합니다. 뷰는 비즈니스 로직을 수행하지않습니다.
반대로, 리액터는 뷰의 상태를 관리합니다. 뷰에서 액션을 전달받으면 비즈니스 로직을 수행한 뒤 상태를 변경하여 다시 뷰에 전달합니다. 리액터는 UI 레이어에서 독립적이기 때문에 비교적 테스트하기 쉽습니다.
그리고 테스트 부분에서 리액터를 통해 액션을 쉽게 전달하고 액션에 대한 아웃풋을 currentState를 통해 쉽게 확인할 수 있습니다. 테스트 부분에서도 굉장히 편리합니다.

간단한 흐름은 View -> Action -> Reactor -> State -> View 이런 단방향 데이터 흐름을 가지고 있습니다. 좀더 디테일한 흐름은 뷰가 리액터의 액션에 바인딩되어 이벤트 전달 -> mutate 함수가 실행 되고 변경할 상태를 변경하여 Mutation을 리턴 -> reduce 함수에서 State, Mutation을 받아 최선 State를 뷰에게 전달 -> 리액터의 state와 바인딩 된 View가 새로운 State 구조체를 받아 뷰를 업데이트 이런 흐름을 가지고 있습니다. 데이터의 흐름이 세분화 되있으므로 코드를 분석하는 것이 수월합니다.

## ReactorKit의 장점과 단점

### 장점

1. 데이터 흐름이 좀더 세분화 되어 코드를 분석하는 것이 수월하다.
 - 리액터의 mutate 함수를 보면 action들을 switch문으로 관리합니다. 그렇기때문에 각 액션에 따른 상태 변경 및 데이터 가공 코드를 분석하는 것이 수월합니다. 저는 개인적으로 이 부분이 정말 좋았습니다. 또, Mutation을 받아 새로운 State를 만드는 reduce 함수도 존재합니다. 이렇게 상태를 변경하는 과정이 세분화 되어 코드를 분석하는 것이 수월합니다.
 
2. 단방향 아키텍처를 사용하기 위한 기능이 모두 구현 되어 있다.
 - MVVM 패턴을 새로 작성할 경우 추상화를 위한 프로토콜 작성이나 바인딩 구현 등 다양한 코드를 작성해야합니다. 또 개인마다 구현 방식에 차이가 있기때문에 서로 코드를 이해하는데 어느정도 시간이 들 수 있습니다. 
 - ReactorKit은 프레임워크이므로 단방향 아키텍처 개발을 위한 기능이 모두 구현 되어 있습니다. 이 차이는 마치 빈칸에 글씨를 채우냐 아니면 글을 처음부터 모두 작성하느냐 같은 느낌이라고 생각합니다. (물론 MVVM도 한번 템플릿화 해놓으면 재사용이 가능합니다..)

3. 유닛 테스트가 매우 편리하다.
 - 이 부분은 사실 MVVM의 장점과 동일합니다.
 - 리액터는 UI 레이어에서 독립적이기 때문에 테스트하기 쉽습니다.
 - 리액터를 테스트 할때 인풋(액션) 아웃풋(state)에 대한 접근이 굉장히 쉽기때문에 테스트가 매우 수월합니다.

### 단점
 - 빈번한 상태가 업데이트 된다면 계속해서 새로운 State 이벤트가 발생하는 데 그렇게 되면 state에 바인딩 된 뷰들이 계속해서 업데이트 될 것입니다. 그 중에는 어떤 액션을 받으면 애니메이션 이펙트를 실행한다던가하는 뷰들도 있을 수 있는데 의도하지 않은 이펙트가 발생할 수 있을 것입니다. RxSwift의 오퍼레이터인 distinctUntillChanged() 통해 값이 변하였을 때만 이벤트를 다음 스트림으로 전달할 수 있겠지만 때마다 distinctUntillChanged를 작성 하는 것에 대해 신경을 써야하는 것이 좀 번거로울 수 있을 것 같다고 생각합니다.
 
### 참고 자료

[Flux 소개 사이트](https://haruair.github.io/flux/docs/overview.html)

[ReactorKit Github](https://github.com/ReactorKit/ReactorKit)

[전수열님의 미디엄 글](https://medium.com/styleshare/reactorkit-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-c7b52fbb131a)