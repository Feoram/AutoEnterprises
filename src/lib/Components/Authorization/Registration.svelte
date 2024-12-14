<script>
    let isLogin = true;

    // Поля для регистрации
    let regName = "";
    let regPassword = "";
    let regPasswordRepeat = "";
    let regError = "";

    // Поля для авторизации
    let loginName = "";
    let loginPassword = "";
    let loginError = "";

    // Переключение между формами
    const toggleForm = () => {
        isLogin = !isLogin;
        clearErrors();
        clearFields();
    };

    // Очистка ошибок
    const clearErrors = () => {
        regError = "";
        loginError = "";
    };

    // Очистка полей формы
    const clearFields = () => {
        regName = "";
        regPassword = "";
        regPasswordRepeat = "";
        loginName = "";
        loginPassword = "";
    };

    // Обработка регистрации
    const handleRegister = () => {
        if (regPassword !== regPasswordRepeat) {
            regError = "Пароли не совпадают!";
            return;
        }
        window.location.href = "/home";
    };

    // Обработка авторизации
    const handleLogin = () => {
        window.location.href = "/home";
    };

    // Обработчик для нажатия клавиши Enter
    const handleKeydown = (event) => {
        if (event.key === "Enter") {
            if (isLogin) {
                handleLogin();
            } else {
                handleRegister();
            }
        }
    };
</script>

<div class="auth-container" on:keydown={handleKeydown} tabindex="0">
    <div class="form-container">
        {#if isLogin}
            <h2 class="form-title">Авторизация</h2>
            <input type="text" placeholder="Имя" bind:value={loginName} class="input-field" />
            <input type="password" placeholder="Пароль" bind:value={loginPassword} class="input-field" />
            {#if loginError}
                <div class="error-message">{loginError}</div>
            {/if}
            <button class="auth-button" on:click={handleLogin}>Войти</button>
            <div class="switch">
                <span>Нет аккаунта? <span class="switch-link" on:click={toggleForm}>Зарегистрироваться</span></span>
            </div>
        {:else}
            <h2 class="form-title">Регистрация</h2>
            <input type="text" placeholder="Имя" bind:value={regName} class="input-field" />
            <input type="password" placeholder="Пароль" bind:value={regPassword} class="input-field" />
            <input type="password" placeholder="Повторите пароль" bind:value={regPasswordRepeat} class="input-field" />
            {#if regError}
                <div class="error-message">{regError}</div>
            {/if}
            <button class="auth-button" on:click={handleRegister}>Зарегистрироваться</button>
            <div class="switch">
                <span>Уже есть аккаунт? <span class="switch-link" on:click={toggleForm}>Войти</span></span>
            </div>
        {/if}
    </div>
</div>


<style>
    .auth-container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background-color: #1e1e1e;
        color: #fff;
        font-family: 'Arial', sans-serif;
    }

    .form-container {
        width: 100%;
        max-width: 400px;
        padding: 30px;
        background-color: #2c2c2c;
        border-radius: 12px;
        box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.5);
    }

    .form-title {
        text-align: center;
        font-size: 24px;
        margin-bottom: 20px;
        color: #ffc107;
    }

    .input-field {
        width: 100%;
        padding: 12px;
        margin-bottom: 15px;
        background-color: #3b3b3b;
        border: 1px solid #555;
        color: #fff;
        border-radius: 6px;
        font-size: 16px;
        box-sizing: border-box;
    }

    .input-field::placeholder {
        color: #aaa;
    }

    .auth-button {
        width: 100%;
        padding: 12px;
        background-color: #007BFF;
        color: white;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s;
    }

    .auth-button:hover {
        background-color: #0056b3;
    }

    .switch {
        text-align: center;
        margin-top: 15px;
        font-size: 14px;
    }

    .switch-link {
        color: #ffc107;
        cursor: pointer;
        text-decoration: underline;
        transition: color 0.3s;
    }

    .switch-link:hover {
        color: #ffdd57;
    }

    .error-message {
        color: #dc3545;
        margin-bottom: 15px;
        text-align: center;
    }
</style>
