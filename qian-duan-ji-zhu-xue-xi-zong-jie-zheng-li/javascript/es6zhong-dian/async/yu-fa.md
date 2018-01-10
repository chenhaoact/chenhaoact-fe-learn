## 二 语法

在 **async function 中**，可**通过 await 关键字来等待一个 Promise 被 resolve（或者 reject，此时会抛出异常）**， 

```
const fn = async function() {
  const user = await getUser();
  const posts = await fetchPosts(user.id);
  return { user, posts };
};
fn().then(res => console.log(res)).catch(err => console.error(err.stack));
```



