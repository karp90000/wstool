## 基于fork 的项目 修改了 onmessage  将接收的 blob 格式转换为可识别的字符串


```js
  wsInstance.onmessage = function (ev) {
        console.warn(ev)
        if (!_this.recvPause) {
            let data = ev.data
            if (_this.recvClean) _this.messageData = [];

            let reader = new FileReader();
            reader.readAsArrayBuffer(data,'utf-8');
            reader.onload = function(){
                console.log("blob转arrayBuffer", reader.result);
                let inflatedData = pako.inflate(reader.result, {
                    to:"string"
                })

                _this.writeNews(0, inflatedData);
            }

        }
    }
```
