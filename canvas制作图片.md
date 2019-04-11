```
<img id="canvasShow" />
<canvas id="mycanvas" width="750" height="1130" style="display: none;"></canvas>
//需要引入的js
<script src="./static/js/jquery.js"></script>
<script src="./static/js/html2canvas.js"></script>

<script>
    //本地缓存变量
    var val = localStorage.getItem('name'),
        //需要p到底图上的图片
        ha = './static/images/join_code.jpg';
    window.onload = function() {
        tupian(val, ha);
    }


    function tupian(a, h){
        var cvs = document.getElementById('mycanvas');
        var ctx=cvs.getContext("2d");
        var bj = new Image();
        // let max = 1, min = 5;
        // let ran0 = parseInt(Math.random()*(max-min+1)+min,5);
        // console.log(ran0);
        bj.src='./static/images/back.jpg';
        // bj.setAttribute("crossOrigin",'Anonymous')
        // console.log(bj.src);
        bj.onload=function() {
            ctx.drawImage(bj, 0, 0, 750, 1130);
            var erweima = new Image();
            // erweima.src = "/static/xzh/images/code.png";
            // erweima.onload=function(){
            // ctx.drawImage(erweima, 42, 850, 130, 130)
            var head = new Image();
            head.src=h;
            head.setAttribute("crossOrigin",'Anonymous')

            head.onload = function() {
                circleImg(ctx, head, 150, 44, 43);
                draw(a);

            }
            // }
        }
        function draw(a){
            // a = a+'的朋友圈分析';
            ctx.font = "normal normal normal 38px iconfont ";
            ctx.fillStyle = "#362f58";
            ctx.textAlign = 'left';
            ctx.textBaseline = 'top';
            // var txt = a.split(''), arr = [];;
            // for(let i = 0; i < txt.length; i++) {
            //     arr.push(txt[i] + '');
            // }
            // var atxt = arr.join(' ')
            // console.log(atxt);
            setTimeout(function() {
                ctx.fillText(a, 180, 284);
                saveImageInfo();
            }, 300);
        }
        //将画布生成图片
        function saveImageInfo() {
            var mycanvas = document.getElementById("mycanvas");
            var image = mycanvas.toDataURL("image/png");
            $("#canvasShow").attr("src",image)
            setTimeout(function(){
                // $("#loading").css({"display":"none"})
                $("#canvasShow").css({"display":"block"})
            }, 500)
        }
    }
    $('.btn').on('click', function() {
        tupian(val, ha);
    });
    function circleImg(ctx, img, x, y, r) {
        ctx.save();
        var d =2 * r;
        var cx = x + r;
        var cy = y + r;
        ctx.arc(cx, cy, r, 0, 2 * Math.PI);
        ctx.clip();
        ctx.drawImage(img, x, y, d, d);
        ctx.restore();
    }
    function getDom(id){
        return document.getElementById(id);
    }

    CanvasRenderingContext2D.prototype.fillTextVertical = function (text, x, y) {
        var context = this;
        var canvas = context.canvas;

        var arrText = text.split('');
        var arrWidth = arrText.map(function (letter) {
            return context.measureText(letter).width;
        });

        var align = context.textAlign;
        var baseline = context.textBaseline;

        if (align == 'left') {
            x = x + Math.max.apply(null, arrWidth) / 2;
        } else if (align == 'right') {
            x = x - Math.max.apply(null, arrWidth) / 2;
        }
        if (baseline == 'bottom' || baseline == 'alphabetic' || baseline == 'ideographic') {
            y = y - arrWidth[0] / 2;
        } else if (baseline == 'top' || baseline == 'hanging') {
            y = y + arrWidth[0] / 2;
        }

        context.textAlign = 'center';
        context.textBaseline = 'middle';

        // 开始逐字绘制
        arrText.forEach(function (letter, index) {
            // 确定下一个字符的纵坐标位置
            var letterWidth = arrWidth[index];
            // 是否需要旋转判断
            var code = letter.charCodeAt(0);
            if (code <= 256) {
                context.translate(x, y);
                // 英文字符，旋转90°
                context.rotate(90 * Math.PI / 180);
                context.translate(-x, -y);
            } else if (index > 0 && text.charCodeAt(index - 1) < 256) {
                // y修正
                y = y + arrWidth[index - 1] / 2;
            }
            context.fillText(letter, x, y);
            // 旋转坐标系还原成初始态
            context.setTransform(1, 0, 0, 1, 0, 0);
            // 确定下一个字符的纵坐标位置
            var letterWidth = arrWidth[index];
            y = y + letterWidth;
        });
        // 水平垂直对齐方式还原
        context.textAlign = align;
        context.textBaseline = baseline;
    };
</script>

```