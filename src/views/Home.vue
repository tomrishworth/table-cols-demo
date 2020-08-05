<template>
  <div class="home">
    <b-popover target="popover-target-1" placement="bottomleft">
      <draggable v-model="fields" @start="drag = true" @end="drag = false">
        <div class="list-group-item d-flex" v-for="field in fields" :key="field.key">
          <div>
            <b-icon-grip-horizontal style="font-size:20px"></b-icon-grip-horizontal>
            {{ field.label }}
          </div>
          <div class="ml-auto">
            <b-form-checkbox :id="field.key" v-model="field.visible" :name="field.key"></b-form-checkbox>
          </div>
        </div>
      </draggable>
    </b-popover>

    <div class="position-relative">
      <button class="btn settings-btn" id="popover-target-1">
        <b-icon-gear-fill></b-icon-gear-fill>
      </button>
      <b-table table-variant="light" :fields="visibleCols" :items="items"></b-table>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import draggable from "vuedraggable";

export default {
  name: "Home",
  components: {
    draggable,
  },
  data() {
    return {
      fields: [
        {
          key: "first_name",
          label: "First Name",
          visible: true,
        },
        {
          key: "last_name",
          label: "Last Name",
          visible: true,
        },
        {
          key: "role",
          label: "Role",
          visible: true,
        },
        {
          key: "age",
          label: "Age",
          visible: true,
        },
      ],
      items: [
        {
          age: 40,
          first_name: "Dickerson",
          last_name: "Macdonald",
          role: "Manager",
        },
        { age: 21, first_name: "Larsen", last_name: "Shaw", role: "Developer" },
        {
          age: 36,
          first_name: "Geneva",
          last_name: "Wilson",
          role: "Designer",
        },
        { age: 38, first_name: "Jami", last_name: "Carney", role: "Developer" },
      ],
    };
  },
  computed: {
    visibleCols() {
      return this.fields.filter((field) => {
        return field.visible === true;
      });
    },
  },
};
</script>

<style lang="scss">
body {
  background-color: #f6f6f6;
}
.settings-btn {
  position: absolute;
  right: 5px;
  top: 6px;
}

.list-group-item {
  border: none;
  border-bottom: 1px solid #ddd;
  cursor: grab;
}

.popover-body {
  // background-color: #f6f6f6;
  min-width: 200px;
  padding: 0;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.b-table {
  thead {
    background-color: #f6f6f6;
    border: none;
  }
  th {
    border: none;
    font-size: 12px;
    color: #777;
    font-weight: normal;
  }
  tr {
    border-bottom: 1px solid #ddd;
  }
  td {
    border-bottom: 1px solid #ddd;
  }
}
</style>
