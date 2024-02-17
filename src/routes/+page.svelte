<script lang="ts">
    const numbers = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "."];
    const operations = ["/", "x", "+", "-", "="];


    let selectedOperation = "";
    let display = "";
    let firstNumber = "";
    let secondNumber = "";
    let isDisplayResults = false

    const handleOperationClick = (operator: string) => {
        if(!firstNumber) return;
        if(operator === "="){
            if(!secondNumber) return;
            const firstNum = parseInt(firstNumber)
            const secondNum = parseInt(secondNumber)

            let results = ""

            switch(selectedOperation){
                case "/":
                results = (firstNum / secondNum).toFixed(2);
                break;

                case "x":
                results = (firstNum * secondNum).toFixed(2);
                break;
                case "+":
                results = (firstNum + secondNum).toFixed(2);
                break;

                case "-":
                results = (firstNum - secondNum).toFixed(2);
                break;

            }

            display = results

            isDisplayResults = true;
        }
        selectedOperation = operator
        
    };

    const handleClear = () => {
        firstNumber = ""
        secondNumber = ""
        selectedOperation =  ""
        display = ""
        isDisplayResults = false;
    }

    const handleNumberClick = (number: string) => {
        if(isDisplayResults){
            handleClear()
        }
        if (display === "" && number === "0") return;
        if (number === "." && display.includes('.')) return;

        if(display === "" && number === "."){
            return display = "0.";
        }


        if (!selectedOperation) {
            if(display === "" && number === "."){
            firstNumber = "0."
            return display = "0.";
            }
            firstNumber = `${firstNumber}${number}`;
           return display = firstNumber;
        }else{
            if(display === "" && number === "."){
            secondNumber = "0.";
            return (display = secondNumber);
            }

            secondNumber = `${secondNumber}${number}`;
           return display = secondNumber;
        }
    };

    
</script>


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator App</title>
</head>
<body>
    <main>
    
    <div class="calculator">
        <div class="result">
            {display}
        </div>
        <div class="digit">
            <div class="numbers">
                <button class="btn btn-xlg" on:click={handleClear}> C </button>
                {#each numbers as number (number)}

                    <button class={`btn ${number === "0" ? "btn-lg" : null}`} on:click={() => handleNumberClick(number)}>
                        {number} 
                    </button>
                {/each}
            </div>

            <div class="operations ">
                {#each operations as operator (operator)}
                    <button class={`btn btn-orange ${operator === selectedOperation ? "btn-sliver" : "btn-orange"}`}

                     on:click={() => handleOperationClick(operator)}>
                     
                     {operator}</button>
                {/each}

                <!--<button class="btn btn-orange"> / </button>
                <button class="btn btn-orange"> x </button>
                <button class="btn btn-orange"> + </button>
                <button class="btn btn-orange"> - </button>
                <button class="btn btn-orange"> = </button> -->
            </div>
        </div>
    </div>
</main>
</body>
</html>



<style>
    main{
        width: 100vw;
        height: 100vh;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    
    .calculator{
        background: rgb(28, 28, 28);
        width: 240px;
        padding: 15px;
        border-radius: 7px;
    }

    .result{
        height: 60px;
        color: #fff;
        font-size: 50px;
        display: flex;
        flex-direction: row-reverse;
        margin: 10px;
        overflow: hidden;
    }

    .digit{
        display: flex;
        align-items: center;
    }

    .numbers{
        display: flex;
        flex-wrap: wrap;
        width: 200px;
    }

    .operations{
        display: flex;
        flex-direction: column;
        
    }


    .btn{
        text-align: center;
        padding: 10px;
        background-color: rgb(114, 113, 113);
        font-size: 20px;
        font-weight: bold;
        margin: 5px;
        border: none;
        width: 50px;
        height: 50px;
        border-radius: 100px;
        color: #fff;
    }

    .btn-lg{
        width: 110px;
    }

    .btn-orange{
        background: orange;
    }

    .btn-sliver{
        background-color: silver;
    }

    .btn-xlg{
        width: 170px;
    }



</style>