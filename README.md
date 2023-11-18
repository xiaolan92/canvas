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
