Daily Codewars #2019-03-01
--------------------------

### Question

**문제링크** : [[8 kyu]What's up next?](https://www.codewars.com/kata/whats-up-next)

Given a sequence of items and a specific item in that sequence, return the item immediately following the item specified. If the item occurs more than once in a sequence, return the item after the first occurence. This should work for a sequence of any type.

When the item isn't present or nothing follows it, the function should return nil in Clojure and Elixir, Nothing in Haskell, undefined in JavaScript, None in Python.

```
(next-item (range 1 10000) 7) ;=> 8
(next-item ["Joe" "Bob" "Sally"] "Bob") ;=> "Sally"
```

### My Solution

```javascript
function nextItem(xs, item) {

		var finalValue;
		var exists = false;

		for (var i of xs) {
			if (exists) {
				finalValue = i;
				break;
			}

			if (i === item) {
				exists = true;
			}
		}

		return finalValue;

	}
```

> 처음에는 엄청 쉬울줄 알았는데. **Generator functions** 이 테스트 케이스에 있어서 엄청 고생하고 코딩하는데 시간이 많이 걸렸다. **Generator functions** 을 이번에 처음 알게 되어서 일반적인 for문에서 배열[index]가 오류가 발생하여 일반적인 방법으로 for문이 실행이 되지 않아 너무 고생했다.

### @zvytas Solution

```javascript
function nextItem(xs, item) {
  var found = false;
  for (var x of xs) {
    if (found) return x;
    if (x == item) found = true;
  }
  return undefined;
}
```

> **Generator functions** 까지 고려해서 for ( of )를 사용했다. 값을 못찾을시 undefined에 대한 고려와 값 찾을시 return이 잘 개발 되어 있다.

### @acraileanu Solution

```javascript
function nextItem(xs, item){
  var iterator = xs[Symbol.iterator]();
  var found = false, x;
  while ((x = iterator.next()) && !found)
  {
    if (x.done){
      return undefined;
    }
    if (x.value == item){
      found = true;
    }
  }
  return x.value;
}
```

> 일반 배열과 **Generator functions** 이 파라미터로 같이 존재하여 해당 타입별 처리가 까다로웠는데요. 이 사람은 **var iterator = xs\[Symbol.iterator];** 를 사용해서 배열도 iterator 로 변환해서 그 문제를 해결했다. 이런 방법도 있다는 것을 처음 알았다.

### @YOSYA Solution

```javascript
function nextItem(xs, item) {
  console.log(item)
  if (xs.length==undefined)
  {
    var arr=[];
    for (var i=0; i<=item; ++i)
      arr.push(xs.next());
      console.log(arr[660]);
    for (var i=0; i<arr.length; ++i)
      if (arr[i].value==item)
        return arr[i+1].value;
    return undefined;
  }
  return xs.indexOf(item)==-1?undefined:xs[xs.indexOf(item)+1]
}
```

> 나와 같은 **Generator functions** 과 배열문제를 **xs.length==undefined** 로 분기해서 처리했다. 배열에서 **xs.indexOf(item)==-1** 을 사용한 것도 인상적이다.

### 결론

-	Generator functions 은 for ( of ) 를 사용해서 for문을 돌린다.
-	var iterator = xs\[Symbol.iterator](); 으로 배열을 iterator로 만들 수 있다.
-	array.indexOf(item)==-1 로 배열에 값 존재 여부를 확인 할 수 있다.
-	javascript 문제는 처음 풀어 보았는데 ES6에 대한 공부가 필요한 것 같다.
