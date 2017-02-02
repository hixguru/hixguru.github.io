---
layout: "post"
title: "[Javascript] 전화번호 입력시 Auto Dash"
date: "2017-02-02 23:33"
---

### 전화번호 입력시 Auto Dash 기능

웹 페이지에서 회원가입 할 때와 같은 경우 대부분 핸드폰 번호를 입력하기 마련이다. 이 때 사용자에게 `-을 제외한 숫자만 입력해주세요` 와 같은 가이드를 줄 수 있지만, 숫자만 입력했을 때 자동으로 `-`가 붙는다면 사용자에게 더 좋은 경험을 줄 수 있을 것이다. 간단한 기능인 것 같지만 의외로 마음에 드는 예제가 없어서 직접 여러 코드를 참조하여서 만들었다. 이 또한 완벽한 방법도 아니고 모든 케이스에 대한 처리가 된 것은 아니지만, 내가 보기 편한 코드를 만들어보자 해서 작성하게 됐다.

- 아마 대부분 리액트를 사용하지 않는다면, JQuery를 사용하여서 이벤트 핸들링을 할 것이다. 구체적인 코드는 직접 작성해보기 바란다. 대략적인 이벤트 핸들링 코드는

```javascript
$('.foo').keyup(function(e) {
  if (e.keyCode === BACK_SAPCE_KEY) return; // BACK SPACE의 경우 해당 로직을 태우지 않는다.
  var phoneNumber = getPhoneNumberWithHyphen($(this).val());
  $(this).val(phoneNumber);
});

function getPhoneNumberWithDash(phoneNumber) {
  var length = phoneNumber.length;
  var numRegex = /^[0-9-]*$/;
  var twoUnitRegex = /^(01[0|1|6|7|8|9])([0-9])$/;
  var threeUnitRegex = /^(01[0|1|6|7|8|9])-?([0-9]{4})([0-9])$/;
  var finalUnitRegex = /^(01[0|1|6|7|8|9])-?([0-9]{3,4})-?([0-9]{4})$/;

  if (!numRegex.test(phoneNumber)) {
    alert('숫자만 입력이 가능합니다.');
    return phoneNumber.substring(0, length - 1);
  }

  if (length === 4) return phoneNumber.replace(twoUnitRegex, '$1-$2');
  if (length === 9) return phoneNumber.replace(threeUnitRegex, '$1-$2-$3');
  if (length >= 12) return phoneNumber.split('-').join('').replace(finalUnitRegex, '$1-$2-$3');

  return phoneNumber;
}
```

사실 위의 코드를 작성할 때 애매했던 부분은 더이상 누가 쓰고 있을지 모를 011, 016, 018, 019 에 대한 middle number의 3자리 처리였다. 기본적인 동작은 3자리 입력 후(010-4) 4자리 입력했을 때 사이에 `-` 추가 8자리 입력 후(010-1234-5) 9자리 입력했을 때 사이에 `-`를 추가하고, 마지막 12자리 13자리 있을 때 자리를 재배열하는 식으로 작성했다. 대부분의 예제처럼 swith & if & if & if.. 노가다로 처리할 수 있겠지만, 그래도 좀 더 깔끔한 코드를 써보고자 했기에 정규표현식이랑 조합하여 만들어봤다. 부디 다른 분들에게 도움이 되기를.. 또는 더 좋은 로직이 있으면 언제든지 댓글 부탁드립니다 : D
