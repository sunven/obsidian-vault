
https://stackoverflow.com/questions/11922964/how-do-i-view-the-storage-of-a-chrome-extension-ive-installed
https://developer.chrome.com/docs/extensions/reference/api/storage

1. **chrome.storage API**: 这是Chrome提供的专门用于扩展存储数据的API。它有两个主要的存储区域：
    - `chrome.storage.sync`: 用于存储用户的扩展数据，并且可以在用户登录其Chrome账户并启用同步时跨多个设备进行同步。
    - `chrome.storage.local`: 用于本地存储数据，不会跨设备同步。
    这两个存储区域都是异步的，并且受到配额限制，但通常对于扩展来说是足够的。
2. **IndexedDB**: 这是一个低级的API，用于在浏览器中存储大量结构化数据。这也可以在Chrome扩展中使用，并且适合复杂的或大量的数据存储需求。
3. **Cookies**: 通过`chrome.cookies` API，扩展可以读取和写入cookies。这通常用于存储与特定网站或域相关的小量数据。
4. **WebSQL 和 localStorage**: 虽然WebSQL已经不再推荐使用，并且localStorage在扩展中有其局限性（例如，它是同步的，并且有更严格的存储限制），但这些技术在一些老的扩展中可能仍然会被使用。
    
## indexedDB

### openCursor

### IDBObjectStore.getAll

```js
function openDb(name) {
  // 打开数据库 数据库名称 版本号
  const requestDB = indexedDB.open(name) // 监听 IndexedDB 是否创建成功
  requestDB.onsuccess = e => {
    const db = requestDB.result
    console.log('数据库打开成功') // 访问数据库中的所有对象存储
    const transaction = db.transaction(db.objectStoreNames)
    Array.from(db.objectStoreNames).forEach(c => {
      const objectStore = transaction.objectStore(c)
      const all = objectStore.getAll()
      all.onsuccess = e => {
        console.log(c, e.target.result)
      }
    })
  }
  requestDB.onerror = e => {
    console.log('数据库打开报错', e)
  }
}
openDb('WebHighlights')
```
