# 샘플 소스
```
<!DOCTYPE html>
<html lang='ko'>
<head>
    <meta charset='UTF-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1.0'>
    <meta http-equiv='X-UA-Compatible' content='ie=edge'>
    <title>비디오 예제</title>

    <link rel='stylesheet' href='./dist/plyr.css' />

    <style>
        #container {width: 800px;}
        #go_btn {cursor: pointer; color: tomato}

        /*프로그레스바 클릭안되게 처리*/
        .plyr__progress{ pointer-events: none; }
    </style>
</head>
<body>
    <div id='container'>
        <div id='player' data-plyr-provider='youtube' data-plyr-embed-id='CNeNwplE_aw'></div>
    </div>

    <p>현재 플레이 위치 : <span id='current'></span></p>
    <p><a id='go_btn'>3분 55초 부터 시작하기</a></p>
    <p>참고사이트 : <a href='https://github.com/sampotts/plyr' target="_blank">https://github.com/sampotts/plyr</a></p>

    <script src='./dist/plyr.polyfilled.min.js'></script>

    <script>
        var player = new Plyr('#player', {
            controls : ['progress', 'current-time', 'mute', 'volume', 'fullscreen'],
            invertTime : false,
            keyboard : {
                focused: false, 
                global: false
            },
            listeners: {
                // 리스너로 seek 안되게 처리할려면 요렇게
                seek: function customSeekBehavior(e) {
                    //e.preventDefault();
                    //alert('변경 불가능');
                    //return false;
                }
            }
        });

        player.on('timeupdate', function(e) {
            document.getElementById('current').textContent = e.detail.plyr.currentTime + ' / ' + player.duration;
        });

        player.on('ended', function(e) {
            console.log(e.detail.plyr);
            alert('비디오 재생이 끝났음');
        });

        document.getElementById('go_btn').addEventListener('click', function(e) {
            player.pause();
            player.currentTime = 60*3 + 55;
            player.play();
        });
    </script>
</body>
</html>
```