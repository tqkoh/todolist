<template>
  <div>
    <div>タスク追加</div>
    <div>
      <label>
        内容
        <input type="text" v-model="newItemName" />
      </label>
      <label>
        期限
        <input type="text" v-model="newItemPrice" />
      </label>
      <button @click="addItem">add</button>
    </div>
    <table border="0">
      <tr>
        <th>内容</th>
        <th>期限</th>
        <th>状態</th>
        <th></th>
        <th></th>
      </tr>
      <tr v-for="item in items" :key="item.name">
        <td>{{ item.name }}</td>
        <td>{{ item.deadline }}</td>
        <td>{{ item.done }}</td>
        <td>
          <button @click="toggleDone(item.id)">{{ item.donejp }}</button>
        </td>
        <td><button @click="erase(item.id)">消去</button></td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "ItemList",
  data() {
    return {
      items: [],
      newItemName: "",
      newItemPrice: "",
      sum: 0,
    };
  },
  methods: {
    addItem() {
      this.items.push({
        name: this.newItemName,
        deadline: this.newItemPrice,
        done: "✔",
        donejp: ":fastparrot:",
        id: this.sum++,
      });
      this.toggleDone(this.sum - 1);
    },
    toggleDone(id) {
      var ct = 0;
      while (ct < this.items.length && this.items[ct].id != id) ++ct;
      var item;
      if (this.items[ct].done == "❌") {
        this.items[ct].done = "✔";
        this.items[ct].donejp = "未完にする";
        item = JSON.parse(JSON.stringify(this.items[ct]));
        this.erase(this.items[ct].id);
        while (ct < this.items.length && this.items[ct].done == "❌") ++ct;
        this.items.splice(ct, 0, item);
      } else {
        this.items[ct].done = "❌";
        this.items[ct].donejp = "完了にする";
        item = JSON.parse(JSON.stringify(this.items[ct]));
        this.erase(this.items[ct].id);
        this.items.unshift(item);
      }
    },
    erase(id) {
      var ct = 0;
      while (ct < this.items.length && this.items[ct].id != id) ++ct;
      this.items.splice(ct, 1);
    },
  },
};
</script>
