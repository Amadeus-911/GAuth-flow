<template>
    <h2>Redirecting</h2>
</template>

<script>
    import router from '@/router'

    export default {
        name: 'parse',
        created() {},
        mounted() {
            console.log('parsing')
            const url = new URL(window.location.href)
            const fragment = url.hash
            const cleanedFragment = fragment.slice(1)
            const paramsArray = cleanedFragment.split('&')
            const params = {}
            paramsArray.forEach((param) => {
                const [key, value] = param.split('=')
                params[key] = value
            })

            localStorage.setItem('accessToken', params.access_token)

            if (params.access_token) {
                const cleanUrl = () => {
                    console.log('cleaningUrl')
                    const cleanURL = window.location.protocol + '//' + window.location.host + window.location.pathname
                    window.history.replaceState({}, document.title, cleanURL)
                }
                cleanUrl()
                router.push('/')
            } else {
                router.push('/login?login_failed=1')
            }
        },
    }
</script>

<style></style>
