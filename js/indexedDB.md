
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