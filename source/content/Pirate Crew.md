<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Costs</title>

  <!-- DataTables CSS -->
  <link rel="stylesheet" href="https://cdn.datatables.net/1.13.8/css/jquery.dataTables.min.css">

  <!-- jQuery (required by DataTables) -->
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

  <!-- DataTables JS -->
  <script src="https://cdn.datatables.net/1.13.8/js/jquery.dataTables.min.js"></script>
</head>

<body>

<h2>Crew Members</h2>

<select id="statusFilter">
  <option value="">All</option>
  <option value="Active">Alive</option>
  <option value="Paused">Dead</option>
</select>

<table id="npcTable" class="display">
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Cost (GP)</th>
		<th>Ship</th>
      <th>Status</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Tacht Crest</td>
      <td>Player</td>
      <td>0</td>
      <td>Nyra</td>
      <td>Alive</td>
    </tr>
    <tr>
      <td>Clove</td>
      <td>NPC</td>
      <td>0</td>
      <td>Nyra</td>
      <td>Alive</td>
    </tr>
  </tbody>
</table>

<h3 id="totalCost"></h3>


<script>
$(document).ready(function () {

  let table = $('#npcTable').DataTable({
    paging: false,
    info: false
  });

  function calculateTotal() {
    let total = 0;

    table.column(2, { search: 'applied' }).data().each(function (value) {
      total += Number(value);
    });

    $('#totalCost').text("Total Daily Cost: " + total);
  }

  calculateTotal();

  table.on('search.dt', function () {
    calculateTotal();
  });

  $('#statusFilter').on('change', function () {
    table.column(4).search(this.value).draw();
  });

});
</script>

</body>
</html>
