<template>
     <a-row class="table-wrapper">
      <a-col :span="14" :offset="5">
        <a-table :columns="columns" :data-source="employees" bordered :pagination="{pageSize: 8}">
        <a slot="fullname" slot-scope="text">{{ text }}</a>
        <a-tag key="gender" slot="gender" :color="text === 'Male' ? `geekblue` : `volcano`"  slot-scope="text">{{ text }}</a-tag>
        <a slot="salary" slot-scope="text">{{ `${text}$` }}</a>
        </a-table>
      </a-col>
    </a-row>
</template>

<script>
import Prismic from '@prismicio/client';

const api = Prismic.client("http://kozaktest.cdn.prismic.io/api")

const columns = [
  {
    title: 'Full Name',
    key: 'fullname',
    dataIndex: 'fullname',
    scopedSlots: { customRender: 'fullname' },
  },
  {
    title: 'Gender',
    dataIndex: 'gender',
    key: 'gender',
    scopedSlots: { customRender: 'gender' },
  },
  {
    title: 'Contacts',
    dataIndex: 'contacts',
    key: 'contacts',
  },
  {
    title: 'Joining date',
    dataIndex: 'joining_date',
    key: 'joining_date',
  },
  {
    title: 'Salary',
    dataIndex: 'salary',
    key: 'salary',
    scopedSlots: { customRender: 'salary' },
  },
  {
    title: 'Position',
    dataIndex: 'position',
    key: 'position',
  }
];

export default {
  data() {
    return {
      columns,
      employees: []
    };
  },
  async fetch(){
      // const response = await this.$prismic.api.query(
      //       this.$prismic.predicates.at("document.type", "employee"),
            // { orderings : '[my.employee.joining_date desc]', fetchLinks: 'employee' }
        // );
      // const response2 = await this.$prismic.api.getSingle('content', { fetchLinks: 'employee' });

    try{
      const response = await api.query(Prismic.Predicates.at('document.type', 'content'), { fetchLinks: ['employee.fullname','employee.gender','employee.contacts','employee.joining_date', 'employee.salary', 'employee.position'] });

      // const response = await api.getByUID('content', 'content', {fetchLinks: 'employee.gender'});

      console.log(response.results[0].data.content);

      // Object.values(response.data).forEach(e => console.log(e));
      // response.results[0].data.content.employees_table.value.forEach(e => {
      //   console.log(e);
      // });
      // console.log();
      // console.log(response.results[0].data.content.employees_table.value.forEach(e => {
      //   console.log(api.as, e);
      // }));

    //   const mySuperGraphQuery = `{
    //     content{
    //       data
    //     }
    //   }`

    //   const result = await api.getSingle('content',
    //     { 'graphQuery': mySuperGraphQuery }
    //   );

    //   console.log(result);
      return {
        components: []
      }
    }catch(e){
      console.log("Error: ", e);
    }

        // console.log("DATA CONTENT: ", response);
        // response.data.forEach(e => console.log(e))

        // console.log("DATA CONTENT2: ");
        // console.log(response2.data.test111);
        // response2.data.test111.forEach(e => console.log(e.test.data))

        // if(response && response.results && response.results.length !== 0){
        //     const results = response.results.map(e => ({
        //         ...e.data,
        //         fullname: this.$prismic.asText(e.data.fullname),
        //         contacts: this.$prismic.asText(e.data.contacts)
        //     }));
        //     this.employees = results;
        // }
  },
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