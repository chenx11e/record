# record

就想随便写写

## 1-lazy-load 图片懒加载

1. 首先，将需要懒加载的图片的src属性保存在一个自定义的属性中，比如**data-src**。
2. 当页面加载完成时，获取所有需要懒加载的图片标签，并将它们的src属性设置为空字符串。
3. **监听页面的滚动事件**，当滚动到需要懒加载的图片时，将保存在data-src属性中的图片地址赋值给图片的src属性，然后将data-src属性置为空字符串，这样就可以实现懒加载了。



## 2.下拉刷新和触底加载

当用户在移动端下拉页面到达顶部时，会触发下拉刷新的功能，重新加载最新的数据。当用户滚动页面到达底部时，会触发触底加载的功能，加载更多的数据。

具体实现：

1. 定义了两个变量 `isLoading` 和 `isRefreshing`，用于标记当前是否在加载数据和刷新数据中，防止同时发起多个请求。
2. 定义了一个 `loadData` 函数，用于加载更多的数据。当加载数据时，先判断当前是否正在加载数据，避免重复请求。然后通过 `setTimeout` 模拟异步请求数据，向列表中添加10个新的列表项，最后将 `isLoading` 变量设置为 `false`，表示加载数据完成。
3. 定义了一个 `refreshData` 函数，用于下拉刷新数据。当下拉刷新时，先判断当前是否正在刷新数据，避免重复请求。然后通过 `setTimeout` 模拟异步请求数据，清空列表中原有的内容，重新加载数据，最后将 `isRefreshing` 变量设置为 `false`，表示刷新数据完成。
4. 给窗口添加了 `scroll` 事件监听器，当页面滚动到底部时触发 `loadData` 函数，加载更多的数据。
5. 给页面顶部的内容容器 `content` 添加了 `touchstart` 事件监听器，记录下当前触摸的位置。在触摸移动时，如果滑动到页面的顶部，且滚动条的位置为0，就认为用户进行了下拉刷新，此时触发 `refreshData` 函数，刷新数据。
6. 最后，在页面加载完毕后，调用 `loadData` 函数，首次加载数据。

