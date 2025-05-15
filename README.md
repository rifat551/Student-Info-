# Student-Info-
<!DOCTYPE html>
<html lang="bn">
<head>
  <meta charset="UTF-8" />
  <title>স্টুডেন্ট ফর্ম</title>
  <style>
    body { font-family: sans-serif; max-width: 600px; margin: auto; padding: 20px; }
    input, button { padding: 10px; margin: 5px 0; width: 100%; }
    table { border-collapse: collapse; width: 100%; margin-top: 20px; }
    th, td { border: 1px solid #000; padding: 8px; text-align: left; }
  </style>
</head>
<body>
  <h2>তথ্য দিন</h2>
  <form id="form">
    <input type="text" id="name" placeholder="নাম" required />
    <input type="text" id="roll" placeholder="রোল নম্বর" required />
    <input type="text" id="mobile" placeholder="মোবাইল নম্বর" required />
    <button type="submit">সাবমিট</button>
  </form>

  <h3>তালিকা</h3>
  <table id="dataTable">
    <thead>
      <tr><th>নাম</th><th>রোল</th><th>মোবাইল</th></tr>
    </thead>
    <tbody></tbody>
  </table>

  <script>
    const form = document.getElementById('form');
    const tbody = document.querySelector('#dataTable tbody');

    form.addEventListener('submit', function(e) {
      e.preventDefault();

      const name = document.getElementById('name').value.trim();
      const roll = document.getElementById('roll').value.trim();
      const mobile = document.getElementById('mobile').value.trim();

      if (!name || !roll || !mobile) return alert("সব ফিল্ড পূরণ করুন");

      const row = document.createElement('tr');
      row.innerHTML = `<td>${name}</td><td>${roll}</td><td>${mobile}</td>`;
      tbody.appendChild(row);

      // LocalStorage-এ সেভ
      const data = JSON.parse(localStorage.getItem('students') || '[]');
      data.push({ name, roll, mobile });
      localStorage.setItem('students', JSON.stringify(data));

      form.reset();
    });

    // পেজ লোডে পুরাতন ডেটা দেখাও
    window.onload = function () {
      const data = JSON.parse(localStorage.getItem('students') || '[]');
      data.forEach(({ name, roll, mobile }) => {
        const row = document.createElement('tr');
        row.innerHTML = `<td>${name}</td><td>${roll}</td><td>${mobile}</td>`;
        tbody.appendChild(row);
      });
    };
  </script>
</body>
</html>
