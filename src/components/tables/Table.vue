<script>
  import data from '@/data.json'
  import Status from "@/components/ui/status/Status.vue";
  import Search from "@/components/ui/inputs/Search.vue";
  import Button from "@/components/ui/bttons/Button.vue";

export default {
  props: {
    search: {
      type: String,
    }
  },
  components: { Status, Search, Button },
  data() {
    return {
      data,
      pageSize: 10,
      currentPage: 1,
      sortColumn: null, 
      sortDirection: 'asc', 
    };
  },
  computed: {
    paginatedData() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;

      // Применение сортировки к данным
      const sortedData = this.sortData(this.data.sessions);

      return sortedData.filter(session =>
        session.module.toLowerCase().includes(this.search.toLowerCase())
      ).slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.data.sessions.length / this.pageSize);
    }
  },
  methods: {
    changePage(page) {
      if (page >= 1 && page <= this.totalPages) {
        this.currentPage = page;
      }
    },
    setPage(page) {
      this.currentPage = page;
    },
    shouldShowEllipsis(index) {
      return (index === 1 && this.currentPage > 3) ||
        (index === this.totalPages - 2 && this.currentPage < this.totalPages - 2);
    },
    sessionSwitch(props) {
      switch (props.name) {
        case "accreditation":
          return "Аккредитация"
        case "lesson":
          return "Урок"
        case "examination":
          return "Экзамен"
        default: return "Пара"
      }
    },
    returnRooms(props) {
      let result = "";
      for (let item of props) {
        if (item.name.includes("Комната")) result += item.name + " ";
        else result += "Комната " + item.name + " ";
      }
      return result
    },
    returnGroup(props) {
      let result = "";
      for (let item of props) {
        result += item.name + " "
      }
      return result;
    },
    returnTimes(start, end) {
      let r_start = new Date(start);
      let r_end = new Date(end);

      return r_start.toLocaleString("ru-RU", {
        year: 'numeric',
        month: '2-digit',
        day: '2-digit',
        hour: '2-digit',
        minute: '2-digit',
      }) + "-" + r_end.toLocaleTimeString("ru-RU", { hour: "2-digit", minute: "2-digit" });
    },
    sortData(data) {
      if (this.sortColumn === null) return data;

      return data.sort((a, b) => {
        const aValue = a[this.sortColumn];
        const bValue = b[this.sortColumn];

        if (aValue < bValue) return this.sortDirection === 'asc' ? -1 : 1;
        if (aValue > bValue) return this.sortDirection === 'asc' ? 1 : -1;
        return 0;
      });
    },
    sortBy(column) {
      if (this.sortColumn === column) {
        this.sortDirection = this.sortDirection === 'asc' ? 'desc' : 'asc';
      } else {
        this.sortColumn = column;
        this.sortDirection = 'asc';
      }
    }
  }
};
</script>

<template>
  <div>
    <div :class="$style['table-wrapper']">
      <table>
        <thead :class="$style['table_head']">
          <tr>
            <th @click="sortBy('start')"> Дата и время</th>
            <th @click="sortBy('status.name')">Статус</th>
            <th @click="sortBy('module')">Название учебного модуля</th>
            <th @click="sortBy('type')">Тип сессии</th>
            <th @click="sortBy('rooms')">Комната</th>
            <th @click="sortBy('groups')">Группа</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item) in paginatedData" :key="item.id">
            <td style="min-width: 15rem">{{ returnTimes(item.start, item.end) }}</td>
            <td>
              <Status :type="item.status.name" />
            </td>
            <td>{{ item.module }}</td>
            <td>{{ sessionSwitch(item.type) }}</td>
            <td>{{ returnRooms(item.rooms) }}</td>
            <td>{{ returnGroup(item.groups) }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div :class="$style['pagination']">
      <Button type="outlet" @click="changePage(currentPage - 1)" :disabled="currentPage === 1" text="<"></Button>
      <span v-for="(item, index) in paginatedData">
        <Button
          v-show="(index + 1 >= currentPage - 1) && (index + 1 <= currentPage + 1) || (index === 0) || (index === totalPages - 1)"
          :type="(index + 1) === currentPage ? 'foreground' : 'outlet'"
          :isActive="(index + 1) === currentPage"
          @click="setPage(index + 1)" :text="index + 1"></Button>
        <span v-if="shouldShowEllipsis(index)">...</span>
      </span>
      <Button type="outlet" @click="changePage(currentPage + 1)" :disabled="currentPage === totalPages" text=">"></Button>
    </div>
  </div>
</template>



<style module>


.active {
  font-weight: bold;
  opacity: 0.7;; 
}

.unnacti::after {
  content: '↑'; 
}

.desc::after {
  content: '↓'; 
}


.pagination{
  display: flex;
  justify-content: start;
  align-items: center;
  max-height: 30px;
  margin-top: 1rem;
}

.disable{
  pointer-events: none;
  user-select: none;
  cursor: not-allowed;
}

.table_head{
  font-weight: bold;
  font-size: var(--text-lg);
  background-color: #F5F7F9;
}

.table-wrapper {
  min-height: 80vh;
  max-height: 80vh;
  border-radius: var(--rounded-md);  /* Округляем углы обертки */
  overflow-y: scroll;     /* Убираем переполнение, чтобы углы не срезались */
}

.table-wrapper::-webkit-scrollbar {
  width: 5px;
}

.table-wrapper::-webkit-scrollbar-track {
  border-radius: 8px;
  background-color: #e7e7e7;
  /* border: 1px solid #cacaca; */
}

.table-wrapper::-webkit-scrollbar-thumb {
  border-radius: 8px;
  /* border: 3px solid transparent; */
  background-clip: content-box;
  background-color: rgba(196, 196, 196, 0.35);
}


table {
  width: 100%;
}
tr:nth-child(even){
  background-color: #F5F7F9;

}

th, td {
  padding: 10px;
  border: 1px solid #ddd;
}


.pagination {
  margin-top: 10px;
  text-align: center;
}

button {
  padding: 5px 15px;
  margin: 0 10px;
  cursor: pointer;
}

button:disabled {
  cursor: not-allowed;
  opacity: 0.5;
}

</style>
