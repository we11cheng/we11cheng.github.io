---
layout:     post
title:      "使用UIEdgeInsetsMake调整UIButton图片和标题位置"
subtitle:   ""
date:       2018-01-11 16:00:00
author:     "管维诚"
header-img: "img/post-bg-rwd.jpg"
---

#### 首先简单介绍一下UIButton UIEdgeInsetsMake的用法。
#### UIButton.h
```objc
@property(nonatomic)          UIEdgeInsets titleEdgeInsets;                // default is UIEdgeInsetsZero
@property(nonatomic)          UIEdgeInsets imageEdgeInsets;                // default is UIEdgeInsetsZero
```
#### UIEdgeInsets
```objc
typedef struct UIEdgeInsets {
    CGFloat top, left, bottom, right;  // specify amount to inset (positive) for each of the edges. values can be negative to 'outset'
} UIEdgeInsets;
```
#### Edge字面意思就是表示四个边距。所以我们可以通过更改UIButton的imageEdgeInsets、titleEdgeInsets来实现按钮image和title的各种样式。为了便于使用。我们将实现封装在UIButton category中。详见代码

#### UIButton+WCButtonWithEdgeInset.m 文件

```objc
#import <UIKit/UIKit.h>

typedef NS_ENUM(NSUInteger, WCButtonEdgeInsetsStyle) {
    WCButtonEdgeInsetsStyleTop = 0,//图片在上，title在下
    WCButtonEdgeInsetsStyleLeft = 1,//图片在左，title在右
    WCButtonEdgeInsetsStyleBottom = 2,//图片在下，title在上
    WCButtonEdgeInsetsStyleRight = 3,//图片在右，title在左
};

@interface UIButton (WCButtonWithEdgeInset)

- (void)wcButtonWithEdgeInsetsStyle:(WCButtonEdgeInsetsStyle)style
                    imageTitleSpace:(CGFloat)space;//space:图片和标题间距

@end
```
#### UIButton+WCButtonWithEdgeInset.m 文件
```objc
#import "UIButton+WCButtonWithEdgeInset.h"

@implementation UIButton (WCButtonWithEdgeInset)

- (void)wcButtonWithEdgeInsetsStyle:(WCButtonEdgeInsetsStyle)style
                        imageTitleSpace:(CGFloat)space {
    CGFloat imageWith = self.currentImage.size.width;
    CGFloat imageHeight = self.currentImage.size.height;
    CGFloat labelWidth = 0.0;
    CGFloat labelHeight = 0.0;
    if ([UIDevice currentDevice].systemVersion.floatValue >= 8.0) {
        // 由于iOS8中titleLabel的size为0，用下面的这种设置
        labelWidth = self.titleLabel.intrinsicContentSize.width;
        labelHeight = self.titleLabel.intrinsicContentSize.height;
    } else {
        labelWidth = self.titleLabel.frame.size.width;
        labelHeight = self.titleLabel.frame.size.height;
    }
    
    // 2. 声明全局的imageEdgeInsets和labelEdgeInsets
    UIEdgeInsets imageEdgeInsets = UIEdgeInsetsZero;
    UIEdgeInsets labelEdgeInsets = UIEdgeInsetsZero;
    
    // 3. 根据style和space得到imageEdgeInsets和labelEdgeInsets的值
    switch (style) {
        case WCButtonEdgeInsetsStyleTop: {
            imageEdgeInsets = UIEdgeInsetsMake(-labelHeight-space, 0, 0, -labelWidth);
            labelEdgeInsets = UIEdgeInsetsMake(0, -imageWith, -imageHeight-space, 0);
        }
            break;
        case WCButtonEdgeInsetsStyleLeft: {
            imageEdgeInsets = UIEdgeInsetsMake(0, -space, 0, space);
            labelEdgeInsets = UIEdgeInsetsMake(0, space, 0, -space);
        }
            break;
        case WCButtonEdgeInsetsStyleBottom: {
            imageEdgeInsets = UIEdgeInsetsMake(0, 0, -labelHeight-space, -labelWidth);
            labelEdgeInsets = UIEdgeInsetsMake(-imageHeight-space, -imageWith, 0, 0);
        }
            break;
        case WCButtonEdgeInsetsStyleRight: {
            imageEdgeInsets = UIEdgeInsetsMake(0, labelWidth+space, 0, -labelWidth-space);
            labelEdgeInsets = UIEdgeInsetsMake(0, -imageWith-space, 0, imageWith+space);
        }
            break;
        default:
            break;
    }
    // 4. 赋值
    self.titleEdgeInsets = labelEdgeInsets;
    self.imageEdgeInsets = imageEdgeInsets;
}

@end
```
#### 具体使用及效果

```objc
UIButton *button = [UIButton buttonWithType:UIButtonTypeCustom];
    button.frame = CGRectMake((kMainScreenWidth - 264)/2, 100, 264, 264);
    [button setImage:[UIImage imageNamed:@"go_shopdetail"] forState:UIControlStateNormal];
    button.backgroundColor = [UIColor purpleColor];
    [button setTitle:@"点击购买" forState:UIControlStateNormal];
    [button setTintColor:[UIColor redColor]];
    [button wcButtonWithEdgeInsetsStyle:WCButtonEdgeInsetsStyleRight imageTitleSpace:15];
    [self.view addSubview:button];
```
#### 这个方法需要在设置图片和文字之后才可以调用，且button的大小要大于 图片大小+文字大小+space。
#### 效果图
#### 图片在上
![图片在上](http://p2bzzkn05.bkt.clouddn.com/18-1-11/77787130.jpg)
#### 图片在左
![](http://p2bzzkn05.bkt.clouddn.com/18-1-11/72999315.jpg)
#### 图片在下
![](http://p2bzzkn05.bkt.clouddn.com/18-1-11/54002071.jpg)
#### 图片在右
![](http://p2bzzkn05.bkt.clouddn.com/18-1-11/39958724.jpg)


