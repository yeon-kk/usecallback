## useCallback 이해하기
1. 기본형: useCallback(콜백,의존성 배열) => 의존성 배열 [ ] 안의 함수(의 주소값)이 변경(재랜더링)되면서 호출되는 것을 막는다. 왜냐면 실제로 useCallback의 매개변수 안에 있는 콜백함수가 어떤 변화도 없었는데, App()의 어떤 state가 변경되면서 재랜더링 되었기 때문에 해당 콜백함수도 주솟값이 변경되는 것.

2. 처음에 코드짤 때 함수가 호출되는지 어떻게 알지? 했는데, useEffect를 사용해서, 두번째 매개변수인 의존성 함수에 확인하고 싶은 콜백 함수를 넣어주면 됨. 그리고 첫번째 매개변수에는 어떤 출력 .. 예를들면 console.log()를 띄워서 확인해보면 된다.

3. state하나만으로는 비교가 어려운것 같아서, 다른 state를 하나 더 만들어준다.
그러면 그 state가 변경될 때 다른 함수(주소값을 받는)도 재생성 되는것을 확인.
따라서, 재랜더링 되는 것을 막기 위해 useCallback를 만들고, 해당 함수에서 필요한 state만 의존성 배열에 지정한다.

![image](https://user-images.githubusercontent.com/86847564/189472439-6e5dfbce-420a-4ff5-bd8d-903c9974bd0f.png)

이미지에서 보이는 것처럼, toggle버튼으로 toggle true<->false로 변경되지만 number가 변경되지 않기 때문에 "checkNumber :: 변경"이 콘솔에 찍히지 않는다는 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/86847564/189475886-bc878a64-841c-4759-8d56-29b90e00ca0c.png)
크기를 200으로 시작하고, 색상을 변경해주는 코드 작성. useEffect를 하면 숫자를 변경했을 때 색상 부분의 함수도 호출되는데, 그때 useCallback를 사용하면 숫자가 변경되더라도 콘솔에서 색상이 출력되지 않는다.
