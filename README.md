[fibonacci caragol.html](https://github.com/user-attachments/files/33484435/fibonacci.caragol.html)
<!DOCTYPE html>
<html>
<head>
	<meta http-equiv="content-type" content="text/html; charset=utf-8"/>
	<title></title>
	<meta name="generator" content="LibreOffice 25.8.1.1 (Windows)"/>
	<meta name="created" content="2026-10-15T11:14:25.301975500"/>
	<meta name="changed" content="2026-10-15T11:14:51.447728900"/>
	<style type="text/css">
		@page { size: 21cm 29.7cm; margin: 2cm }
		p { line-height: 115%; margin-bottom: 0.25cm; background: transparent }
		a:link { color: #000080; text-decoration: underline }
		a:visited { color: #800000; text-decoration: underline }
	</style>
</head>
<body lang="ca-ES" link="#000080" vlink="#800000" dir="ltr"><p style="margin-bottom: 0cm; line-height: 100%">
&lt;!DOCTYPE html&gt;<br/>
&lt;html lang=&quot;ca&quot;&gt;<br/>
&lt;head&gt;<br/>

   &lt;meta charset=&quot;UTF-8&quot;&gt;<br/>
    &lt;meta
name=&quot;viewport&quot; content=&quot;width=device-width,
initial-scale=1.0&quot;&gt;<br/>
    &lt;title&gt;Joc Interactiu:
L'Espiral de Fibonacci en Cubs&lt;/title&gt;<br/>
    &lt;style&gt;<br/>

       body {<br/>
            font-family: 'Segoe UI', Tahoma,
Geneva, Verdana, sans-serif;<br/>
            background-color:
#f0f4f8;<br/>
            color: #333;<br/>
            display:
flex;<br/>
            flex-direction: column;<br/>
           
align-items: center;<br/>
            margin: 0;<br/>
           
padding: 20px;<br/>
        }<br/>
<br/>
        h1 {<br/>
          
 color: #2c3e50;<br/>
            margin-bottom: 5px;<br/>
       
}<br/>
<br/>
        p {<br/>
            color: #555;<br/>
         
  max-width: 600px;<br/>
            text-align: center;<br/>
       
    margin-bottom: 25px;<br/>
        }<br/>
<br/>
       
#game-container {<br/>
            display: flex;<br/>
           
flex-direction: row;<br/>
            gap: 40px;<br/>
           
background: white;<br/>
            padding: 20px;<br/>
           
border-radius: 15px;<br/>
            box-shadow: 0 10px 25px
rgba(0,0,0,0.1);<br/>
            align-items: center;<br/>
       
}<br/>
<br/>
        #canvas-container {<br/>
            position:
relative;<br/>
            width: 500px;<br/>
            height:
500px;<br/>
            border: 2px dashed #bdc3c7;<br/>
           
border-radius: 10px;<br/>
            background: #fafafa;<br/>
     
  }<br/>
<br/>
        /* Zones on s'han de deixar caure els cubs */<br/>

       .drop-zone {<br/>
            position: absolute;<br/>
       
    border: 3px dotted #3498db;<br/>
            border-radius: 50%;<br/>

           display: flex;<br/>
            justify-content: center;<br/>

           align-items: center;<br/>
            transform:
translate(-50%, -50%);<br/>
            background-color: rgba(52,
152, 219, 0.05);<br/>
            transition: background-color 0.3s;<br/>

       }<br/>
<br/>
        .drop-zone.hovered {<br/>
           
background-color: rgba(52, 152, 219, 0.2);<br/>
           
border-style: solid;<br/>
        }<br/>
<br/>
        /* Contenidor
de les peces disponibles */<br/>
        #blocks-pool {<br/>
        
   display: flex;<br/>
            flex-direction: column;<br/>
     
      gap: 15px;<br/>
            width: 150px;<br/>
           
align-items: center;<br/>
            justify-content: center;<br/>
 
          background: #fdfefe;<br/>
            border: 1px solid
#e2e8f0;<br/>
            padding: 15px;<br/>
           
border-radius: 10px;<br/>
            min-height: 400px;<br/>
       
}<br/>
<br/>
        /* Estil dels cubs de colors */<br/>
       
.cube-block {<br/>
            display: flex;<br/>
           
justify-content: center;<br/>
            align-items: center;<br/>
 
          color: white;<br/>
            font-weight: bold;<br/>
    
       border-radius: 8px;<br/>
            cursor: grab;<br/>
      
     box-shadow: 0 4px 6px rgba(0,0,0,0.15);<br/>
           
user-select: none;<br/>
            transition: transform 0.2s;<br/>

       }<br/>
