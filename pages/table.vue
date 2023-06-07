<template>
  <div class="container">
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th v-for="item of tableContent.headers">{{ item }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="row of tableContent.contents">
            <td>{{ row.no }}</td>
            <td>{{ row.name }}</td>
            <td>{{ row.email }}</td>
            <td class="tooltip-button-column">
              <div class="tooltip-button">
                <Tooltip :placement="row.position">
                  <template v-slot:content>
                    <button>ボタン</button>
                  </template>
                  <template v-slot:tooltip>
                    <div>
                      <p>ツールチップコンテンツ1</p>
                      <p>ツールチップコンテンツ2</p>
                      <p>ツールチップコンテンツ3</p>
                    </div>
                  </template>
                </Tooltip>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script lang="ts">
import { Instance, createPopper } from "@popperjs/core";
import Tooltip from "~/components/Tooltip.vue";

type DataType = {
  tableContent: any;
};

export default {
  components: { Tooltip },
  data(): DataType {
    return {
      tableContent: {
        headers: ["No.", "Name", "Email", "Other"],
        contents: [
          { no: 1, name: "Name1", email: "email1@email.com", position: "top" },
          { no: 2, name: "Name2", email: "email2@email.com", position: "left" },
          {
            no: 3,
            name: "Name3",
            email: "email3@email.com",
            position: "bottom",
          },
          {
            no: 4,
            name: "Name4",
            email: "email4@email.com",
            position: "right",
          },
          {
            no: 5,
            name: "Name5",
            email: "email5@email.com",
            position: "top-start",
          },
          {
            no: 6,
            name: "Name6",
            email: "email6@email.com",
            position: "top-end",
          },
          {
            no: 7,
            name: "Name7",
            email: "email7@email.com",
            position: "bottom-start",
          },
          {
            no: 8,
            name: "Name8",
            email: "email8@email.com",
            position: "bottom-end",
          },
          { no: 9, name: "Name9", email: "email9@email.com", position: "top" },
          {
            no: 10,
            name: "Name10",
            email: "email10@email.com",
            position: "top",
          },
        ],
      },
    };
  },
  methods: {},
  setup() {},
  mounted() {},
};
</script>

<style lang="scss" scoped>
.container {
  padding: 100px;

  .table-container {
    width: 100%;
    background-color: #888;

    position: relative;
    overflow: scroll;

    table {
      width: 100%;
      background-color: #ccc;

      text-align: left;

      border-collapse: collapse;
      border: dashed 1px;

      th,
      td {
        padding: 8px 12px;
        border: solid 1px;
        border-color: #999;
      }

      .tooltip-button-column {
        text-align: center;
        .tooltip-button {
          display: inline-block;
        }
      }
    }
  }
}
</style>
