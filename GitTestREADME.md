- š Hi, Iām @swiftGrinder
- š Iām interested in ...
- š± Iām currently learning ...
- šļø Iām looking to collaborate on ...
- š« How to reach me ...

<!---
swiftGrinder/swiftGrinder is a āØ special āØ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body {
            font: 100% Lucida Sans, Verdana;
            margin: 20px;
            line-height: 26px;

        }
        .container {
            min-width: 900px;
        }
        .wrapper {
            position: relative;
            overflow: auto;

        }
        #top,#sidebar, #bottom, .menuitem{
            border-radius: 4px;
            margin: 4px;

        }
        #top {
            background-color: #4CAF50;
            color: #ffffff;
            padding: 15px;

        }
        #menubar {
            width: 200px;
            float: left
        }

        #main{
            padding: 10px;
            margin: 0 210px;

        }
        #sidebar {
            background-color: #32a4e7;
            color: #ffffff;
            padding: 10px;
            width: 180px;
            bottom: 0;
            top: 0;
            right: 0;
            position: absolute;

        }
        #bottom {
            border: 1px solid #d4d4d4;
            background-color: #f1f1f1;
            text-align: center;
            padding: 10px;
            font-size: 70%;
            line-height: 14px;

        }
        #top h1, #top p, #menulist {
            margin: 0;
            padding: 0;

        }
        .menuitem {
            background-color: #f1f1f1;
            border: 1px solid #d4d4d4;
            list-style-type: none;
            padding: 4px;
            cursor: pointer;

        }
        .a{
            color: #000000;
            text-decoration: underline;

        }
        a:hover{
            text-decoration: none;
        }
        @media (max-width:800px) {
            #sidebar {
                width: auto;
                position: relative;

            }
            #main {
                margin-right: 0;
            }
        }
        @media (max-width: 600px) {
            #menubar {
                width: auto;
                float: none;
            }
            #main {
                margin: 0;
            }    
        }
        .info {
            width: 150px;
            margin-bottom: 10px;

        }
        th{
            width: 100px;
            padding-left: 5px;

        }
        .title{
            height: 30px;
            background: purple;
            color: rgb(251, 8, 8);

        }
        td{
            height: 30px;
            padding-left: 5px;

        }

    </style>
</head>
<body>
    <div class="container wrapper">
        <div id="top">
            <h2>Hello OpenCV.js</h2>
            <!--č„ opencv.js ęä»¶å č½½ęåļ¼åä¼ę¾ē¤ŗāopencv.js is ready.ā-->
            <p id="status">OpenCV.js is loading...</p>
        </div>
        <div class="wrapper">
            <div id="menubar">
                <ul id="menulist">
                    <!--å¾ēčÆ»å„åŗå-->
                    <div class="menuitem">č¾å„å¾ē<input type="file" id="fileInput" accept="image/*" name="file" /></div>
                    <div id="savefull" class="menuitem">äæå­ęä»¶<button id="save">äæå­</button></div>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <br/>
                    <h4>äŗå¼åéå¼č®¾ē½®</h4>
                    <input type="range" id="myRange" min="0" max="255" step="1" value="0">
                    <p id="demo"></p>
                    <button class="menuitem" id="getImgBtn">åå¾åŗēØäŗå¼å</button>
                    <br>
                    <button class="menuitem" id="erode">å¾åčč</button>
                    <button class="menuitem" id="dilate">å¾åčØč</button>
                    <button class="menuitem" id="contourm">éåč½®å»å¹¶č®”ē®ęÆä¾</button></p>
                    <p id="areaOutput"></p>
                </ul>
            </div>
            <canvas id="fullImgInput" width="5000" height="5000" style="width: 5000px;height: 5000px;position:fixed;left:100%;"></canvas>
            <canvas id="fullImgOutput" width="5000" height="5000" style="width: 5000px;height: 5000px;position:fixed;left:100%;"></canvas>
            <div id="main">
                <div>
                    <canvas id="canvasInput" width="640" height="360"></canvas>
                </div>
                <hr>
                <div>
                    <div>č¾åŗå¾ē</div>
                    <canvas id="canvasOutput"></canvas>
                </div>
            </div>
            <div id="sidebar">
                <h1>é¢ē§ÆęÆä¾č”Ø</h1>
                <table border="1" cellspacing="0" cellpadding="0" style="text-align: left;margin-top: 20px;">
                    <tr class="title">
                        <th>ęä½ę¬”åŗ</th>
                        <th>čæä¼¼é¢ē§Æ</th>
                        <th>ęÆä¾(%)</th>
                    </tr>
                </table>
            </div>
        </div>
    </div>
    <div id="bottom">
        <p>Created and Modfied By Sarira Shi #</p>
    </div>
