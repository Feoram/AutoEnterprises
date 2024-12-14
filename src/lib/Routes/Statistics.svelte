<script>
    import { onMount } from "svelte";
    import { Chart, registerables } from "chart.js";

    Chart.register(...registerables);

    let charts = [];

    // Данные для заглушек
    let fleetData = "Всего автомобилей: 50";
    let driversData = "Водителей: 35";
    let driverDistribution = [15, 10, 5, 20];
    let routesData = "Маршруты: 10";
    let mileageData = "Пробег за месяц: 12000 км";
    let repairData = "Ремонты: 8, Общая стоимость: 50000 руб.";

    onMount(() => {
        // График распределения водителей по автомобилям
        createChart("driversChart", {
            type: "bar",
            data: {
                labels: ["Автомобиль 1", "Автомобиль 2", "Автомобиль 3", "Автомобиль 4"],
                datasets: [
                    {
                        label: "Количество водителей",
                        data: driverDistribution,
                        backgroundColor: "#007BFF",
                    },
                ],
            },
        });

        // График распределения пассажирского автотранспорта по маршрутам
        createChart("routesChart", {
            type: "pie",
            data: {
                labels: ["Маршрут 1", "Маршрут 2", "Маршрут 3", "Маршрут 4"],
                datasets: [
                    {
                        label: "Автотранспорт",
                        data: [10, 20, 30, 40],
                        backgroundColor: ["#007BFF", "#28a745", "#ffc107", "#dc3545"],
                    },
                ],
            },
        });
    });

    // Функция для создания графика
    function createChart(id, config) {
        const ctx = document.getElementById(id).getContext("2d");
        const chart = new Chart(ctx, config);
        charts.push(chart);
    }
</script>

<div class="statistics-container">
    <h2 class="statistics-title">Статистика автопарка</h2>

    <div class="cards-container">
        <div class="stat-card">
            <h3>Данные об автопарке</h3>
            <p>{fleetData}</p>
        </div>
        <div class="stat-card">
            <h3>Перечень водителей</h3>
            <p>{driversData}</p>
        </div>
        <div class="stat-card">
            <h3>Данные о пробеге</h3>
            <p>{mileageData}</p>
        </div>
        <div class="stat-card">
            <h3>Данные о ремонтах</h3>
            <p>{repairData}</p>
        </div>
    </div>

    <div class="charts-container">
        <div class="chart-section">
            <h3>Распределение водителей по автомобилям</h3>
            <canvas id="driversChart" width="400" height="200"></canvas>
        </div>

        <div class="chart-section">
            <h3>Распределение пассажирского автотранспорта по маршрутам</h3>
            <canvas id="routesChart" width="400" height="200"></canvas>
        </div>
    </div>
</div>

<style>
    .statistics-container {
        max-width: 1200px;
        margin: 50px auto;
        padding: 20px;
        background-color: #2c2c2c;
        border-radius: 8px;
        box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.5);
        color: #fff;
        font-family: Arial, sans-serif;
    }

    .statistics-title {
        text-align: center;
        margin-bottom: 20px;
        font-size: 28px;
    }

    .cards-container {
        display: flex;
        flex-wrap: wrap;
        gap: 20px;
        justify-content: space-around;
        margin-bottom: 40px;
    }

    .stat-card {
        background-color: #3b3b3b;
        border: 1px solid #555;
        padding: 20px;
        border-radius: 8px;
        width: 250px;
        text-align: center;
        box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.3);
    }

    .stat-card h3 {
        margin-bottom: 10px;
        color: #007BFF;
    }

    .charts-container {
        display: flex;
        flex-direction: column;
        gap: 40px;
    }

    .chart-section {
        background-color: #3b3b3b;
        padding: 20px;
        border-radius: 8px;
        border: 1px solid #555;
        box-shadow: 0px 5px 10px rgba(0, 0, 0, 0.3);
        text-align: center;
    }

    .chart-section h3 {
        margin-bottom: 20px;
        color: #ffc107;
    }
</style>
