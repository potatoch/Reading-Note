一、动画中的三角学
    1、角度和弧度互换
        radians = drgrees * Math.PI / 180;
        degrees = radians * 180 / Math.PI;
    2、朝向鼠标旋转
        dx = mouse.x - object.x;
        dy = mouse.y - object.y;
        object.rotation = Math.atan2(dy,dx) * 180 / Math.PI;
    3、创建波
        (function drawFrame(){
            window.requestAnimationFrame(drawFrame,canvas);
            value = center + Math.sin(angle) * range;
            angle += speed;
        }())
    4、创建圆形
        (function drawFrame(){
            window.requestAnimationFrame(drawFrame,canvas);
            xposition = centerX + Math.cos(angle) * radius;
            yposition = centerY + Math.sin(angle) * raidus;
            angle += speed;
        }())
    5、创建椭圆形
        (function drawFrame(){
            window.requestAnimationFrame(drawFrame,canvas);
            xposition = centerX + Math.cos(angle) * radiusX;
            yposition = centerY + Math.sin(angle) * radiusY;
            angle += speed;
        }())
    6、获取两点间的距离
        dx = x2 - x1;
        dy = y2 - y1;
        dis = Math.sqrt(dx * dx + dy * dy);
二、色彩
    1、组合三原色
        color = red << 16 | green << 8 | blue;
    2、提取三原色
        red = color >> 16 & 0xFF;
        green = color >> 8 & 0xFF;
        blue = color & 0xFF;
    3、绘制一条穿越某个点的曲线
        x1 = xt * 2 - (x0 + x2) / 2;
        y1 = yt * 2 - (y0 + y2) / 2;
        context.moveTo(x0,y0);
        context.quardraticCurveTo(x1,y1,x2,y2);
        //(x1,y1)是控制点，(x2,y2)是重点

