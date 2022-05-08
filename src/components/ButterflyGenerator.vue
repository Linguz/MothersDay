<template>
    <img src="../assets/tempbutterfly.gif">
    <div id="ButterflyHolder">Hello</div>
</template>

<script>
    import { h } from 'vue';

    export default {
        data() {
            return {
                butterflyNum: 2,
                Ymax: 8,
                Xmax: 8,
                Tmax: 10000,
                wind_w: window.innerWidth,
                wind_h: window.innerHeight,
                t: '',
                IDs: new Array(),
                floatimages: new Array()
            }
        },
        methods: {
            init(){
                for(var i=0; i<this.butterflyNum; i++){
                    this.IDs[i]=document.getElementById('pic'+i)

                    this.IDs[i].W=document.images["p"+i].width;
                    this.IDs[i].H=document.images["p"+i].height;

                    this.getnewprops(i);
                    this.moveidto(i , Math.floor(Math.random()*(this.wind_w-this.IDs[i].W)), Math.floor(Math.random()*(this.wind_h-this.IDs[i].H)));
                    this.IDs[i].style.visibility = "visible";

                    // Needs to be remade?
                    // startfly=setInterval('moveimage('+i+')',Math.floor(Math.random()*100)+100);
                }
            },

            getnewprops(num){
                this.IDs[num].Ydir=Math.floor(Math.random()*2)>0;
                this.IDs[num].Xdir=Math.floor(Math.random()*2)>0;
                this.IDs[num].Ystep=Math.ceil(Math.random()*this.Ymax);
                this.IDs[num].Xstep=Math.ceil(Math.random()*this.Xmax)
                setTimeout('getnewprops('+num+')', Math.floor(Math.random()*this.Tmax));
            },

            moveidto(num,x,y){
                this.IDs[num].style.left=x+'px';
                this.IDs[num].style.top=y+'px';
            },

            // eslint-disable-next-line
            moveimage(num){
                if(this.getidleft(num)+this.IDs[num].W+this.IDs[num].Xstep >= this.wind_w+this.getscrollx()) this.IDs[num].Xdir=false;
                if(this.getidleft(num)-this.IDs[num].Xstep<=this.getscrollx()) this.IDs[num].Xdir=true;
                if(this.getidtop(num)+this.IDs[num].H+this.IDs[num].Ystep >= this.wind_h+this.getscrolly()) this.IDs[num].Ydir=false;
                if(this.getidtop(num)-this.IDs[num].Ystep<=this.getscrolly()) this.IDs[num].Ydir=true;
                this.moveidby(num, (this.IDs[num].Xdir)? this.IDs[num].Xstep : -this.IDs[num].Xstep , (this.IDs[num].Ydir)? this.IDs[num].Ystep: -this.IDs[num].Ystep);
            },

            getidleft(num) {
                return parseInt(this.IDs[num].style.left);
            },

            getidtop(num){
                return parseInt(this.IDs[num].style.top);
            },

            moveidby(num,dx,dy){
                this.IDs[num].style.left=(this.getidleft(num)+dx)+'px';
                this.IDs[num].style.top=(this.getidtop(num)+dy)+'px';
            },

            getscrollx(){
                return window.pageXOffset;
            },

            getscrolly(){
                return window.pageYOffset;
            }
        },
        mounted() {
            for(var i = 0; i < this.butterflyNum; i++)
            {
                this.floatimages[i] = "../assets/tempbutterfly.gif"
            }

            for(i = 0; i<this.floatimages.length; i++){
                this.t+='<img src="'+this.floatimages[i]+'" name="p'+i+'" border="0">';
            }

            //document.write(this.t)
            h('span', { id: 'foo' });

            this.init();
        }
        // when resized, need a hook
    }
</script>

<style scoped>

</style>