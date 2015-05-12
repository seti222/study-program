#JavaScript MV* Framework 핵심 	
######원본 : http://www.sitepoint.com/anatomy-javascript-mv-framework/

JavaScript MV\* Framework 빠르게 익히는 바법의 공동된 Framework 의 특징을 익히는 것이다.
MV* Application 의 주요 특징으로는 Routing, Data Binding, Templates/Views, Models, Data Access 입니다. 이 글은 AngularJS, Backbone, Ember의 예제 코드와 주요 특징을 설명할 것이며, 각 Framework의 차이점과 공통점을 이해하는데 도움이 목표입니다.그리고 한 Framework 이 다른 Frameowork의 성공에서 무엇을 차용하고 추구하는지 알게 될 것입니다.

모든 코드에 대해서 이해해야 하는 것은 아닙니다. 우선은 Framework 가 어떻게 하는지 문제를 어떻게 해결했는지를 주목하십시오.

##Routing

Routing 은 URLs을 처리하는 함수의 작은 지도이지만 View 의 상태변환을 관리하기 위한 "state machine" 이라는 디자인패턴 구현에 관한 것입니다. 만얀 Server-side의 Rails, CakePHP, ASP.NET 등의 MVC Framework 의 Router를 써봤다면 JavaScript MV* Rounter는 클라이언트에서 사용하는 JavaSciprt routing 이라고 생각할 수 있습니다. 

이전의 브라우저에서 작업을 해보았다면 어떻게 동작하는지 놀랄 것입니다. Url 의 해쉬 Tag 뒤의 값에 따라서, HTML 의 push 상태를 설정되었거나, 해쉬 이전의 url 과 매치된 페이지에서 자바스크립트는 동작하는데 해쉬 이후 값에 따라서 처리됩니다. 

이제 코드를 보도록 합시다.

###Backbone Example

아래의 코드는 Backbone.js 에서 roungting 처리 간단한 예제입니다.
<iframe frameborder="0" height="600" src="http://jsfiddle.net/cmckeachie/WSX5E/embedded/js,html,result/light" width="100%"></iframe>

AppRounter Object 를 주목하십시오. routes 는 함수와 맵핑됩니다. 그 함수는 view Object에 있으며 URL 변경될때 화면에 DOM 일부를 추가하거나 관리합니다. Backbone.history.start() 는 URL 변경에 대해서 Backbone 이 hitory를 기록을 시작합니다.

###AngularJS Example

아래의 코드는 AngularJS 에서 roungting를 처리하는 간단한 예제입니다.
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/mtV62/embedded/js,html,result/light" width="100%" data-en_id="14380405"></iframe>

AngularJS는 Backbone 예제에서 쓰인 routes map 이 없고 templateUrl 과 Controller 함수로 처리되어 좀더 간단합니다.

###Ember Example

아래는 Ember의 routing 예제 코드입니다. 
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/QZW8T/embedded/js,html,result/light" width="100%" data-en_id="88713691"></iframe>

this.route 함수의 첫번째 Parameter는 "resource" Object의 ==rounteName== 이고 두번째 Paramter는 URL로 다른 두 Framework 보다 더 간결합니다. 이러한 파라메터 순서에서 path 값은 optional 하며 About 화면에 적용되어 있습니다. 위 예제에서 사용된 Ember templates 은 뒤의 Template section 에서 나오니 우선은 =={{outlet}}== 이 template이 들어가는 자리라고 알아두십시요.

##데이타 바인딩

데이타 바인딩은 Model의 변경을 View 를 업데이트 하거나 혹은 View 가 변경되어 모델을 추가적 코드 없이 자동으로 업데이트 하는 것입니다. 단방향 데이타 바인딩은 보통 모델의 변경을 View에 전달하는 것을 말합니다. 양뱡향 데이타 바인딩은 추가로 View 변경 즉시 모델에 적용하는 것입니다. 데이타 바인딩은 개발자가 작성할 많은 코드들을 제거하여 어플리케이션의 문제에 집중할 수 있게 해 줍니다.

###AngularJS Example
다음 예제는 양방향 데이터 바인딩를 AngularJS로 만들어진 예제입니다. input 상자에 텍스트를 입력하면 Welcome 메세지에 출력합니다. 
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/Y8Jg6/embedded/html,js,result/light" width="100%" data-en_id="79701689"></iframe>

###Backbone Example

Backbone 은 자동 바인딩이 아닙니다. 하지만 메뉴얼로 가능한데, 단방향 데이터 바인딩에서 model이 View를 업데이트 하는 방식이 매우 유용해서 이러한 방식으로 모델을 변경합니다. View 에서 모델을 연결하는 데이터 바인딩 방식이 일반적이지는 않습니다.

아래 소스가 양 방향 데이타 바인딩을 구현한 예입니다.
<iframe frameborder="0" height="400" src="http://jsfiddle.net/cmckeachie/7fGrD/embedded/js,html,result/light" width="100%" data-en_id="93344089"></iframe>

