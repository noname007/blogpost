
# backbone router test case

```
var QuqiRouter = Backbone.Router.extend({
    routes:{
        'm/:quqi_id':'role',             //匹配示例 m/123 m/abcde 
        'd/:quqi_id/:tree_id/:node_id(/:isDoc)':'node', //匹配示例  d/1/2/3/0  d/1/2/3  这里特别强调 d/1/2/3/不会匹配到这里
        ':quqi_id/:node_id(?:query)':'innerlink',//匹配示例 1/2?abcde  1/2
        'c:quqi_id/d:item_id':'collect' //匹配示例 c123/d456  cabc/dlmn
        'file/*path':'download'        //匹配示例 file/123  file/abdioi/wewew
        'node/:node1-:node2':'nodeI'      //匹配示例 node/1-2  node/m-n
        /^(.*?)\/test/:'test'         //匹配示例 gadd02312-231/test 
        /(\d+)\/(\d+)/:'test3'     //匹配示例 123/456  789/321  
    }
});

```


具体的路由器原理