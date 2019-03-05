
Apollo
=

[Apollo Android](https://github.com/apollographql/apollo-android) 는 **Android 에서 GraphQL API를 쉽게 사용할 수있게 해주는GraphQL 클라이언트입니다.** Apollo는 네트워킹 클라이언트로 OkHTTP를 사용합니다. OkHTTP를 사용하여헤더와 인터셉터를 추가 할 수 있습니다.


Apollo CodeGen
=

**Apollo Codegen**는 ButterKnife와 같은 코드를 생성하는 그라디언트 플러그인이며, graphql 쿼리와 스키마를 가져와서 Java 클래스를 생성합니다. 또한 코드 생성을 통해 Apollo는 reflection없이 네트워크에서 응답을 읽고 unmarshalling 할 수 있습니다. 어떻게 작동하는지 알아 보겠습니다.

-   **java / res** 폴더 와 같은 레벨의 **src / main** 폴더를 만듭니다 . 그 안에 graphql 폴더를 추가합니다.
-   **schema.json** 파일을 graphql 폴더에 추가합니다. `apollo schema:download --endpoint= (something)schema.js` 
-   **.graphql 확장명** 을 가진 GraphQL 쿼리 파일을 같은 폴더에 추가하면이 쿼리가 apollo codegen에서 데이터 모델을 생성하는 데 사용됩니다.
- 스키마와 .graphql 파일을 추가 한 후 프로젝트를 다시 빌드합니다. Apollo는 쿼리와 스키마를 구문 분석하고 코드를 생성합니다. 빌드가 완료되면 **app / build / generated / source / graphql** 폴더 로 이동하여 생성 된 파일을 찾을 수 있습니다 . (이 파일은 Apollo가 생성하는 파일이므로 변경할 수 없습니다)


GraphQL API에 요청
=

생성된 클래스를 사용하여 GraphQL API에 요청할 수 있습니다.

~~~
apolloClient.query(
  FeedQuery.builder()
    .limit(10)
    .type(FeedType.HOT)
    .build()
).enqueue(new ApolloCall.Callback<FeedQuery.Data>() {

  @Override public void onResponse(@NotNull Response<FeedQuery.Data> dataResponse) {

    final StringBuffer buffer = new StringBuffer();
    for (FeedQuery.Data.Feed feed : dataResponse.data().feed()) {
      buffer.append("name:" + feed.repository().fragments().repositoryFragment().name());
      buffer.append(" owner: " + feed.repository().fragments().repositoryFragment().owner().login());
      buffer.append(" postedBy: " + feed.postedBy().login());
      buffer.append("\n~~~~~~~~~~~");
      buffer.append("\n\n");
    }

    // onResponse returns on a background thread. If you want to make UI updates make sure they are done on the Main Thread.
    MainActivity.this.runOnUiThread(new Runnable() {
      @Override public void run() {
        TextView txtResponse = (TextView) findViewById(R.id.txtResponse);
        txtResponse.setText(buffer.toString());
      }
    });
      
  }

  @Override public void onFailure(@NotNull Throwable t) {
    Log.e(TAG, t.getMessage(), t);
  }
});
~~~

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNTQxNzIyOTRdfQ==
-->