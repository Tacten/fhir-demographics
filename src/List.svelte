<script>
  import { onMount } from "svelte";
  import { fhir } from "./fhir";
  import {Link} from "svelte-routing"

    let data = []
    onMount(async ()=>{
       const r =  await fhir.get('/Patient')
       console.log(r)
       data = r.data?.entry
    })
</script>
<div class="p-10">
    <h1 class="text-3xl font-sans font-bold">Patients</h1>
    <Link to='/patient'>
        <button class="my-10 px-4 py-2 rounded-md text-white bg-green-600" >Add patient</button>
    </Link>
    <div class="mt-10 flex justify-center flex-col gap-10">
        {#each data as patient}
            <Link to={`patient/${patient.resource.id}`}  class="bg-gray-200 shadow-md px-14 py-4 text-left text-blue-500">{patient.resource.name[0].given}</Link>
        {/each}
    </div>
</div>