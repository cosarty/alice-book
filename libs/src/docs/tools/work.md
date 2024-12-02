# 接口

## post请求传二进制


```ts
export function addPost(data) {
  const formdata = new FormData();
  formdata.append('file',data); //转二进制
  return request({
    url: '',
    method: 'post',
    data: formdata,
    headers: { 'Content-Type': 'multipart/form-data' },
  })
}

```