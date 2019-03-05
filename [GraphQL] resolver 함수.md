
resolver
=
GraphQL 쿼리의 각 필드는 타입을 반환하는 타입의 함수입니다.
타입의 각 필드는 GraphQL 서버개발자가 만든 resolver 함수에 의해 실행됩니다. **resolver 함수는 데이터베이스에 접근하여 객체를 생성하고 반환합니다.**

~~~
Query: {
  human(obj, args, context) {
    return context.db.loadHumanByID(args.id).then(
      userData => new Human(userData)
    )
  }
}
~~~
위의 예제에서 Query 타입은 id 값을 받아 human 필드를 반환합니다. 이 필드의 resolver 함수는 데이터베이스에 접근한 다음 Human 객체를 생성하고 반환합니다.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc5OTE1NzY0XX0=
-->