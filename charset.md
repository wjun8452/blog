字符集与字符编码

http://www.regexlab.com/zh/encoding.htm 这篇文章很好！理论性的总结了方方面面。
https://www.ibm.com/developerworks/cn/java/j-lo-chinesecoding/index.html 这篇文章中关于Java编解码中文字符的示例很精彩！


win10 default charset is: Windows-1252
Mac, Fedora4.5, default charset is: UTF-8

一个字符"$"，在不同的字符集中对应的内码相同吗？
答：UNICODE字符集，内码相同。ANSI字符集，内码不同。

操作系统是如何能用正确的字符集来显示SD卡中的文件名称的？

文件名用Windows-1252编码存储在默认编码为UTF-8的电脑上，用java File读出来的文件名正确吗？

ISO-8859-1



对编码的误解一，是sdcardvalidator犯下的错误。


** MEX-Méx_idlookup.sqlite, length=23
--encoding by GBK
   decoding by GBK, MEX-Méx_idlookup.sqlite, length=23,bytes=24, detected_charset=IBM866
   decoding by WINDOWS-1252, MEX-M¨¦x_idlookup.sqlite, length=24,bytes=24, detected_charset=IBM866
   decoding by UTF-8, MEX-M��x_idlookup.sqlite, length=24,bytes=24, detected_charset=IBM866
--encoding by WINDOWS-1252
   decoding by GBK, MEX-M閤_idlookup.sqlite, length=22,bytes=23, detected_charset=WINDOWS-1252
   decoding by WINDOWS-1252, MEX-Méx_idlookup.sqlite, length=23,bytes=23, detected_charset=WINDOWS-1252
   decoding by UTF-8, MEX-M�x_idlookup.sqlite, length=23,bytes=23, detected_charset=WINDOWS-1252
--encoding by UTF-8
   decoding by GBK, MEX-M茅x_idlookup.sqlite, length=23,bytes=24, detected_charset=UTF-8
   decoding by WINDOWS-1252, MEX-MÃ©x_idlookup.sqlite, length=24,bytes=24, detected_charset=UTF-8
   decoding by UTF-8, MEX-Méx_idlookup.sqlite, length=23,bytes=24, detected_charset=UTF-8