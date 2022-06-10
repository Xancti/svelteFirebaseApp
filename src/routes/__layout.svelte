<script>
    import App from "./fb";
    import { onMount } from 'svelte'; // Life-cycle method; after all components load, do x-y-z
    import { getAuth, onAuthStateChanged } from 'firebase/auth';
    import { goto } from "$app/navigation";

    onMount(() => {
        const auth = getAuth();
        onAuthStateChanged(auth, (user) => {
            if(user) {
                console.log('Welcome to file portal!');
            }
            else {
                goto('/login');
            }
        })
    })

</script>

<slot></slot>