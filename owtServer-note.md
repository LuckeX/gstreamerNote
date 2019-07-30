### 1 management_api

1 requestHandler.js

-   addServerSideSubscription(roomId, subReq, callback)###

#### 1.1 resource

2.  analyticsResource.js
    

-   getList(req,res,next)
    
-   add(req,res,next)
    
    > Add analytics for room,调用requestHandler.js的addServerSideSubscription函数
    
-   delete(req,res,next)
    

#### 1.2 rpc

1 rpc.js

-   callRpc(to, method, args, callbacks, timeout)

> 发送消息到exchange，routingkey=to（简单理解为给to发送消息）

-   connect(options)
    
    > 创建一个owtRpc（exchange），并创建一个queue，该queue与owtRpc绑定（direct方式），然后subscribe该queue
    

### 2 agent

#### 2.1 analytics

1 analytics-agent.js

-   AddonEngine类
    
    > 1 setInput(...) //给input stream 设置source（FrameSource类）和
    > 
    > ```
    >                     // decoder
    > ```
    > 
    > 2 unsetInput(...) //与setInput相反
    > 
    > 3 addOutput(...) // add processer, analyzer, encoder and streamID
    > 
    > ```
    >                          // for outputs
    > ```
    > 
    > 4 removeOutput(...)
    > 
    > 5 close()
    

2 base-agent.js

3 InternalConnectionFactory.js

4 InternalIn.h

### 3 owt 加log步骤

> 开启analytics ，首先sub选择9735，video，audio_codec，h264-CB，设置下streaming，启动

> 1.  修改js，加打印
>     
> 2.  ./scripts/build.js -t //只build某一个模块
>     
> 3.  ./scripts/pack.js -t //只pack某一个模块
>     
> 4.  把 libmyplugin.so 拷贝到 ./dist/analytics_agent/lib里面
>     
> 5.  安装openh264 ./install_openh264.sh
>     
> 6.  启动owt__
>     

`./scripts/build.js -t video-analyzer-sw && ./scripts/pack.js -t analytics-agent && cp ../libmyplugin.so ./dist/analytics_agent/lib/ && ./dist/analytics_agent/install_openh264.sh `

`rm -fr logs/ && ./bin/stop-all.sh && kill -9 $(pidof node) && ./bin/start-all.sh `
