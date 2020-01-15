<script>
    export let rowName;
    export let nativeLanguageInfo;
    export let targetLanguageInfo;

</script>

<style>
    .comparison-row{
        display:grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
    }
    h2{
        display: flex;
        justify-content: center;
        align-items: center;
        padding-right: 10px;
    }
    h3{
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>

<div class = "comparison-row">
    <h2>{rowName}</h2>
    <h3>{nativeLanguageInfo}</h3>
    <h3> - </h3>
    <h3>{targetLanguageInfo}</h3>
</div>