Daily Codewars #2019-03-06
--------------------------

### Question

**문제링크** : [[8 kyu]DNA to RNA Conversion](https://www.codewars.com/kata/dna-to-rna-conversion)

Deoxyribonucleic acid, DNA is the primary information storage molecule in biological systems. It is composed of four nucleic acid bases Guanine ('G'), Cytosine ('C'), Adenine ('A'), and Thymine ('T').

Ribonucleic acid, RNA, is the primary messenger molecule in cells. RNA differs slightly from DNA its chemical structure and contains no Thymine. In RNA Thymine is replaced by another nucleic acid Uracil ('U').

Create a funciton which translates a given DNA string into RNA.

For example:

`new Bio().dnaToRna("GCAT") // returns "GCAU"`

The input string can be of arbitrary length - in particular, it may be empty. All input is guaranteed to be valid, i.e. each input string will only ever consist of `'G'`, `'C'`, `'A'` and/or `'T'`.

### My Solution

```java
public class Bio {
    public String dnaToRna(String dna) {
        return dna.replace("T", "U");
    }
}
```

> 너무 쉬운데...7 kyu를 해야할려나...

### @bekh6ex Solution

```java
public class Bio{
    public String dnaToRna(String dna){
        return dna.replace("T", "U");
    }
}
```

> replace가 하나만 나꾸는줄 알았는데 다 바뀐다는걸 알게 되었다. 오늘 회사 업무에서도 replace로 전체를 다 바꾸는 소스를 봤었는데 다시 한번 알게 되었다.

### @free_sBaitso Solution

```java
public class Bio {
    public String dnaToRna(String dna) {
      String str = dna.replaceAll("T","U");
      return str;  // Do your magic!
    }
}

```

> 나와 동일하다.

### 결론

-	replace와 replaceAll의 차이점을 알게 되었다.
-	replace는 문자 그대로 인식한다.
-	replaceAll은 정규표현식으로 인식한다.
-	replaceAll로 정규표현식으로 원치 않는 결과를 얻을 수도 있다.
-	replace가 전체 다 특정 문자열을 원하는 문자열로 치환한다는 것을 알고 있자.
