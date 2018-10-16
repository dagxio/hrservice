
## ubuntu安装依赖

```sh
sudo apt-get install -y nodejs
sudo ln -s /usr/bin/nodejs /usr/sbin/node
sudo apt-get install npm
npm install -g n
n lts
npm install -g pm2
sudo apt-get install sqlite3
```

### 第一次运行设置devicename和密码
```sh
./setinfo.sh devicename passphrase
```
```javascript
 //更改play/rpc_service.js中加密密码 
 var encryptkey = "12345678123456781234567812345678";
 ```

## 运行

```sh
node start.js
```

## 后台运行

```sh
pm2 start start.js
```
运行后控制台会打印一个地址

Witness SingleAddress --------------> 

#
#

## 接口说明
接口协议：rpc

[rpc示例文档](https://github.com/dagxio/Bsure-api-wal)

接口地址 http://localhost:6332

**以post方式发送json串**
```json
{"jsonrpc":"2.0","id":1,"method":"methodname","params":[]}
```
**返回格式**
```json
{
"jsonrpc": "2.0",
"result": true,
"id": 1
}
```

```json
//错误
{
    "jsonrpc": "2.0",
    "error": {
        "code": -32700,
        "message": "Invalid Request"
    },
    "id": null
}
```

##### 查询某个收款地址历史
`参数address为商品地址`
```json
{"jsonrpc":"2.0","id":1,"method":"listtransactions","params":{"address": "VXA5Q27TPFZAO4DGKRR3W2D62YIM7GPD"}}
```

**返回：**
```json
{
"jsonrpc": "2.0",
"result": [{
    "action": "received",
    "amount": 100000,//金额
    "my_address": "VXA5Q27TPFZAO4DGKRR3W2D62YIM7GPD",//商品地址
    "arrPayerAddresses": [
        null
    ],
    "confirmations": 1,
    "unit": "DKEqxD6E93TEm+6P088U+0g2eCh7PRp/xLC55YfVohc=",
    "fee": 954,//手续费
    "time": "1536807729",
    "level": null,
    "mci": 977739,
    "asset": "jH12XQGk0JJxYAO7j/lK0jrRjKVuEFc9mfTUc14mx1g="//资产
}],
"id": 1
}
```

##### 生成地址
```json
{"jsonrpc":"2.0","id":1,"method":"getnewaddress","params":[]}
```
**返回:**
```json
{
    "jsonrpc": "2.0",
    "result": "",
    "id": 0
}
```
##### 简历上链
```json
{"jsonrpc":"2.0","id":0,"method":"addjobseeker","params":["TATKLD6GFKWKZVYMCCTA3RNOWIIFDMK5",{"name":"王浩然","sex":"男","nationality":"汉","idnum":"0000000000001","birth":"03580106","address":"长安","jobtarget":"诗人","skill":"写诗","bank":"00000000","phone":"000000"}]}
```
返回
```json
{
    "jsonrpc": "2.0",
    "result": "查看unit: https://explorer.bsure.vip/#Q5s9r6qGkWpMTYa02OH/MSr6OnlnWRqMhkVrL4Zys3I=\n\n [private profile](profile:eyJ1bml0IjoiUTVzOXI2cUdrV3BNVFlhMDJPSC9NU3I2T25sbldScU1oa1ZyTDRaeXMzST0iLCJwYXlsb2FkX2hhc2giOiJzeXBCUEV5WnNUVVFTeWVOTCtWSnNGdHF0blFWVVZvTVNnVWpUV1pDdWJJPSIsInNyY19wcm9maWxlIjp7IuWnk+WQjSI6WyLnjovmtannhLYiLCIzaHZqa3ZjQldvb0NRdGJiIl0sIuaAp+WIqyI6WyLnlLciLCJROFN0Q2g5WDlzSWpqT3RqIl0sIuawkeaXjyI6WyLmsYkiLCJaaldNZ25nMHE5V0VPMThuIl0sIui6q+S7veivgSI6WyJTL3Y5ckZrZ0xPQzVTUWpnaXh5bmpnPT0iLCJQNmxZdlliYXlrYW1pd2I5Il0sIuWHuueUn+aXpeacnyI6WyIwMzU4LTAxLTA2IiwiTjlHNjJxaVhBVVBGNDBFRCJdLCLkvY/lnYAiOlsi6ZW/5a6JIiwieExMK1dSWGV0SHRwZVAwTCJdLCLmsYLogYzmhI/lkJEiOlsi6K+X5Lq6IiwiUFhHNHM0QnJwZTN0c1VxNyJdLCLnibnplb8iOlsi5YaZ6K+XIiwiSy9vMlRsRmExc0l0azBmaCJdLCLpk7booYzljaHlj7ciOlsieG0wVnlWRWJ5QU5GREh1bUV5c2I0UT09IiwiVjdmZzVvQ1dmUC85b1dUZCJdLCLnlLXor50iOlsicDNIWFY1cmZPeWxHaWdma3Vzdk4zQT09IiwiUlZMZ1BVQ1BpeWRSSE1KTyJdfX0=) ",
    "id": 0
}
```

