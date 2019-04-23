Git push가 안되는 경우 (refusing to merge unrelated histories)
=
깃허브 사이트를 통해 만든 저장소에 로컬에 있는 프로젝트를 push 하는 경우에 `refusing to merge unrelated histories`	라는 에러가 뜨면서 안되는 경우가 있다.

push 전에 프로젝트를 병합해줘야한다
`git pull origin [branch name] --allow-unrelated-histories`

이미 존재하는 두 프로젝트의 기록(history)을 저장하는 드문 상황에 사용된다고 한다. 즉, git에서는 서로 관련 기록이 없는 이질적인 두 프로젝트를 병합할 때 기본적으로 거부하는데, 이것을 허용해 주는 것이다.



-----
참고 : [https://gdtbgl93.tistory.com/63](https://gdtbgl93.tistory.com/63)


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExNjI0OTQ5MzJdfQ==
-->