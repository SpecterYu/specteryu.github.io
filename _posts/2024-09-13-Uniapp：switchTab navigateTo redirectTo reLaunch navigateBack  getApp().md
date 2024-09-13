# Uniapp中的页面跳转方式——switchTab、navigateTo、redirectTo、reLaunch和navigateBack

在Uniapp中，我们经常需要进行页面之间的跳转，以实现不同页面之间的交互和流程控制。Uniapp提供了几种不同的页面跳转方式，适用于不同的跳转场景。本文将详细介绍Uniapp中的五种页面跳转方式：switchTab、navigateTo、redirectTo、reLaunch和navigateBack。

## switchTab

在Uniapp中，通过使用`switchTab`方法可以实现Tab切换效果。该方法用于跳转到具有`"tabBar"`属性的页面，并且不会关闭其他非`tabBar`的页面。

```markdown
uni.switchTab({
  url: '/pages/tabbar/home'   // 跳转的页面路径
})
```

通过`switchTab`跳转页面时，URL中只需填写要跳转的Tab页面的路径即可。需要注意的是，该方法不支持传递参数给目标页面。

## navigateTo

`navigateTo`方法用于打开新页面，可以在Navigator栏显示并支持返回操作。在新页面打开的同时，原页面仍然存在，不会被关闭。

```markdown
uni.navigateTo({
  url: '/pages/detail?id=1'   // 跳转的页面路径，可以带参数
})
```

通过`navigateTo`跳转页面时，URL中可以传递参数，以供目标页面使用。

## redirectTo

`redirectTo`方法用于关闭当前页面并打开新页面。新页面将替换当前页面，显示在页面栈的最上方。

```markdown
uni.redirectTo({
  url: '/pages/login'   // 跳转的页面路径
})
```

通过`redirectTo`跳转页面时，当前页面将被关闭，被替换成新的页面。

## reLaunch

`reLaunch`方法用于关闭所有页面并打开新页面。新页面将成为页面栈中的第一个页面。

```markdown
uni.reLaunch({
  url: '/pages/index'   // 跳转的页面路径
})
```

通过`reLaunch`跳转页面时，所有页面都将被关闭，只打开新的页面。

## navigateBack

`navigateBack`方法用于返回上一个页面。

```markdown
uni.navigateBack()
```

通过`navigateBack`跳转页面时，将返回上一个页面。该方法也可以接收一个参数，代表返回的层数。

## 总结

以上就是Uniapp中常用的五种页面跳转方式。根据实际需求，我们可以选择合适的方法进行页面跳转。记得在进行页面跳转时，根据实际情况选择使用不同的跳转方式，以实现最佳的用户体验。

希望本文能为你提供一些关于Uniapp页面跳转的帮助和指导。如果你有任何疑问或建议，欢迎留言讨论！
参考文献：

1. [Uniapp：编译器#ifdef --- #endif](https://www.jjblogs.com/post/1135879)