모델의 변경 이벤트와 view 그리고 View 에 모델을 가지고 와 그리는 프로퍼티이다. input 의 keyup 이벤트 리슨너 그리고 input 값을 가지고 모델을 변경한다. 하나의 view는 수정할 수 있는 하나의 모델을 가진다. 이 예제로 데이타 바인딩을 하는 방법을 어떻게 하는지 알수 있을 것이다. Backbone 에서 데이타바인딩을 위한 몇개의 플러그인들중에 하나이다. 

###Ember Exmaple

아래는 Ember 데이타바인딩 예제이다.
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/gXcfL/embedded/js,html,result/light" width="100%"></iframe>

Ember는 흔히 Handlebars 템플릿을 사용합니다만 "input helpers"를 프레임웍엑서 포함시켜 폼의 input 필드와 연결시킵니다. 예제에서 input의 =={{== 를 ==<== 로 변경하고 ==name== 프로퍼티에 값을 바인딩합니다.

##Templates/Views

Templates은 Html 페이지입니다. 다이나믹한 데이타을 포함한 표현식을 포함한 데이타 바인딩을 가진 Html의 작은 부분이기도 합니다. 화면에 로직이 적게하거나 없애는 것이 템플릿의 철학입니다. 템플릿에서 자바스크립트를 직업 포함하기도 합니다. 템플릿은 DOM 기반으로 하거나 다이나믹한 데이타를 DOM에서 삽입하여 사용하거나 문자열 기반으로 한다(동적인 부분의 문자열을 변경하거나 html 문자열로 취급한다.)

예제를 통해서 알아봅시다.

###AnaularJS Example

아래 AngularJS 의 템플릿 예제입니다.

<iframe frameborder="0" height="400" src="http://jsfiddle.net/cmckeachie/aq676/embedded/js,html,result/light" width="100%"></iframe>

이전의 라이팅 예제에 데이타바인딩을 더해서 템플릿을 어떻게 하는지 간단하게 살펴 볼수 있다. Html 의 ==Script== 태그를 사용해서 템플릿을 포함하는 jsfiddle.net 에서 쉽게 볼수 있다. 하지만 AngularJS 에서는 ==$routeProvider== 의 설정에 따라서 유효한 파일 경로인 ==templateUrl== 프로퍼티 값에 따라서 외부의 view를 사용할 수 있다.

큰 규모의 어플리케이션에서 템플릿을 사용하는 방법처리하는 것은 좋은 방법으로 [grunt-angular-templates](https://www.npmjs.com/package/grunt-angular-templates)를 사용해서 컴파일 타임시에 Angular ==$templateCache== 에 연결하고 등록하는 것입니다.

###Ember Example

아래는 Ember 의 템플릿 예제입니다.

<iframe frameborder="0" height="400" src="http://jsfiddle.net/cmckeachie/79e6c/embedded/js,html,result/light" width="100%"></iframe>

Ember Route 오브젝트는 모델을 표현하는 템플릿을 호출합니다. Route의 기본적인 템플릿, 데이타를 읽어들이는 리소스 관리라고 생각합니다. 만약 화려하고 어플리케이션의 상태를 저장하는 기능이 필요하다면 컨트롤러가 필요할것입니다.

###Backbone Example

이제 Backbone의 템플릿 예제입니다.

<iframe frameborder="0" height="400" src="http://jsfiddle.net/cmckeachie/hvqjG/embedded/js,html,result/light" width="100%"></iframe>

위의 예제는 Routing 소스를 수정한 것이지만, Html 은 View object에 템플릿 속성에 hard-code 되는 대신에 Html 페이지안에 있는 ==id==속성이 있는 ==script== 태그내에 있다(브라우저는 script type의 속성이 text/template인 템플릿을 보여주거나 실행하지 않는다). jQuery 셀럿터==script== 태그의 ==id== 를 사용하여 찾는다. 

##Models
모델은 보통 비지니스 오브젝트, 도메인 오브젝트 혹은 엔티티의 클라이언트 웹브라우저에서 버전을 말합니다. 일반적으로, 클라이언트 측의 MV* 프레임웍 모델의 기본 개념은 데이터 캡슐화되어야 하며, 애플리케이션의 데이터뿐만 아니라 임의의 동작에 대한 중심을 확립하는 것이다. 이 모델은 모델 데이터 일반적 DOM에 저장되어 서버 MVC 에 jQuery를 더한 구조와 대조 될 수있다.모델을 가짐으로써 목표 DOM로부터 데이터 및 상태를 제거하고 재사용 할 수있는 공통의 장소에 보관한다.

###Backbone Example
모델은 데이타를 가지고, Dom의 외부에서 유지하고, 다양한 뷰의 변화 이벤트를 전달하여 화면이 적절히 반응하게 하거나 필요한 모든 곳의 사용자 인터페이스를 업데이트 합니다. 사용자 인터페이스에 없는 하나의 모델을 가지게 됩니다.

<iframe frameborder="0" height="730" src="http://jsfiddle.net/cmckeachie/8AH3t/embedded/js,html,result/light" width="100%"></iframe>
이전의 데이타 바인딩 예제에서 동일한 Person Model Object를 보는 새 템플릿 과 view를 추가하였습니다. 이전에 Person model를 간단하게 즉석에서 선언했지만 이 예제에서는 Backbone.Model.extend()를 사용하여 모델의 prototype을 만드는 방법을 보여 기존 프로그램에서 보여주는 클래스와 비슷한 방식을 사용하였습니다. 두가지 예제 모두 Person model object(Change 이벤트)의 변화나, 업데이트 합니다. 하나의 데이타 소스를 가지고 많은 특정 Dom 엘리먼트의 호출을 캡슐화할 수 있으며 하나의 모델로 많은 Dom 엘리먼트에 정보를 제공할 수 있습니다.


###AngularJS Example
AngularJS에 어플리케이션의 상태에 관련해서 하나의 상태 모델이라는 것이 있습니다만, 평범한 자바스크립트 Object를 모델로 사용하고 ng-model property를 View에 추가합니다. ng-model은 자동으로 어플리케이션의 같은 모델을 연결한 Dom 엘리먼트를 업데이트하는 프로그램을 호출합니다.

아래 AngularJS 데이타 바인딩 예제는 ng-model 하나를 통해서 View의 두 부분을 업데이트합니다.
<iframe frameborder="0" height="300" src="http://jsfiddle.net/cmckeachie/k5GqX/embedded/html,js,result/light" width="100%"></iframe>

##DataAccess
DataAccess 는 어플리케이션을 위한 data 저장이나 가져오는 것에 대한 것입니다. 보통 Framework 는 JSON를 리턴하는 Api 를 호출하는 것을 가정했습니다.

###AngularJS Example

AngularJS는 두 가지 방법으로 데이터를 처리합니다. 첫번째는 메뉴얼 ajax 호출를 지원하는데 $http를 통해서 jQuery의 $.ajax와 유사한 방식으로 호출합니다. 백엔드가 엄격한 RESTful 서비스인 경우 서비스 호출이 간결한 $resource 클래스를 제공합니다.

==$http== Example
```
app.factory('myService', function($http) {
  return {
    getFooOldSchool: function(callback) {
      $http.get('foo.json').success(callback);
    }
  };
});
 
app.controller('MainCtrl', function($scope, myService) {
  myService.getFooOldSchool(function(data) {
    $scope.foo = data;
  });
});
```

==$resource== Example
```
//create a todo
var todo1 = new Todo();
todo1.foo = 'bar';
todo1.something = 123;
todo1.$save();
 
//get and update a todo
var todo2 = Todo.get({id: 123});
todo2.foo += '!';
todo2.$save();
 
//delete a todo
Todo.$delete({id: 123});
```

##Backbone Example

Backbone은 RESTful Api를 사용하는 것을 가정하지만, Backbone.sync() 메소드를 override 하여 대체 할 수 있습니다. 모델이 서버(the URL) 에 있는 resource 로 가져오거나  save()를 호출할 수 있습니다.

```
var UserModel = Backbone.Model.extend({
  urlRoot: '/user',
  defaults: {
    name: '',
    email: ''
  }
});
var user = new Usermodel();
// Notice that we haven't set an `id`
var userDetails = {
  name: 'Craig',
  email: 'craigmc@funnyant.com'
};
// Because we have not set an `id` the server will call
// POST /user with a payload of {name:'Craig', email: 'craigmc@funnyant.com'}
// The server should save the data and return a response containing the new `id`
user.save(userDetails, {
  success: function (user) {
    alert(user.toJSON());
  }
});
```

###Ember Example

Ember는 강력한 data persistence/data storage 를 제공하기 위해서 Core Framework에 존재하지 않고 별도의 Ember Data를 가지고 있습니다. 보통 대부분은 ActiveRecord(RubyOnRails)와 같은 서버의 ORM 기술을 찾고 많이 제공하지만 Ember Data는 브라우저상의 자바스크립트 환경에 맞게 설계되어 있습니다. 글 쓰는 시점에서 Ember Core Team이 Ember Data v1.0를 출시하였지만, 아직은 많은 Ember Project에서는 위의 예제중 AngularJS에서 $http 를 사용하는 것 처럼 jQuery의 $.ajax 를 사용하고 있습니다.

##결론

이글은 javascipt MV* 프레임웍이 제공하는 기능에 대한 통찰력과 유사하게 구현되어 있다는 사실을 독자에게 주고자 하는 것이다. 프레임웍의 기능을 이해하고 나면 여러 프레임웍을 빠르게 배우는게 쉬워지며, 여러분의 프로젝트에 적합한 것을 찾을 수 있게 됩니다. 

