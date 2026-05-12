<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Critical Error</title>

<style>
body{
    margin:0;
    background:#0078D7;
    overflow:hidden;
    font-family:Arial;
    color:white;
    text-align:center;
}

#box{
    margin-top:35vh;
}

#persen{
    font-size:70px;
}

#error{
    display:none;
    background:black;
    color:red;
    width:100vw;
    height:100vh;
    position:fixed;
    top:0;
    left:0;
    padding-top:20vh;
    animation:kedip 0.4s infinite;
}

@keyframes kedip{
    0%{background:black;}
    50%{background:darkred;}
    100%{background:black;}
}
</style>
</head>

<body onclick="mulaiAudio()">

<div id="box">
    <h1>Installing Security Update...</h1>
    <div id="persen">0%</div>
    <p>Klik layar untuk memulai 😹</p>
</div>

<div id="error">
    <h1>⚠ SYSTEM FAILURE ⚠</h1>
    <h2>Virus Detected 💀</h2>
    <h3 id="hapus">Deleting Files: 9999</h3>
</div>

<script>
let audioCtx;

function beep(){
    const osc = audioCtx.createOscillator();
    const gain = audioCtx.createGain();

    osc.type = "square";
    osc.frequency.value = 500;

    osc.connect(gain);
    gain.connect(audioCtx.destination);

    osc.start();

    gain.gain.exponentialRampToValueAtTime(
        0.00001,
        audioCtx.currentTime + 0.2
    );
}

function mulaiAudio(){

    if(!audioCtx){
        audioCtx = new (window.AudioContext || window.webkitAudioContext)();
    }

    let persen = 0;

    let loading = setInterval(() => {

        persen++;
        document.getElementById("persen").innerText = persen + "%";

        if(persen >= 100){

            clearInterval(loading);

            document.getElementById("box").style.display = "none";
            document.getElementById("error").style.display = "block";

            let file = 9999;

            setInterval(() => {

                beep();

                file -= Math.floor(Math.random()*20);

                if(file < 0){
                    file = 0;
                }

                document.getElementById("hapus")
                .innerText = "Deleting Files: " + file;

            }, 300);
        }

    }, 80);

    document.body.onclick = null;
}
</script>

</body>
</html>
