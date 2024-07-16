```http
GET /s?wd=wrn HTTP/1.1   
	请求方式 uri 协议/版本号
Host: www.baidu.com 
	主机
Cookie: BIDUPSID=32F4BDE23517E7D2E257867CE90BF9B0; PSTM=1709738839; BAIDUID=32F4BDE23517E7D247314C8202488CB5:FG=1; H_PS_PSSID=40154_40170_39661_40210_40207_40217_40223_40250_40294_40290_40288_40286_40317_40079_40365_40352_40303_40378; BD_UPN=12314753; BA_HECTOR=a80l04a5a40l0ka184ag250gukut9j1iuh2qt1t; BAIDUID_BFESS=32F4BDE23517E7D247314C8202488CB5:FG=1; ZFY=u:AyuDGrxoVVoPE2MxrlIEreTpbqUAcS5IjLrG8Blezs:C; BDORZ=B490B5EBF6F3CD402E515D22BCDA1598; rsv_jmp_slow=1709739285888; BD_CK_SAM=1; PSINO=3; delPer=0; H_PS_645EC=e7f55B9VH72xEblVqj2u3VAjI7nuwwLHvooxQs7mmOKfBtBAMDed9HAdDnw; COOKIE_SESSION=0_0_1_1_0_1_1_0_1_1_9_0_0_0_0_0_0_0_1709739397%7C1%230_0_1709739397%7C1
	浏览器端鉴权信息；对应服务器端session
Cache-Control: max-age=0
Sec-Ch-Ua: "Chromium";v="103", ".Not/A)Brand";v="99"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.5060.134 Safari/537.36
	客户端告诉服务器用了啥浏览器
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
	接收什么返回值
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate
	接收的压缩方式
Accept-Language: zh-CN,zh;q=0.9
Connection: close
防盗链
Origin:uri
	被哪个网页引用
Referer:uri
	从哪个网页跳转的

```


https:=http+ssl