<br/>
        .cube-block:active {<br/>
           
cursor: grabbing;<br/>
        }<br/>
<br/>
        /* Missatge de
victòria */<br/>
        #victory-message {<br/>
           
display: none;<br/>
            margin-top: 20px;<br/>
           
padding: 15px 30px;<br/>
            background-color: #2ecc71;<br/>

           color: white;<br/>
            font-size: 1.2rem;<br/>
   
        font-weight: bold;<br/>
            border-radius: 8px;<br/>

           animation: pop 0.5s ease;<br/>
        }<br/>
<br/>
      
 @keyframes pop {<br/>
            0% { transform: scale(0.8);
opacity: 0; }<br/>
            100% { transform: scale(1); opacity:
1; }<br/>
        }<br/>
    &lt;/style&gt;<br/>
&lt;/head&gt;<br/>
&lt;body&gt;<br/>
<br/>

   &lt;h1&gt;L'Espiral dels Cubs de Fibonacci&lt;/h1&gt;<br/>
   
&lt;p&gt;Arrossega cada cub (el valor del nombre de Fibonacci elevat
a 3: &lt;b&gt;F&lt;sub&gt;n&lt;/sub&gt;&lt;sup&gt;3&lt;/sup&gt;&lt;/b&gt;)
a la seva posició correcta a l'espiral del caragol, des del més
petit al més gran.&lt;/p&gt;<br/>
<br/>
    &lt;div
id=&quot;game-container&quot;&gt;<br/>
        &lt;!-- Tauler de
l'espiral --&gt;<br/>
        &lt;div id=&quot;canvas-container&quot;
id=&quot;spiral-board&quot;&gt;<br/>
            &lt;!-- Les zones de
destí es generaran dinàmicament aquí amb JS --&gt;<br/>
       
&lt;/div&gt;<br/>
<br/>
        &lt;!-- Piscina de blocs per
arrossegar --&gt;<br/>
        &lt;div id=&quot;blocks-pool&quot;&gt;<br/>

           &lt;!-- Els blocs es generaran aquí --&gt;<br/>
       
&lt;/div&gt;<br/>
    &lt;/div&gt;<br/>
<br/>
    &lt;div
id=&quot;victory-message&quot;&gt;🎉 Felicitats! Has completat
l'espiral de caragol perfectament!&lt;/div&gt;<br/>
<br/>
   
&lt;script&gt;<br/>
        // Sèrie de Fibonacci base: 1, 1, 2, 3,
5, 8<br/>
        // Valors dels CUBS (F^3): 1, 1, 8, 27, 125, 512<br/>

       const fibonacciCubes = [<br/>
            { id: 1, fib: 1,
cubeValue: 1, color: '#e74c3c', size: 30 },<br/>
            { id: 2,
fib: 1, cubeValue: 1, color: '#e67e22', size: 35 },<br/>
           
{ id: 3, fib: 2, cubeValue: 8, color: '#f1c40f', size: 45 },<br/>
   
        { id: 4, fib: 3, cubeValue: 27, color: '#2ecc71', size: 60
},<br/>
            { id: 5, fib: 5, cubeValue: 125, color:
'#3498db', size: 80 },<br/>
            { id: 6, fib: 8, cubeValue:
512, color: '#9b59b6', size: 110 }<br/>
        ];<br/>
<br/>
       
const board = document.getElementById('canvas-container');<br/>
     
  const pool = document.getElementById('blocks-pool');<br/>
       
const victoryMsg = document.getElementById('victory-message');<br/>
 
      <br/>
        let correctPlacements = 0;<br/>
<br/>
        //
1. Càlcul de les posicions de l'espiral tipus &quot;caragol&quot;
(coordenades polars convertides a cartesianes)<br/>
        const
centerX = 250;<br/>
        const centerY = 250;<br/>
        <br/>
 
      // Definim angles i radis creixents per fer la forma de caragol
