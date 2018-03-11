# DSMagnifierView
## DSMagnifierView是一个有放大镜子效果的自定义控件。

先看效果：

![放大镜效果](http://img.blog.csdn.net/20180311133048275?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRGVyZWtfbWlzcw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

其实很简单，就是把UIWindow的图层给渲染到DSMagnifierView上。
由于这个放大镜要处于屏幕最上层，最好是UIWindow的子类，这样可以设置它的视图层级。

## 使用方法

### 1.初始化后设置用来渲染的视图renderView。

```
- (DSMagnifierView *)magnifierView {
    if (nil == _magnifierView) {
        _magnifierView = [[DSMagnifierView alloc] init];
        _magnifierView.renderView = self.view.window;
    }
    return _magnifierView;
}
```

### 2.在触摸屏幕的时候设置magnifierView的frame和渲染点renderPoint。

```
- (void)touchesMoved:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [super touchesMoved:touches withEvent:event];
    
    NSLog(@"touching");
    
    // 获取触摸点
    UITouch *touch = [touches anyObject];
    CGPoint p = [touch locationInView:self.view];
    
    //window的hidden默认为YES
    self.magnifierView.hidden = NO;
    
    //设置magnifierView的frame
    self.magnifierView.frame = CGRectMake(0, 0, 150, 150);
    self.magnifierView.center = p;
    
    //设置渲染的中心点
    self.magnifierView.renderPoint = p;
}
```

### 3.用完后销毁

```
- (void)touchesEnded:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event {
    [super touchesEnded:touches withEvent:event];
    
    //用完一定要记得置nil。
    self.magnifierView = nil;
}
```

### 4.如果有任何疑问可以联系我，如果觉得对你有所帮助话给个Star✨吧！！🙂
