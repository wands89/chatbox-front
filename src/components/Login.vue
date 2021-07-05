<template>
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
            rules: [{ required: true, message: 'Please input your password!' }],
          },
        ]"
      />
    </a-form-item>
    <a-form-item :wrapper-col="{ span: 12, offset: 5 }">
      <a-button type="primary" html-type="submit"> 登录 </a-button>
    </a-form-item>
  </a-form>
</template>

<script>
import axios from "axios";
import { message } from "ant-design-vue";
import Register from "@/components/Register";
export default {
  data() {
    return {
      formLayout: "horizontal",
      form: this.$form.createForm(this, { name: "coordinated" }),
    };
  },
  components: {
    register: Register,
  },
  methods: {
    handleSubmit(e) {
      e.preventDefault();
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log("Received values of form: ", values);
        }
        axios
          .post("/user/login", values)
          .then(function (response) {
            var code = response.data.code;
            var msg = response.data.msg;
            console.log(response);
            console.log(code, msg);
            if (code == 200) {
              //跳转聊天页面
              this.$router.push("ChatBox");
              console.log(this.$router);
            }
            if (code == 400) {
              message.warning(msg);
            }
            if (code == 500) {
              message.error(msg);
            }
          })
          .catch(function (error) {
            console.log(error);
            message.error(error);
          });
      });
    },
    handleSelectChange(value) {
      console.log(value);
      this.form.setFieldsValue({
        note: `Hi, ${value === "male" ? "man" : "lady"}!`,
      });
    },
    loginSuccess() {
      this.$router.push("Login");
      console.log(this.$router);
    },
  },
};
</script>