<script>
    import '@fontsource/poppins';

    let questions = [
        { id: 1, text: "Who made this website?" },
        { id: 2, text: "What's Authwise?" },
        { id: 3, text: "Where are you located?" },
        { id: 4, text: "What are your three favorite colors?" },
        { id: 5, text: "Wow, you're sooo cool! Can I be your girlfriend?" },
        { id: 6, text: "This website's design SUCKS! Are you actually stupid?" },
    ];

    let answers = [
        { id: 1, text: "This website was made by me, Will, as a way to practice web development for my employer, Authwise."},
        {
            id: 2,
            text: "Authwise is an upcoming identity provider that features near-endless scalability, support for " +
                "OAuth, OIDC, and SAML, an integrated SCIM API, universal login compatibility, total " +
                "administrative flexibility, and more. It's still in active development, so features may change."
        },
        {
            id: 3,
            text: "I live in Snohomish, Washington, but spend most of my waking hours in the nearby city " +
                "of Bothell. Authwise is based in Seattle, and you can find us (for now) at 1201 2nd Ave, 9th floor, room 942B."},
        {
            id: 4,
            text: "Purple, slate gray, and sea green."
        },
        {
            id: 5,
            text: "Unfortunately, due to unforeseen personal circumstances I'm not accepting girlfriend applications at the moment. " +
                "Sorry for the inconvenience."
        },
        {
            id:6,
            text: "Look man, I'm a software developer, not a graphic designer. If you know one who would work for me without " +
                "pay my contact page is open.\nThe UX does need work, though..."
        },
    ];

    let selected = questions[0];
</script>


<h3>Now <strong>you</strong> get to do the talking, ask away.</h3>

<select bind:value={selected}>
    {#each questions as question}
        <option value={question}>{question.text}</option>
    {/each}
</select>
<p>{answers?.at(selected.id - 1)?.text}</p>
{#if selected.id === 1}
    <img src={'thisguy.jpg'} alt="" width={200}>
    <p>Here you can see the one good picture of me</p>
{/if}

<style>
    h3 {
        color: darkcyan;
        outline: black 5px;
    }

    strong {
        font-family: "poppins", sans-serif;
        color: blue;
    }
</style>