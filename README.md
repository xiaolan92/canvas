最近公司需要给上传的图片加一个上传的文字水印，防止盗用，由于公司有这个业务需求，我就抽空研究一下，以此记录笔记：

往canvas上添加图片和文字：
```
 const img = new Image();
    const canvas  = document.createElement('canvas'),
           ctx = canvas.getContext('2d');

    img.width =  canvas.width = 300;
    img.height =  canvas.height = 300;
    img.onload = ()=>{
        ctx.drawImage(img,0,0,img.width,img.height,0,0,canvas.width,canvas.height)
        ctx.font = `bold 30px arial`;
        ctx.fillStyle = 'rgba(255, 0, 0, .2)';
        ctx.textBaseline = 'bottom';
        // 弧度制  可以通过角度值计算：degree * Math.PI / 180
        // 旋转
        ctx.rotate(45 * Math.PI / 180);
        // 移动
        ctx.translate(130,20)
        let txt = '1234567';
        ctx.fillText(txt, 0, 0);
        document.body.appendChild(canvas);
    }
    img.url = '图片地址';
```
***
```
// File转DataURL
function readBlobAsDataURL (file,callback){
  const fr = new FileReader();
  fr.onload = (e)=>{
     // e.target.result 为图片的url
    callback(e.target.result);
  }
  fr.readAsDataURL(file);
}

```
***
```
//  type 图片的mime
 const formatUrl =canvas.toDataURL(type)
```
***
```
function dataURLtoBlob(url) {

  let arr = url.split(','), mime = arr[0].match(/:(.*?);/)[1],

      bstr = atob(arr[1]), i = bstr.length, u8arr = new Uint8Array(i);

  while(i--){

    u8arr[i] = bstr.charCodeAt(i);

  }

  return new Blob([u8arr], {type:mime});

}
```
***
```
new File([dataURLtoBlob(formatUrl)], name, { type })
```
***

```
 // 在页面渲染合成后的图像，释放创建的 URL 对象。
 URL.revokeObjectURL(img.url);
```
