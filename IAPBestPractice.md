IAP 最佳实践

1. Add a transaction queue observer at application launch
   
   原因: 当由于重启或者启动APP的原因导致的payment queue发生变化时SK会自动通知你的observer。所以说在应用启动时就持久化的持有observer的引用。如果不在应用启动时初始化，可能接下来就不会受到transaction的通知
2. Query the App Store for product information before presenting your app's store UI.

  原因：你的应用在从App Store购买之前需要发起product request来允许你决定在商店哪些商品可售。在你发起请求后，商店会返回给你SKResponse
  
3. Provide a UI for restoring products

	原因: 如果你的app销售非消耗性、自动续订或者不可续订的商品的话，你必须提供UI来是他们能撤销购买。
	
4. Process the transaction 

   原因:queue 创建了一个transaction对象来处理的交易请求。当transcation的状态发生变化时，SK会通过调用```paymentQueue:updatedTransactions```通知你的observer
   
5. Provide the paid content

	原因:当app收到transaction 的状态为SKPaymentTranscationStatePurchased 或者 SKPaymentTransactionStateRestored 时，我们就可以将支付内容进行交付
	
6. Finish the transaction.

  原因：transcation会一直在payment queue中	除非你去移除。SK会在每次应用启动后或者从后台恢复后，调用observer的paymentQueue:updatedTranscation直到transcation从中移除，否则你的用户会一直被询问是否购买
  
7. Test your implementation of In-App Purchase

  原因：在你的应用提交审核前必须经过完整的测试，建议读以下两个:<https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/StoreKitGuide/Chapters/DeliverProduct.html#//apple_ref/doc/uid/TP40008267-CH5-SW12>、<https://developer.apple.com/library/ios/technotes/tn2259/_index.html#//apple_ref/doc/uid/DTS40009578-CH1-FREQUENTLY_ASKED_QUESTIONS>
  
8. 以production URL来检验账单优先 
  
  原因：注意对21007进行再次连接验证，这个是在审核时可能会返回的状态，如果收到此code，那就需要去沙盒环境下再次验证