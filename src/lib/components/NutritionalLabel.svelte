<script>
    export let nutritionData;
    export let defaultData = {};
    import Arrow from "./Arrow.svelte";
    
    // function className(name) {
    //     let range = 10;
    //     const arr = ["calories", "sodium", "size", "cholesterol", "potassium"]
    //     const arr2 = ["fat", "sat_fat", "trans_fat", "carbs", "sugar", "protein"]
    //     if (arr.includes(name)) {
    //         range = 50;
    //     } 
    //     else if (arr2.includes(name)) {
    //         range = 5;
    //     }

    //     let ans = "m-1"
    //     console.log(nutritionData[name])
    //     if (parseFloat(defaultData[name]) == parseFloat(nutritionData[name])) {
    //         ans += " border-2 border-green-500"
    //     }
    //     else if (parseFloat(defaultData[name]) - parseFloat(nutritionData[name]) < range && defaultData[name] - nutritionData[name] > range) {
    //         ans += " border-2 border-yellow-500"
    //     }
    //     return ans;        
    // }

    const VITAMIN_A_MAX = 3000;
    const VITAMIN_B_MAX = 2.4;
    const VITAMIN_C_MAX = 90;
    const VITAMIN_D_MAX = 600;
    const VITAMIN_E_MAX = 15;

    let percent = 0;

    $: {
        console.log(defaultData);
        console.log(nutritionData);
        let calp = 0.11 * (1 - Math.abs(parseFloat(nutritionData.calories)-parseFloat(defaultData.calories))/(parseFloat(nutritionData.calories)+parseFloat(defaultData.calories)+Math.PI/100));
        let sodp = 0.10 * (1 - Math.abs(parseFloat(nutritionData.sodium)-parseFloat(defaultData.sodium))/(parseFloat(nutritionData.sodium)+parseFloat(defaultData.sodium)+Math.PI/100));
        let sugp = 0.10 * (1 - Math.abs(parseFloat(nutritionData.sugar)-parseFloat(defaultData.sugar))/(parseFloat(nutritionData.sugar)+parseFloat(defaultData.sugar)+Math.PI/100));
        let fatp = 0.15 * (1 - Math.abs(parseFloat(nutritionData.fat)-parseFloat(defaultData.fat))/(parseFloat(nutritionData.fat)+parseFloat(defaultData.fat)+Math.PI/100));
        let protp = 0.15 * (1 - Math.abs(parseFloat(nutritionData.protein)-parseFloat(defaultData.protein))/(parseFloat(nutritionData.protein)+parseFloat(defaultData.protein)+Math.PI/100));
        let carbp = 0.15 * (1 - Math.abs(parseFloat(nutritionData.carbs)-parseFloat(defaultData.carbs))/(parseFloat(nutritionData.carbs)+parseFloat(defaultData.carbs)+Math.PI/100));
        let satp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.sat_fat)-parseFloat(defaultData.sat_fat))/(parseFloat(nutritionData.sat_fat)+parseFloat(defaultData.sat_fat)+Math.PI/100));
        let transp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.trans_fat)-parseFloat(defaultData.trans_fat))/(parseFloat(nutritionData.trans_fat)+parseFloat(defaultData.trans_fat)+Math.PI/100));
        let chop = 0.02 * (1 - Math.abs(parseFloat(nutritionData.cholesterol)-parseFloat(defaultData.cholesterol))/(parseFloat(nutritionData.cholesterol)+parseFloat(defaultData.cholesterol)+Math.PI/100));
        let vitap = 0.02 * (1 - Math.abs(parseFloat(nutritionData.vitamin_a)-parseFloat(defaultData.vitamin_a))/(parseFloat(nutritionData.vitamin_a)+parseFloat(defaultData.vitamin_a)+Math.PI/100));
        let vitbp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.vitamin_b)-parseFloat(defaultData.vitamin_b))/(parseFloat(nutritionData.vitamin_b)+parseFloat(defaultData.vitamin_b)+Math.PI/100));
        let vitcp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.vitamin_c)-parseFloat(defaultData.vitamin_c))/(parseFloat(nutritionData.vitamin_c)+parseFloat(defaultData.vitamin_c)+Math.PI/100));
        let vitdp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.vitamin_d)-parseFloat(defaultData.vitamin_d))/(parseFloat(nutritionData.vitamin_d)+parseFloat(defaultData.vitamin_d)+Math.PI/100));
        let vitep = 0.02 * (1 - Math.abs(parseFloat(nutritionData.vitamin_e)-parseFloat(defaultData.vitamin_e))/(parseFloat(nutritionData.vitamin_e)+parseFloat(defaultData.vitamin_e)+Math.PI/100));
        let fibp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.fiber)-parseFloat(defaultData.fiber))/(parseFloat(nutritionData.fiber)+parseFloat(defaultData.fiber)+Math.PI/100));
        let potp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.potassium)-parseFloat(defaultData.potassium))/(parseFloat(nutritionData.potassium)+parseFloat(defaultData.potassium)+Math.PI/100));
        let ironp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.iron)-parseFloat(defaultData.iron))/(parseFloat(nutritionData.iron)+parseFloat(defaultData.iron)+Math.PI/100));
        let calcp = 0.02 * (1 - Math.abs(parseFloat(nutritionData.calcium)-parseFloat(defaultData.calcium))/(parseFloat(nutritionData.calcium)+parseFloat(defaultData.calcium)+Math.PI/100));
        percent = calp+sodp+sugp+fatp+protp+carbp+satp+transp+chop+vitap+vitbp+vitcp+vitdp+vitep+fibp+potp+ironp+calcp;
        percent *= 100;
        percent = Math.round(percent);
        console.log(calp)
        console.log(percent)
    }   

</script>

