<template>
    <div id="Feliz">Feliz Dia de la Madre</div>
    <div class="polaroid" v-if="!alt">
        <a href="#" v-for="item in cI" :key="item.img">
            <img :src="item.img" />
        </a>
    </div>
    <div class="polaroid-alt" v-else>
        <a href="#" v-for="item in cI" :key="item.img">
            <img :src="item.img" />
        </a>
    </div>
</template>

<script>
    var images = new Array();
    var imagesAvailable = 35;
    var imagesToGet = 6;
    for (var i = 0; i < imagesToGet; i++)
    {
        if (i == imagesAvailable)
        {
            console.log("Acquired all images, leaving loop. Contact Carlos please.")
            break;
        }
        var chosenImage = -1;
        while (chosenImage < 0 || images.includes(chosenImage.toString().padStart(2, '0')))
            chosenImage = Math.ceil(Math.random()*imagesAvailable);
        images[i] = chosenImage.toString().padStart(2, '0');
    }

    function importAll(r) {
        let images = {};
        r.keys().map((item) => { images[item.replace('./', '')] = r(item); });
        return images;
    }

    const allImages = importAll(require.context('../assets/pics', false, /\.(png|jpe?g|svg)$/));

    var alt = false;
    if(/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(navigator.userAgent)){
    // true for mobile device
        console.log("mobile device");
        alt = true;
    } else {
    // false for not mobile device
        console.log("not mobile device");
    }

    export default {
        data() {
            return {
                cI: [{img: allImages[images[0] + '.jpg']},
                     {img: allImages[images[1] + '.jpg']},
                     {img: allImages[images[2] + '.jpg']},
                     {img: allImages[images[3] + '.jpg']},
                     {img: allImages[images[4] + '.jpg']},
                     {img: allImages[images[5] + '.jpg']}],
                alternate: alt
            }
        }
    }
    
</script>

<style scoped>
    @font-face {
        font-family: butterflyFont;
        src: url('../assets/krbutterfly-xobv-webfont.woff');
    }

    #Feliz {
        position: fixed;
        top: 30%;
        left: 10%;
        right: 10%;
        color:purple;
        font-size: 8vw;
        -webkit-text-stroke-width: 2px;
        -webkit-text-stroke-color: black;
        font-family: butterflyFont;
        pointer-events: none;
    }

    .polaroid img {
        background: #ffffff;
        max-height: 300px;
        max-width: 26%;
        margin: 2% 2% 2%;
        padding: 1% 1% 1%;
        -webkit-box-shadow: 0 4px 6px rgba(0, 0, 0, .3);
        -moz-box-shadow: 0 4px 6px rgba(0, 0, 0, .3);
        box-shadow: 0 4px 6px rgba(0, 0, 0, .3);
        -webkit-transition: all .20s linear;
        -moz-transition: all .20s linear;
        transition: all .20s linear;
        z-index: -1;
        display: inline-block;
    }

    .polaroid img:hover {
        -webkit-transform: scale(1.5);
        -moz-transform: scale(1.5);
        transform: scale(1.5);
        z-index: 10;
        -webkit-box-shadow: 0 10px 20px rgba(0, 0, 0, .7);
        -moz-box-shadow: 0 10px 20px rgba(0, 0, 0, .7);
        box-shadow: 0 10px 20px rgba(0, 0, 0, .7);
    }

    .polaroid-alt img {
        background: #ffffff;
        max-height: 300px;
        max-width: 300px;
        margin: 2% 2% 2%;
        padding: 1% 1% 1%;
        -webkit-box-shadow: 0 4px 6px rgba(0, 0, 0, .3);
        -moz-box-shadow: 0 4px 6px rgba(0, 0, 0, .3);
        box-shadow: 0 4px 6px rgba(0, 0, 0, .3);
        -webkit-transition: all .20s linear;
        -moz-transition: all .20s linear;
        transition: all .20s linear;
        z-index: -1;
        display: inline-block;
    }

    .polaroid-alt img:hover {
        -webkit-transform: scale(1.5);
        -moz-transform: scale(1.5);
        transform: scale(1.5);
        z-index: 10;
        -webkit-box-shadow: 0 10px 20px rgba(0, 0, 0, .7);
        -moz-box-shadow: 0 10px 20px rgba(0, 0, 0, .7);
        box-shadow: 0 10px 20px rgba(0, 0, 0, .7);
    }
</style>