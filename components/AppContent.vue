<template>
  <a-row class="table-wrapper">
    <a-col :span="14" :offset="5">
      <a-table
        :columns="columns"
        :data-source="employees"
        bordered
        :pagination="{ pageSize: 8 }"
      >
        <a slot="fullname" slot-scope="text">{{ text }}</a>
        <a-tag
          key="gender"
          slot="gender"
          :color="text === 'Male' ? `geekblue` : `volcano`"
          slot-scope="text"
          >{{ text }}</a-tag
        >
        <a slot="salary" slot-scope="text">{{ `${text}$` }}</a>
      </a-table>
    </a-col>
  </a-row>
</template>

<script>
const columns = [
  {
    title: "Full Name",
    key: "fullname",
    dataIndex: "fullname",
    scopedSlots: { customRender: "fullname" }
  },
  {
    title: "Gender",
    dataIndex: "gender",
    key: "gender",
    scopedSlots: { customRender: "gender" }
  },
  {
    title: "Contacts",
    dataIndex: "contacts",
    key: "contacts"
  },
  {
    title: "Joining date",
    dataIndex: "joining_date",
    key: "joining_date"
  },
  {
    title: "Salary",
    dataIndex: "salary",
    key: "salary",
    scopedSlots: { customRender: "salary" }
  },
  {
    title: "Position",
    dataIndex: "position",
    key: "position"
  }
];

export default {
  data() {
    return {
      columns,
      employees: []
    };
  },
  async fetch() {
    try {
      const response = await this.$prismic.api.query(
        this.$prismic.predicates.at("document.type", "content"),
        {
          fetchLinks: [
            "employee.fullname",
            "employee.gender",
            "employee.contacts",
            "employee.joining_date",
            "employee.salary",
            "employee.position"
          ]
        }
      );

      if (response.results && response.results.length > 0) {
        let employeesArray = response.results[0].data.employees_table;

        if (employeesArray.length === 0) return;

        const employeesTableData = employeesArray.map(e => {
          const empData = e.employee.data;

          return {
            ...empData,
            fullname: this.$prismic.asText(empData.fullname),
            contacts: this.$prismic.asText(empData.contacts)
          };
        });

        this.employees = employeesTableData;
      }
    } catch (e) {
      console.log("Error: ", e);
    }
  }
};
</script>

<style>
.table-wrapper {
  margin: 100px 0;
}
.ant-table-body {
  min-height: 500px;
}
</style>
