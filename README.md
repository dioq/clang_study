# clang 编译

-fobjc-arc     		指定内存管理方式为ARC (自动引用计数)	
-isysroot      		指定系统SDK路径(只有编译iOS 工程时需要) 如: -isysroot /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk	
-framework    		指定 framework 库 一般为 Foundation	
-fmodules      		自动寻找到需要的系统库 如果加了这一项 就没必要使用 -framework Foundation	
-arch	       		指定编译的架构, 如: -arch arm64		
-mios-version-min=	指定最小支持的 iOS 系统(只有编译iOS 工程时需要,其实不加不影响程序执行), 如: -mios-version-min= 9.0	
-shared			编译成动态库	
