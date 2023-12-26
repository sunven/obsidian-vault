
https://stackoverflow.com/questions/11922964/how-do-i-view-the-storage-of-a-chrome-extension-ive-installed
https://developer.chrome.com/docs/extensions/reference/api/storage

```js
function log(transaction, storeName) {

  // db.transaction(db.objectStoreNames) 访问数据库中的所有对象存储

  const objectStore = transaction.objectStore(storeName)

  const request = objectStore.openCursor()

  request.onsuccess = event => {

    const cursor = event.target.result

    if (cursor) {

      console.log('cursor ', cursor.value)

      cursor.continue()

    } else {

      console.log('没有更多数据了！')

    }

  }

}

  

function openDb(name) {

  // 打开数据库 数据库名称 版本号

  const requestDB = indexedDB.open(name)

  // 监听 IndexedDB 是否创建成功

  requestDB.onsuccess = e => {

    const db = requestDB.result

    console.log('数据库打开成功', Array.from(db.objectStoreNames))

    // 访问数据库中的所有对象存储

    const transaction = db.transaction(db.objectStoreNames)

    Array.from(db.objectStoreNames).forEach(c => {

      log(transaction, c)

    })

  }

  requestDB.onerror = e => {

    console.log('数据库打开报错', e)

  }

}

  

openDb('WebHighlights')
```