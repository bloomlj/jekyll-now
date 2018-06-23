---
layout: post
title: csrf-is-missing
---

为comftest项目编写代码时候，发现使用multer来解析带有文件上传内容，type为multipart/form-data的表单时候，会不断出现csrf tocken is missing的错误。网上检索了很多解决方案，基本上不靠谱。
分析了产生错误提示的函数，发现实际上lusca库的csrf.js得到的是一个空的req.body；实际上，multer是可以正常解析表单的，这在multer的网页上说的很清楚。那么也就是可能顺序上出了问题。
果然，在router里面，取消默认的csrf验证，将csrf验证放到multer之后进行，一切就都ok了。
