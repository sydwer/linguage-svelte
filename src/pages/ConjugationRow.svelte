<script>
    export let info;
    export let generatedInfo;
</script>

<style>
   h3{
       border-bottom: 1px double black;
       margin: 0;
       display: grid;
       grid-template-columns: 1fr 1fr;
   }
   span{
       display: flex;
       justify-content: center;
   }
   #info{
       color: grey;
       border-right: 1px dotted black;
   }
</style>


<h3><span id="info">{info}</span>  <span>{generatedInfo}</span></h3>
