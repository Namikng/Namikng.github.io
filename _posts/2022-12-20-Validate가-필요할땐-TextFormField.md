---
layout: post
title:  "Validate가 필요할땐 Form"
date:   2022-12-20
last_modified_at: 2022-12-20
categories: [개발]
tags: [Flutter]
---

간단한 회원가입 페이지를 만들 일이 있었다. 그리고 나는 익숙한 TextField를 사용했다.

그런데 Flutter in Action 책을 읽다가 사용자의 입력값을 Validate 해야하는 필드가 여러개 있다면

**TextFormField**를 사용하는게 편하다는 것을 알게 되어 정리해본다!

<br/>

## 단순한 TextField 대신 Form을 사용하면 좋은 점?
- 모든 필드값을 한번에 처리할 수 있다.
- validate 후 에러 메시지 처리가 간단하다.
- validate 할 때 레이아웃 처리를 알아서 예쁘게 해준다.

![스크린샷](https://namikng.github.io/assets/images/textFormField.gif)

valid, invalid 경우 각각의 UI를 알아서 애니메이션까지 예쁘게 해준다!

에러 메시지도 그냥 입력만 하면됨

<br/>

## 기억할 점❗️
그냥 TextFormField만 사용해도 validate는 되지만 그 입력값을 받아오려면

**GlobalKey, Form** 위젯이 필요하다. 

코드를 보자!

```dart
class _MyHomePageState extends State<MyHomePage> {
  // GlobalKey 선언 => Form의 현재 상태를 관리하는데 사용한다!
  final _formKey = GlobalKey<FormState>();

  @override
  Widget build(BuildContext context) {
    // Form으로 감싸주고 formkey 할당
    // -> 키를 이용해 Form의 모든 자식 위젯에서 Form의 상태에 접근할 수 있음
    return Form(
      key: _formKey,
      child: Scaffold(
        appBar: AppBar(
          title: const Text('TextFormField 연습해볼까?'),
        ),
        body: Center(
          child: Padding(
            padding: const EdgeInsets.all(20.0),
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                TextFormField(
                  decoration: const InputDecoration(
                    labelText: '이메일',
                  ),
                  // 이 모드를 설정해주어야 실시간으로 validate 에러 메시지를 보여준다!
                  autovalidateMode: AutovalidateMode.always,
                  validator: (value) {
                    if (value == null || value.isEmpty) {
                      return '이메일을 입력해주세요.';
                    }
                    // 이 부분이 valid한 경우
                    return null;
                  },
                ),
                ......
              ],
            ),
          ),
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            // 이렇게 FormKey를 이용해 한번에 편리하게 validate 가능!
            if (_formKey.currentState!.validate()) {
              ScaffoldMessenger.of(context).showSnackBar(
                const SnackBar(
                  content: Text('가입 완료!'),
                ),
              );
            }
          },
          tooltip: '가입하기',
          child: const Icon(Icons.send),
        ),
      ),
    );
  }
}
```
<br/>









