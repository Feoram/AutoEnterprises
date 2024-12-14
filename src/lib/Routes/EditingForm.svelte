<script>
    // Категории данных для выбора
    const categories = [
        { id: 'items', name: 'Элементы' },
        { id: 'fleets', name: 'Автопарки' },
        { id: 'drivers', name: 'Водители' },
    ];

    // Текущая выбранная категория
    let selectedCategory = 'items';

    // Данные для элементов
    let items = [
        {
            id: 1,
            name: 'Элемент 1',
            carNumber: 'A123BC',
            mileage: 15000,
            repairCost: 5000,
            runIn: 'Да',
            isEditing: false,
            originalData: {},
        },
        {
            id: 2,
            name: 'Элемент 2',
            carNumber: 'B456DE',
            mileage: 30000,
            repairCost: 10000,
            runIn: 'Нет',
            isEditing: false,
            originalData: {},
        },
        {
            id: 3,
            name: 'Элемент 3',
            carNumber: 'C789FG',
            mileage: 20000,
            repairCost: 7500,
            runIn: 'Да',
            isEditing: false,
            originalData: {},
        },
    ];

    // Данные для автопарков
    let fleets = [
        {
            id: 1,
            name: 'Автопарк №1',
            vehicleCount: 20,
            location: 'Москва',
            isEditing: false,
            originalData: {},
        },
        {
            id: 2,
            name: 'Автопарк №2',
            vehicleCount: 35,
            location: 'Санкт-Петербург',
            isEditing: false,
            originalData: {},
        },
    ];

    // Данные для водителей
    let drivers = [
        {
            id: 1,
            name: 'Иван Иванов',
            age: 35,
            licenseNumber: 'AB12345',
            assignedCar: 'A123BC',
            isEditing: false,
            originalData: {},
        },
        {
            id: 2,
            name: 'Петр Петров',
            age: 40,
            licenseNumber: 'CD67890',
            assignedCar: 'B456DE',
            isEditing: false,
            originalData: {},
        },
    ];

    let showDeleteModal = false;
    let itemToDelete = null;

    // Функция для выбора категории
    const selectCategory = (category) => {
        selectedCategory = category;
    };

    const editItem = (id) => {
        setCurrentData(
            getCurrentData().map((item) =>
                item.id === id ? { ...item, isEditing: true, originalData: { ...item } } : item
            )
        );
    };


    const cancelEdit = (id) => {
        setCurrentData(
            getCurrentData().map((item) =>
                item.id === id ? { ...item.originalData, isEditing: false } : item
            )
        );
    };

    const confirmEdit = (id) => {
        setCurrentData(
            getCurrentData().map((item) =>
                item.id === id ? { ...item, isEditing: false } : item
            )
        );
    };

    // Функция для получения данных текущей категории
    const getCurrentData = () => {
        if (selectedCategory === 'items') return items;
        if (selectedCategory === 'fleets') return fleets;
        if (selectedCategory === 'drivers') return drivers;
    };

    // Функция для обновления данных текущей категории
    const setCurrentData = (newData) => {
        if (selectedCategory === 'items') items = newData;
        if (selectedCategory === 'fleets') fleets = newData;
        if (selectedCategory === 'drivers') drivers = newData;
    };



    // Функция для открытия модального окна удаления
    const openDeleteModal = (id) => {
        itemToDelete = id;
        showDeleteModal = true;
    };

    // Функция для закрытия модального окна
    const closeDeleteModal = () => {
        itemToDelete = null;
        showDeleteModal = false;
    };

    // Функция для удаления элемента
    const deleteItem = () => {
        setCurrentData(getCurrentData().filter((item) => item.id !== itemToDelete));
        closeDeleteModal();
    };
</script>

