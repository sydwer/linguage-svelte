<script>
    export let message
</script>

<style>
#loading-bar{
    color: #598502;
    display: flex;
    flex-direction: row;
    align-items: center;
}

@keyframes blink {
    0% {
      opacity: .2;
    }
    20% {
      opacity: 1;
    }
    100% {
      opacity: .2;
    }
}

.loading span {
    animation-name: blink;
    animation-duration: 1.4s;
    animation-iteration-count: infinite;
    animation-fill-mode: both;
}

.loading span:nth-child(2) {
    animation-delay: .2s;
}

.loading span:nth-child(3) {
    animation-delay: .4s;
}

</style>

<h1 id="loading-bar"> {message}<p class="loading"><span>.</span><span>.</span><span>.</span></p></h1>
