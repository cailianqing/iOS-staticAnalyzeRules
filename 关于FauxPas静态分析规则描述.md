### 关于FauxPas静态分析规则描述
1. **[查看更多](http://www.mikeash.com/pyblog/friday-qa-2009-05-22-objective-c-class-loading-and-initialization.html)**
  
 	```
 	规则描述：
	 	+[NSObject load] method without an @autoreleasepool
 	 	当执行+[NSObject load]这里不会产生aotoreleasepool，所以必须手动创建一个
 	原文梗概：
 		 +load:
 		 	1.当一个类完全被加载的时候+load方法会被调用。
 		 	2.如果在应用、Framework中声明了+load方法，+load会比main()更优先执行。
 		 	3.在+load方法中frameworks、父类都已经完全被加载，所以+load是个安全的方法。
 		 	4.在+load方法中不会创建自动释放池，所以这里需要把你的代码用一个自动释放池包起来、
 		 	5.+load方法是Method Swizzling最好的地方、
 		 +initialize:
 		 	1.类第一次加载会调用，如果第一次向class发消息。runtime会检测哈是否调用+initialize。
 		 	2.+initialize调用比较延后。所以不是注册类的最佳位置。
 		 总结:
 		 	1.一旦calss被夹在+load方法就会被调用。
 		 	2.+initialize方法是一个非常好的地方来做初始化。因为执行时机比较靠后。
 	 
 	```
 
2. **Assigning delegate property**
   
 	```
 	规则描述：
	 	Delegate属性应该用weak声明而不是用assign。Weak会在Object释放之后置nil，所以更加安全。	 
 	```
 	
3. **[查看更多](https://mjtsai.com/blog/2014/01/16/associated-objects-on-value-types/)**

 	 ```
 	规则描述：
	 	不能使用objc_setAssociatedObject()来关键不可变值比如NSNumber，NSDate，NSString。
	 	原因：https://www.jianshu.com/p/d417e3038a04	 
 	```
 	
4. **[查看更多](https://developer.apple.com/library/archive/documentation/General/Conceptual/DevPedia-CocoaCore/ObjectComparison.html)**

 	 ```
 	规则描述：
	 	如果两个objects isEqual相同，那么它们一定拥有相同的hash值。相反则不成立。	 
 	```
 	
5. **[查看更多](https://www.bignerdranch.com/blog/notifications-part-3-gotchas/)**

 	 ```
 	规则描述：
	 	-[NSNotificationCenter removeObserver:self]用来移除当前类的所有通知。
	 	如果父类或者子类想继续保持某些通知，那么这么调用销毁通知就会产生问题。
	原文梗概：
 		 1.自定义的通知，要么在主线程上发送，要么通过设计或编码约定确保通知程序能够在任何线程运行。
 		 例外情况（使用块和通知队列）在这种情况可以通过[NSopuralQuealMeQueQue]来保证通知快始终在
 		 主队列上发布
 		 2.如果在使用Block通知可能会产生循环引用
 		 3.注意通知死锁
 	``` 	
6. **[查看更多](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ProgrammingWithObjectiveC/CustomizingExistingClasses/CustomizingExistingClasses.html)**

 	```
 	规则描述：
	 	如果类中和分类中同时定义了一个方法，那么在运行时具体使用哪一个方法的声明是不确定的
 	``` 	
 	
7. **[查看更多](https://stackoverflow.com/questions/8972221/would-it-be-beneficial-to-begin-using-instancetype-instead-of-id)**

	```
 	规则描述：
	 	工厂方法的返回值类型应该填写instancetype而不是id。因为instancetype会做类型检查
 	``` 	
 	
8. **持续更新中....**