
# ERPageController

## 带编辑菜单的分页选择器

<br/>

![gif](http://www.code4app.com/data/attachment/forum/201707/07/153006zi63kbnk68ttw74r.gif)

### 使用方法:

### 特别声明: 数据模型我使用的是``` (NSMutableArray <NSDictionary *> *)  ``` 通过 "name" 获取页面标题 (可根据自己需求更改)

### 初始化控件

```
    ERSegmentController *pageManager = [[ERSegmentController alloc] init];
    pageManager.view.frame = CGRectMake(0, 64, ScreenWidth, ScreenHeight - 64 - 49);
    pageManager.segmentHeight = 25;//导航条高度
    pageManager.progressWidth = 15;//导航条底横线度宽度
    pageManager.progressHeight = 1;//导航条底横线高
    pageManager.itemMinimumSpace = 10;//导航条item直接的间距
    pageManager.normalTextFont = [UIFont systemFontOfSize:12];//未选中字体大小
    pageManager.selectedTextFont = [UIFont systemFontOfSize:16];//已选中字体大小
    pageManager.normalTextColor = [UIColor blackColor];//未选中字体颜色
    pageManager.selectedTextColor = [UIColor redColor];//已选中字体颜色
    pageManager.dataSource = self;//页面管理数据源
    pageManager.menuDataSource = self;//菜单管理数据源, 如果不设置改代理则没有菜单按钮
    pageManager.editMenuIconIgV.image = [UIImage imageNamed:@"editButtonImage"];//编辑菜单icon (按需设置)
    pageManager.delegate = self;//相关事件返回代理
    [self.view addSubview:pageManager.view];
    [self addChildViewController:pageManager];
```
### 通过 dataSource 获取所有页面的数据源 

```
@protocol ERPageViewControllerDataSource <NSObject>

@required

/**
 返回子控制器总数,类似TableViewDataSource

 @param pageViewController self
 @return 子控制器总数
 */
- (NSInteger)numberOfControllersInPageViewController:(ERPageViewController *)pageViewController;


/**
 返回对应index的ViewController

 @param pageViewController self
 @param index 当前index
 @return 需要展示的ViewController
 */
- (UIViewController *)pageViewController:(ERPageViewController *)pageViewController childControllerAtIndex:(NSInteger)index;

/**
 子控制器title

 @param pageViewController self
 @param index 当前index
 @return title
 */
- (NSString *)pageViewController:(ERPageViewController *)pageViewController titleForChildControllerAtIndex:(NSInteger)index;



@end

```

##### 通过 menuDataSource 获取编辑菜单的数据源,如不需要则不用设置该代理

```
@protocol ERSegmentMenuControllerDataSource <NSObject>

@required;

/**
 已经选择的频道列表信息

 @param segmentMenuController self
 @return 必须为字典型数组(必须包含一个KEY为@"name"的字符串)
 */
- (NSMutableArray<NSDictionary *> *)selectedChannelLisInSegmentMenuController:(ERSegmentMenuController *)segmentMenuController;

@optional;

/**
 未选择的频道列表信息
 
 @param segmentMenuController self
 @return 可以为nil ,若不为nil则必须为字典型数组(必须包含一个KEY为@"name"的字符串)
 */
- (NSMutableArray<NSDictionary *> *)unSelectChannelListInSegmentMenuController:(ERSegmentMenuController *)segmentMenuController;


/**
 每组标题

 @param segmentMenuController segmentMenuController
 @param sectionHeaderLabel 组头Label
 @param section section
 @return title
 */
- (NSString *)segmentMenuController:(ERSegmentMenuController *)segmentMenuController sectionHeaderLabel:(UILabel *)sectionHeaderLabel titleForHeaderInSection:(NSInteger)section;

@end

```

##### delegate 可以获取点击事件(双击导航条item)已经滚动事件的回调,用于自定义处理

```
@protocol ERSegmentControllerDelegte <NSObject>

@optional

/**
 导航按钮点击事件回调

 @param segmentController self
 @param indexPath indexPath
 */
- (void)segmentController:(ERSegmentController *)segmentController didSelectItemAtIndexPath:(NSIndexPath *)indexPath;

/**
 导航菜单编辑按钮点击回调

 @param segmentController self
 @param editMenuButton editMenuButton
 */
- (void)segmentController:(ERSegmentController *)segmentController didSelectEditMenuButton:(UIButton *)editMenuButton;
/**
 导航按钮双击事件回调
 
 @param segmentController self
 @param indexPath indexPath
 */
- (void)segmentController:(ERSegmentController *)segmentController itemDoubleClickAtIndexPath:(NSIndexPath *)indexPath;

/**
 页面切换滚动完成回调

 @param pageController superClass
 @param fromIndex fromIndex
 @param toIndex toIndex
 */
- (void)pageControllerDidScroll:(ERPageViewController *)pageController fromIndex:(NSInteger)fromIndex toIndex:(NSInteger)toIndex;

@end

```

<br/>

### 参考类库/文章 (已表感谢 ! 学习并膜拜大神们 ~)

[DDNews](https://github.com/iDvel/DDNews)<br/>
[ZYColumnViewController](https://github.com/r9ronaldozhang/ZYColumnViewController)<br/>
[LXReorderableCollectionViewFlowLayout](https://github.com/lxcid/LXReorderableCollectionViewFlowLayout)<br/>
[TYPagerController](https://github.com/12207480/TYPagerController)<br/>

