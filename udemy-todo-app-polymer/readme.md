# TODO APP POLYMER
## 1.0.0 project init
* enable git 
* create git ignore (.idea,bower_components)
* terminal bower init
* bower init

## 1.0.1 install polymer
* bower install --save Polymer/polymer#^1.1.4 -> polymer
* bower install --save PolymerElements/iron-elements#^1.0.0 -> https://elements.polymer-project.org/browse?package=iron-elements
* bower install --save PolymerElements/paper-elements#^1.0.1 -> https://elements.polymer-project.org/browse?package=paper-elements

## 1.0.2 index.html
* create index.html
* <script src="bower_components/webcomponentsjs/webcomponents-lite.js"></script> for polymer

## 1.0.3 todo-data
* create elements folder for our elements
* create todo-data.html for todo-data element
* add todo data dom element -> https://www.polymer-project.org/1.0/docs/start/quick-tour.html#add-local-dom
* create dom module with properties todo-data
* notify:true for two way binding
* create elements.html for import your elements
* import elemets.html from index.html
* in todo-data create template for visualize data 
* data binding  {{???}} -> https://www.polymer-project.org/1.0/docs/devguide/data-binding.html
* in template write "Todos : <span>{{todos}}</span> " run but it's wrong Object:Object
* so we put some function _toJSON function its create object json
* Todos : <span>\[\[_toJSON(todos)]]</span><br/> right one 

## 1.0.4 todo-view
* create todo-view.html
* add todo-view.html to elements.html (remove <link rel="import" href="../bower_components/paper-drawer-panel/paper-drawer-panel.html">)
* remove todo-data unnessary codes
* bind todos todo-data to todo-view  <todo-data todos={{todos}} <todo-view todos={{todos}} two todos are sycn
* change index.html 

## 1.0.5 todo-list
* create todo-list.html
* import todo-list.html from todo-view.html
* show no todos message for empty todos
* template dom-repeat -> https://www.polymer-project.org/1.0/docs/devguide/templates.html

## 1.0.6 todo-item
* create todo-item.html
* import todo-item.html from todo-list.html
* todo-item.html todo import object
* replace span to todo-item in todo-list  <todo-item todo="{{todo}}"></todo-item>

## 1.0.7 todo-item check-box
* add paper-checkbox.html to todo-item -> https://elements.polymer-project.org/elements/paper-checkbox
* add remove span and add paper-checkbox <paper-checkbox checked="{{todo.done}}">{{todo.name}}</paper-checkbox>

## 1.0.8 todo-list filter
* filter by done so we have all, completed, uncompleted
* we need an property for filterBy add filterBy property to todo-list.html default value = all
* create a function _filter function
* add filter attr to template filter="{{_computeFilter(filterBy)}}"
* add filterBy (filter-by) property to todo-list in todo-view change all, completed, uncompleted
    show them 
    <todo-list todos="{{todos}}" filter-by="completed"></todo-list>
    <todo-list todos="{{todos}}" filter-by="uncompleted"></todo-list>
    <todo-list todos="{{todos}}" filter-by="all"></todo-list>
* something wrong becuse when you complete or uncomplete item view doesn't refresh so add observe="done" to todo-item 
  templete so observe to done propterty for items if anything change it triggers the filter agian
  
## 1.0.9 todo-input
* add some style first for layout horizontal vertical layout something so we use iron elements for this iron flex layout https://elements.polymer-project.org/elements/iron-flex-layout
* put iron lemets url to elements.html
* so in todo-view creat layout hozriontal for split screen into two put list to left flex-6 (col6 for bootstrap) 
* create todo-input.html it, we use here paper-input and we need paper-button https://elements.polymer-project.org/elements/paper-button,https://elements.polymer-project.org/elements/paper-input
* import todo-input.html into todo-view add insert into right side of screen and add handlers for add function https://www.polymer-project.org/1.0/docs/migration.html#declarative-handlers
    on-add-todo="_addTodo"
    and create _addTodo function into todo-view.html its push new item into todos
* now we create _add function into todo-input check value if has value send add-todo event to parent view (todo-view)
* add on-keydown evetn paper-input to understand user pressed enter add _checkAdd method to if user pressed enter call add method

## 1.0.10 some ui
* change todo-view make some padding left and right 
* Make 2 list Todos and Completed Todos 

## 1.0.11 search in todos
* add query property to todo-list
* add paper input to view  (add<link rel="import" href="../bower_components/paper-input/paper-input.html"> to todo-view) and add paper input
* value is query and add query propties to todo and completed todo-list
* add queryChange method to todo-list property if query changed call filter method (!!!!!!!!!!!!!!ignore this)
* and change filter method

## 1.0.12 archive All button
* first add archive button between Todo's and completed todo's
* create _calcHasCompletedTodos method for this use underscore bower install underscore --save and add to index html 
    <script src="bower_components/underscore/underscore.js"></script> (http://underscorejs.org/)
* _calcHasCompletedTodos set hasCompletedTodos value
* use observer here define observers in tod0-view.html observers: ['_calcHideCompletedTodos(todos.*)' ]  call _calcHideCompletedTodos when todos.array size changed
* add Archive All papaer-button 

## 1.0.13 archive
* implement _archiveAll function 
* add hideArchive property to todo-list.html (fix iif hideArchive exists true not exists false  in code this is not like that)
* add hideArchive to _filter method in todo-list.html
*---!!!!!!!!!!!!!!! Fix it
 in todo-list.html
hideArchive: {
          type: Boolean,
          value: false
        }
-- int todo-view.html
<todo-list todos="{{todos}}" filter-by="uncompleted" query="{{query}}"></todo-list>  /////// <todo-list todos="{{todos}}" filter-by="uncompleted" query="{{query}}" hide-archive></todo-list>
<todo-list todos="{{todos}}" filter-by="completed" query="{{query}}"
                   hidden="{{hideCompletedTodos}}"></todo-list>  /////// <todo-list todos="{{todos}}" filter-by="completed" query="{{query}}"
                                                                                            hidden="{{hideCompletedTodos}}" hide-archive></todo-list>

## 1.0.14 some ui add header and navigation
* paper-toolbar.html, paper-tabs, iron-pages added to elements.html
* create a paper panel creat tag <div class="app-name">Do</div> creat call app-name make it bold
* then cretae paper-tabs for navigation add Home and archive 
* add div for content and add iron-pages first one containt home other contains archive
* for now archive only has placeholder writes archive 
* and app first opened doesn't show anything becasuse selected is not set

## 1.0.15 some routing
* we use https://github.com/visionmedia/page.js/ this 
* from terminal bower install --save visionmedia/page.js#^1.6.3
* create routing.html
* add routing / -> home means selected tab 0, /archive-> archive sleected tab 1
* add routing.html to elements.html
* for app variable we have to set this so create app.js
* index.html template id is app

## 1.0.16 archive screen
* create todo-archive-view.html has only search input todos list but hidearcive is false and filterBy all
* and add todo-archive.view.html to elements.html
* now change todo-item.html for archive items.
* todo-list change _filter funciton

## 1.0.17 todo-item for archived items
* add archive property to new items
* change todo-item for two if archived and not archived 
* add iron-icons and paper-icon-button for undo 
* add _undo funciton
* ups list doesn't update so add observer