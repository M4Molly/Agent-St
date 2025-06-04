# Agent-St<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>M4Molly Footwear Catalog</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      max-width: 480px;
      margin: 20px auto;
      padding: 20px;
      background: #f5f5f5;
      border-radius: 10px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    h1 {
      text-align: center;
      color: #222;
    }
    ul {
      list-style: none;
      padding: 0;
      margin: 15px 0;
    }
    li {
      background: #fff;
      margin-bottom: 10px;
      padding: 12px 15px;
      border-radius: 6px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border: 1px solid #ddd;
    }
    label {
      flex: 1;
      font-size: 16px;
      color: #333;
      cursor: pointer;
    }
    input[type="number"] {
      width: 60px;
      padding: 6px;
      border-radius: 5px;
      border: 1px solid #ccc;
      font-size: 14px;
      margin-left: 10px;
    }
    .add-shoe {
      display: flex;
      margin-top: 20px;
      margin-bottom: 20px;
    }
    .add-shoe input[type="text"] {
      flex: 1;
      padding: 8px;
      border-radius: 5px 0 0 5px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    .add-shoe button {
      padding: 8px 15px;
      border: none;
      background-color: #007bff;
      color: white;
      font-size: 16px;
      border-radius: 0 5px 5px 0;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    .add-shoe button:hover {
      background-color: #0056b3;
    }
    button#send-order {
      width: 100%;
      background-color: #25d366;
      color: white;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      padding: 12px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    button#send-order:hover {
      background-color: #128c36;
    }
    .note {
      font-size: 14px;
      color: #555;
      margin-top: 10px;
      text-align: center;
    }
  </style>
</head>
<body>
  <h1>M4Molly Footwear Catalog</h1>

  <ul id="shoe-list">
    <li>
      <label>
        <input type="checkbox" value="Sneakers" />
        Sneakers
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Loafers" />
        Loafers
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Boots" />
        Boots
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Sandals" />
        Sandals
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Oxfords" />
        Oxfords
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Heels" />
        Heels
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Flats" />
        Flats
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Athletic Shoes" />
        Athletic Shoes
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Slip-Ons" />
        Slip-Ons
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
    <li>
      <label>
        <input type="checkbox" value="Moccasins" />
        Moccasins
      </label>
      <input type="number" min="1" placeholder="Qty" disabled />
    </li>
  </ul>

  <div class="add-shoe">
    <input type="text" id="new-shoe" placeholder="Add your shoe type..." />
    <button onclick="addShoe()">Add</button>
  </div>

  <button id="send-order">Send Order on WhatsApp</button>

  <p class="note">* Select shoes and enter quantity before sending your order.</p>

  <script>
    const shoeList = document.getElementById('shoe-list');

    // Enable quantity input only if checkbox is checked
    shoeList.addEventListener('change', function(e) {
      if (e.target.tagName === 'INPUT' && e.target.type === 'checkbox') {
        const qtyInput = e.target.closest('li').querySelector('input[type="number"]');
        qtyInput.disabled = !e.target.checked;
        if (!e.target.checked) qtyInput.value = '';
      }
    });

    // Add new shoe type
    function addShoe() {
      const input = document.getElementById('new-shoe');
      const value = input.value.trim();
      if (value === '') {
        alert('Please enter a shoe type.');
        return;
      }
      // Check if shoe type already exists
      const existing = [...shoeList.querySelectorAll('input[type="checkbox"]')].some(cb => cb.value.toLowerCase() === value.toLowerCase());
      if (existing) {
        alert('This shoe type already exists.');
        input.value = '';
        return;
      }

      const li = document.createElement('li');

      li.innerHTML = `
        <label>
          <input type="checkbox" value="${value}" />
          ${value}
        </label>
        <input type="number" min="1" placeholder="Qty" disabled />
      `;

      shoeList.appendChild(li);
      input.value = '';
    }

    // Send order via WhatsApp
    document.getElementById('send-order').addEventListener('click', () => {
      const phoneNumber = '+2348160717897';  // Your WhatsApp number in international format
      const selectedShoes = [];

      shoeList.querySelectorAll('li').forEach(li => {
        const checkbox = li.querySelector('input[type="checkbox"]');
        const qtyInput = li.querySelector('input[type="number"]');
        if (checkbox.checked && qtyInput.value && parseInt(qtyInput.value) > 0) {
          selectedShoes.push(`${checkbox.value} (Qty: ${qtyInput.value})`);
        }
      });

      if (selectedShoes.length === 0) {
        alert('Please select at least one shoe type and enter quantity.');
        return;
      }

      const message = encodeURIComponent(
        `Hello M4Molly,\nI would like to order the following shoes:\n- ${selectedShoes.join('\n- ')}\n\nPlease provide pricing and more details.`
      );

      const whatsappUrl = `https://wa.me/${phoneNumber.replace(/\D/g, '')}?text=${message}`;

      window.open(whatsappUrl, '_blank');
    });
  </script>
</body>
</html>
