#### preLoader设计

- 在Application.onCreate中加载地址数据，在需要用到地址的页面中获取预加载的数据
- 在启动页中预加载app主页所需的数据，减少用户等待时间
- startActivity之前就开始预加载，UI初始化完成后显示预加载的数据
- 复杂页面(UI初始化耗时较多的页面)内部在UI初始化开始之前预加载数据，UI初始化完成后显示预加载的数据
-  ListView/RecyclerView在上拉加载更多之前预加载下一页的数据

