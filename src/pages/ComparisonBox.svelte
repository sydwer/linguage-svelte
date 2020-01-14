<script>
    export let comparison;
</script>

<style>
#main{
    width: 75%;
}
#comparison-info-header{
    display:grid;
    grid-template-columns: 1fr 1fr 1fr;
}
h1{
    display: flex;
    justify-content: center;
}
</style>

<div id="main">
<div id="comparison-info-header">
    <h1>{comparison.native_language.name}:</h1>
    <h1> vs.</h1>
    <h1>{comparison.target_language.name}:</h1>
</div>
</div>