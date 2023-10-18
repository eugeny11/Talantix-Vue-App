<template>
  <div>
    <label>Город:</label>
    <select v-model="selectedCity" @change="updateDepartment">
      <option v-for="city in cities" :key="city">{{ city }}</option>
    </select>
    
    <label>Цех:</label>
    <select v-model="selectedDepartment" @change="updateEmployee">
      <option v-for="department in departments" :key="department">{{ department }}</option>
    </select>
    
    <label>Сотрудник:</label>
    <select v-model="selectedEmployee">
      <option v-for="employee in employees" :key="employee">{{ employee }}</option>
    </select>

    <label>Смена:</label>
    <select v-model="selectedShift">
      <option v-for="shift in shifts" :key="shift">{{ shift }}</option>
    </select>

    <button @click="saveData">Сохранить</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'ShiftSelector',
  setup() {
    const cities = ref(['Москва', 'Санкт-Петербург', 'Екатеринбург']);
    const shifts = ref(['Первая (8:00 - 20:00)', 'Вторая (20:00 - 8:00)']);
    const cityToDepartments = {
    'Москва': ['Цех1', 'Цех2', 'Цех7'],
    'Санкт-Петербург': ['Цех3', 'Цех4', 'Цех8'],
    'Екатеринбург': ['Цех5', 'Цех6', 'Цех9']
};

const departmentToEmployees = {
  'Цех1': ['Иван', 'Мария'],
  'Цех2': ['Дмитрий', 'Елена'],
  'Цех3': ['Алексей', 'Светлана'],
  'Цех4': ['Владимир', 'Ольга'],
  'Цех5': ['Михаил', 'Анна'],
  'Цех6': ['Сергей', 'Татьяна'],
  'Цех7': ['Антон', 'Наталия'],
  'Цех8': ['Павел', 'Ирина'],
  'Цех9': ['Георгий', 'Дарья']
};

    const selectedCity = ref(cities.value[0]);
    const selectedDepartment = ref(cityToDepartments[selectedCity.value][0]);
    const selectedEmployee = ref(departmentToEmployees[selectedDepartment.value][0]);
    const selectedShift = ref(shifts.value[0]);

    const departments = ref(cityToDepartments[selectedCity.value]);
    const employees = ref(departmentToEmployees[selectedDepartment.value]);

    const updateDepartment = () => {
      departments.value = cityToDepartments[selectedCity.value];
      selectedDepartment.value = departments.value[0];
      updateEmployee();
    };

    const updateEmployee = () => {
      employees.value = departmentToEmployees[selectedDepartment.value];
      selectedEmployee.value = employees.value[0];
    };

    const saveData = () => {
      document.cookie = `city=${selectedCity.value}`;
      document.cookie = `department=${selectedDepartment.value}`;
      document.cookie = `employee=${selectedEmployee.value}`;
      document.cookie = `shift=${selectedShift.value}`;
      alert('Данные сохранены!');
    };

    return {
      cities, shifts, selectedCity, selectedDepartment, selectedEmployee, selectedShift,
      departments, employees, updateDepartment, saveData
    };
  }
}
</script>

<style scoped>
div {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 5px;
}

select {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 14px;
}

button {
    align-self: flex-end;
    padding: 10px 20px;
    background-color: #007BFF;
    color: #fff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.2s;
}

button:hover {
    background-color: #0056b3;
}
</style>

