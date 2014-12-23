#JavaScript MV* Framework 핵심 [원본](http://www.sitepoint.com/anatomy-javascript-mv-framework/)

JavaScript MV\* Framework 빠르게 익히는 바법의 공동된 Framework 의 특징을 익히는 것이다.
MV* Application 의 주요 특징으로는 Routing, Data Binding, Templates/Views, Models, Data Access 이다. 이 글은 AngularJS, Backbone, Ember의 예제 코드와 주요 특징을 설명할 것이다. 각 Framework의 차이점과 공통점을 이해하는데 도움이 될 것이다. 이러한 것으로 그 Framework 이 다른 Frameowork의 성공에서 무엇을 가져오고 추구하는지 알게 될것이다. 

모든 코드에 대해서 이해 해야하는 것인지 걱정하지 말아라. 우선은 Framework 가 어떻게 하는지 문제를 어떻게 해결했는지를 주목하라. 

##Routing

Routing 은 URLs을 처리하는 함수의 작은 지도이지만 View 의 상태변환을 관리하기 위한 "state machine" 디자인패턴 구현에 관한 것이다. 만얀 Server-side의 Rails, CakePHP, ASP.NET 등등의 MVC Framework 의 Router를 써봤다면 JavaScript MV* Rount는 클라이언트에서 사용하는 JavaSciprt routing 이라고 생각할 수 있을 것이다. 

이전의 브라우저에서 작업을 해보았다면 어떻게 동작하는지 놀랄 것이다. Url 의 해쉬 Tag 뒤의 값에 따라서, HTML 의 push 상태를 설정되었거나, 해쉬 이전의 url 과 매치된 페이지에서 자바스크립트는 동작하는데 해쉬 이후 값에 따라서 처리된다. 

이제 코드를 보도록하자.

###Backbone Example

아래의 코드는 Backbone.js 에서 roungting 처리 간단한 예제이다.
<iframe frameborder="0" height="600" src="http://jsfiddle.net/cmckeachie/WSX5E/embedded/js,html,result/light" width="100%"></iframe>

AppRounter Object 를 주복하자. routes 는 함수와 맵핑된다. 그 함수는 view Object에 있으며 URL 변경될때 화면에 DOM 일부를 추가하거나 관리한다. Backbone.history.start() 는 URL 변경에 대해서 Backbone 이 감시를 시작한다.

###AngularJS Example

아래의 코드는 AngularJS 에서 roungting 처리 간단한 예제이다.
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/mtV62/embedded/js,html,result/light" width="100%" data-en_id="14380405"></iframe>

AngularJS는 Backbone 예제의 routes map 이 없고 templateUrl 과 Controller 함수로 처리하여 더욱 Simple 하다.

###Ember Example

아래는 Ember의 routing 예제 코드이다. 
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/QZW8T/embedded/js,html,result/light" width="100%" data-en_id="88713691"></iframe>

Ember.js 의 첫번째 Parameter는 router의 resource Object의 rounteName 이고 두번째 Paramter는 URL로 다른 두 Framework 보다 더욱 간단하다. 이러한 path의 설정은 선택적이고 자주이거나 나에게는 혼란스러워서 About 화면과 같은 규칙을 적용한다. 위 예제에서 사용된 Ember templates 은 뒤의 Template section 에서 나오니 우선은 {{outlet}} 이 template이 들어가는 자리라고 알아두자.