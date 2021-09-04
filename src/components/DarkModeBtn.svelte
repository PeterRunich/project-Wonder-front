<script lang="ts">
    function switch_theme() {
        console.log(localStorage.theme || localStorage.theme === 'light')
        if (localStorage.theme === undefined || localStorage.theme === 'light') {
            localStorage.theme = 'dark'
            document.documentElement.classList.add('dark')

        } else {
            localStorage.theme = 'light'
            document.documentElement.classList.remove('dark')
        }
    }
</script>

<button on:click={switch_theme}>
    Switch
</button>
