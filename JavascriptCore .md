# JavascriptCore 

## JSContext

执行JS代码时所处的上下文环境

## JSValue
JSValue是对所有JS类型的一个wrapper，并且提供了转换的方法

JS Type|JSValue Method|Obj-C type|
----|----|----|
string |toString| NSString|
boolean|toBool| Bool|
number|toNumber toDouble toInt32 toUInt32|NSNumber double int32\_t uint32\_t
date|toDate|NSDate
Array|toArray | NSArray|
Object|toDictionary|NSDictionary|
Object|toObject toObjectClass:|custom type


## JsManagedValue

"condtional retain"

如果以下两个条件都不满足，那么managed value会将其value属性置空，并且释放其下的JSValue的对象