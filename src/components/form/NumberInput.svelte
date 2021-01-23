<svelte:options tag="number-input" />

<input type="text" bind:this={element} bind:value={value} style="text-align: right" />

<script>
import { onMount, afterUpdate } from 'svelte'

export let value
export let name
let rawvalue
let numberFormat
let element

onMount(() => {
    numberFormat = new Intl.NumberFormat(
        'en-US',
        {
            style: 'decimal'
        }
    )
})

function parseInput(inputValue) {
    let parsed = inputValue

    //remove non-numeric characters
    parsed = parsed.replace(/[^\-\.0-9]/g, '')
    
    // Wait more number after '.' ending
    if(parsed.charAt(parsed.length-1) !== '.')
        parsed = parseFloat(parsed)
    
    return parsed
}

afterUpdate(() => {
    if (typeof value === 'undefined' || value.charAt(value.length-1) === '.')
        return true

    rawvalue = parseInput(value)

    if(Number.isNaN(rawvalue) || rawvalue === 'NaN')
        rawvalue = 0

    value = numberFormat.format(rawvalue)
    element.dispatchEvent(new CustomEvent('number-input-update--' + name , {
        detail: { rawvalue },
        bubbles: true,
        composed: true, // needed for the event to traverse beyond shadow dom
    }))
})
</script>
