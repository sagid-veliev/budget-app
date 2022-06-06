 <template>
  <div id="app">
    <h1>BudgetList</h1>
    <Form @submitForm="onFormSubmit"/>
    <budget-list :list='list' @deleteItem='onDeleteItem'/>
    <total-balance :total='totalBalance'/>
  </div>
</template>

<script>

import BudgetList from '@/components/BudgetList';
import TotalBalance from '@/components/TotalBalance';
import Form from '@/components/Form'
export default {
  name: 'app',
  components: {
    BudgetList,
    TotalBalance,
    Form
  },
  data: () => ({
    list: {
      1: {
        id: 1,
        type: 'INCOME',
        value: 100,
        comment: 'Some comment'
      },
      2: {
        id: 2,
        type: 'OUTCOME',
        value: -50,
        comment: 'Some outcome comment'
      }
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        0
      );
    }
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.$set(this.list, newObj.id, newObj);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
