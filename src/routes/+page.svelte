<script>
    import axios from "axios"
	import { onMount } from "svelte";

    const GetJokes = async ()=>{
        const response = await axios.get('https://api.chucknorris.io/jokes/random')
        return response
    }

    $:jokes = []

    onMount(async()=>{
        const joke = await GetJokes()

        jokes=[joke.data]

        console.log(jokes);
    })

    let refresh = setInterval(async()=>{
            const response = await GetJokes()
            jokes = [...jokes,response.data]

            console.log(response)
    },3500)

    // clearInterval(refresh)
</script>

<div class="w-full h-[100vh] bg-[#d3cefc] flex justify-center items-center">
        <div class="flex flex-col shadow-md h-[20rem] w-[20rem] rounded-md bg-white p-4">
            <h1 class="text-black text-center text-4xl">Chuck Norris</h1>

            <div class="flex flex-col gap-4 h-[18rem] overflow-auto">
                {#each jokes as joke}

                <div class="flex w-[100%] h-[100%] border-[#d3cefc] border-b"><h1>{joke.value}</h1></div>
                {/each}
            </div>
        </div>
</div>