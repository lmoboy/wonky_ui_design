<script>
    //region IMPORTS
    import { fade } from "svelte/transition";
    
    //endregion
    
    //region VARIABLES
    let input = $state([0,0,0,0,0,0]);
    let output = $state([]);
    

    const braille = {
        '000000': ' ',
        '100000': 'a',
        '110000': 'b',
        '100100': 'c',
        '100110': 'd',
        '100010': 'e',
        '110100': 'f',
        '110110': 'g',
        '110010': 'h',
        '010100': 'i',
        '010110': 'j',
        '101000': 'k',
        '111000': 'l',
        '101100': 'm',
        '101110': 'n',
        '101010': 'o',
        '111100': 'p',
        '111110': 'q',
        '111010': 'r',
        '011100': 's',
        '011110': 't',
        '101001': 'u',
        '111001': 'v',
        '010111': 'w',
        '101101': 'x',
        '101111': 'y',
        '101011': 'z',
        '010011': '.',
        '010000': ',',
        '011001': '?',
        '011010': '!',
        '010010': ':',
        '011000': ';',
        '001001': '-',
        '010101': '<',
        '101010': '>',
        '110001': '(',
        '001110': ')',
    }

    const brailleNumber = {
        '100000': '1',
        '110000': '2',
        '100100': '3',
        '100110': '4',
        '100010': '5',
        '110100': '6',
        '110110': '7',
        '110010': '8',
        '010100': '9',
        '010110': '0',
    }
    // endregion

    //region FUNCTIONS
    const brailleFunctions = {
        '000001': (nextChar) => {
            if (!nextChar) {
                return '';
            }
            return braille[nextChar].toUpperCase();
        },
        '000101': (nextNumber)=>{
            if(!nextNumber) return '';
            return brailleNumber[nextNumber];
        }
    }

    function isValidBraille(inputArray) {
    const inputString = parseArray(inputArray);

    return Object.keys(braille).includes(inputString) || Object.keys(brailleNumber).includes(inputString) || Object.keys(brailleFunctions).includes(inputString);
}

    function parseArray(inputArray){
        let outputString = '';

        inputArray.forEach(element => {
            if(element == true){
                outputString += '1';
            }else{
                outputString += '0';
            }
        });
        return outputString;
    }

    function parse(inputArray){
        let copy = inputArray
        let outputString = '';
        let shouldSkip = false;
        let index = 0
        copy.forEach(element => {

            try {
                switch (element) {
                    case '000001':
                    outputString += brailleFunctions[element](copy[index + 1]);
                    shouldSkip = true;
                        break;
                    case '000101':
                    outputString += brailleFunctions[element](copy[index + 1]);
                    shouldSkip = true;

                        break;
                    default:
                        if(shouldSkip){
                            shouldSkip = false;
                            break;
                        }
                        
                        outputString += braille[element];
                        break;
                }
            } catch (error) {
                return '';
            }
            index++

        })
        
        return outputString
    }

    function onAppend(){
        if(!isValidBraille(input)){return}
        output.push(parseArray(input)); 
        input = [0,0,0,0,0,0];
    }

    function onRemove(){
        output = output.slice(0, -1);
    }

    //endregion


</script>
    <h2>
        <code>Braille input aka blind people friendly!</code>
    </h2>


    <!-- svelte-ignore a11y_click_events_have_key_events -->
    <!-- svelte-ignore a11y_no_static_element_interactions -->
    <div class="braille-container">
        <input type="text" value={parse(output)} disabled>
        <div class="braille">
            <div class="{"dot" + (input[0]  ? " active" : "")}" onclick="{()=>{input[0] = !input[0]}}" style={`grid-column: 1; grid-row: 1;`}></div>
            <div class="{"dot" + (input[1]  ? " active" : "")}" onclick="{()=>{input[1] = !input[1]}}" style={`grid-column: 1; grid-row: 2;`}></div>
            <div class="{"dot" + (input[2]  ? " active" : "")}" onclick="{()=>{input[2] = !input[2]}}" style={`grid-column: 1; grid-row: 3;`}></div>
            <div class="{"dot" + (input[3]  ? " active" : "")}" onclick="{()=>{input[3] = !input[3]}}" style={`grid-column: 2; grid-row: 1;`}></div>
            <div class="{"dot" + (input[4]  ? " active" : "")}" onclick="{()=>{input[4] = !input[4]}}" style={`grid-column: 2; grid-row: 2;`}></div>
            <div class="{"dot" + (input[5]  ? " active" : "")}" onclick="{()=>{input[5] = !input[5]}}" style={`grid-column: 2; grid-row: 3;`}></div>
        </div> 
        <button onclick="{()=>{onAppend()}}">
            append
        </button>
        <button onclick="{()=>{onRemove()}}">
            delete
        </button>
     </div>




    <style>
        .dot{
            transition: background-color 0.2s;
            width: 20px;
            height: 20px;
            margin: 10px;
            border-radius: 10px;
            background-color: white;
        }
        .dot.active{
            background-color: black;
        }
        .braille {
            width: fit-content;
            display: grid;
            grid-template: repeat(3, 1fr) / repeat(2, 1fr);
        }
        .braille-container{
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
        }
    </style>