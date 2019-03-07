프래그먼트
=
내용이 중복되는 필드를 최소 두번이상 반복하는 경우 재사용이 가능한fragment 라는 개념을 사용하여 이를 해소 할 수 있습니다.
~~~
** Query **
{
  leftComparison: hero(episode: EMPIRE) {
    ...comparisonFields
  }
  rightComparison: hero(episode: JEDI) {
    ...comparisonFields
  }
}

fragment comparisonFields on Character {
  name
  appearsIn
  friends {
    name
  }
}

** Response **
{
  "data": {
    "leftComparison": {
      "name": "Luke Skywalker",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ],
      "friends": [
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        },
        {
          "name": "C-3PO"
        },
        {
          "name": "R2-D2"
        }
      ]
    },
    "rightComparison": {
      "name": "R2-D2",
      "appearsIn": [
        "NEWHOPE",
        "EMPIRE",
        "JEDI"
      ],
      "friends": [
        {
          "name": "Luke Skywalker"
        },
        {
          "name": "Han Solo"
        },
        {
          "name": "Leia Organa"
        }
      ]
    }
  }
}
~~~

필드가 반복될 경우 위 쿼리가 꽤 반복될 것을 알 수 있습니다. 프래그먼트 개념은 복잡한 응용 프로그램의 데이터 요구사항을 작은 단위로 분할하는데 사용됩니다.


인라인 프래그먼트
=

다른 여러타입 시스템과 마찬가지로 GraphQL 스키마에는 인터페이스와 유니온 타입을 정의하는 기능이 포함되어있습니다. 인터페이스나 유니온 타입을 반환하는 필드를 쿼리하는 경우, 인라인 프래그먼트를 사용해야합니다.

~~~

** Query **
query HeroForEpisode($ep: Episode!) {
  hero(episode: $ep) {
    name
    ... on Droid {
      primaryFunction
    }
    ... on Human {
      height
    }
  }
}
-------------------------------
{
  "ep": "JEDI"
}

** Response **
{
  "data": {
    "hero": {
      "name": "R2-D2",
      "primaryFunction": "Astromech"
    }
  }
}

~~~

이 쿼리에서 hero 필드는 episode 인자에 따라서 Human이나 Droid중 하나일 수 있습니다. 필드를 직접 선택할 때에는 name과 같이 character 인터페이스에 존재하는 필드만 요청할 수 있습니다. 특정한 타입의 필드를 요청하려면 타입 조건과 함께 인라인 프래그먼트를 사용해야합니다. 첫번째 프래그먼트는 ...On Droid 라는 레이블이 있기 때문에 PrimaryFunction 필드는 hero에서 반환된 character가 Droid타입인 경우에만 실행됩니다. Human 타입의 height 필드도 마찬가지 입니다.
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzIyNTYyNDZdfQ==
-->