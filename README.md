# iOS-CALayerAnimation6

```objc 

- (void) moveAnimation {
    
    // 移动动画
    CABasicAnimation *animation = [CABasicAnimation animation];
    animation.keyPath = @"position.x";
    animation.fromValue     = @77;
    animation.toValue       = @300;
    animation.duration      = 1;
    /*
     fillMode
     kCAFillModeForwards
     kCAFillModeBackwards
     kCAFillModeBoth
     kCAFillModeRemoved
     */
    animation.fillMode      =  kCAFillModeForwards; // 设置留在最终状态/ 或最终位置
    // 防止它被自动移除
    animation.removedOnCompletion = false;
    
    [self.myView.layer addAnimation:animation forKey:@"basic"];

}

- (void) animation {
    CABasicAnimation * animation    = [CABasicAnimation animationWithKeyPath:@"position"];
    animation.duration              = 2;
    animation.repeatCount           = 2;
    // 指定动画开始时间。从开始指定延迟几秒执行的话，请设置为 「CACurrentMediaTime() + 秒数」的形式。
    animation.beginTime             = CACurrentMediaTime() + 2; // 两秒后执行
    // 设置动画速度变化  // 动画先加速后减速
    animation.timingFunction        = [CAMediaTimingFunction functionWithName: kCAMediaTimingFunctionEaseInEaseOut];
    animation.autoreverses          = true; // 动画结束时是否执行逆动画
    
    // 动画终了后不返回初始状态
    animation.removedOnCompletion = NO;
    animation.fillMode = kCAFillModeForwards;
    
    // 设定动画起始帧和结束帧
    animation.fromValue = [NSValue valueWithCGPoint:CGPointMake(0, 0)]; // 起始点
    animation.toValue = [NSValue valueWithCGPoint:CGPointMake(320, 480)]; // 终了点
    
    [_myView.layer addAnimation:animation forKey:@"move-layer"];
}

- (void) moveAnimation1 {
    
    /* 移动 */
    CABasicAnimation *animation = [CABasicAnimation animationWithKeyPath:@"position"];
    
    // 动画选项的设定
    animation.duration = 2.5; // 持续时间
    animation.repeatCount = 3; // 重复次数
    
    // 起始帧和终了帧的设定
    animation.fromValue = [NSValue valueWithCGPoint:_myView.layer.position]; // 起始帧
    animation.toValue = [NSValue valueWithCGPoint:CGPointMake(320, 480)]; // 终了帧
    
    // 添加动画
    [_myView.layer addAnimation:animation forKey:@"move-layer"];
}

- (void) rotationAnimation2 {
    
    /* 旋转 */
    
    // 对Y轴进行旋转（指定Z轴的话，就和UIView的动画一样绕中心旋转）
    CABasicAnimation *animation = [CABasicAnimation animationWithKeyPath:@"transform.rotation.z"];
    
    // 设定动画选项
    animation.duration = 2.5; // 持续时间
    animation.repeatCount = 3; // 重复次数
    
    // 设定旋转角度
    animation.fromValue = [NSNumber numberWithFloat:0.0]; // 起始角度
    animation.toValue = [NSNumber numberWithFloat:22 * M_PI]; // 终止角度
    
    // 添加动画
    [_myView.layer addAnimation:animation forKey:@"rotate-layer"];
}


- (void) scaleAnimation3 {
    
    /* 放大缩小 */
    
    // 设定为缩放
    CABasicAnimation *animation = [CABasicAnimation animationWithKeyPath:@"transform.scale"];
    
    // 动画选项设定
    animation.duration = 2.5; // 动画持续时间
    animation.repeatCount = 1; // 重复次数
    animation.autoreverses = YES; // 动画结束时执行逆动画
    
    // 缩放倍数
    animation.fromValue = [NSNumber numberWithFloat:1.0]; // 开始时的倍率
    animation.toValue = [NSNumber numberWithFloat:2.0]; // 结束时的倍率
    
    // 添加动画
    [_myView.layer addAnimation:animation forKey:@"scale-layer"];
}

- (void) groupAnimation4 {
    /* 动画1（在X轴方向移动） */
    CABasicAnimation *animation1 =
    [CABasicAnimation animationWithKeyPath:@"transform.translation.x"];
    
    // 终点设定
    animation1.toValue = [NSNumber numberWithFloat:80];; // 終点
    
    
    /* 动画2（绕Z轴中心旋转） */
    CABasicAnimation *animation2 =
    [CABasicAnimation animationWithKeyPath:@"transform.rotation.z"];
    
    // 设定旋转角度
    animation2.fromValue = [NSNumber numberWithFloat:0.0]; // 开始时的角度
    animation2.toValue = [NSNumber numberWithFloat:44 * M_PI]; // 结束时的角度
    
    
    /* 动画组 */
    CAAnimationGroup *group = [CAAnimationGroup animation];
    
    // 动画选项设定
    group.duration = 3.0;
    group.repeatCount = 3;
    
    // 添加动画
    group.animations = [NSArray arrayWithObjects:animation1, animation2, nil];
    [_myView.layer addAnimation:group forKey:@"move-rotate-layer"];
}



```
* 创建带圆角的矩形

```objc 
    //创建带圆角的矩形  圆角半径：20
//    UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:CGRectMake(60, 100, 200, 200) cornerRadius:20];
    
    //创建可以指定圆角位置的矩形
    //第一个参数一样是传了个矩形
    //第二个参数是指定在哪个方向画圆角
    //第三个参数是一个CGSize类型，用来指定水平和垂直方向的半径的大小
    UIBezierPath *path = [UIBezierPath bezierPathWithRoundedRect:CGRectMake(60, 100, 200, 200) byRoundingCorners:UIRectCornerTopLeft cornerRadii:CGSizeMake(100, 50)];
    
    //配置属性
    [[UIColor yellowColor] setFill];    //设置填充颜色
    [[UIColor redColor] setStroke];     //设置描边颜色
    
    path.lineWidth = 3;     //设置线宽
    
    //渲染
    [path stroke];
    [path fill];

```