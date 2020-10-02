<script>
    import { goto } from '@sveltech/routify';
    import { jwt } from '../../stores.js';

    const creds = {
        'username': 'test',
        'password': 'test'
    }

    let username, password;

    let authenticate = () => {
        // TODO
        if (creds.username == username && creds.password == password){
            jwt.set(true)
            $goto('/')
        } else {
            alert("Username and/or password is incorrect.")
        }  
    }
</script>

<div class="temp-auth">
    <div class="auth-card">
        <h1>Hey There!</h1>
        <form on:submit={authenticate} action="">
            <div class="form-item">
                <label for="username">Username</label>
                <input required type="text" bind:value={username}>
            </div>
            <div class="form-item">
                <label for="password">Password</label>
                <input required type="password" bind:value={password}>    
            </div>
            <button>Submit</button>
        </form>
    </div>
</div>

<style>
    h1 {
        padding-top: .5em;
    }

    .temp-auth {
        display: flex;
        height: 100vh;
        width: 100vw;
        color: aliceblue;
        justify-content: center;
        align-items: center;
        background-image: url("https://pressstart.vip/images/uploads/assets/cityskyline.png");
    }

    .auth-card {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: rgba(250,250,250,.5);
        width: 250px;
        padding-bottom: 1em;
        border-radius: 10px;
    }

    form {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    button {
        margin-top: 1em;
    }

</style>