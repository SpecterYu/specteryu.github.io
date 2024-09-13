# Uniapp：uni-app中Vue3生命周期

在Uniapp中，Vue3相比于Vue2版本增加了一些新的生命周期钩子。这些新的生命周期钩子为开发者提供了更多的灵活性和控制权。本文将介绍Vue3中新增的生命周期钩子`beforeUnmount`、`unmounted`、`renderTracked`和`renderTriggered`。

## beforeUnmount

`beforeUnmount`是Vue3中引入的一个新的生命周期钩子。它会在组件销毁之前被调用，可以用来进行一些清理工作，例如关闭网络请求、清理定时器等。在该钩子函数内，你可以访问组件的`props`、`data`、`computed`以及`methods`。

```javascript
export default {
  beforeUnmount() {
    // 在组件销毁之前执行清理操作
  },
};
```

## unmounted

`unmounted`是Vue3中另一个新增的生命周期钩子。它会在组件销毁之后被调用，可以用来进行一些最后的清理工作，例如清理事件监听器、解绑全局事件等。在该钩子函数内，你不能再访问组件的任何属性和方法，因为它们已经被销毁了。

```javascript
export default {
  unmounted() {
    // 在组件销毁之后执行最后的清理操作
  },
};
```

## renderTracked

`renderTracked`是Vue3中一个用于追踪渲染时候的钩子函数。它会在组件的渲染过程中被调用，并且每个被追踪的响应式属性都会触发该钩子函数的调用。在该钩子函数内，你可以获取到触发渲染的属性名和当前组件实例。

```javascript
export default {
  renderTracked(effects) {
    // 在渲染时追踪到更新响应式属性时调用
    effects.forEach((effect) => {
      console.log(`Render tracked: ${effect.name}`);
      console.log(`Component instance: ${this}`);
    });
  },
};
```

## renderTriggered

`renderTriggered`是Vue3中与`renderTracked`相对应的钩子函数。它会在组件的渲染过程中被调用，并且每个被追踪的响应式属性的更新都会触发该钩子函数的调用。与`renderTracked`不同的是，`renderTriggered`会在属性更新后立即调用。

```javascript
export default {
  renderTriggered(effects) {
    // 渲染时跟踪到响应式属性更新后调用
    effects.forEach((effect) => {
      console.log(`Render triggered: ${effect.name}`);
      console.log(`Component instance: ${this}`);
    });
  },
};
```

以上就是Uniapp中Vue3新增的四个生命周期钩子的介绍。通过使用这些新的生命周期钩子，我们可以更好地控制组件的生命周期，实现更加精细的逻辑处理。希望本文能对你在使用Uniapp开发过程中有所帮助！
参考文献：

1. [Uniapp：uni-app中vue2生命周期--11个](https://www.jjblogs.com/post/114333)