<div class="border-2 border-r-4 bg-white border-black mt-4 border-b-0 ps-3 bg-white">
    {#if (defaultData.name == undefined)}
        <p class="text-black text-4xl">Mystery Food</p>
        <p class="absolute text-sm">(serving size standardized to 100g)</p>  
    {:else}
        <div class="flex justify-between items-center">
            <p class="text-black text-4xl">{nutritionData["name"]}</p>
            <p class="text-black text-4xl pe-2">{percent}%</p>
        </div>  
    {/if}
</div>
<div class="border-2 bg-white border-black border-r-4 border-b-4 bg-white p-5">
    <div class="grid grid-cols-3 gap-2 text-xl text-center mb-2">
        <div>
        <!-- <div class={className("calories")}> -->
            <p class="sm:text-4xl text-2xl">{nutritionData.calories} Cal</p>
            <p>Calories<Arrow guess={nutritionData.calories} real={defaultData.calories} /></p>
        </div>
        <div>
        <!-- <div class={className("sodium")}> -->
            <p class="sm:text-4xl text-2xl">{nutritionData.sodium}mg</p>
            <p>Sodium<Arrow guess={nutritionData.sodium} real={defaultData.sodium} /></p>
        </div>
        <div>
        <!-- <div class={className("sugar")}> -->
            <p class="sm:text-4xl text-2xl">{nutritionData.sugar}g</p>
            <p>Sugar<Arrow guess={nutritionData.sugar} real={defaultData.sugar}/></p>
        </div>
    </div>
    <div class="grid grid-cols-3 gap-2 text-xl sm:text-lg text-center mb-2">
        
        <div>
        <!-- <div class={className("fat")}> -->
            <p class="sm:text-4xl text-2xl">{nutritionData.fat}g</p>
            <p>Fat<Arrow guess={nutritionData.fat} real={defaultData.fat} /></p>
        </div>
        <div>
        <!-- <div class={className("protein")}> -->
            <p class="sm:text-4xl text-2xl">{nutritionData.protein}g</p>
            <p>Protein<Arrow guess={nutritionData.protein} real={defaultData.protein} /></p>
        </div>
        <div>
        <!-- <div class={className("carbs")}> -->
            <p class="sm:text-4xl text-2xl">{nutritionData.carbs}g</p>
            <p>Carbs<Arrow guess={nutritionData.carbs} real={defaultData.carbs} /></p>
        </div>
    </div>
    <div class="sm:grid grid-cols-3 gap-2 text-md text-center">
        <div class="m-1">
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("sat_fat")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Saturated Fat:</p>
                <p>{nutritionData.sat_fat}g<Arrow guess={nutritionData.sat_fat} real={defaultData.sat_fat} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("trans_fat")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Trans Fat:</p>
                <p>{nutritionData.trans_fat}g<Arrow guess={nutritionData.trans_fat} real={defaultData.trans_fat} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("cholesterol")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Cholesterol:</p>
                <p>{nutritionData.cholesterol}mg<Arrow guess={nutritionData.cholesterol} real={defaultData.cholesterol} /></p>
            </div>
        </div>
        <div class="m-1">
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
            <!-- <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2 class={className("vitamin_a")}"> -->
                <p class="mr-2">Vitamin A:</p>
                <p>{(nutritionData.vitamin_a / VITAMIN_A_MAX * 100).toFixed(2)}%<Arrow guess={nutritionData.vitamin_a / VITAMIN_A_MAX} real={defaultData.vitamin_a / VITAMIN_A_MAX} /></p>
            </div>
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("vitamin_b")}"> -->
                <p class="mr-2">Vitamin B:</p>
                <p>{(nutritionData.vitamin_b / VITAMIN_B_MAX * 100).toFixed(2)}%<Arrow guess={nutritionData.vitamin_b / VITAMIN_B_MAX} real={defaultData.vitamin_b / VITAMIN_B_MAX} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("vitamin_c")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Vitamin C:</p>
                <p>{(nutritionData.vitamin_c / VITAMIN_C_MAX * 100).toFixed(2)}%<Arrow guess={nutritionData.vitamin_c / VITAMIN_C_MAX} real={defaultData.vitamin_c / VITAMIN_C_MAX} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("vitamin_d")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Vitamin D:</p>
                <p>{(nutritionData.vitamin_d / VITAMIN_D_MAX * 100).toFixed(2)}%<Arrow guess={nutritionData.vitamin_d / VITAMIN_D_MAX} real={defaultData.vitamin_d / VITAMIN_D_MAX} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("vitamin_e")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Vitamin E:</p>
                <p>{(nutritionData.vitamin_e / VITAMIN_E_MAX * 100).toFixed(2)}%<Arrow guess={nutritionData.vitamin_e / VITAMIN_E_MAX} real={defaultData.vitamin_e / VITAMIN_E_MAX} /></p>
            </div>
        </div>
        <div class="m-1">
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("fiber")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Fiber:</p>
                <p>{nutritionData.fiber}g<Arrow guess={nutritionData.fiber} real={defaultData.fiber} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("potassium")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Potassium:</p>
                <p>{nutritionData.potassium}mg<Arrow guess={nutritionData.potassium} real={defaultData.potassium} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("iron")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Iron:</p>
                <p>{nutritionData.iron}mg<Arrow guess={nutritionData.iron} real={defaultData.iron} /></p>
            </div>
            <!-- <div class="flex justify-between items-center ps-2 pe-2 class={className("calcium")}"> -->
            <div class="flex sm:justify-around justify-between sm:border-none border-b border-black items-center ps-2 pe-2}">
                <p class="mr-2">Calcium:</p>
                <p>{nutritionData.calcium}mg<Arrow guess={nutritionData.calcium} real={defaultData.calcium} /></p>
            </div>
        </div>
    </div>
</div>