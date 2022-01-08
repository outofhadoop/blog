[TOC]


# Redux 核心概念

## State 

例如一个 TODO 的 state 可能会是下面这样, 就是一个简单的对象

```javascript

{
  todos: [{
    text: 'Eat food',
    completed: true
  }, {
    text: 'Exercise',
    completed: false
  }],
  visibilityFilter: 'SHOW_COMPLETED'
}

```

## Action  

描述发生了什么的对象

> 要想更新 state 中的数据，你需要发起一个 action
> actions 只是描述了有事情发生了这一事实，并没有描述应用如何更新 state。

```javascript

{ type: 'ADD_TODO', text: 'Go to swimming pool' }
{ type: 'TOGGLE_TODO', index: 1 }
{ type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }

```

创建 Action 的函数被称为 Action 创建函数

```javascript
// 一般都会统一写到一个文件中便于管理
const ADD_TODO = 'ADD_TODO'

function addTodo (text) {
  return {
    type: ADD_TODO,
    text,
  }
}
```



## Reducer

> 为了把 action 和 state 串起来，开发一些函数，这就是 reducer

> reducer 只是一个接收 state 和 action，并返回新的 state 的函数。

```javascript

function visibilityFilter(state = 'SHOW_ALL', action) {
  if (action.type === 'SET_VISIBILITY_FILTER') {
    return action.filter;
  } else {
    return state;
  }
}

function todos(state = [], action) {
  switch (action.type) {
  case 'ADD_TODO':
    return state.concat([{ text: action.text, completed: false }]);
  case 'TOGGLE_TODO':
    return state.map((todo, index) =>
      action.index === index ?
        { text: todo.text, completed: !todo.completed } :
        todo
   )
  default:
    return state;
  }
}

```

> 再写一个 reducer 来方便调用上面两个 reducer , 进而管理整个应用的 state

```javascript

function todoApp(state = {}, action) {
  return {
    todos: todos(state.todos, action),
    visibilityFilter: visibilityFilter(state.visibilityFilter, action)
  };
}

```

> 这差不多就是 Redux 思想的全部


## 三大原则

1. 单一数据源
2. State只读
3. 使用纯函数来执行修改


有兴趣可以去看一看 [redux 的来源](https://www.redux.org.cn/docs/introduction/PriorArt.html)



# 在 React 中使用

渲染一个简单的列表和输入框 , 列表展示输入框添加的数据 

```javascript
// 引入 react-redux connect 方法, 
import { connect } from "react-redux"


/**
 * Action Type
 */
// action 的所有类型应该单独定义在一个文件中便于管理
const ACTION_TYPE = {
  ADD_ITEM: 'ADD_ITEM'
}

/**
 * Reducer
 */
// 要展示的列表数据
const list = (state = [], action) => {
  switch (action.type) {
    case: ACTION_TYPE.ADD_ITEM:
      return [
        ...state,
        // 处理 action 带来的数据, 添加一项
        {
          id: action.id,
          text: action.text,
          status: false,
        }
      ]
    default: 
      return state
  }
}



```






























# 参考

[[1] Redux 中文文档](https://www.redux.org.cn/)
