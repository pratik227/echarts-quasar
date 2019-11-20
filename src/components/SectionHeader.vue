<template>
  <div>
    post_title {{postTitle}}
    <br/>
    class-name {{className}}
    <br/>
    canvas {{canvas}}
    <br/>
    <heading2 post-title="postTitle"></heading2>
    <br/>
    <component v-bind:is="stepComponent"></component>
  </div>
</template>

<script>
    import Heading2 from "./headings/heading2";

    export default {
        name: "SectionHeader",
        components: {
            Heading2,
        },
        props: ['postTitle', 'className', 'canvas'],
        computed: {
            stepComponent() {
                let data = this.canvas.split('/')[2];
                return () => import(`./animations/${data}`);
            }
        },
    }
</script>
