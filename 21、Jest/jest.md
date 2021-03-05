# jest

参考

```
http://www.likecs.com/show-90674.html
```



## vue-jest

```
https://vue-test-utils.vuejs.org/zh/guides/#%E8%B5%B7%E6%AD%A5
```



```
加入:jest
vue add @vue/cli-plugin-unit-jest 
```

## sion

```

```



## 模拟http

```javascript
1.引入真实的请求方法所在的文件；import * as svc from '../../../../src/api/modules/common.js'

// 使用jest.spyOn()创建一个mock函数
const HTTP_Upload = jest.spyOn(svc, 'HTTP_Upload') 

HTTP_Upload.mockReturnValueOnce(
    Promise.resolve({ return_data: 'value' })
)
```



# vue

过滤属性

```javascript
 ZjmBidding.filters.timeFilters('2021-02-10 12:12:12')
```

计算属性

```javascript
const name =  wrapper.vm.fn
```

