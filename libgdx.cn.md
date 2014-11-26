Libgdx官方文档翻译

Tile maps

Maps
	Libgdx 提供一套公有的地图api。所有地图相关的类都可以在com.badlogic.gdx.maps包下找到，根目录下都是一些基础类，而次级目录则是tilemap或者其他形式地图的实现。
基础类
	为了不仅能适应tilemap还要兼容其他格式的地图，这组基础类必须公有。
	一张地图是一组层。一层包含一组对象。地图，层和对象都有一些基于地图格式的属性。我们专门为一些特殊格式的地图写了实现类。
	基类的层级如下图所示：
属性
	地图、图层和对象的属性由MapProperties来描述。这个类本质上来说是由属性名和属性值构成的hashmap。
	哪些键值对有用，取决于地图、图层和对象是基于哪种类型的地图的。你可以用以下方法轻松获取属性：
		map.getProperties().get("custom-property", String.class);
		layer.getProperties().get("another-property", Float.class);
		object.getProperties().get("foo", Boolean.class);
地图图层
	地图中的图层是有序的，第一个为0，你可以用下面的方法获取它：
	Maplayer layer = map.getLayers().get(0);
	你也可以用名字来获取：
	MapLayer layer = map.getLayers().get("my-layer");
	这些方法通常会返回一个Maplayer类，对于一些特殊的Maplayer你可以强制转换：
	TiledMapTileLayer tiledLayer = (TiledMapTileLayer)map.getLayers().get(0);
	每个层都有一些所有类型map都有的常规属性；
	String name = layer.getName();
	float opacity = layer.getOpacity();
	boolean isVisible = layer.isVisible();
	你可以修改这些属性来改变图层渲染。
	除了这些常规属性，你还可以用这些方法获取更多的公有属性。

	获取图层中的对象，非常简单：
	MapObjects objects = layer.getObjects();
	MapOBject实例允许你通过名称，索引和类型查找对象，你也可以快速插入或者删除对象。

地图对象
	API确实为专门的地图提供了一些非常有用的对象，比如CircleMapObject等等。
	该地图格式的加载器灰解析这些对象并将他们放入maplayer中。

	对于所有支持的格式，我们试图去提取如下的常规属性：
	String name = object.getName();
	float opacity = object.getOpacity();
	boolean isVisible = object.isVisible();
	Color color = object.getColor();
	一些特殊的地图对象 例如 PolygonMapObject 会有附加属性
	Polygon poly = polyObject.getPolygon();
	改变这些属性来改变对象的渲染。
	和maps layers一样，我么也可以获取更多的其他属性。

	提示：瓦片地图的瓦片不是对象哟~他们是特殊涂层。
地图渲染：
	MapRender 接口定义了一些方法允许你去渲染地图的图层和对象。
	开始渲染前，你必须设置地图上的view。
	想象这个view像你看到的窗口一样。最简单的方法是让map用OrthographicCamera去渲染：
	mapRenderer.setView(camera);
	你也可以手动的用矩阵定义一个边界：
	mapRenderer.setView(projectionMatrix, startX, startY, endx, endY);
	这个view的边界在x-y平面上，y轴朝上。
	这些单位使用对地图来说很特殊；渲染地图和图层很简单：
	mapRenderer.render();
	如果你想控制更多，你可以指定哪些图层需要去渲染。假如你有三个图层，两个背景和一个前景，你像去渲染处于前景和背景的自定义精灵，你可以这么做：
	int[] backgroundLayers = { 0, 1 }; // don't allocate every frame!
	int[] foregroundLayers = { 2 };    // don't allocate every frame!
	mapRenderer.render(backgroundLayers);
	renderMyCustomSprites();
	mapRenderer.render(foregroundLayers);
	通过单独渲染每个图层和修改图层的view，你也可以得到视差效果。

Tiled Maps
























