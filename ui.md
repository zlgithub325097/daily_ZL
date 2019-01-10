* [x] > ### 弹框蒙版

```
_popView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, ScrW, ScrH)];
[win addSubview:_popView];

UIButton *btn = [UIButton buttonWithType:UIButtonTypeCustom];
btn.frame = _popView.frame;
btn.backgroundColor = [UIColor darkGrayColor];
btn.alpha = 0.4;
[_popView addSubview:btn];
[btn addTarget:self action:@selector(dissmiss) forControlEvents:UIControlEventTouchUpInside];

UIView *bigView = [[UIView alloc] initWithFrame:CGRectMake((ScrW - 291)/2,(ScrH - 265)/2, 291, 265)];
bigView.layer.cornerRadius = 11;
UILabel *lbl = [[UILabel alloc] initWithFrame:CGRectMake((bigView.frame.size.width - 100)/2, 22, 100, 18)];
[bigView addSubview:lbl];
lbl.text = @"手机号说明";
lbl.textAlignment = NSTextAlignmentCenter;
lbl.font = [UIFont systemFontOfSize:16];
lbl.textColor = [UIColor colorWithRed:102/255.0 green:102/255.0 blue:102/255.0 alpha:1.0];
[_popView addSubview:bigView];
bigView.backgroundColor = [UIColor whiteColor];
UIView *redView = [[UIView alloc] initWithFrame:CGRectMake((bigView.frame.size.width - 240)/2, CGRectGetMaxY(lbl.frame)+18, 240, 90)];
redView.layer.cornerRadius = 4;
redView.backgroundColor = [UIColor colorWithRed:255/255.0 green:157/255.0 blue:157/255.0 alpha:1.0];
[bigView addSubview:redView];
UILabel *lblCard = [[UILabel alloc] initWithFrame:CGRectMake((redView.frame.size.width - 135)/2, 10, 135, 18)];
[redView addSubview:lblCard];
lblCard.text = @"银行卡申请人资料";
lblCard.textAlignment = NSTextAlignmentCenter;
lblCard.font = [UIFont systemFontOfSize:16];
lblCard.textColor = [UIColor whiteColor];
UIView *lineView = [[UIView alloc] initWithFrame:CGRectMake(0, CGRectGetMaxY(lblCard.frame) +6, redView.frame.size.width, 1)];
lineView.backgroundColor = [UIColor whiteColor];
[redView addSubview:lineView];
UILabel *lbl2 = [[UILabel alloc] initWithFrame:CGRectMake(14, CGRectGetMaxY(lineView.frame)+10, 35, 15)];
[redView addSubview:lbl2];
lbl2.textColor = [UIColor whiteColor];
lbl2.textAlignment = NSTextAlignmentLeft;
lbl2.text = @"****";
lbl2.font = [UIFont systemFontOfSize:16];
UILabel *lbl3 = [[UILabel alloc] initWithFrame:CGRectMake(14, CGRectGetMaxY(lbl2.frame)+ 5, redView.frame.size.width - 14, 16)];
[redView addSubview:lbl3];
lbl3.textColor = [UIColor whiteColor];
lbl3.textAlignment = NSTextAlignmentLeft;
lbl3.text = @"手机号 ***********";
lbl3.font = [UIFont systemFontOfSize:16];
UILabel *lbl4 = [[UILabel alloc] initWithFrame:CGRectMake((bigView.frame.size.width - 240)/2, CGRectGetMaxY(redView.frame)+ 8, 240, 40)];
lbl4.numberOfLines = 0;
[bigView addSubview:lbl4];
lbl4.textColor = [UIColor colorWithRed:102/255.0 green:102/255.0 blue:102/255.0 alpha:1.0];
lbl4.textAlignment = NSTextAlignmentLeft;
lbl4.text = @"银行预留的手机号是办理该银行卡时所填写的手机号码。";
lbl4.font = [UIFont systemFontOfSize:13];
UILabel *lbl5 = [[UILabel alloc] initWithFrame:CGRectMake((bigView.frame.size.width - 240)/2, CGRectGetMaxY(lbl4.frame), 240, 50)];
lbl5.numberOfLines = 0;
[bigView addSubview:lbl5];
lbl5.textColor = [UIColor colorWithRed:102/255.0 green:102/255.0 blue:102/255.0 alpha:1.0];
lbl5.textAlignment = NSTextAlignmentLeft;
lbl5.text = @"没有预留、手机号忘记或者已停用，请联系银行更新处理。";
lbl5.font = [UIFont systemFontOfSize:13];


-(void)dissmiss
{
   [_popView removeFromSuperview];
}
```

