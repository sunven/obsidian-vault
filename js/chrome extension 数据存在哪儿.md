
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

IDBObjectStore.getAll

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

```js
function* cursorGenerator(objectStore) {
  let request = objectStore.openCursor();
  let cursor = yield request;

  while (cursor) {
    yield cursor.value;  // 返回当前游标指向的记录
    cursor = yield cursor.continue();  // 移动到下一个记录
  }
}

// 这是一个用来处理生成器的函数，它会处理所有异步操作
function runCursorGenerator(generator, callback) {
  let gen = generator();

  // 处理每一个yield返回的请求
  function handleRequest(request) {
    request.onsuccess = () => {
      let result = gen.next(request.result);
      if (!result.done) {
        // 如果生成器还未完成，继续处理
        handleRequest(result.value);
      } else {
        // 如果生成器已经完成，调用回调函数
        callback();
      }
    };
    request.onerror = (error) => {
      // 处理错误
      console.error('Cursor iteration failed', error);
    };
  }

  // 开始迭代
  handleRequest(gen.next().value);
}

// 使用封装的Generator函数
const request = indexedDB.open('my_database', 1);

request.onsuccess = function(event) {
  const db = event.target.result;
  const transaction = db.transaction(['my_object_store'], 'readonly');
  const objectStore = transaction.objectStore('my_object_store');

  // 使用runCursorGenerator来执行cursorGenerator
  runCursorGenerator(cursorGenerator.bind(null, objectStore), () => {
    console.log('Cursor iteration complete.');
  });
};

request.onupgradeneeded = function(event) {
  const db = event.target.result;
  db.createObjectStore('my_object_store', { keyPath: 'id' });
};

request.onerror = function(event) {
  console.error('Database error:', event.target.errorCode);
};
```