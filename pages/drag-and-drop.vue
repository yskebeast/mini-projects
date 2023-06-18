<template>
  <fs-project-container title="drag and drop">
    <div class="drag-and-drop">
      <div class="main">
        <div>
          <input type="text" v-model="message" />
          <button @click="addItem">ADD</button>
        </div>
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>NAME</th>
              <th>ORDER</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="(item, i) in list" :key="i" draggable @dragstart="dragList($event, i)" @drop.stop="dropList($event, i)" @dragover.prevent @dragenter.prevent>
              <td>{{ item.id }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.order }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </fs-project-container>
</template>

<script>
export default {
  name: "drag-and-drop",
  data() {
    return {
      message: "",
      list: [
        {
          id: 1,
          name: "ProductA",
          order: 1,
        },
        {
          id: 2,
          name: "ProductB",
          order: 2,
        },
        {
          id: 3,
          name: "ProductC",
          order: 3,
        },
        {
          id: 4,
          name: "ProductD",
          order: 4,
        },
        {
          id: 5,
          name: "ProductE",
          order: 5,
        },
      ],
    };
  },
  methods: {
    addItem() {
      const item = {
        id: this.list.length,
        name: this.message,
        order: this.list.length,
      };
      this.list.push(item);
    },

    dragList(event, dragIndex) {
      console.log("drag", { event, dragIndex });
      event.dataTransfer.effectAllowed = "move";
      event.dataTransfer.dropEffect = "move";
      event.dataTransfer.setData("drag-index", dragIndex);
    },

    dropList(event, dropIndex) {
      console.log("drop", { event, dropIndex });
      const dragIndex = event.dataTransfer.getData("drag-index");
      const deleteList = this.list.splice(dragIndex, 1);
      this.list.splice(dropIndex, 0, deleteList[0]);
      this.list.map((list, index) => {
        list.order = index + 1;
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.drag-and-drop {
  margin: 0 auto;
  padding: 3rem 0;
  height: 100vh;
  background-color: #ececec;
}

.main {
  width: 800px;
  margin: 0 auto;
}

table {
  width: 100%;
}
thead {
  background-color: #000;
  color: #fff;
}

th,
td {
  padding: 1rem;
  cursor: pointer;
}

tr {
  &:hover {
    outline: 1px solid red;
  }
}

tbody {
  tr:nth-child(odd) {
    background-color: gray;
  }
  tr:nth-child(even) {
    background-color: #fff;
  }
}
</style>