* [ ] > ### TableView 注册的几种方式

  简书：[https://www.jianshu.com/p/6798662454e1](https://www.jianshu.com/p/6798662454e1)  \(很规范的自定义cell\)

```
【1】、在viewDidLoad 方法里面注册 
 [self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:@"cell"];

【2】、系统推荐用这个方法，这个方法在某些情况下更加能避免循环复用（像你在cell里面修改某个控件内容的时候）
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{

UITableViewCell * cell = [tableView dequeueReusableCellWithIdentifier:@"cell"];

  //如果队列中没有该类型cell，则会返回nil，这个时候就需要自己创建一个cell
 if (cell == nil) {

  cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"cell"];

    }
}

```

```
2、自定制cell
```

```
【1】，不使用xib的情况下
  <1>、[self.tableView registerClass:[xxxxCell class] forCellReuseIdentifier:@"cell"];
    xxxxCell *cell = [tableView dequeueReusableCellWithIdentifier:@"cell" forIndexPath:indexPath];
  <2>、xxxxCell *cell=[tableView dequeueReusableCellWithIdentifier:@"cell"];
  if (cell==nil) {
      cell=[[xxxxCell alloc]initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"cell"];
}

【2】，在使用xib的情况下
  <1>、[tableView registerNib:[UINib nibWithNibName:@"xxxxViewCell" bundle:nil] forCellReuseIdentifier:@"Cell"];  
    xxxxCell *cell = [tableView dequeueReusableCellWithIdentifier:@"Cell" forIndexPath:indexPath];
  <2>、xxxxCell *cell=[tableView dequeueReusableCellWithIdentifier:@"cell"];
    if (cell == nil) {
        cell=[[[NSBundle mainBundle]loadNibNamed:@“xxxxCell" owner:self options:nil]lastObject];
    }
```

```
3，最后在使用自定制cell的时候，如果不使用xib，那么要调一下方法
```

```
//创建cell的时候就会默认调用这个方法
- (instancetype)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier
{
    if (self = [super initWithStyle:style reuseIdentifier:reuseIdentifier]) {
        //在这里创建你自己的子控件
        self.iconView = [[UIImageView alloc] init];
        self.titleLabel = [[UILabel alloc] init];
        self.detailLabel = [[UILabel alloc] init];
        self.priceLabel = [[UILabel alloc] init];
        self.titleLabel.backgroundColor = [UIColor redColor];
        self.detailLabel.backgroundColor = [UIColor greenColor];
        self.priceLabel.backgroundColor = [UIColor cyanColor];

        //添加子控件
        [self.contentView addSubview:self.iconView];
        [self.contentView addSubview:self.titleLabel];
        [self.contentView addSubview:self.detailLabel];
        [self.contentView addSubview:self.priceLabel];
    }
    return self;
}


//即将布局子控件就会调用这个方法，我们在这里完成cell里面子控件的相对布局
- (void)layoutSubviews
{
    //重写这个方法，一定要记得手动调用父类方法。
    [super layoutSubviews];

}

在使用xib的时候直接拉控件就可以啦
```

* [ ] > ### 自定义UITableViewCell大致有两类方法：

```
【1】使用nib

1、xib中指定cell的Class为自定义cell类型（注意不是设置File's Owner的class）
2、调用 tableView 的 registerNib:forCellReuseIdentifier:方法向数据源注册cell
[_tableView registerNib:[UINib nibWithNibName:@"xxxxxCell" bundle:nil] forCellReuseIdentifier:kCellIdentify];
3、在cellForRowAtIndexPath中使用dequeueReuseableCellWithIdentifier:forIndexPath:获取重用的cell，若无重用的cell，
将自动使用所提供的nib文件创建cell并返回（若使用旧式dequeueReuseableCellWithIdentifier:方法需要判断返回是否为空而进行新建）
xxxxxCell *cell = [tableView dequeueReusableCellWithIdentifier:kCellIdentify forIndexPath:indexPath];
4、获取cell时若无可重用cell，将创建新的cell并调用其中的awakeFromNib方法，可通过重写这个方法添加更多页面内容

【2】不使用nib

1、重写自定义cell的initWithStyle:withReuseableCellIdentifier:方法进行布局
(id)initWithStyle:(UITableViewCellStyle)style reuseIdentifier:(NSString *)reuseIdentifier
{
self = [super initWithStyle:style reuseIdentifier:reuseIdentifier];

if (self)

{

    // cell页面布局

    [self setupView];

}

return self;
}
2、为tableView注册cell，使用registerClass:forCellReuseIdentifier:方法注册（注意是Class）
[_tableView registerClass:[xxxxxCell class] forCellReuseIdentifier:kCellIdentify];
3、在cellForRowAtIndexPath中使用dequeueReuseableCellWithIdentifier:forIndexPath:获取重用的cell，若无重用的cell，
将自动使用所提供的class类创建cell并返回
xxxxxCell *cell = [tableView dequeueReusableCellWithIdentifier:kCellIdentify forIndexPath:indexPath];
4、获取cell时若无可重用cell，将调用cell中的initWithStyle:withReuseableCellIdentifier:方法创建新的cell
另外要注意的：
1、dequeueReuseableCellWithIdentifier:与dequeueReuseableCellWithIdentifier:forIndexPath:的区别：
前者不必向tableView注册cell的Identifier，但需要判断获取的cell是否为nil；
后者则必须向table注册cell，可省略判断获取的cell是否为空，因为无可复用cell时runtime将使用注册时提供的资源去新建一个cell并返回
2、自定义cell时，记得将其他内容加到self.contentView 上，而不是直接添加到 cell 本身上
总结：
1.自定义cell时，
若使用nib，使用 registerNib: 注册，dequeue时会调用 cell 的 -(void)awakeFromNib
不使用nib，使用 registerClass: 注册, dequeue时会调用 cell 的 - (id)initWithStyle:withReuseableCellIdentifier:
2.需不需要注册？
使用dequeueReuseableCellWithIdentifier:可不注册，但是必须对获取回来的cell进行判断是否为空，若空则手动创建新的cell；
使用dequeueReuseableCellWithIdentifier:forIndexPath:必须注册，但返回的cell可省略空值判断的步骤。
```

* [ ] > ### 新建pch文件注意

```
新建pch文件之后需要设置
```

![](/assets/pch.png)

* [ ] > ### CoocaPods 文件

```
注意：Podfile 文件和Xcode项目必须处于同一个目录下！！！
1：touch Podfile
2: platform:ios,'9.0'      target 'coding++' do       pod 'Marsonry'   end
3: pod install
```



