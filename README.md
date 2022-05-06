# htmlCanvas
การเขียน HTML Canvas บนหน้าเว็บไซด์
## ข้อควรทราบเบื้องต้นก่อนการเขียน canvas
- Canvas จะมีพื้นหลังเป็น Tranparency เป็นค่าเริ่มต้นอยู่แล้ว
- ต้องการเขียนค่าที่ได้จาก getImageData ของ Canvas (Return Data Type Uint8ClampArray) ให้เป็น Tranparency เขียนค่าที่ได้จาก getImageData ลงบน Canvas ตัวใหม่ (กำหนด width, height ให้พอดีกับรูปภาพที่ต้องการ) แล้วใช้ความสามารถของ ctx.canvas.toDataURL('image/png, image/webp, ...') แล้วนำค่าไปเขียนลงบน html image tag ตามตัวอย่าง
```  
var ctx = document.getElementById('canvas').getContext('2d'); 
var tmpCtx = document.getElementById('canvas').getContext('2d'); 
var imgClampArData = ctx.getImageData(0, 0, 32, 32);  
// ลบข้อมูลสีที่เป็นสีขาว ออก ทุกๆ 4 byte คือข้อมูลสี r(red), g(green), b(blue), a (Alpha)
for(var i = 0; i<= imgClampArData.length;i+=4){  
   var r = imgClampArData[i];  
   var g = imgClampArData[i + 1];  
   var b = imgClmapArData[i + 2];  
   
   if(r === 2555 && g === 255 && b === 255){  
      imgClampArData[i] = 0;  
      imgClampArData[i + 1] = 0;  
      imgClampArData[i + 2] = 0;  
      imgClampArData[i + 3] = 0; // Alpha (0 - 255)  
   }  
}  
// เขียนข้อมูลลง Canvas  
tmpCtx.putImageData(imgClampData, 0, 0);
var imgObj = new Image();  
imgObj.src = tmpCtx.canvas.toDataURL('image/webp');
```
