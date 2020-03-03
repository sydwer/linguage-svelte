<script>
    export let syllables;
    export let nouns;
    export let verbs;
    export let adj;
    // the nouns verbs and adj's are universally used so they'll be sent in and sifted through for each language
    // ONLY GRAMMAR BASED AFFIXES CAN BE SEPERATE IN EACH grammarOrigin, dictionary level words have to be parent level component, EventSource.
    const topic = {IPA: undefined, latin: undefined}
    const subject = {IPA: undefined, latin: undefined}
    const object = {IPA: undefined, latin: undefined}
    const also = {IPA: undefined, latin: undefined}
    const from = {IPA: undefined, latin: undefined}
    const location = {IPA: undefined, latin: undefined}
    const and = {IPA: undefined, latin: undefined}
    const possesive = {IPA: undefined, latin: undefined}
    const question = {IPA: undefined, latin: undefined}
    // Declaring like this makes it possible to use 'class' function on the dictionary without needing to repeat variables
    // AND have a findWord function
    const particles = [topic, subject, object, also, from, location, and, possesive, question]

        // will need unique verbs/encodeURIComponent, since verbs carry inflection for ability or thinking/saying etc
</script>