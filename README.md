### Message 全局提示

#### 概述

成功、失败和警告全局提示。

#### 使用说明

*注：该组件须配合Vux使用，ssfe专用*

```
import { mapGetters, mapActions } from 'vuex'
...
methods: {
	 ...mapActions({
        setMessageShow: 'setMessageShow',
      })
}
...
this.setMessageShow({placeHolder:'XXX',kind:'error'[, hideTime: 1500]})
```

#### 参数说明

参数|说明|类型|默认值
---|---|---|---
placeHolder|提示文字|String|无
kind|提示类型|String|'error'
hideTime|提示保持时间|Number|1500
