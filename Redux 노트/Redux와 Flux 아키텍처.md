## Redux와 Flux 아키텍처

참고: https://taegon.kim/archives/5288

참고: https://www.youtube.com/watch?v=zw-Oz6oNjQE

<br>

### 1. MVC 패턴과 그 한계.

Model : 백그라운드에서 동작하는 로직을 처리.

View : 사용자가 보게 될 결과 화면을 출력.

Controller : 사용자의 입력처리와 흐름 제어를 담당.

<br>

#### MVC의 패턴에서의 데이터 흐름.
<img width="1280" alt="1" src="https://user-images.githubusercontent.com/50945715/89033791-8cc9f680-d372-11ea-8a0c-f6592523c32e.png">

MVC 패턴에서 컨트롤러(Controller)는 모델(Model)의 데이터를 조회하거나 업데이트하는 역할을 하며, 모델(Model)의 변화는 뷰(View)에 반영한다. 또한, 사용자는 뷰를 통해 데이터를 입력하는데 사용자의 입력은 모델에 영향을 주기도 한다. 따라서 이와 같은 데이터 흐름은 다음과 같이 그림으로 표현할 수 있다.

<br>

#### MVC의 패턴의 한계.
<img width="1280" alt="2" src="https://user-images.githubusercontent.com/50945715/89033794-8dfb2380-d372-11ea-8262-eac0848a3826.png">

문제는 페이스북과 같은 대규모 애플리케이션에서는 MVC가 너무 빠르게, 너무 복잡해진다는 것이다. 페이스북 개발팀에 따르면 구조가 너무 복잡해진 탓에 새 기능을 추가할 때마다 크고 작은 문제가 생겼으며 코드의 예측이나 테스트가 어려워졌으며 새로운 개발자가 오면 적응하는데만 한참이 걸려서 빠르게 개발할 수가 없었다. 소프트웨어의 품질을 담보하기가 힘들어졌다는 뜻이다.

<br>

### 2. FLUX 아키텍처 고안

Flux는 페이스북에서 MVC의 문제를 해결할 목적으로 고안한 애플리케이션 아키텍처이다.

디스패처(Dispatcher), 스토어(Store), 뷰(View) 구조이다. 

단, 여기서 말하는 뷰는 MVC의 뷰와는 달리 스토어에서 데이터를 가져오는 한편 데이터를 자식 뷰로 전달하기도 하는 일종의 뷰-컨트롤러로 보아야 한다. React를 기반으로 작성된 컴포넌트를 떠올리면 될 것이다.

Flux 아키텍처의 가장 큰 특징으로는 '단방향 데이터 흐름(unidirectional data flow)'을 들 수 있다. 

데이터의 흐름은 언제나 디스패처(Dispatcher)에서 스토어(Store)로, 스토어에서 뷰(View)로, 뷰에서 액션(Action)으로 다시 액션에서 디스패처로 흐른다.

<img width="1280" alt="3" src="https://user-images.githubusercontent.com/50945715/89033796-8e93ba00-d372-11ea-9a9a-3edad0069b26.png">
<img width="1280" alt="4" src="https://user-images.githubusercontent.com/50945715/89033797-8e93ba00-d372-11ea-88fa-b958c3b5107c.png">

페이스북 개발팀은 **양방향 데이터 바인딩이 있기 때문에 한 모델을 업데이트 한 뒤 다른 모델을 업데이트 해야하는 순차적인 업데이트가 발생할 수 밖에 없으며, 애플리케이션의 크기가 증가할수록 이러한 순차적 업데이트가 사용자 인터랙션의 결과를 예측하기 어렵게 한다고 언급**했다. 한편 Flux와 같이 일방적인 데이터 흐름에서 일어나는 데이터 변화는 훨씬 더 예측하기 쉽다고도 말했다.

<br>

### 3. Redux 탄생

페이스북은 Flux 아키텍처를 발표한 후 Flux에 대한 구현체도 공개했는데, 이 구현체에는 디스패처만 구현되어 있어 완전한 Flux 프레임워크라 부르기엔 다소 무리가 있었다. 2015년 10월에 발표한 2.1.0 버전에서 스토어를 지원하기 전까지는 사실상 완전한 공식 Flux 구현체가 없던 셈이다. 이 시기에 많은 Flux 구현체들이 나타났는데, 널리 사용되는 것 중 하나가 [Redux](http://redux.js.org/)인 것이다.

<img width="1280" alt="5" src="https://user-images.githubusercontent.com/50945715/89033799-8f2c5080-d372-11ea-877d-7266c8fcd61f.png">

<br>

참고: https://www.youtube.com/watch?v=zw-Oz6oNjQE
<img width="1280" alt="6" src="https://user-images.githubusercontent.com/50945715/89033800-8f2c5080-d372-11ea-957a-8a8911419eca.png">