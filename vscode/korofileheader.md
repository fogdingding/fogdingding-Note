# koroFileHeader

在撰寫程式的時候，總是會需要打上註解，這時候如果有個工具能夠幫我們先創建一些基本的欄位就能節省不少時間

```bash
control+command+i 文件介紹
control+command+t 函數介紹
```

control+command+i 文件介紹

```javascript
/*
 * @Author: fogdingding
 * @Date: 2020-09-08 10:52:17
 * @LastEditTime: 2020-09-10 17:43:03
 * @LastEditors: Please set LastEditors
 * @Description: 主要進行股票相關資訊介接
 * @FilePath: /Documents/kolinfluence-server-api/src/controllers/stock/stockController.js
 */
```

control+command+t 函數介紹

```javascript
/**
 * @description: 回傳有關於個股的簡介
 * @param {number} stockId 個股編號 
 * @return {Array} promiseArray 等待所有的Promise的資料，promiseArray內的子原件
 */
```

### 欄位介紹

（1）對文件進行描述  
[             @author](http://usejsdoc.org/tags-author.html) —— 指定項目作者  
[             @copyright](http://usejsdoc.org/tags-copyright.html) —— 描述版權信息  
[             @see](http://usejsdoc.org/tags-see.html) —— 描述可以參考外部資源  
[             @version](http://usejsdoc.org/tags-version.html) —— 描述版本信息  
[             @tutorial](http://usejsdoc.org/tags-tutorial.html) —— 插入一個指向教程的鏈接，作爲文檔的一部分  
[             @since](http://usejsdoc.org/tags-since.html) —— 描述該功能哪個版本哪個時間添加進來的  
[             @summary](http://usejsdoc.org/tags-summary.html) —— 描述一個簡寫版本  
[             @file](http://usejsdoc.org/tags-file.html) —— 文件說明，在文件開頭使用  
[             @license](http://usejsdoc.org/tags-license.html) —— 描述代碼纔有那種軟件許可協議

     （2）標註js使用方法  
[             @returns](http://usejsdoc.org/tags-returns.html) —— 描述一個函數的返回值  
[             @param](http://usejsdoc.org/tags-param.html) —— 描述傳遞給函數的參數  
[             @description](http://usejsdoc.org/tags-description.html) —— 描述  
[             @example](http://usejsdoc.org/tags-example.html) —— 舉例  
[             @throws](http://usejsdoc.org/tags-throws.html) —— 描述可能會被拋出什麼樣的錯誤

     （3）開發者備註  
[             @deprecated](http://usejsdoc.org/tags-deprecated.html) —— 標註關聯代碼已經被棄用  
[             @todo](http://usejsdoc.org/tags-todo.html) —— 描述一個將要完成的任務

     （4）文件詳細結構  
[             @abstract](http://usejsdoc.org/tags-abstract.html) —— 標註該成員必須在子類中實現或重寫  
[             @access](http://usejsdoc.org/tags-access.html) —— 標註該成員的訪問級別  
[             @access](http://usejsdoc.org/tags-access.html) private &gt; [@private](http://usejsdoc.org/tags-private.html)  
[             @access](http://usejsdoc.org/tags-access.html) protected &gt; [@protected](http://usejsdoc.org/tags-protected.html)  
[             @access](http://usejsdoc.org/tags-access.html) public &gt; [@public](http://usejsdoc.org/tags-public.html)  
[             @augments](http://usejsdoc.org/tags-augments.html)（[@extends](http://usejsdoc.org/tags-extends.html)） —— 標註這個子類繼承自哪個父類，後面需要加父類名  
[             @class](http://usejsdoc.org/tags-class.html)（[@constructor](http://usejsdoc.org/tags-constructor.html)） —— 標註該函數是一個構造函數，需要使用new來實例化 function MyClass\(\){}  
[             @constant](http://usejsdoc.org/tags-constant.html)（[@const](http://usejsdoc.org/tags-const.html)） —— 標註這個對象是一個常量  
[             @constructs](http://usejsdoc.org/tags-constructs.html) —— 標註這個函數用來作爲類的構造器  
[             @default](http://usejsdoc.org/tags-default.html) —— 標註默認值  
[             @exports](http://usejsdoc.org/tags-exports.html) —— 標註javascript模塊導出的內容  
[             @function](http://usejsdoc.org/tags-function.html)（[@func](http://usejsdoc.org/tags-func.html)、[@method](http://usejsdoc.org/tags-method.html)） —— 標註該對象作爲一個函數  
[             @global](http://usejsdoc.org/tags-global.html) —— 標註爲全局變量（對象）  
[             @implements](http://usejsdoc.org/tags-implements.html) —— 標註實現一個接口  
[             @inheritdoc](http://usejsdoc.org/tags-inheritdoc.html) —— 標註繼承其父類的文檔  
[             @inner](http://usejsdoc.org/tags-inner.html) —— 標註爲其父類的內部成員  
[             @instance](http://usejsdoc.org/tags-instance.html) —— 標註爲其父類的實例成員  
[             @interface](http://usejsdoc.org/tags-interface.html) —— 標註其爲可以實現的接口  
[             @kind](http://usejsdoc.org/tags-kind.html) —— 指明標註的類型（[@kind](http://usejsdoc.org/tags-kind.html) class = [@class](http://usejsdoc.org/tags-class.html)）  
[             @lends](http://usejsdoc.org/tags-lends.html) —— 將一個字面量對象的所有成員標記爲某個類（或模塊）的成員  
[             @memberof](http://usejsdoc.org/tags-memberof.html) —— 標註成員屬於哪個父級  
[             @mixes](http://usejsdoc.org/tags-mixes.html) —— 標註該對象混入了另一個對象的所有成員  
[             @mixin](http://usejsdoc.org/tags-mixin.html) —— 標註一個混入對象  
[             @module](http://usejsdoc.org/tags-module.html) —— 將當前文檔標註爲一個模塊  
[             @protected](http://usejsdoc.org/tags-protected.html)—— 標註爲受保護的  
[             @public](http://usejsdoc.org/tags-public.html) —— 標註爲公開的  
[             @readonly](http://usejsdoc.org/tags-readonly.html) —— 標註爲只讀的  
[             @requires](http://usejsdoc.org/tags-requires.html) —— 標註這個文件需要一個javascript模塊  
[             @static](http://usejsdoc.org/tags-static.html) —— 標註爲靜態的  
[             @type](http://usejsdoc.org/tags-type.html) —— 標註類型  
[             @typeof](http://usejsdoc.org/tags-typeof.html) —— 標註一個自定義的類型  
[             @this](http://usejsdoc.org/tags-this.html) —— 描述this關鍵字的指向  
[             @alias](http://usejsdoc.org/tags-alias.html) —— 標註成員有一個別名  
[             @borrow](http://usejsdoc.org/tags-borrow.html) —— 將另一個標識符的描述添加到當前標識符的描述  
[             @name](http://usejsdoc.org/tags-name.html) —— 強制jsdoc使用這個給定的名稱，而忽略代碼裏的實際名稱  
[             @namespace](http://usejsdoc.org/tags-namespace.html) —— 標註一個命名空間對象  
[             @override](http://usejsdoc.org/tags-override.html) —— 標註覆蓋其父類同名的方法  
[             @private](http://usejsdoc.org/tags-private.html) —— 標註爲私有  
[             @classdesc](http://usejsdoc.org/tags-classdesc.html) —— 與[@class](http://usejsdoc.org/tags-class.html)結合使用，描述類  
[             @callback](http://usejsdoc.org/tags-callback.html) —— 描述一個回調函數  
[             @enum](http://usejsdoc.org/tags-enum.html) —— 描述一個靜態屬性值的全部相同的集合，通常與[@readonly](http://usejsdoc.org/tags-readonly.html)結合使用  
[             @event](http://usejsdoc.org/tags-event.html) —— 描述事件  
[             @member](http://usejsdoc.org/tags-member.html) —— 描述一個成員 [@member](http://usejsdoc.org/tags-member.html) \[\] \[\]  
[             @property](http://usejsdoc.org/tags-property.html) —— 描述一個對象的屬性  
[             @external](http://usejsdoc.org/tags-external.html) —— 標識一個外部的類，命名空間，或模塊  
[             @files](http://usejsdoc.org/tags-files.html) —— 標明當一個方法被調用時將觸發一個指定類型的事件  
[             @listens](http://usejsdoc.org/tags-listens.html) —— 標註監聽事件  
[             @variation](http://usejsdoc.org/tags-variation.html) —— 區分具有相同名稱的不同對象

### 參考資料

* [參考網站](https://www.twblogs.net/a/5d127d0ebd9eee1e5c822fd4)

