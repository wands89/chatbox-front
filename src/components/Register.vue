<template>
  <div>
    <!-- <success></success> -->
  <a-form
    :form="form"
    :label-col="{ span: 5 }"
    :wrapper-col="{ span: 12 }"
    @submit="handleSubmit"
  >
    <a-form-item label="Name">
      <a-input
        v-decorator="[
          'name',
          { rules: [{ required: true, message: 'Please input your name!' }] },
        ]"
      />
    </a-form-item>

    <a-form-item label="Password">
      <a-input
        v-decorator="[
          'password',
          {
            rules: [{ required: true, message: 'Please input your Password!' }],
          },
        ]"
      />
    </a-form-item>
    <a-form-item label="Sex">
      <a-select
        option.initialValue="男"
        v-decorator="[
          'sex',
          {
            rules: [{ required: true, message: 'Please  your gender!' }],
          },
        ]"
      >
        <a-select-option value="男"> 男 </a-select-option>
        <a-select-option value="女"> 女 </a-select-option>
        <a-select-option value="未知"> 未知 </a-select-option>
      </a-select>
    </a-form-item>

    <a-form-item label="Age">
      <a-input
        v-decorator="[
          'age',
          { rules: [{ required: false, message: 'Please input your age!' }] },
        ]"
      />
    </a-form-item>
    <a-form-item label="Address">
      <a-input
        v-decorator="[
          'address',
          {
            rules: [{ required: false, message: 'Please input your address!' }],
          },
        ]"
      />
    </a-form-item>

    <a-form-item :wrapper-col="{ span: 12, offset: 5 }">
      <a-button type="primary" html-type="submit"> Submit </a-button>
    </a-form-item>
  </a-form>
  </div>
</template>

<script>
import axios from "axios";
import { message } from 'ant-design-vue';
export default {
  data() {
    return {
      formLayout: "horizontal",
      form: this.$form.createForm(this, { name: "coordinated" }),
    };
  },
  methods: {
    handleSubmit(e) {
      e.preventDefault();
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log("Received values of form: ", values);
          axios
            .post("/user/register", values)
            .then(function (response) {
              var code =response.data.code;
              var msg=response.data.msg;
              console.log(response)
               console.log(code,msg);
              if(code==200){
                message.success(msg);
              }
              if(code==400){
                message.warning(msg);
              }
              
            })
            .catch(function (error) {
              console.log(error);
              message.error(error);
            });
        }
      });
    },
    handleSelectChange(value) {
      console.log(value);
      this.form.setFieldsValue({
        note: `Hi, ${value === "男" ? "男" : "女"}!`,
      });
    },
  },
};
</script>