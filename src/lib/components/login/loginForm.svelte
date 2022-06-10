<script>
    import { goto } from '$app/navigation';
    import { getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword } from "firebase/auth";

    export let title;

    const auth = getAuth()

    function login() {
        let email = document.getElementById('emailInput').value;
        let password = document.getElementById('passInput').value;
        if(title == 'Login') {
            signInWithEmailAndPassword(auth, email, password).then(
                (userCredential) => {
                    const user =userCredential.user;
                    localStorage.setItem("uid", user.uid); // Using svelte stores caused a lot of errors because of firebase interactions
                    goto("/");
                }
            ).catch((error) => {
                console.error(error);
            });
        }
        else {
            createUserWithEmailAndPassword(auth, email, password).then(
                (userCredential) => {
                    const user =userCredential.user;
                    localStorage.setItem("uid", user.uid); // Using svelte stores caused a lot of errors because of firebase interactions
                    goto("/");
                }
            ).catch((error) => {
                console.error(error);
            });
        }
    }
</script>

<div class="login">
    <div class="card">
        <div class="card-body login-form">
            <h5 class="card-title">{title}</h5>
            <form on:submit|preventDefault={login}>
                <div class="mb-3">
                    <label for="emailInput" class="form-label">Email Address</label>
                    <input 
                        type="text"
                        class="form-control"
                        id="emailInput"
                        aria-describedby="emailHelp"
                        placeholder="Email Address"                        
                    />
                    {#if title != "Login"}
                        <div id="emailHelp" class="form-text">
                            We'll never share your email with anyone else.
                        </div>
                    {/if}
                </div>
                <div class="mb-3">
                    <label for="passwordInput" class="form-label">Password</label>
                    <input 
                        type="text"
                        class="form-control"
                        id="passwordInput"
                        aria-describedby="passwordHelp"
                        placeholder="Password"                        
                    />
                </div>
                <button type="submit" class="btn btn-primary">Submit</button>
            </form>
            {#if title == "Login"}
                <p class="float-end mt-3">
                    Not a user? <a href="/signup" class="card-link">Sign up</a>
                </p>
            {/if}
        </div>
    </div>
</div>

<style>
    .card {
        width: 50%;
        margin: 0 auto;
    }
    .login {
        margin-top: 3em;
        margin-bottom: 3em;
    }
    .login-form {
        width: 60%;
        margin: 0 auto;
    }
    @media only screen and (min-device-width: 320p) and (max-device-width: 480px) {
        .login-form {
            width: 90%;
        }
        .card {
            width: 90%;
        }
    }
</style>
