<script>
(function () {

  function calculateTotal(rows) {
    let total = 0;
    rows.forEach(r => total += Number(r.children[2].textContent));
    return total;
  }

  function updateTable() {
    const filter = document.getElementById("statusFilter").value;
    const rows = Array.from(document.querySelectorAll("#npcTable tbody tr"));

    let visibleRows = [];

    rows.forEach(row => {
      const status = row.children[4].textContent;

      if (!filter || status === filter) {
        row.style.display = "";
        visibleRows.push(row);
      } else {
        row.style.display = "none";
      }
    });

    document.getElementById("totalCost").textContent =
      "Total Cost: " + calculateTotal(visibleRows);
  }

  document.getElementById("statusFilter").addEventListener("change", updateTable);

  updateTable();

})();
</script>
