<script>

    let email = "";
    let username = "Пользователь";
    let currentPassword = "";
    let newPassword = "";
    let confirmPassword = "";
    let theme = "light";
    let notificationsEnabled = true;

    // Заглушка для сохранения email
    const saveEmail = () => {
        alert(`Email "${email}" сохранен!`);
        email = "";
    };

    // Заглушка для сохранения имени пользователя
    const saveUsername = () => {
        alert(`Имя пользователя изменено на "${username}"!`);
    };

    // Заглушка для смены пароля
    const changePassword = () => {
        if (newPassword !== confirmPassword) {
            alert("Пароли не совпадают!");
            return;
        }
        alert("Пароль успешно изменён!");
        currentPassword = "";
        newPassword = "";
        confirmPassword = "";
    };

    // Заглушка для сохранения настроек
    const saveSettings = () => {
        alert(`Настройки сохранены! Тема: "${theme}", Уведомления: "${notificationsEnabled ? 'Включены' : 'Отключены'}"`);
    };

    // Функция для выхода из профиля
    const logout = () => {
        window.location.href="/";
    };
</script>

<div class="settings-container">
    <h2 class="settings-title">Настройки пользователя</h2>

    <div class="settings-section">
        <h3>Изменить Email</h3>
        <input type="email" bind:value={email} placeholder="Введите новый email" class="input" />
        <button class="btn" on:click={saveEmail}>Сохранить Email</button>
    </div>

    <div class="settings-section">
        <h3>Изменить имя пользователя</h3>
        <input type="text" bind:value={username} placeholder="Введите новое имя" class="input" />
        <button class="btn" on:click={saveUsername}>Сохранить имя</button>
    </div>

    <div class="settings-section">
        <h3>Сменить пароль</h3>
        <input type="password" bind:value={currentPassword} placeholder="Текущий пароль" class="input" />
        <input type="password" bind:value={newPassword} placeholder="Новый пароль" class="input" />
        <input type="password" bind:value={confirmPassword} placeholder="Подтвердите новый пароль" class="input" />
        <button class="btn" on:click={changePassword}>Сменить пароль</button>
    </div>

    <div class="settings-section">
        <h3>Дополнительные настройки</h3>
        <div class="setting-option">
            <label>Тема:</label>
            <select bind:value={theme} class="select">
                <option value="light">Светлая</option>
                <option value="dark">Тёмная</option>
            </select>
        </div>
        <div class="setting-option">
            <label>
                <input type="checkbox" bind:checked={notificationsEnabled} class="checkbox" />
                Включить уведомления
            </label>
        </div>
        <button class="btn" on:click={saveSettings}>Сохранить настройки</button>
    </div>

    <div class="logout-section">
        <button class="btn btn-logout" on:click={logout}>Выйти из профиля</button>
    </div>
</div>

<style>
    .settings-container {
        max-width: 600px;
        margin: 50px auto;
        padding: 20px;
        background-color: #2c2c2c;
        border: 1px solid #444;
        border-radius: 8px;
        box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.5);
        color: #fff;
        font-family: Arial, sans-serif;
    }

    .settings-title {
        text-align: center;
        font-size: 28px;
        margin-bottom: 20px;
    }

    .settings-section {
        margin-bottom: 30px;
        padding: 20px;
        background-color: #3b3b3b;
        border-radius: 8px;
        box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.3);
    }

    .settings-section h3 {
        margin-bottom: 15px;
        font-size: 20px;
        color: #ffc107;
    }

    .input {
        width: 100%;
        padding: 10px;
        margin-bottom: 15px;
        background-color: #4b4b4b;
        border: 1px solid #555;
        color: #fff;
        border-radius: 4px;
        box-sizing: border-box;
    }

    .btn {
        background-color: #007BFF;
        color: #fff;
        padding: 10px 20px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s;
        width: 100%;
    }

    .btn:hover {
        background-color: #0056b3;
    }

    .setting-option {
        margin-bottom: 15px;
    }

    .setting-option label {
        display: block;
        margin-bottom: 5px;
    }

    .select {
        width: 100%;
        padding: 10px;
        background-color: #4b4b4b;
        border: 1px solid #555;
        color: #fff;
        border-radius: 4px;
    }

    .checkbox {
        margin-right: 10px;
    }

    .logout-section {
        margin-top: 40px;
        text-align: center;
    }

    .btn-logout {
        background-color: #dc3545;
    }

    .btn-logout:hover {
        background-color: #c82333;
    }
</style>
