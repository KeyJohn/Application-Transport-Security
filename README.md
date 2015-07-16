

# 应用程序数据传输安全

- 最近在使用xcode7进行一个简单的网络请求时程序报错：
> Application Transport Security has blocked a cleartext HTTP (http://) resource load since it is insecure. Temporary exceptions can be configured via your app's Info.plist file.

####先看看这是一个什么错误

		编译器告诉了我们在应用程序中使用了不安全的明文HTTP请求，如果要解决这一异常我们可以在info.plist文件中设置
	

####应用程序安全传输（App Transport Security）

- 我们可以向一个应用程序的Info.plist文件中添加声明指定它需要保密通信领域。ATS防止网络传输数据意外泄漏，提供安全的默认行为，易于采用。因此，无论你是创建一个新的应用程序或更新现有的。你应该采用ATS

- 如果你正在开发一个新的应用程序，你应该使用HTTPS安全协议。如果你有一个现有的应用程序，你应该应该尽可能地使用HTTPS保证应用程序的安全。


####像这样你可以在Info.plist文件中添加如下项：
	<key>NSAppTransportSecurity</key>
	<dict>
	  <key>NSExceptionDomains</key>
	  <dict>
	    <key>yourserver.com</key>
	    <dict>
	      <!--Include to allow subdomains-->
	      <key>NSIncludesSubdomains</key>
	      <true/>
	      <!--Include to allow HTTP requests-->
	      <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
	      <true/>
	      <!--Include to specify minimum TLS version-->
	      <key>NSTemporaryExceptionMinimumTLSVersion</key>
	      <string>TLSv1.1</string>
	    </dict>
	  </dict>
	</dict>
	
####当然，如果不想使用ATS，你可以在Info.plist文件中添加如下项：
	<key>NSAppTransportSecurity</key>
	<dict>
	  <!--Include to allow all connections (DANGER)-->
	  <key>NSAllowsArbitraryLoads</key>
	      <true/>
	</dict>
	
#####也就是这样:
![这里写图片描述](http://img.blog.csdn.net/20150716133020001)