<div class="editing-form-container">
    <h2 class="editing-form-title">Редактирование данных</h2>

    <!-- Подменю для выбора категории -->
    <div class="category-menu">
        {#each categories as category}
            <button class="category-button" on:click={() => selectCategory(category.id)}>
                {category.name}
            </button>
        {/each}
    </div>

    <!-- Таблица для элементов -->
    {#if selectedCategory === 'items'}
        <table class="editing-table">
            <thead>
            <tr>
                <th>ID</th>
                <th>Название</th>
                <th>Номер машины</th>
                <th>Пробег</th>
                <th>Стоимость ремонта</th>
                <th>Обкатка</th>
                <th>Действия</th>
            </tr>
            </thead>
            <tbody>
            {#each items as item}
                <tr>
                    <td class="fixed-width">{item.id}</td>
                    <td class="fixed-width">
                        {#if item.isEditing}
                            <input class="edit-input" type="text" bind:value={item.name} />
                        {:else}
                            {item.name}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if item.isEditing}
                            <input class="edit-input" type="text" bind:value={item.carNumber} />
                        {:else}
                            {item.carNumber}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if item.isEditing}
                            <input class="edit-input" type="number" bind:value={item.mileage} />
                        {:else}
                            {item.mileage}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if item.isEditing}
                            <input class="edit-input" type="number" bind:value={item.repairCost} />
                        {:else}
                            {item.repairCost}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if item.isEditing}
                            <input class="edit-input" type="text" bind:value={item.runIn} />
                        {:else}
                            {item.runIn}
                        {/if}
                    </td>
                    <td class="action-cell">
                        <div class="action-buttons">
                            {#if item.isEditing}
                                <button class="btn btn-confirm" on:click={() => confirmEdit(item.id)}>✔️</button>
                                <button class="btn btn-cancel" on:click={() => cancelEdit(item.id)}>❌</button>
                                <button class="btn btn-delete" on:click={() => openDeleteModal(item.id)}>🗑️</button>
                            {:else}
                                <button class="btn btn-edit" on:click={() => editItem(item.id)}>✏️</button>
                            {/if}
                        </div>
                    </td>
                </tr>
            {/each}
            </tbody>
        </table>
    {/if}
    {#if selectedCategory === 'fleets'}
        <table class="editing-table">
            <thead>
            <tr>
                <th>ID</th>
                <th>Название</th>
                <th>Количество автомобилей</th>
                <th>Расположение</th>
                <th>Действия</th>
            </tr>
            </thead>
            <tbody>
            {#each fleets as fleet}
                <tr>
                    <td class="fixed-width">{fleet.id}</td>
                    <td class="fixed-width">
                        {#if fleet.isEditing}
                            <input class="edit-input" type="text" bind:value={fleet.name} />
                        {:else}
                            {fleet.name}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if fleet.isEditing}
                            <input class="edit-input" type="number" bind:value={fleet.vehicleCount} />
                        {:else}
                            {fleet.vehicleCount}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if fleet.isEditing}
                            <input class="edit-input" type="text" bind:value={fleet.location} />
                        {:else}
                            {fleet.location}
                        {/if}
                    </td>
                    <td class="action-cell">
                        <div class="action-buttons">
                            {#if fleet.isEditing}
                                <button class="btn btn-confirm" on:click={() => confirmEdit(fleet.id)}>✔️</button>
                                <button class="btn btn-cancel" on:click={() => cancelEdit(fleet.id)}>❌</button>
                                <button class="btn btn-delete" on:click={() => openDeleteModal(fleet.id)}>🗑️</button>
                            {:else}
                                <button class="btn btn-edit" on:click={() => editItem(fleet.id)}>✏️</button>
                            {/if}
                        </div>
                    </td>
                </tr>
            {/each}
            </tbody>
        </table>
    {/if}

    {#if selectedCategory === 'drivers'}
        <table class="editing-table">
            <thead>
            <tr>
                <th>ID</th>
                <th>Имя</th>
                <th>Возраст</th>
                <th>Номер лицензии</th>
                <th>Назначенный автомобиль</th>
                <th>Действия</th>
            </tr>
            </thead>
            <tbody>
            {#each drivers as driver}
                <tr>
                    <td class="fixed-width">{driver.id}</td>
                    <td class="fixed-width">
                        {#if driver.isEditing}
                            <input class="edit-input" type="text" bind:value={driver.name} />
                        {:else}
                            {driver.name}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if driver.isEditing}
                            <input class="edit-input" type="number" bind:value={driver.age} />
                        {:else}
                            {driver.age}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if driver.isEditing}
                            <input class="edit-input" type="text" bind:value={driver.licenseNumber} />
                        {:else}
                            {driver.licenseNumber}
                        {/if}
                    </td>
                    <td class="fixed-width">
                        {#if driver.isEditing}
                            <input class="edit-input" type="text" bind:value={driver.assignedCar} />
                        {:else}
                            {driver.assignedCar}
                        {/if}
                    </td>
                    <td class="action-cell">
                        <div class="action-buttons">
                            {#if driver.isEditing}
                                <button class="btn btn-confirm" on:click={() => confirmEdit(driver.id)}>✔️</button>
                                <button class="btn btn-cancel" on:click={() => cancelEdit(driver.id)}>❌</button>
                                <button class="btn btn-delete" on:click={() => openDeleteModal(driver.id)}>🗑️</button>
                            {:else}
                                <button class="btn btn-edit" on:click={() => editItem(driver.id)}>✏️</button>
                            {/if}
                        </div>
                    </td>
                </tr>
            {/each}
            </tbody>
        </table>
    {/if}
</div>

{#if showDeleteModal}
    <div class="modal-backdrop" on:click={closeDeleteModal}>
        <div class="modal" on:click|stopPropagation>
            <h3>Вы уверены, что хотите удалить этот элемент?</h3>
            <div class="modal-buttons">
                <button class="btn btn-modal-confirm" on:click={deleteItem}>Да, удалить</button>
                <button class="btn btn-modal-cancel" on:click={closeDeleteModal}>Отменить</button>
            </div>

        </div>
    </div>
{/if}

<style>
    .editing-form-container {
        max-width: 1000px;
        margin: 50px auto;
        padding: 20px;
        background-color: #2c2c2c;
        border-radius: 8px;
        box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.5);
        color: #fff;
    }

    .editing-form-title {
        text-align: center;
        font-size: 24px;
        margin-bottom: 20px;
    }

    .category-menu {
        display: flex;
        justify-content: center;
        gap: 10px;
        margin-bottom: 20px;
    }

    .category-button {
        background-color: #007bff;
        color: #fff;
        padding: 10px 20px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
    }

    .editing-table {
        width: 100%;
        border-collapse: collapse;
    }

    .editing-table th,
    .editing-table td {
        border: 1px solid #555;
        padding: 12px;
        text-align: center;
    }

    .fixed-width {
        width: 150px;
    }

    .edit-input {
        width: 100%;
        padding: 8px;
        background-color: #3b3b3b;
        border: 1px solid #555;
        color: #fff;
        border-radius: 4px;
    }

    .action-cell {
        padding: 8px;                  /* Уменьшаем отступы для компактности */
        white-space: nowrap;           /* Предотвращаем перенос кнопок */
        text-align: center;            /* Центрируем содержимое ячейки */
    }

    .action-buttons {
        display: flex;
        justify-content: center;       /* Центрирование кнопок по горизонтали */
        align-items: center;           /* Центрирование кнопок по вертикали */
        gap: 8px;                      /* Устанавливаем промежуток между кнопками */
    }

    .btn {
        padding: 4px 6px;              /* Уменьшаем внутренние отступы кнопок */
        min-width: 32px;               /* Минимальная ширина кнопки */
        height: 32px;                  /* Фиксированная высота кнопки */
        display: flex;
        justify-content: center;
        align-items: center;
        font-size: 18px;               /* Размер иконок/текста */
        border: none;                  /* Убираем границы */
        border-radius: 4px;            /* Скруглённые углы */
        cursor: pointer;
        color: #fff;
    }

    .btn:hover {
        opacity: 0.8;                  /* Эффект затемнения при наведении */
    }
    .btn-confirm { background-color: #28a745; }
    .btn-cancel  { background-color: #dc3545; }
    .btn-delete  { background-color: #6c757d; }
    .btn-edit    { background-color: #ffc107; }

    .modal-backdrop {
        position: fixed;
        top: 0; left: 0; width: 100%; height: 100%;
        background: rgba(0, 0, 0, 0.7);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        background-color: #2c2c2c;
        padding: 30px;
        border-radius: 8px;
        text-align: center;
    }

    .modal-buttons {
        display: flex;
        justify-content: center;       /* Центрирование кнопок по горизонтали */
        gap: 15px;                     /* Промежуток между кнопками */
        margin-top: 20px;              /* Отступ сверху для разделения от текста */
    }

    .btn-modal-confirm {
        background-color: #28a745;     /* Зелёный цвет для подтверждения */
        padding: 10px 20px;
        font-size: 16px;
        border: none;
        border-radius: 4px;
        color: #fff;
        cursor: pointer;
        transition: background-color 0.2s;
    }

    .btn-modal-confirm:hover {
        background-color: #218838;     /* Тёмно-зелёный цвет при наведении */
    }

    .btn-modal-cancel {
        background-color: #dc3545;     /* Красный цвет для отмены */
        padding: 10px 20px;
        font-size: 16px;
        border: none;
        border-radius: 4px;
        color: #fff;
        cursor: pointer;
        transition: background-color 0.2s;
    }

    .btn-modal-cancel:hover {
        background-color: #c82333;     /* Тёмно-красный цвет при наведении */
    }
</style>
