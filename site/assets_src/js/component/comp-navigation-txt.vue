/**
* -----------------------------------------------------
* Created by uforgot on 2017. 9. 20.
* zanybros
* -----------------------------------------------------
*/

<template>
    <div class="txt">
        <ul :style="{
                'margin-top': currentTop + 'px'
            }"
        >
            <li>OUR WORKS</li>
            <li>ABOUT US</li>
            <li>WHAT WE DO</li>
            <li>OUR WORKS</li>
            <li>ABOUT US</li>
        </ul>
    </div>
</template>

<style scoped lang="scss">
    @import "~scssMixin";
</style>

<script>
    import TWEEN from '../vendor/Tween';

    export default {
        mixins: [],
        components: {},

        props: {
            'data-index':Number
        },
        data: function () {
            return {
                currentTop:Number
            };
        },

        computed: {
            marginTop : function() {

            }
        },
        methods: {
        },
        watch: {
            dataIndex : function($newValue, $oldValue){

                if (this.getRouterFlowDirection($oldValue, $newValue) === 'slide-left') {
                    if(this.currentTop < -30) {
                        this.currentTop = 0;
                    }
                } else if (this.getRouterFlowDirection($oldValue, $newValue) === 'slide-right') {
                    if(this.currentTop > -30) {
                        this.currentTop = -60;
                    }
                }


                function animate() {
                    if (TWEEN.update()) {
                        requestAnimationFrame(animate);
                    }
                }

                new TWEEN.Tween({ tweeningNumber :  this.currentTop })
                    .to({ tweeningNumber : (($newValue +1)*-15) }, 200).easing(TWEEN.Easing.Quadratic.Out)
                    .onUpdate(($e) =>
                        {
                            this.currentTop = Number($e.tweeningNumber.toFixed(2));
                        }
                    )
                    .start();
                animate();
            }
        },

        //life cycle
        //beforeCreate : function() {},
        //created : function() {},
        //beforeMount : function() {},
        //mounted : function() {},
        //beforeUpdate : function() {},
        //updated : function() {},
        //activated : function() {},
        //deactivated : function() {},
        //beforeDestroy : function () {},
        //destroyed : function() {},
        dummy: {}
    }
</script>
