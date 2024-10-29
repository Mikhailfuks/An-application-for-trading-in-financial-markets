<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Торговля акциями</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <h1>Торговля акциями</h1>
        <div id="stockList" class="stock-list"></div>
        <h2>Выбор акции</h2>
        <input type="text" id="stockSymbol" placeholder="Введите тикер акции" />
        <input type="number" id="quantity" placeholder="Количество" />
        <button id="buyButton">Купить</button>
        <button id="sellButton">Продать</button>
        <h2>Ваши транзакции</h2>
        <div id="transactions"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>


body {
    font-family: Arial, sans-serif;
    background-color: #f5f5f5;
    margin: 0;
    padding: 20px;
}

.container {
    max-width: 600px;
    margin: auto;
    padding: 20px;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

h1, h2 {
    text-align: center;
}

.stock-list {
    margin: 20px 0;
}

.stock-item {
    display: flex;
    justify-content: space-between;
    padding: 10px;
    border-bottom: 1px solid #ccc;
}

input {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: calc(50% - 10px);
    margin-right: 10px;
}

button {
    padding: 10px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

.transaction-item {
    margin: 10px 0;
    padding: 10px;
    background: #e8f0fe;
    border-radius: 4px;
}


const stocks = [
    { symbol: 'AAPL', name: 'Apple Inc.', price: 150 },
    { symbol: 'GOOGL', name: 'Alphabet Inc.', price: 2500 },
    { symbol: 'AMZN', name: 'Amazon.com Inc.', price: 3500 },
    { symbol: 'MSFT', name: 'Microsoft Corporation', price: 300 },
    { symbol: 'TSLA', name: 'Tesla Inc.', price: 700 }
];

let transactions = [];

function displayStocks() {
    const stockList = document.getElementById('stockList');
    stockList.innerHTML = '';

    stocks.forEach(stock => {
        const stockElement = document.createElement('div');
        stockElement.className = 'stock-item';
        stockElement.innerHTML = `
            <div>${stock.name} (${stock.symbol}) - $${stock.price}</div>
        `;
        stockList.appendChild(stockElement);
    });
}

function buyStock() {
    const symbol = document.getElementById('stockSymbol').value.toUpperCase();
    const quantity = parseInt(document.getElementById('quantity').value);
    
    const stock = stocks.find(s => s.symbol === symbol);
    
    if (stock && quantity > 0) {
        const totalCost = stock.price * quantity;
        transactions.push(`Куплено ${quantity} акций ${stock.name} по $${stock.price} за акцию. Итого: $${totalCost}.`);
        displayTransactions();



        alert(`Вы купили ${quantity} акций ${stock.name} на сумму $${totalCost}.`);
    } else {
        alert('Некорректный тикер или количество акций.');
    }
}

function sellStock() {
    const symbol = document.getElementById('stockSymbol').value.toUpperCase();
    const quantity = parseInt(document.getElementById('quantity').value);
    
    const stock = stocks.find(s => s.symbol === symbol);
    
    if (stock && quantity > 0) {
        const totalSale = stock.price * quantity;
        transactions.push(`Продано ${quantity} акций ${stock.name} по $${stock.price} за акцию. Итого: $${totalSale}.`);
        displayTransactions();
        alert(`Вы продали ${quantity} акций ${stock.name} на сумму $${totalSale}.`);
    } else {
        alert('Некорректный тикер или количество акций.');
    }
}

function displayTransactions() {
    const transactionsDiv = document.getElementById('transactions');
    transactionsDiv.innerHTML = '';
    
    transactions.forEach(transaction => {
        const transactionItem = document.createElement('div');
        transactionItem.className = 'transaction-item';
        transactionItem.innerText = transaction;
        transactionsDiv.appendChild(transactionItem);
    });
}

document.getElementById('buyButton').addEventListener('click', buyStock);
document.getElementById('sellButton').addEventListener('click', sellStock);

displayStocks();