de mar<br/>
        fibonacciCubes.forEach((cube, index) =&gt; {<br/>

           // L'angle gira 90 graus (PI/2 radiants) per cada pas,
imitant el creixement clàssic<br/>
            const angle = index *
(Math.PI / 1.8); <br/>
            // El radi creix proporcionalment
per donar espai als cubs més grans<br/>
            const radius =
25 + (index * 38); <br/>
<br/>
            const x = centerX + radius
* Math.cos(angle);<br/>
            const y = centerY + radius *
Math.sin(angle);<br/>
<br/>
            // Crear la zona de destí
(Drop Zone)<br/>
            const zone =
document.createElement('div');<br/>
            zone.className =
'drop-zone';<br/>
            zone.dataset.targetId = cube.id;<br/>
 
          zone.style.left = `${x}px`;<br/>
            zone.style.top
= `${y}px`;<br/>
            zone.style.width = `${cube.size +
10}px`;<br/>
            zone.style.height = `${cube.size + 10}px`;<br/>

           zone.innerHTML = `&lt;span style=&quot;color:#bdc3c7;
font-size:11px;&quot;&gt;F³&lt;/span&gt;`;<br/>
            <br/>
  
         // Esdeveniments de Drag &amp; Drop per a la zona<br/>
     
      zone.addEventListener('dragover', dragOver);<br/>
           
zone.addEventListener('dragenter', dragEnter);<br/>
           
zone.addEventListener('dragleave', dragLeave);<br/>
           
zone.addEventListener('drop', dropAsset);<br/>
<br/>
           
board.appendChild(zone);<br/>
        });<br/>
<br/>
        // 2.
Generar els blocs jugables (barrejats perquè no estiguin en ordre)<br/>

       const shuffledCubes = [...fibonacciCubes].sort(() =&gt;
Math.random() - 0.5);<br/>
<br/>
        shuffledCubes.forEach(cube
=&gt; {<br/>
            const block =
document.createElement('div');<br/>
            block.className =
'cube-block';<br/>
            block.id = `cube-${cube.id}`;<br/>
   
        block.draggable = true;<br/>
           
block.style.backgroundColor = cube.color;<br/>
           
block.style.width = `${cube.size}px`;<br/>
           
block.style.height = `${cube.size}px`;<br/>
           
block.style.fontSize = `${cube.size * 0.28}px`; // Mida de text
proporcional<br/>
            block.innerText = cube.cubeValue;<br/>
<br/>

           block.addEventListener('dragstart', dragStart);<br/>
     
      block.addEventListener('dragend', dragEnd);<br/>
<br/>
        
   pool.appendChild(block);<br/>
        });<br/>
<br/>
        //
--- Funcions de Lògica de l'Arrossegament ---<br/>
<br/>
       
function dragStart(e) {<br/>
           
e.dataTransfer.setData('text/plain', e.target.id);<br/>
           
setTimeout(() =&gt; {<br/>
                this.style.opacity =
'0.4';<br/>
            }, 0);<br/>
        }<br/>
<br/>
       
function dragEnd() {<br/>
            this.style.opacity = '1';<br/>

       }<br/>
<br/>
        function dragOver(e) {<br/>
           
e.preventDefault(); // Permet el drop<br/>
        }<br/>
<br/>
     
  function dragEnter(e) {<br/>
            e.preventDefault();<br/>
 
          if (!this.classList.contains('occupied')) {<br/>
          
     this.classList.add('hovered');<br/>
            }<br/>
       
}<br/>
<br/>
        function dragLeave() {<br/>
           
this.classList.remove('hovered');<br/>
        }<br/>
<br/>
       
function dropAsset(e) {<br/>
           
this.classList.remove('hovered');<br/>
            <br/>
           
const id = e.dataTransfer.getData('text/plain');<br/>
           
const draggableElement = document.getElementById(id);<br/>
          
 const cubeId = id.replace('cube-', '');<br/>
<br/>
            //
Validar si el cub correspon a la zona correcta<br/>
            if
(this.dataset.targetId === cubeId &amp;&amp;
!this.classList.contains('occupied')) {<br/>
                //
Posicionament correcte<br/>
               
this.classList.add('occupied');<br/>
                this.innerHTML =
&quot;&quot;; // Esborra el text de fons<br/>
                <br/>
 
              // Ajustem l'estil perquè quedi fixat al centre exacte
de la zona<br/>
                draggableElement.style.position =
'static';<br/>
                draggableElement.style.opacity = '1';<br/>

               draggableElement.draggable = false; // Ja no es pot
moure<br/>
                draggableElement.style.cursor =
'default';<br/>
                <br/>
               
this.appendChild(draggableElement);<br/>
               
correctPlacements++;<br/>
<br/>
                // Comprovar si s'ha
guanyat<br/>
                if (correctPlacements ===
fibonacciCubes.length) {<br/>
                   
victoryMsg.style.display = 'block';<br/>
                   
board.style.borderColor = '#2ecc71';<br/>
                }<br/>
    
       } else {<br/>
                // Si és incorrecte, el bloc
torna a la seva opacitat normal a la piscina (ho fa el dragend
automàticament)<br/>
                alert(&quot;Aquest cub no
encaixa en aquesta part de l'espiral!&quot;);<br/>
            }<br/>

       }<br/>
    &lt;/script&gt;<br/>
&lt;/body&gt;<br/>
&lt;/html&gt;<br/>
<br/>

</p>
</body>
</html>
