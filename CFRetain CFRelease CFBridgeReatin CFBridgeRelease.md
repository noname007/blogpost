# CFRetain CFRelease CFBridgeReatin CFBridgeRelease


- CFRetain CFRelease 是对CF对象内存管理的方法，这个的用法是当你从别的地方获取CF对象时(不是由你直接创建的或者拷贝的)，那么你可能会需要持有它，那就应该调用CFRetain，同时释放的责任也会交给你，CFRelease在你需要释放CF对象的地方调用释放就可以了
- CFBridgeReatin CFBridgeRelease是OC对象和CF对象相互转换并交换内存管理责任的方法
	- CFBridgeRelease CF->OC,转交内存管理
	- CFBridgeRetain  OC->CF,转交内存管理 