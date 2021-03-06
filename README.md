# UITableView-HJEmptyView
pod 'UITableView+HJEmptyView', '~> 1.0.0'
   - Homepage: https://github.com/huluo666/UITableView-HJEmptyView
   - Source:   https://github.com/huluo666/UITableView-HJEmptyView.git
   
利用Runtime一行代码实现UITableView的空视图EmptyView显示,省去没必要的判断和几行代码即可快速自定义精致简洁的空视图显示。大大的减少了viewContoller中的代码量。可重用，整个项目在需要显示空视图控制器，加上一行代码即可。

#### 显示空视图，只需一行代码
`self.tableView.HJ_emptyView=self.emptyView;//emptyView需要显示的空视图`

![演示图](https://github.com/huluo666/UITableView-HJEmptyView/blob/master/2016_03_18_120853.gif)

可方便的通过属性修改图标文案，可点击页面回调

### 使用
```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view, typically from a nib.
    [self.view addSubview:self.tableView];//添加表格视图
    
    [self setUpEmptyView];//设置空视图
}

```

### NO.1 使用默认空视图
```objc
-(void)setUpEmptyView
{
   self.emptyView=[HJEmptyView defaultEmptyView];
}
  
```


### 或  NO.2 使用自定义空视图
```objc
-(void)setUpEmptyView
{
    __unsafe_unretained __typeof(self) weakSelf = self;
    
    //自定义空视图
    HJEmptyView  *emptyView=[HJEmptyView showTitle:@"oh,shit!!!" details:@"对不起,没有网络\n请检查网络网络是否打开" iconImag:@"no-wifi" toView:self.view];
    
    self.emptyView=emptyView;
    //点击刷新按钮
    emptyView.refreshBtnClickBlock=^(UIButton *button){
        [weakSelf MJBeginRefreshing];
    };
    
    
    //轻击Empty视图回调
    emptyView.refreshEmptyTapBlock=^(UIView *view){
        [weakSelf MJBeginRefreshing];
    };
    
    self.tableView.HJ_emptyView=self.emptyView;
}
```

