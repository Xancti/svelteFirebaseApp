<script>
    import { goto } from '$app/navigation';
    import { getAuth, signOut } from 'firebase/auth';
    import { isLoggedIn } from "../../../routes/stores/authStore"

    const auth = getAuth();

    function logout() {
        signOut(auth).then(
            () => {
            localStorage.removeItem("uid");
            goto("/login")
            })
            .catch((error) => {
                console.error(error);
            });
    }
</script>

<ul class="nav justify-content-end bg-dark">
    <li class="nav-item">
        <a href="/" aria-current="page" class="nav-link">Home</a>
    </li>
    <li class="nav-item">
        <a href="https://google.com" class="nav-link" target="_blank"> 
            <!-- Link it to a different website -->
            My Website
        </a>
    </li>
    {#if $isLoggedIn}
        <li class="nav-item">
            <a class="nav-link" on:click|preventDefault={logout} href="/"> 
                Sign Out
            </a>
        </li>
    {/if}
</ul>