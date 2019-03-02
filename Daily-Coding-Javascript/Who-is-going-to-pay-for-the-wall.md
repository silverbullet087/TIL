Daily Codewars #2019-03-02
--------------------------

### Question

**문제링크** : [[8 kyu]Who is going to pay for the wall?](https://www.codewars.com/kata/who-is-going-to-pay-for-the-wall)

Don Drumphet lives in a nice neighborhood, but one of his neighbors has started to let his house go. Don Drumphet wants to build a wall between his house and his neighbor’s, and is trying to get the neighborhood association to pay for it. He begins to solicit his neighbors to petition to get the association to build the wall. Unfortunately for Don Drumphet, he cannot read very well, has a very limited attention span, and can only remember two letters from each of his neighbors’ names. As he collects signatures, he insists that his neighbors keep truncating their names until two letters remain, and he can finally read them.

Your code will show Full name of the neighbor and the truncated version of the name as an array. If the number of the characters in name is equal or less than two, it will return an array containing only the name as is"

```javascript
     assert.ok( whoIsPaying("Mexico") == ["Mexico", "Me"], "Passed!" );
      assert.ok( whoIsPaying("Melania") == ["Melania", "Me"], "Passed!" );
      assert.ok( whoIsPaying("Melissa") == ["Melissa", "Me"], "Passed!" );
      assert.ok( whoIsPaying("Me") == ["Me"], "Passed!" );
      assert.ok( whoIsPaying("") == [""], "Passed!" );
      assert.ok( whoIsPaying("I") == ["I"], "Passed!" );
```

### My Solution

```javascript
function whoIsPaying(name){
    var result = [];

		if (name.length == 0) {
			result.push("");
			return result;
		}

		if (name.length < 3) {
			result.push(name)
			return result;
		}

		result.push(name);
		result.push(name.substring(0,2));

		return result;
}
```

### @osofem Solution

```javascript
function whoIsPaying(name){
  return (name.length>2)?([name, name.substr(0,2)]):[name];
}
```

> 한줄이면 되는구나... 내가 쓸데없이 배열에 push해서 코딩했던 것 같다. 조건연산자까지 사용해서 소스가 더 심플해졌다.

### @norb_borb Solution

```javascript
function whoIsPaying(name){
  if (name.length <= 2) return [name]
  return [name, name.slice(0, 2)]
}
```

> 이분은 조건연산자는 사용하지 않았고 심플하게 코딩했다.

### @njohnson7 Solution

```javascript
const whoIsPaying = name =>
      [...new Set([name, name.slice(0, 2)])]
```

> 이건 ES6 코딩방법인가...잘 모르겠다.

### 결론

-	굳이 배열에 push해서 하지 않고도 개발 가능한 코드였다.
-	두가지 분기로 처리 가능한 케이스 였고 조건연산자를 사용해서 심플하게 코딩 가능했다.
-	ES6 공부를 해야하는데...
