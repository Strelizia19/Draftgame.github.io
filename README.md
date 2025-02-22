
<html lang="en">
 <head>
  <meta charset="utf-8"/>
  <meta content="width=device-width, initial-scale=1.0" name="viewport"/>
  <title>
   Draft Game
  </title>
  <script src="https://cdn.tailwindcss.com">
  </script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css" rel="stylesheet"/>
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&amp;display=swap" rel="stylesheet"/>
 </head>
 <body class="bg-gray-100 font-roboto">
  <div class="container mx-auto p-4">
   <div class="bg-white shadow-md rounded-lg p-6">
    <div class="flex justify-between items-center mb-4">
     <div>
      <h1 class="text-2xl font-bold">
       Draft Game
      </h1>
      <p class="text-gray-600">
       Balance:
       <span id="tokenBalance">
        0
       </span>
       Draft Tokens
      </p>
      <p class="text-gray-600">
       Toncoin:
       <span id="toncoinBalance">
        0
       </span>
       TON
      </p>
     </div>
     <div>
      <button class="bg-blue-500 text-white px-4 py-2 rounded" onclick="withdraw()">
       Withdraw
      </button>
      <button class="bg-green-500 text-white px-4 py-2 rounded" onclick="exchange()">
       Exchange
      </button>
     </div>
    </div>
    <div class="bg-yellow-100 p-4 rounded-lg mb-4">
     <img alt="A blank note background" class="w-full h-64 object-cover rounded-lg" height="400" src="https://storage.googleapis.com/a1aa/image/4ojebn5JNm1xgejp0O01SzZzVhBAidXOHjvYkPxh2eU.jpg" width="600"/>
     <div class="flex justify-center mt-4">
      <img alt="A circular note icon" class="w-24 h-24 object-cover rounded-full cursor-pointer" height="100" onclick="tap()" src="https://storage.googleapis.com/a1aa/image/Gn3EQxJRKCsChuRVXmVsBbfb72upvKVM1_Pww4a1c6A.jpg" width="100"/>
     </div>
     <p class="text-center mt-2">
      Energy:
      <span id="energy">
       2000
      </span>
      /2000
     </p>
    </div>
    <div class="bg-gray-200 p-4 rounded-lg">
     <h2 class="text-xl font-bold mb-2">
      Upgrades
     </h2>
     <div class="flex justify-between items-center mb-2">
      <div>
       <p class="font-bold">
        Level 1
       </p>
       <p>
        Cost: 1 TON
       </p>
       <p>
        5 Tokens per tap, Max 5000 Energy
       </p>
      </div>
      <a class="bg-blue-500 text-white px-4 py-2 rounded" href="ton://transfer/UQDPgfaLpilFaLmOejMbqFuKAPmzxWdqEhWjYmuBofNZnS23?amount=1000000000">
       Purchase
      </a>
     </div>
     <div class="flex justify-between items-center">
      <div>
       <p class="font-bold">
        Level 2
       </p>
       <p>
        Cost: 3 TON
       </p>
       <p>
        30 Tokens per tap, Max 10000 Energy
       </p>
      </div>
      <a class="bg-blue-500 text-white px-4 py-2 rounded" href="ton://transfer/UQDPgfaLpilFaLmOejMbqFuKAPmzxWdqEhWjYmuBofNZnS23?amount=3000000000">
       Purchase
      </a>
     </div>
    </div>
    <div class="bg-gray-200 p-4 rounded-lg mt-4">
     <h2 class="text-xl font-bold mb-2">
      History
     </h2>
     <ul class="list-disc pl-5" id="history">
      <!-- History items will be appended here -->
     </ul>
    </div>
   </div>
  </div>
  <script>
   let tokenBalance = 0;
        let toncoinBalance = 0;
        let energy = 2000;
        const maxEnergy = 2000;
        const energyRegenRate = 30; // seconds

        function tap() {
            if (energy > 0) {
                tokenBalance += 1;
                energy -= 1;
                document.getElementById('tokenBalance').innerText = tokenBalance;
                document.getElementById('energy').innerText = energy;
            } else {
                alert('Not enough energy!');
            }
        }

        function withdraw() {
            const address = prompt('Enter your Toncoin address:');
            const amount = prompt('Enter the amount to withdraw:');
            if (address && amount) {
                // Add to history
                const historyItem = document.createElement('li');
                historyItem.innerText = `Withdrawn ${amount} TON to ${address}`;
                document.getElementById('history').appendChild(historyItem);
            }
        }

        function exchange() {
            const amount = prompt('Enter the amount of Draft Tokens to exchange:');
            if (amount && amount <= tokenBalance) {
                const tonAmount = amount * 0.00001;
                tokenBalance -= amount;
                toncoinBalance += tonAmount;
                document.getElementById('tokenBalance').innerText = tokenBalance;
                document.getElementById('toncoinBalance').innerText = toncoinBalance;

                // Add to history
                const historyItem = document.createElement('li');
                historyItem.innerText = `Exchanged ${amount} Draft Tokens for ${tonAmount} TON`;
                document.getElementById('history').appendChild(historyItem);
            } else {
                alert('Not enough Draft Tokens!');
            }
        }

        setInterval(() => {
            if (energy < maxEnergy) {
                energy +
= 1;
                document.getElementById('energy').innerText = energy;
            }
        }, energyRegenRate * 1000);
  </script>
 </body>
</html>
