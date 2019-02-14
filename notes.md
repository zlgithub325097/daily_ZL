* [x] > ### iOS 真机调试包路径

```
/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport
```

* [x] > ### iOS NSString 与NSData 互转

```
1. 字符串转Data

NSString * str =@"str"; 

NSData *data =[str dataUsingEncoding:NSUTF8StringEncoding];

2.NSData 转NSString

NSString * str  =[[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];

3.data 转char

NSData *data; 

char * haha=[data bytes]; 

4. char 转data 

byte * byteData = malloc(sizeof(byte)*16); 

NSData *content=[NSData dataWithBytes:byteData length:16];
```

* [x] > ### 将字典或者数组转化为JSON串

```
- (NSData *)toJSONData:(id)theData{

    NSError *error = nil;
    NSData *jsonData = [NSJSONSerialization dataWithJSONObject:theData
                                                       options:NSJSONWritingPrettyPrinted
                                                         error:&error];

    if ([jsonData length] > 0 && error == nil){
        return jsonData;
    }else{
        return nil;
    }
}
```

* [x] > ### json格式字符串转数组

```
-  (id)toArrayOrNSDictionary:(NSData *)jsonData{

    NSError *error = nil;
    id jsonObject = [NSJSONSerialization JSONObjectWithData:jsonData
                                                    options:NSJSONReadingAllowFragments
                                                      error:nil];

    if (jsonObject != nil && error == nil){
        return jsonObject;
    }else{
        // 解析错误
        return nil;
    }

}
```



