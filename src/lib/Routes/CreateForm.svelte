<script>
    import { onMount } from "svelte";

    // Типы данных для подменю
    const dataOptions = [
        { id: 1, name: "Данные об автопарке" },
        { id: 2, name: "Перечень и число водителей" },
        { id: 3, name: "Распределение водителей" },
        { id: 4, name: "Распределение транспорта по маршрутам" },
        { id: 5, name: "Пробег автотранспорта" },
        { id: 6, name: "Данные о ремонтах" },
    ];

    // Выбранный тип данных
    let selectedOption = null;

    // Динамические поля формы
    let formData = {};

    // Поля для каждого типа данных
    const formFields = {
        1: [{ label: "Название автопарка", key: "fleetName" }, { label: "Количество автомобилей", key: "carCount" }],
        2: [{ label: "Название предприятия", key: "companyName" }, { label: "Номер автомашины", key: "carNumber" }, { label: "Количество водителей", key: "driverCount" }],
        3: [{ label: "Имя водителя", key: "driverName" }, { label: "Номер автомобиля", key: "carNumber" }],
        4: [{ label: "Номер маршрута", key: "routeNumber" }, { label: "Количество автомобилей", key: "carCount" }],
        5: [{ label: "Категория автомобиля", key: "carCategory" }, { label: "Дата пробега", key: "mileageDate" }, { label: "Пробег", key: "mileage" }],
        6: [{ label: "Марка автомобиля", key: "carBrand" }, { label: "Дата ремонта", key: "repairDate" }, { label: "Стоимость ремонта", key: "repairCost" }],
    };

    // Модальное окно
    let showModal = false;

    // Очистка формы
    const clearForm = () => {
        formData = {};
    };

    // Обработка отправки данных
    const handleSubmit = () => {
        showModal = true;
        clearForm();
    };

    // Закрытие модального окна
    const closeModal = () => {
        showModal = false;
    };

    // Установка полей формы при выборе опции
    const selectOption = (optionId) => {
        selectedOption = optionId;
        formData = {};
        formFields[optionId].forEach((field) => (formData[field.key] = ""));
    };
</script>

<div class="create-form-container">
    <h2 class="create-form-title">Добавить данные</h2>

    <!-- Подменю -->
    <div class="submenu">
        {#each dataOptions as option}
            <button class="submenu-button" on:click={() => selectOption(option.id)}>
                {option.name}
            </button>
        {/each}
    </div>

    {#if selectedOption}
        <form class="dynamic-form" on:submit|preventDefault={handleSubmit}>
            {#each formFields[selectedOption] as field}
                <input
                        type="text"
                        class="dynamic-form-input"
                        placeholder={field.label}
                        bind:value={formData[field.key]}
                        required
                />
            {/each}
            <button type="submit" class="dynamic-form-button">Отправить</button>
        </form>
    {/if}
</div>

{#if showModal}
    <div class="modal-backdrop" on:click={closeModal}>
        <div class="modal" on:click|stopPropagation>
            <h3 class="modal-title">Данные успешно отправлены!</h3>
            <button class="modal-button" on:click={closeModal}>Закрыть</button>
        </div>
    </div>
{/if}

<style>
    .create-form-container {
        max-width: 600px;
        margin: 50px auto;
        padding: 20px;
        background-color: #2c2c2c;
        border: 1px solid #444;
        border-radius: 8px;
        box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.5);
        color: #fff;
        font-family: Arial, sans-serif;
        text-align: center;
    }

    .create-form-title {
        margin-bottom: 20px;
        font-size: 24px;
        color: #ffc107;
    }

    .submenu {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 10px;
        margin-bottom: 20px;
    }

    .submenu-button {
        background-color: #007BFF;
        color: white;
        border: none;
        padding: 10px 15px;
        border-radius: 6px;
        cursor: pointer;
        font-size: 14px;
        transition: background-color 0.3s;
    }

    .submenu-button:hover {
        background-color: #0056b3;
    }

    .dynamic-form {
        margin-top: 20px;
    }

    .dynamic-form-input {
        width: 100%;
        padding: 10px;
        margin-bottom: 15px;
        background-color: #3b3b3b;
        border: 1px solid #555;
        color: #fff;
        border-radius: 6px;
        font-size: 16px;
    }

    .dynamic-form-input::placeholder {
        color: #aaa;
    }

    .dynamic-form-button {
        width: 100%;
        padding: 12px;
        background-color: #28a745;
        color: white;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        font-size: 16px;
        transition: background-color 0.3s;
    }

    .dynamic-form-button:hover {
        background-color: #218838;
    }

    .modal-backdrop {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.7);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 1000;
    }

    .modal {
        background-color: #2c2c2c;
        padding: 30px;
        border-radius: 8px;
        box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.7);
        text-align: center;
        width: 300px;
    }

    .modal-title {
        margin-bottom: 20px;
        color: #fff;
    }

    .modal-button {
        padding: 10px 20px;
        background-color: #007BFF;
        color: #fff;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 14px;
    }

    .modal-button:hover {
        background-color: #0056b3;
    }
</style>
