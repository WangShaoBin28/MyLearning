
openssl一直是觉得是个奇葩的工具，非人类，下辖的各种command和option同名...各种凌乱

## 正文

[从这里抄的命令](https://techglimpse.com/sha256-hash-certificate-openssl/)
```
openssl req -x509 -nodes -sha256 -days 365 -newkey rsa:2048 -keyout techglimpse.com.key -out techglimpse.com.crt
```

从这里面查些要素，然后引申做个笔记

## req command

man里面反正这么写的
 
> req - PKCS#10 certificate request and certificate generating utility

### -x509

这个就是用来创建自签名证书的，用了这个说明这个证书还是一个CA的root，当然是没有人认证你的，浏览器也不可能默认导入你

这个option和x509这个openssl的command的区别是我比较感兴趣的
* manual这command的意思估计是这个option是用来自签名的，对于一般人来说也就是伪造的意思，
* 而x509这个command的意思就是一个签名工具（当然还有好多别的用途，比如格式转换等等）,这个x509 command还有个option是-req，挺变态的吧，这个叫做-req的option是归类在这个command的sign option里的
 
> by default a certificate is expected on input. With this option a certificate request is expected instead.

也就是说本来期待提供一个证书来签名的，结果这个设置使得这个工具，变成了期待一个证书的request，我靠，这个request哪儿来的？就是用req那个命令搞出来的东西啊，也就是所谓[CSR](https://www.sslshopper.com/what-is-a-csr-certificate-signing-request.html)，至少朕目前是这么理解的，还有这个[参考](https://en.wikipedia.org/wiki/Certificate_signing_request)


