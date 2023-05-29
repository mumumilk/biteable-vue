<template>
  <table>
    <thead>
      <tr>
        <th>State/Territory</th>
        <th>Capital</th>
        <th>Population</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Australian Capital Territory</td>
        <td>Canberra</td>
        <td>395,200</td>
      </tr>
      <tr>
        <td>New South Wales</td>
        <td>Sydney</td>
        <td>7,704,300</td>
      </tr>
      <tr>
        <td>Northern Territory</td>
        <td>Darwin</td>
        <td>244,000</td>
      </tr>
      <tr>
        <td>Queensland</td>
        <td>Brisbane</td>
        <td>4,827,000</td>
      </tr>
      <tr>
        <td>South Australia</td>
        <td>Adeld</td>
        <td>1,706,500</td>
      </tr>
      <tr>
        <td>Tasmania</td>
        <td>Hobart</td>
        <td>518,500</td>
      </tr>
      <tr>
        <td>Victoria</td>
        <td>Melbourne</td>
        <td>6,039,100</td>
      </tr>
      <tr>
        <td>Western Australia</td>
        <td colspan="2">No data</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td>Total</td>
        <td></td>
        <td>24,048,300</td>
      </tr>
    </tfoot>
  </table>
</template>

<style scoped>
  table {
    width: 100%;
    background-color: var(--color-gray-100);
    border-spacing: 0 2px;
    padding: 0 2px;
    border-radius: 2px;
  }

  thead {
    background-color: var(--color-gray-100);
  }

  td,
  th {
    padding: 1rem;
  }

  td:first-child,
  th:first-child {
    text-align: left;
  }

  td:not(:first-child, :last-child),
  th:not(:first-child, :last-child) {
    text-align: center;
  }

  td:last-child,
  th:last-child {
    text-align: right;
  }

  tbody tr {
    background-color: var(--color-white);
    border: 2px solid transparent;
    border-radius: var(--border-radius);
    transition: box-shadow 0.15s;
  }

  tbody tr:hover {
    box-shadow: 0 0 0 0 var(--color-white) inset, var(--color-primary) 0 0 0 2px;
  }

  tbody td:first-child {
    border-top-left-radius: var(--border-radius);
    border-bottom-left-radius: var(--border-radius);
  }

  tbody td:last-child {
    border-top-right-radius: var(--border-radius);
    border-bottom-right-radius: var(--border-radius);
  }
</style>
