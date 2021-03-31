<h1 class="r-fit-text">Dr Konstantinos Vasilakos</h1>
<h2 class="r-fit-text">Istanbul Technical University</h2>
<h3 class="r-fit-text">Center for Advanced Studies in Music</h3>

<aside class="notes">
Hello my name is Konstantinos Vasilakos. I am teaching at the Istanbul Technical University, in the Center for Advanced Studies in Music.
</aside>


## Lick the toad
### A web-based Interface for collective sonification
<img class="r=stretch" src="./img/lickImage.jpg">

<aside class="notes">
I am going to talk about my work in progress, Lick The Toad.
</aside>



# Some Background
<p class="fragment">Performance with networked music systems.</p>
<p class="fragment">Live Coding performance</p>
<p class="fragment">Sonification</p>

<aside class="notes">
I am interested in the following topics and my work elaborates in performance with networked music systems.
</aside>


## Previous & similar work
IPSOS: interactive physics sonification system (ipsos.web.cern.ch/)
Interactive web based sonification of particle collision data, a collaboration with:
<p class="fragment">Tom McCaulley (CMS/CERN)</p>
<p class="fragment">Scott Wilson (UoB)</p>
  <p class="fragment fade-in-then-out">Supporting web-site for the app:</p>
<p class="fragment">Emma Watson</p>
<p class="fragment">Milad K. Mardakheh</p>

<aside class="notes">
Previous work in the field includes IPSOS, which uses particle data to control parameters in the browser and can be used from every mobile device like smartphones and tablets.
</aside>



# Sonification
<section>
  <p>What is Sonification, Kramer et al state in:
    <q cite="https://digitalcommons.unl.edu/psychfacpub/444/">Sonification Report: Status of the Field and Research Agenda</q>
  - (Kramer et al., 2010)</p>
<blockquote cite="https://digitalcommons.unl.edu/psychfacpub/444/">
Sonification is defined as the use of nonspeech audio to convey information. More
specifically, sonification is the transformation of data relations into perceived relations in an
acoustic signal for the purposes of facilitating communication or interpretation.</blockquote>
</section>

<aside class="notes">
Lick the toad is a tool for diverse sonification practices; according to Kramer,  Sonification is defined as the use of nonspeech audio to convey information. More
specifically, sonification is the transformation of data relations into perceived relations in an
acoustic signal for the purposes of facilitating communication or interpretation. So data can be used as raw material to create mappings between arbitrary data and control synthesis parameters of synthesis algorithms.
</aside>



# Project aims and capabilities
<img class="fragment fade-in-then-out" class="r-stretch" src="./img/main_image.png" style="border: solid 4px #37474F" width="500">
<p class="fragment">Sonification/Visualization</p>
<p class="fragment">Interaction via the browser</p>
<p class="fragment">Control of Remote Sound Engines</p>
<p class="fragment">plus some _intelligence_</p>

<aside class="notes">
The system can receive data from the user, but I also have tested it with generating and collecting data from SC, as it is shown in the previous screenshot. And it also supports a real time graph to monitor the progress of the training of the model.
</aside>


## Under the hood
<img src="img/mermaid-diagram.svg" width="450">

<aside class="notes">
The platform provides an interface, a main hub which receives all users' data, a neural network, and a server to support all broadcasting and communication with other components such as the sound generation. It also works with various sound engines that support OSC communication protocol to sonify the data. This is extremely handy as it can be used for live coding ensembles that can sonify this data while the platorm is running.
In a nutshell this project provides a tool for remote interactions, generating data which can be transcoded/rendered to multiple formats, such as sound and visual. The project was designed to support sonification, interaction via the browser, and control remote sound engines. The system is running as a web app and the user can log in via a URL which will open an interface, basically controlling a visual element, that generates some data including a specified value which can be used as the target, more on this later.
</aside>


## ltt: development
<p class="fragment">Cross platform app</p>
<p class="fragment">Using ML5 JS tools for machine learning in the browser</p>
<p class="fragment">P5JS interactive visualizations of data</p>
<p class="fragment">Socket.io for broadcasting data</p>
<p class="fragment">OSC.js for OSC communication support</p>
<p class="fragment">Tone.js for embedded sound synthesis in the browser</p>

<aside class="notes">
The system runs on any modern browser and is developed as a JavaScript application using nodeJS for the backend. Like server support and broadcasting data using Socket.io. It also uses P5.JS library for the visualization and ML5 library which plays very well with P5JS. I have used OSC.js to send and receive osc messages from and to SuperCollider. I have also experimented with embedding sound libraries in the browser but it feels somehow limited since I am coming from a SuperCollider background, but it's possible and for remote hosting it will be probably better but it will also mean abandoning some flexibility since the synths will be fixed. Links for all the components used in the project are provided at the end of the presentation.
</aside>


## ltt: interface
<iframe class="r-stretch" data-autoplay; data-src="https://www.youtube-nocookie.com/embed/WXKyS5dSVFo?autoplay=1&rel=0" title="YouTube video player" frameborder="0" allow="autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen style="border: solid 4px #37474F"></iframe>

<aside class="notes">
The users can see each other in the same network via mobile devices and smartphones. Each user broadcasts current position while monitoring the others. Further direction will provide most likely the physical input of each user, using geolocation positioning. 
</aside>


# Training: looking into data
<img src="img/training.png" class="r-stretch">
<aside class="notes">
Besides the location position of the users, the training data needs an output in order to generate the prediction output between data. How this can be used then, once the training is done, the output will provide several data including the X and Y locations of the cursor position in the prediction interface. While it will also generate a regression value based on the training of the model and how the data was logged in. For this an extra parameter is used, providing the targets.
</aside>