</body>  
<body>
<script type="text/javascript">
    let inputElement = document.getElementById('fileInput');
    let imgBtn = document.getElementById('getImgBtn');
    let img = new Image();
    let loading = true;
    let x = document.getElementById('myRange');
    let r = 0;//äæ”å·é
    let p = 0;//äæ”å·é
    let q = 1;//äæ”å·é
    let fileOrder = 0;//č”Øę ¼ęä½ę¬”åŗ
    let name =  0;//äøč½½ęä»¶åē§°
    document.getElementById("demo").innerHTML = x.value;
    inputElement.addEventListener('change', (e) => {
        img.src = URL.createObjectURL(e.target.files[0]);
        q = 1;
    }, false);
    x.addEventListener('change',(e) => {
        p = x.value;
        document.getElementById("demo").innerHTML = p ;
        p = parseFloat(p)
        q = 1;
        r = 0;
    }, false);
    img.onload = function() {
        let inCanvas = document.getElementById('canvasInput')
        let fullinCanvas = document.getElementById('fullImgInput')
        let inCanvasCtx = inCanvas.getContext('2d')
        let infullCanvasCtx =fullinCanvas.getContext('2d')
        fullinCanvas.width = img.width
        fullinCanvas.height = img.height
        inCanvasCtx.drawImage(img,0,0,img.width,img.height,0,0,640,360)
        infullCanvasCtx.drawImage(img,0,0,img.width,img.height,0,0,img.width,img.height)
        /*if(img.width!==640 ||  img.height!==360) {
            inCanvas.toBlob(function(blob) {
                console.log()
                img.src = URL.createObjectURL(blob);
            })
        }*/
    };
    imgBtn.addEventListener('click', (e) => {
        // if(loading) {
        //     return alert('ę­£åØå č½½opencv.jsåęØ”åęä»¶')
        // }
        if(!img.src) {
            return alert('čÆ·åäøä¼ å¾ē')
        }
        let src = cv.imread('canvasInput');
        let src1 = cv.imread('fullImgInput')
        let gray = new cv.Mat();
        let gray1 = new cv.Mat();
        let gray2 = new cv.Mat();
        let gray3 = new cv.Mat();
        cv.cvtColor(src, gray, cv.COLOR_BGR2GRAY);
        cv.cvtColor(src1, gray1, cv.COLOR_BGR2GRAY);
        cv.threshold (gray, gray2, p, 255, cv.THRESH_BINARY);
        cv.threshold (gray1, gray3 , p, 255, cv.THRESH_BINARY);
        cv.imshow('canvasOutput',gray2);
        cv.imshow('fullImgOutput',gray3);
        r = 1;
        src.delete();src1.delete();gray.delete();gray1.delete();gray2.delete();gray3.delete();
    });
    erode.addEventListener('click',(e) =>{
        if(!r){
            return alert('čÆ·ååŗēØäŗå¼å')
        }
        let src = cv.imread('canvasOutput');
        let src1 = cv.imread('fullImgOutput')
        let dst = new cv.Mat();
        let dst1 = new cv.Mat();
        let M = cv.Mat.ones(2, 2, cv.CV_8U);
        let anchor = new cv.Point(-1, -1);
        // You can try more different parameters
        cv.erode(src, dst, M, anchor, 1, cv.BORDER_CONSTANT, cv.morphologyDefaultBorderValue());
        cv.erode(src1, dst1, M, anchor, 1, cv.BORDER_CONSTANT, cv.morphologyDefaultBorderValue());
        cv.imshow('canvasOutput', dst);
        cv.imshow('fullImgOutput', dst1);
        src.delete();src1.delete();dst.delete(); M.delete();dst1.delete();
    })

	dilate.addEventListener('click',(e) =>{
        if(!r){
            return alert('čÆ·ååŗēØäŗå¼å')
        }
        let src = cv.imread('canvasOutput');
        let src1 = cv.imread('fullImgOutput')
        let dst = new cv.Mat();
        let dst1 = new cv.Mat();
        let M = cv.Mat.ones(2, 2, cv.CV_8U);
        let anchor = new cv.Point(-1, -1);
        // You can try more different parameters
        cv.dilate(src, dst, M, anchor, 1, cv.BORDER_CONSTANT, cv.morphologyDefaultBorderValue());
        cv.dilate(src1, dst1, M, anchor, 1, cv.BORDER_CONSTANT, cv.morphologyDefaultBorderValue());
        cv.imshow('canvasOutput', dst);
        cv.imshow('fullImgOutput', dst1);
        src.delete();src1.delete();dst.delete(); M.delete();dst1.delete();
    })
    contourm.addEventListener('click',(e) =>{
        if(!r){
            return alert('čÆ·ååŗēØäŗå¼å')
        }
        if(q){
            q = 0;
            let src = cv.imread('canvasOutput');
            let src1 = cv.imread('fullImgOutput');
            let dst = cv.Mat.zeros(src.rows, src.cols, cv.CV_8UC3);
            let dst1 = cv.Mat.zeros(src1.rows, src1.cols, cv.CV_8UC3);
            cv.cvtColor(src, src, cv.COLOR_BGR2GRAY);
            cv.cvtColor(src1, src1, cv.COLOR_BGR2GRAY);
            let contours = new cv.MatVector();
            let contours1 = new cv.MatVector();
            let hierarchy = new cv.Mat();
            let hierarchy1 = new cv.Mat();
            // You can try more different parameters
            cv.findContours(src, contours, hierarchy, cv.RETR_EXTERNAL, cv.CHAIN_APPROX_SIMPLE);
            cv.findContours(src1, contours1, hierarchy1, cv.RETR_EXTERNAL, cv.CHAIN_APPROX_SIMPLE);
            let color = new cv.Scalar(255,255,0);
            for (let i = 0; i < contours.size(); ++i) {
                cv.drawContours(dst, contours, i, color, 1, cv.LINE_8, hierarchy, 100);
            }
            for (let i = 0; i < contours1.size(); ++i){
                cv.drawContours(dst1, contours1, i, color, 1, cv.LINE_8, hierarchy1, 100);
            }
            cv.imshow('canvasOutput', dst);
            cv.imshow('fullImgOutput', dst1);
            let cnt = new cv.Mat();
            let area = 0;
            for (let i = 0; i < contours1.size();++i)
            {
                cnt = contours1.get(i);
                area = area + cv.contourArea(cnt);
            }
            areaOutput.innerHTML = area;
            parseFloat(area);
            var table = document.getElementsByTagName('table')[0];
            var tr = document.createElement('tr');
            var ratio = 100*area/(img.height*img.width);
            tr.innerHTML = "<td>"+(++fileOrder)+"</td><td>"+area+"</td><td>"+ratio.toFixed(2)+"</td>";
            table.appendChild(tr);
            src.delete(); dst.delete(); contours.delete(); hierarchy.delete();contours1.delete(); hierarchy1.delete();src1.delete();dst1.delete();
            }
        else
            return alert('ę“ę¹å¾åęäŗå¼ååę°ååčÆčÆå§');
    })
    save.addEventListener('click',(e) =>{
        if(!img.src)
        {
            return alert('čÆ·åäøä¼ å¾ē')
        }
        let event = new MouseEvent('click');//åå»ŗåå»äŗä»¶
        const canvas = document.getElementById('fullImgOutput');
        url = canvas.toDataURL('image/png');
        let a = document.createElement("a"); // ēęäøäøŖaåē“  
        a.download = (++name)+'.png' || "photo"; // č®¾ē½®å¾ēåē§°
        a.href = url; // å°ēęēURLč®¾ē½®äøŗa.hrefå±ę§    
        a.dispatchEvent(event);
    })
    function onOpenUtilsReady() {
        let utils = new Utils('errorMessage');
        utils.loadOpenCv(() => {
        let cvFile = 'opencv.js';
        utils.createFileFromUrl(cvFile, cvFile, () => {
            document.getElementById('status').innerHTML = 'OpenCV.js is ready.';
            loading = false;
        });
    })
    };
    
    </script>
    <script async src="./utils.js" onload="onOpenUtilsReady();" type="text/javascript"></script>
    <script async src="./opencv.js" onload="onOpenCvReady();" type="text/javascript"></script>
    <style>
    .inputoutput{
        display: inline-block;
    }
    </style>
</body>   
</html>
