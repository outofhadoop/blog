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

```javascript

{ type: 'ADD_TODO', text: 'Go to swimming pool' }
{ type: 'TOGGLE_TODO', index: 1 }
{ type: 'SET_VISIBILITY_FILTER', filter: 'SHOW_ALL' }

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


































# 参考

[[1] Redux 中文文档](https://www.redux.org.cn/)