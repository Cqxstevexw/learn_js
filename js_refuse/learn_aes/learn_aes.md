# 对称加密之所以对称就是因为这类算法对明文的加密和解密使用的是同一个密钥
# 加密三要素
## AES支持三种长度的密钥:128位，192位，256位
## 填充
- 说道填充一定要说下AES分组加密的特性，aes加密并不是一股脑将明文加密成密文的，而是把明文拆分成一个个独立的明文块，且每个明文块128bit
- 假如一段明文长度是196bit，如果按每128bit一个明文块拆分的话，第二个明文块只有64bit，不足128bit就需要对明文块进行填充(Padding)
- 下列模式：
    - NoPadding 
    - PKCS7Padding
    - ZeroPadding
    - AnsiX923
    - Iso10126
    - Iso97971
## 模式
- AES的工作模式，体现在把明文块加密成密文块的处理过程中。AES加密算法提供了五种不同的工作模式：
    CBC、ECB、CTR、CFB、OFB、
    - ECB模式是最简单的工作模式，该模式下，每一个明文块的加密都是完全独立，互不干涉
        相同的明文块经过加密会变成相同的明文块，因此安全性较差
    - CBC模式引入一个新的概念:初始向量IV(IV是，它的作用和MD5的加盐有些类似，目的是防止同样的明文块始终加密成同样的密文块)
        CBC模块在每一个明文块加密前会让那个明文块和一个值先做异或处理。
        IV作为初始化向量，参与第一个明文块的异或，后续的每一个明文块和它前一个明文块所加加密出的米文块相异或，这样相同的明文块加密出的
        密文块显然是不一样的
            好处：安全性更高
            坏处：无法并行计算，性能上比不上ECB，引入初始化向量IV，增加复杂度

# AES加密流程总结
    - 把明文按照128bit拆分成若干个明文块
    - 按照选择的填充方式来填充最后一个明文块
    - 每一个明文块利用AES加密器和密钥，加密成密文块
    - 拼接所有的密文块，成为最终的密文结果