## Data collection
<section>
<pre><code data-line-numbers="10-12|22-24|39-40">
{
    "data":[
        {
            "xs":{
                "x":385.5262585136709,
                "y":336.23547933556256
            },
            "ys":{
                "0":22.499027759485152
            }
        }
    ]
}
//
{
   "data":[
      {
         "xs":{
            "x":226.322645526962,
            "y":84.91814510458188
         },
         "ys":{
            "frequency":660
         }
      }
   ]
}
//
{
    "data":[
        {
            "xs":{
                "x":338.3214102025017,
                "y":286.8948783827702,
                "r":21.84568433662578
            },
            "ys":{
                "0":"WDgTyTdSGRcjJcJjAABQ"
            }
        }
    ]
}
</code></pre>
</section>

<aside class="notes">
While this is customized the data can be adapted to various inputs and outs. I have experimented so far with different targets including floats, frequency, and strings, like labels for sounds (low, med, high or slow, fast etc.) So in this example, the data includes X and Y, and various targets as shown in the snippet here.
</aside>


## Training: media
<iframe class="r-stretch"  data-autoplay; data-src="https://www.youtube-nocookie.com/embed/mMl7lO877GM?autoplay=1&rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="border: solid 4px #37474F"></iframe>



## Prediction process
<p class="fragment">Vizualization of data</p>
<p class="fragment">Cursor (X, Y) position generates a regression float value</p>
<p class="fragment">Controlled manually/automatically with perlin noise algorithm</p>

<aside class="notes">
Aside of the first visualization in the hub, the system will also load what was collected. Providing a visualization of the predictions and cursor which is used as the location of the prediction data.



## Prediction:
### Example_1.0
<iframe class="r-stretch"  data-autoplay; data-src="https://www.youtube-nocookie.com/embed/Zcq0u-0Vtqo?autoplay=1&rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; picture-in-picture" allowfullscreen style="border: solid 4px #37474F"></iframe> 



## Prediction: 
### Example_2.0
<iframe class="r-stretch"  data-autoplay; data-src="https://www.youtube-nocookie.com/embed/3pv9Ez2m4jo?autoplay=1&rel=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; picture-in-picture" allowfullscreen style="border: solid 4px #37474F"></iframe>

<aside class="notes">
Prediction starts after the training/learning mode is finished. Once this is done the interface will switch to a different mode, that is prediction and it will provide the prediction data based in the trained model, as well as the interface will provide visualization of these.
</aside>


## Creative Outcomes
A web app which can be used in the following set-ups:
<p class="fragment fade-in-then-out">Web-app</p>
<p class="fragment">On site installation</p>
<p class="fragment">Live Coding</p>

<aside class="notes">
Assuming, the model is trained used targets such as sound labelled as certain ranges, this can trigger specific sounds from SuperCollider, and create a real time composition in an on site location with various users. And/or the generated data can be sonified in real time as streaming sonification raw information for the coder.
</aside>



## Future Directions
<p class="fragment fade-in-then-out">Server deployment</p>
<p class="fragment fade-in-then-out">Host Remote Interaction</p>
<p class="fragment highlight-red">Support Online Collaboration</p>

<aside class="notes">
The main goal is to make this an online web app and support distant interaction.
</aside>



## Links
* Lick the toad (GitHub repo) https://konvas.github.io/lick-the-toad/
* ML5.js https://ml5js.org
* SuperCollider https://supercollider.github.io
* P5.js https://p5js.org
* Socket.io https://socket.io
* OSC.js https://github.com/colinbdclark/osc.js/
* NodeJS https://nodejs.org/en/

<aside class="notes">
Links to technology and other mentioned in my presentation are here.
</aside>


# Acknowledgments
Daniel Shifman for his numerous tutorials about P5.js and ML5.js respectively.

<aside class="notes">
I would like to thanks Daniel Shifman for his tutorial on P5.js and ML5.js.
</aside>



### References
1. de Campo, A. (2007). A DATA SONIFICATION DESIGN SPACE MAP. 4.
2. Hermann, T., Bovermann, T., Riedenklau, E., & Ritter, H. (2007). TANGIBLE COMPUTING FOR INTERACTIVE SONIFICATION OF MULTIVARIATE DATA. 5.
3. Hill, E., Cherston, J., Goldfarb, S., & Paradiso, J. (2017). ATLAS data sonification: A new interface for musical expression. Proceedings of 38th International Conference on High Energy Physics — PoS(ICHEP2016), 1042. https://doi.org/10.22323/1.282.1042
4. Listening to data from the Large Hadron Collider | Lily Asquith |TEDxZurich. (n.d.). Retrieved January 22, 2020, from https://www.youtube.com/watch?v=iQiPytKHEwY
5. Vasilakos, K. (2019). Emerging Dark Matter Through Diverse Sonification Practices. Proceedings of the International Music and Sciences Symposium. International Music and Sciences Symposium, Istanbul. http://www.tmdk.itu.edu.tr/docs/librariesprovider5/kitap-i-çerik/muzikvebilimler2019.pdf
6. Vasilakos, K. n/a, Wilson, S., McCauley, T., Yeung, T. W., Margetson, E., & Khosravi Mardakheh, M. (2020). Sonification of High Energy Physics Data Using Live Coding and Web Based Interfaces. In R. Michon & F. Schroeder (Eds.), Proceedings of the International Conference on New Interfaces for Musical Expression (pp. 464–470). Birmingham City University. pdfs/nime2020_paper76.pdf
7. Kramer, G., Walker, B., Bonebright, T., Cook, P., Flowers, J. H., Miner, N., & Neuhoff, J. (2010). Sonification Report: Status of the Field and Research Agenda. 31.
8. Hermann, T., Hunt, A., & Neuhoff, J. G. (Eds.). (2011). The sonification handbook. Logos Verlag.
