#### js对象引用和赋值

- 引用类型赋值中，想要复制对象互不影响，可以用**转换赋值****或**遍历key：value**

  - **转换赋值**

  ```javascript
  var data = {b:[0,1]};
  var str = JSON.stringify(data);
  var data1 = JSON.parse(str);
  data1["b"][0]=1;
  console.log(data["b"][0]);//1
  ```

#### Object类型的赋值

- 两种方式：字面直接量赋值和.赋值

  - 字面直接量

    ```javascript
    d1 = new Object({a:1});
    ```

  - .赋值

    ```javascript
    d1 = new Object();
    d1.a = 1;
    ```

 