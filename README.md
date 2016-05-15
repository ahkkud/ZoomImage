# ZoomImage
图片放大缩小，居中显示

//1、设置 UIScrollView的位置与屏幕大小相同
_imageScrollView =[[UIScrollView alloc]initWithFrame:self.view.bounds];
_imageScrollView.backgroundColor = [UIColor blackColor];
[self.view.window addSubview:_imageScrollView];

//2、添加图片
UIImage * image = [UIImage imageNamed:@"imageName"];
_imageView =[[UIImageView alloc]init];
_imageView.image=image;
_imageView.frame=CGRectMake(0, self.view.height/2 - self.view.width/2, self.view.width, self.view.width);
[_imageScrollView addSubview:_imageView];

//3、设置代理scrollview的代理对象
_imageScrollView.delegate=self;
//设置最大伸缩比例
_imageScrollView.maximumZoomScale=5.0;
//设置最小伸缩比例
_imageScrollView.minimumZoomScale=0.5;

//4、实现两个代理方法
-(UIView *)viewForZoomingInScrollView:(UIScrollView *)scrollView
{
return _imageView;
}

//实现图片在缩放过程中居中
- (void)scrollViewDidZoom:(UIScrollView *)scrollView
{
CGFloat offsetX = (scrollView.bounds.size.width > scrollView.contentSize.width)?(scrollView.bounds.size.width - scrollView.contentSize.width)/2 : 0.0;
CGFloat offsetY = (scrollView.bounds.size.height > scrollView.contentSize.height)?(scrollView.bounds.size.height - scrollView.contentSize.height)/2 : 0.0;
_imageView.center = CGPointMake(scrollView.contentSize.width/2 + offsetX,scrollView.contentSize.height/2 + offsetY);
}
