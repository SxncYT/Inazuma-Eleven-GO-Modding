<script>
    import motions from '$lib/dataFiles/motions.json';

    function padId(id) {
        return id.toString().padStart(3, '0');
    }

    function decodeShiftJIS(str) {
    // Convert each char code to a byte
    const bytes = new Uint8Array([...str].map(c => c.charCodeAt(0)));
    // Decode as Shift-JIS
    try {
        return new TextDecoder('shift-jis').decode(bytes);
    } catch (e) {
        return '[Invalid Shift-JIS]';
    }
}
</script>

<h1>Motions</h1>
<p>This is the motions page.</p>

<ul>
    {#each motions as motion}
        <li>
            <img src={"motionsClips/motion_" + padId(motion.id) + ".gif"} alt={motion.motion} width="100" height="100"/>
            <p>Motion {motion.id}</p>
            <span>{decodeShiftJIS(motion.motion)}</span>
        </li>
    {/each}
</ul>

<style>
    * {
        color: white;
    }

    ul {
        display: flex;
        flex-direction: row;
        justify-content: flex-start;
        flex-wrap: wrap;
        list-style-type: "";
        width: 100%;
        gap: 1rem;
    }

    li {
        display: flex;
        flex-direction: column;
        align-items: center;
        flex: 1 1 25%;
        max-width: calc(25% - 1rem);
        border: 0.1rem solid white;
        padding: 1rem;
    }

    img {
        width: 100%;
        height: auto;
        border: 0.1rem solid white;
    }
</style>