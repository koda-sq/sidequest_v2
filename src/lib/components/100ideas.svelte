<script lang="ts">
    // @ts-ignore
    export let id: string;
    export let ideaData: {
        Heading: string;
        Description: string;
        ideas: { Category: string; Ideas: string[] }[];
    };
    
    // Helper function to get starting index for each category
    // @ts-ignore
    function getStartIndex(categoryIndex) {
        console.log("getStartIndex called with categoryIndex:", categoryIndex);
        let count = 1;
        console.log(ideaData);
        for (let i = 0; i < categoryIndex; i++) {
            // @ts-ignore
            count += ideaData?.ideas[i]?.Ideas?.length || 0;
        }
        return count;
    }
</script>

<style>
    .idea {
        background: none;
        padding: 80px 20px;
        text-align: center;
    }

    .idea h2 {
        font-size: 4rem;
        letter-spacing: -4px;
        font-weight: 600;
        color: var(--yellow);
        margin-bottom: 30px;
    }
    .idea h3 {
        font-size: 1.25rem;
        color: #ffffff;
        margin: 50px 200px;
    }

    .list {
        width: 90%;
        max-width: 1000px;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        gap: 20px;
    }

    .card {
        background: #141414;
        border-left: 2px solid var(--yellow);
        padding: 20px;
        border-radius: 8px;
        text-align: left;
    }

    .card h4 {
        font-size: 1.75rem;
        color: var(--yellow);
        margin-bottom: 20px;
    }

    .card p {
        font-size: 1.1rem;
        margin-bottom: 2px;
        color: var(--yellow);
    }

    .idea .description {
        max-width: 700px;
        margin: 50px auto 0;
        font-size: 1rem;
        line-height: 1.6;
        color: var(--yellow);
    }

    a {
        color: var(--yellow);
    }
</style>

<section class="idea" id={id}>
    <h2>{ideaData?.Heading}</h2>
    <h3>{ideaData?.Description}</h3>
    <div class="list">
        {#each ideaData?.ideas as category, categoryIndex}
            <div class="card">
                <h4>{category.Category} (<a href="/apply">apply with one of these ideas</a>):</h4>
                {#each category.Ideas as idea, ideaIndex}
                    {#if getStartIndex}
                        <p class="standard-text">{getStartIndex(categoryIndex) + ideaIndex}. {idea}</p>
                    {/if}
                {/each}
            </div>
        {/each}
    </div>
    <div class="description">
        {ideaData?.Description}
    </div>
</section>