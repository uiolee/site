---
title: Deployer
---

deployer เป็นตัวช่วยให้ผู้ใช้ deploy เว็บไซต์ไปถึง remote server โดยไม่ต้องใช้คำสั่งซับซ้อน

## Synopsis

``` js
hexo.extend.deployer.register(name, function(args){
  // ...
});
```

argument `args` จะเข้า function และ argument นี้จะส่ง input ของผู้ใช้เข้า terminal `args` เป็น argument ท่ีจะส่งเข้า function   ในไฟล์ `_config.yml` มีค่า `deploy` และคำสั่งท่ีผู้ใช้ต้องการพิมพ์ลงเข้า terminal
