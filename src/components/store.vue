<script>
export default {
    fetch: (key) => JSON.parse(window.localStorage.getItem(key)),
    save: (data, key) => window.localStorage.setItem(key, JSON.stringify(data)),
}
</script>